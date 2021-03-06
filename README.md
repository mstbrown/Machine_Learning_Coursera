# Machine_Learning_Coursera
Final Course Project


MachineLearning_CourseProject
RStudio
Sunday, February 22, 2015

This R Markdown document was created using data from: Velloso, E.; Bulling, A.; Gellersen, H.; Ugulino, W.; Fuks, H. Qualitative Activity Recognition of Weight Lifting Exercises. Proceedings of 4th International Conference in Cooperation with SIGCHI (Augmented Human ’13) . Stuttgart, Germany: ACM SIGCHI, 2013.

General description of the data: Six young health participants were asked to perform one set of 10 repetitions of the Unilateral Dumbbell Biceps Curl in five different fashions: exactly according to the specification (Class A), throwing the elbows to the front (Class B), lifting the dumbbell only halfway (Class C), lowering the dumbbell only halfway (Class D) and throwing the hips to the front (Class E). To summarize, group A is correct. B-E are common mistakes.

In a few sentences, the goal of this project is to build a predictive machine learning model that can correctly identify if new additional Unilateral Dumbbell Biceps Curl observations were completed exactly according to the specification or if instead the study participant made a common mistake with the dumbbell. My approach first drops all but summative data and then runs a boost model using controlling for the study participant and using data from sensors as predictors. There were six participants in the study.

setwd("C:/Users/owner/Dropbox/2014 Fall/Machine Learning - Spring 2014")
training_data<-read.csv("pml-training.csv")
#drop all the rows of non summative data
data_subset<-subset(training_data,training_data$stddev_roll_dumbbell>.00001)
#delete a column with mostly #DIV/0! entries
data_subset2<-data_subset[,-(14),drop=FALSE]

#note there are some #DIV/0! entries; skip the removal and try running model anyway

#idea, some of the incorrect methods should be very ovservable - for example only lifting the dumbbell halfway!
#Create a dummy variable for classe=C, lifting the dumbbell only halfway
a<-rep(0,186) #188:253
b<-rep(1,66)
c<-rep(0,138)
in_C<-c(a,b,c)
data_dummy<-cbind(data_subset2,in_C)

#running a logit regression to determine if average pitch of the dumbell matters for predicting if it was only lifted halfway
logit_model<-glm(in_C~pitch_dumbbell,data=data_dummy,family="binomial")
summary(logit_model) #pitch_dumbbell variable is very significant

## 
## Call:
## glm(formula = in_C ~ pitch_dumbbell, family = "binomial", data = data_dummy)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -1.1067  -0.6721  -0.5407  -0.3723   2.5970  
## 
## Coefficients:
##                 Estimate Std. Error z value Pr(>|z|)    
## (Intercept)    -1.923532   0.181223 -10.614  < 2e-16 ***
## pitch_dumbbell -0.016892   0.004508  -3.747 0.000179 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 354.64  on 389  degrees of freedom
## Residual deviance: 337.91  on 388  degrees of freedom
## AIC: 341.91
## 
## Number of Fisher Scoring iterations: 5

    #given there are just five outcomes, a variant of the logit model might work well

#use LogitBoost
library(caret)

## Warning: package 'caret' was built under R version 3.1.2

## Loading required package: lattice
## Loading required package: ggplot2

modFitAll<-train(classe~user_name+roll_belt+pitch_belt+roll_arm+pitch_arm+yaw_arm+total_accel_arm+roll_dumbbell+pitch_dumbbell+yaw_dumbbell+roll_forearm+pitch_forearm+yaw_forearm+yaw_belt+total_accel_belt+total_accel_dumbbell+total_accel_forearm,method="LogitBoost",data=data_subset2)

## Loading required package: caTools

## Warning: package 'caTools' was built under R version 3.1.2

#modFitAll #64% accurate with some seeds, give it a try! #note, lost accuracy when I added three gyros_belt x,y,z variables

A plot helping motivate the logit model. Notice the third color has almost all values below 50; the third color is “lifting the dumbbell only halfway.”

Performing cross validation Method 1: k folds

# define training control
train_control <- trainControl(method="cv", number=10)
# train the model
model <- train(classe~user_name+roll_belt+pitch_belt+roll_arm+pitch_arm+yaw_arm+total_accel_arm+roll_dumbbell+pitch_dumbbell+yaw_dumbbell+roll_forearm+pitch_forearm+yaw_forearm+yaw_belt+total_accel_belt+total_accel_dumbbell+total_accel_forearm, data=data_subset2, trControl=train_control, method="LogitBoost")
# make predictions
predictions <- predict(model, data_subset2[,1:159])
# summarize results
confusionMatrix(predictions, data_subset2$classe)

## Confusion Matrix and Statistics
## 
##           Reference
## Prediction  A  B  C  D  E
##          A 95  1  0  0  0
##          B  1 60  1  2  0
##          C  1  4 59  4  0
##          D  2  1  0 42  1
##          E  0  0  0  1 67
## 
## Overall Statistics
##                                           
##                Accuracy : 0.9444          
##                  95% CI : (0.9146, 0.9662)
##     No Information Rate : 0.2895          
##     P-Value [Acc > NIR] : < 2.2e-16       
##                                           
##                   Kappa : 0.9296          
##  Mcnemar's Test P-Value : NA              
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity            0.9596   0.9091   0.9833   0.8571   0.9853
## Specificity            0.9959   0.9855   0.9681   0.9863   0.9964
## Pos Pred Value         0.9896   0.9375   0.8676   0.9130   0.9853
## Neg Pred Value         0.9837   0.9784   0.9964   0.9764   0.9964
## Prevalence             0.2895   0.1930   0.1754   0.1433   0.1988
## Detection Rate         0.2778   0.1754   0.1725   0.1228   0.1959
## Detection Prevalence   0.2807   0.1871   0.1988   0.1345   0.1988
## Balanced Accuracy      0.9777   0.9473   0.9757   0.9217   0.9908

    #results: please see confusion matrix. In this subsetted data, we could consider the accuracy in identifying A-correct form exercise lifting. For predicting A, sensitivity is high at 95/99 and specificity is high at 228/241.

Method 2: Bootstrapping

#set seed so that bootstraps are comparable
set.seed(1)
#run the model using 25 bootstrap repetitions
modFitAll<-train(classe~user_name+roll_belt+pitch_belt+roll_arm+pitch_arm+yaw_arm+total_accel_arm+roll_dumbbell+pitch_dumbbell+yaw_dumbbell+roll_forearm+pitch_forearm+yaw_forearm+yaw_belt+total_accel_belt+total_accel_dumbbell+total_accel_forearm,method="LogitBoost",data=data_subset2)
#output accuracy statistics
modFitAll

## Boosted Logistic Regression 
## 
## 390 samples
## 158 predictors
##   5 classes: 'A', 'B', 'C', 'D', 'E' 
## 
## No pre-processing
## Resampling: Bootstrapped (25 reps) 
## 
## Summary of sample sizes: 390, 390, 390, 390, 390, 390, ... 
## 
## Resampling results across tuning parameters:
## 
##   nIter  Accuracy   Kappa      Accuracy SD  Kappa SD  
##   11     0.6232642  0.5188757  0.07169875   0.08885463
##   21     0.6257155  0.5230658  0.06090335   0.07457827
##   31     0.6449161  0.5486461  0.06271180   0.07784943
## 
## Accuracy was used to select the optimal model using  the largest value.
## The final value used for the model was nIter = 31.

    #results: using the optimal tuning parameters, the model accuracy is 0.65. It is also useful to use the Kappa statistic in order to normalize our correct matches by how many correct matches random chance would have gotten anyway. Kappa ranges from 0 to 1 and 0 indicates random chance agreement. My model's kappa value of 0.55 indicates a fair improvement on random chance agreement.

Now use the model to form predictions. BELOW ARE MY MODEL’S PREDICTIONS

test_data<-read.csv("pml-testing.csv")
prediction <- predict(modFitAll, test_data)
prediction

##  [1] B    <NA> <NA> <NA> C    E    C    D    A    A    B    C    B    A   
## [15] E    A    A    B    A    B   
## Levels: A B C D E

Now use the model to form predictions

#note below I use the instructor's suggested code
pml_write_files = function(x){
    n = length(x)
    for(i in 1:n){
        filename = paste0("problem_id_",i,".txt")
        write.table(x[i],file=filename,quote=FALSE,row.names=FALSE,col.names=FALSE)
    }
}
pml_write_files(prediction)

Note that the echo = FALSE parameter was added to the code chunk to prevent printing of the R code that generated the plot.

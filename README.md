@@ -0,0 +1,230 @@
<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">

<head>

<meta charset="utf-8">
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<meta name="generator" content="pandoc" />

<meta name="author" content="RStudio" />


<title>MachineLearning_CourseProject</title>

<script src="data:application/x-javascript,%2F%2A%21%20jQuery%20v1%2E11%2E0%20%7C%20%28c%29%202005%2C%202014%20jQuery%20Foundation%2C%20Inc%2E%20%7C%20jquery%2Eorg%2Flicense%20%2A%2F%0A%21function%28a%2Cb%29%7B%22object%22%3D%3Dtypeof%20module%26%26%22object%22%3D%3Dtypeof%20module%2Eexports%3Fmodule%2Eexports%3Da%2Edocument%3Fb%28a%2C%210%29%3Afunction%28a%29%7Bif%28%21a%2Edocument%29throw%20new%20Error%28%22jQuery%20requires%20a%20window%20with%20a%20document%22%29%3Breturn%20b%28a%29%7D%3Ab%28a%29%7D%28%...(line truncated)...
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<link href="data:text/css,%2F%2A%21%0A%20%2A%20Bootstrap%20v2%2E3%2E2%0A%20%2A%0A%20%2A%20Copyright%202013%20Twitter%2C%20Inc%0A%20%2A%20Licensed%20under%20the%20Apache%20License%20v2%2E0%0A%20%2A%20http%3A%2F%2Fwww%2Eapache%2Eorg%2Flicenses%2FLICENSE%2D2%2E0%0A%20%2A%0A%20%2A%20Designed%20and%20built%20with%20all%20the%20love%20in%20the%20world%20by%20%40mdo%20and%20%40fat%2E%0A%20%2A%2F%2Eclearfix%7B%2Azoom%3A1%7D%2Eclearfix%3Abefore%2C%2Eclearfix%3Aafter%7Bdisplay%3Atable%3Bline%2Dheight%3A0%3Bcontent%3A...(line truncated)...
<link href="data:text/css,%2F%2A%21%0A%20%2A%20Bootstrap%20Responsive%20v2%2E3%2E2%0A%20%2A%0A%20%2A%20Copyright%202013%20Twitter%2C%20Inc%0A%20%2A%20Licensed%20under%20the%20Apache%20License%20v2%2E0%0A%20%2A%20http%3A%2F%2Fwww%2Eapache%2Eorg%2Flicenses%2FLICENSE%2D2%2E0%0A%20%2A%0A%20%2A%20Designed%20and%20built%20with%20all%20the%20love%20in%20the%20world%20by%20%40mdo%20and%20%40fat%2E%0A%20%2A%2F%2Eclearfix%7B%2Azoom%3A1%7D%2Eclearfix%3Abefore%2C%2Eclearfix%3Aafter%7Bdisplay%3Atable%3Bline%2Dheight%3A0...(line truncated)...
<script src="data:application/x-javascript,%2F%2A%21%0A%2A%20Bootstrap%2Ejs%20by%20%40fat%20%26%20%40mdo%0A%2A%20Copyright%202013%20Twitter%2C%20Inc%2E%0A%2A%20http%3A%2F%2Fwww%2Eapache%2Eorg%2Flicenses%2FLICENSE%2D2%2E0%2Etxt%0A%2A%2F%0A%21function%28e%29%7B%22use%20strict%22%3Be%28function%28%29%7Be%2Esupport%2Etransition%3Dfunction%28%29%7Bvar%20e%3Dfunction%28%29%7Bvar%20e%3Ddocument%2EcreateElement%28%22bootstrap%22%29%2Ct%3D%7BWebkitTransition%3A%22webkitTransitionEnd%22%2CMozTransition%3A%22transitio...(line truncated)...

<style type="text/css">code{white-space: pre;}</style>
<link href="data:text/css,pre%20%2Eoperator%2C%0Apre%20%2Eparen%20%7B%0A%20color%3A%20rgb%28104%2C%20118%2C%20135%29%0A%7D%0A%0Apre%20%2Eliteral%20%7B%0A%20color%3A%20%23990073%0A%7D%0A%0Apre%20%2Enumber%20%7B%0A%20color%3A%20%23099%3B%0A%7D%0A%0Apre%20%2Ecomment%20%7B%0A%20color%3A%20%23998%3B%0A%20font%2Dstyle%3A%20italic%0A%7D%0A%0Apre%20%2Ekeyword%20%7B%0A%20color%3A%20%23900%3B%0A%20font%2Dweight%3A%20bold%0A%7D%0A%0Apre%20%2Eidentifier%20%7B%0A%20color%3A%20rgb%280%2C%200%2C%200%29%3B%0A%7D%0A%0Apre%2...(line truncated)...
<script src="data:application/x-javascript,%0Avar%20hljs%3Dnew%20function%28%29%7Bfunction%20m%28p%29%7Breturn%20p%2Ereplace%28%2F%26%2Fgm%2C%22%26amp%3B%22%29%2Ereplace%28%2F%3C%2Fgm%2C%22%26lt%3B%22%29%7Dfunction%20f%28r%2Cq%2Cp%29%7Breturn%20RegExp%28q%2C%22m%22%2B%28r%2EcI%3F%22i%22%3A%22%22%29%2B%28p%3F%22g%22%3A%22%22%29%29%7Dfunction%20b%28r%29%7Bfor%28var%20p%3D0%3Bp%3Cr%2EchildNodes%2Elength%3Bp%2B%2B%29%7Bvar%20q%3Dr%2EchildNodes%5Bp%5D%3Bif%28q%2EnodeName%3D%3D%22CODE%22%29%7Breturn%20q%7Dif%28%2...(line truncated)...
<style type="text/css">
  pre:not([class]) {
    background-color: white;
  }
</style>
<script type="text/javascript">
if (window.hljs && document.readyState && document.readyState === "complete") {
   window.setTimeout(function() {
      hljs.initHighlighting();
   }, 0);
}
</script>



</head>

<body>

<style type="text/css">
.main-container {
  max-width: 940px;
  margin-left: auto;
  margin-right: auto;
}
</style>
<div class="container-fluid main-container">


<div id="header">
<h1 class="title">MachineLearning_CourseProject</h1>
<h4 class="author"><em>RStudio</em></h4>
<h4 class="date"><em>Sunday, February 22, 2015</em></h4>
</div>


<p>This R Markdown document was created using data from: Velloso, E.; Bulling, A.; Gellersen, H.; Ugulino, W.; Fuks, H. Qualitative Activity Recognition of Weight Lifting Exercises. Proceedings of 4th International Conference in Cooperation with SIGCHI (Augmented Human ’13) . Stuttgart, Germany: ACM SIGCHI, 2013.</p>
<p>General description of the data: Six young health participants were asked to perform one set of 10 repetitions of the Unilateral Dumbbell Biceps Curl in five different fashions: exactly according to the specification (Class A), throwing the elbows to the front (Class B), lifting the dumbbell only halfway (Class C), lowering the dumbbell only halfway (Class D) and throwing the hips to the front (Class E). To summarize, group A is correct. B-E are common mistakes.</p>
<p>In a few sentences, the goal of this project is to build a predictive machine learning model that can correctly identify if new additional Unilateral Dumbbell Biceps Curl observations were completed exactly according to the specification or if instead the study participant made a common mistake with the dumbbell. My approach first drops all but summative data and then runs a boost model using controlling for the study participant and using data from sensors as predictors. There were six participants in t...(line truncated)...
<pre class="r"><code>setwd(&quot;C:/Users/owner/Dropbox/2014 Fall/Machine Learning - Spring 2014&quot;)
training_data&lt;-read.csv(&quot;pml-training.csv&quot;)
#drop all the rows of non summative data
data_subset&lt;-subset(training_data,training_data$stddev_roll_dumbbell&gt;.00001)
#delete a column with mostly #DIV/0! entries
data_subset2&lt;-data_subset[,-(14),drop=FALSE]

#note there are some #DIV/0! entries; skip the removal and try running model anyway

#idea, some of the incorrect methods should be very ovservable - for example only lifting the dumbbell halfway!
#Create a dummy variable for classe=C, lifting the dumbbell only halfway
a&lt;-rep(0,186) #188:253
b&lt;-rep(1,66)
c&lt;-rep(0,138)
in_C&lt;-c(a,b,c)
data_dummy&lt;-cbind(data_subset2,in_C)

#running a logit regression to determine if average pitch of the dumbell matters for predicting if it was only lifted halfway
logit_model&lt;-glm(in_C~pitch_dumbbell,data=data_dummy,family=&quot;binomial&quot;)
summary(logit_model) #pitch_dumbbell variable is very significant</code></pre>
<pre><code>## 
## Call:
## glm(formula = in_C ~ pitch_dumbbell, family = &quot;binomial&quot;, data = data_dummy)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -1.1067  -0.6721  -0.5407  -0.3723   2.5970  
## 
## Coefficients:
##                 Estimate Std. Error z value Pr(&gt;|z|)    
## (Intercept)    -1.923532   0.181223 -10.614  &lt; 2e-16 ***
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
## Number of Fisher Scoring iterations: 5</code></pre>
<pre class="r"><code>    #given there are just five outcomes, a variant of the logit model might work well

#use LogitBoost
library(caret)</code></pre>
<pre><code>## Warning: package 'caret' was built under R version 3.1.2</code></pre>
<pre><code>## Loading required package: lattice
## Loading required package: ggplot2</code></pre>
<pre class="r"><code>modFitAll&lt;-train(classe~user_name+roll_belt+pitch_belt+roll_arm+pitch_arm+yaw_arm+total_accel_arm+roll_dumbbell+pitch_dumbbell+yaw_dumbbell+roll_forearm+pitch_forearm+yaw_forearm+yaw_belt+total_accel_belt+total_accel_dumbbell+total_accel_forearm,method=&quot;LogitBoost&quot;,data=data_subset2)</code></pre>
<pre><code>## Loading required package: caTools</code></pre>
<pre><code>## Warning: package 'caTools' was built under R version 3.1.2</code></pre>
<pre class="r"><code>#modFitAll #64% accurate with some seeds, give it a try! #note, lost accuracy when I added three gyros_belt x,y,z variables</code></pre>
<p>A plot helping motivate the logit model. Notice the third color has almost all values below 50; the third color is “lifting the dumbbell only halfway.”</p>
<p><img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABUAAAAPACAMAAADDuCPrAAAAZlBMVEUAAAAAADoAAGYAAP8AOmYAOpAAZmYAZpAAZrYAzQAA//86AAA6kJA6kNtmAABmAGZmOgBmOpBmtv+QOgCQkDqQ2/+2ZgC225C2///bkDrb/7bb////AAD/tmb/25D//7b//9v///+7Kz4QAAAACXBIWXMAAB2HAAAdhwGP5fFlAAAgAElEQVR4nO29i3rkNtJgmd01vWOp1p5de1rb2i5Vme//kpPJKwCCFwRuAfKcb/42lEmCFEc+BhCB4KMDAAARj9o3AADQKggUAEAIAgUAEIJAAQCEIFAAACEIFABACAIFABCCQAEAhCBQAAAhCBQAQAgCBQAQgkABAIQgUAAAIQgUAEAIAgUAEIJAAQCEIFAAACEIFABACAIFABCCQAEAhCBQAAAhCBQAQAgCBQAQgkABAIQgUAAAIQgUA...(line truncated)...
<p>Performing cross validation Method 1: k folds</p>
<pre class="r"><code># define training control
train_control &lt;- trainControl(method=&quot;cv&quot;, number=10)
# train the model
model &lt;- train(classe~user_name+roll_belt+pitch_belt+roll_arm+pitch_arm+yaw_arm+total_accel_arm+roll_dumbbell+pitch_dumbbell+yaw_dumbbell+roll_forearm+pitch_forearm+yaw_forearm+yaw_belt+total_accel_belt+total_accel_dumbbell+total_accel_forearm, data=data_subset2, trControl=train_control, method=&quot;LogitBoost&quot;)
# make predictions
predictions &lt;- predict(model, data_subset2[,1:159])
# summarize results
confusionMatrix(predictions, data_subset2$classe)</code></pre>
<pre><code>## Confusion Matrix and Statistics
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
##     P-Value [Acc &gt; NIR] : &lt; 2.2e-16       
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
## Balanced Accuracy      0.9777   0.9473   0.9757   0.9217   0.9908</code></pre>
<pre class="r"><code>    #results: please see confusion matrix. In this subsetted data, we could consider the accuracy in identifying A-correct form exercise lifting. For predicting A, sensitivity is high at 95/99 and specificity is high at 228/241.</code></pre>
<p>Method 2: Bootstrapping</p>
<pre class="r"><code>#set seed so that bootstraps are comparable
set.seed(1)
#run the model using 25 bootstrap repetitions
modFitAll&lt;-train(classe~user_name+roll_belt+pitch_belt+roll_arm+pitch_arm+yaw_arm+total_accel_arm+roll_dumbbell+pitch_dumbbell+yaw_dumbbell+roll_forearm+pitch_forearm+yaw_forearm+yaw_belt+total_accel_belt+total_accel_dumbbell+total_accel_forearm,method=&quot;LogitBoost&quot;,data=data_subset2)
#output accuracy statistics
modFitAll</code></pre>
<pre><code>## Boosted Logistic Regression 
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
## The final value used for the model was nIter = 31.</code></pre>
<pre class="r"><code>    #results: using the optimal tuning parameters, the model accuracy is 0.65. It is also useful to use the Kappa statistic in order to normalize our correct matches by how many correct matches random chance would have gotten anyway. Kappa ranges from 0 to 1 and 0 indicates random chance agreement. My model's kappa value of 0.55 indicates a fair improvement on random chance agreement.</code></pre>
<p>Now use the model to form predictions. <strong>BELOW ARE MY MODEL’S PREDICTIONS</strong></p>
<pre class="r"><code>test_data&lt;-read.csv(&quot;pml-testing.csv&quot;)
prediction &lt;- predict(modFitAll, test_data)
prediction</code></pre>
<pre><code>##  [1] B    &lt;NA&gt; &lt;NA&gt; &lt;NA&gt; C    E    C    D    A    A    B    C    B    A   
## [15] E    A    A    B    A    B   
## Levels: A B C D E</code></pre>
<p>Now use the model to form predictions</p>
<pre class="r"><code>#note below I use the instructor's suggested code
pml_write_files = function(x){
    n = length(x)
    for(i in 1:n){
        filename = paste0(&quot;problem_id_&quot;,i,&quot;.txt&quot;)
        write.table(x[i],file=filename,quote=FALSE,row.names=FALSE,col.names=FALSE)
    }
}
pml_write_files(prediction)</code></pre>
<p>Note that the <code>echo = FALSE</code> parameter was added to the code chunk to prevent printing of the R code that generated the plot.</p>


</div>

<script>

// add bootstrap table styles to pandoc tables
$(document).ready(function () {
  $('tr.header').parent('thead').parent('table').addClass('table table-condensed');
});

</script>

<!-- dynamically load mathjax for compatibility with self-contained -->
<script>
  (function () {
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src  = "https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML";
    document.getElementsByTagName("head")[0].appendChild(script);
  })();
</script>

</body>
</html>

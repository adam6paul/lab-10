Lab 10 - Grading the professor, Pt. 2
================
Adam Paul
5-6-2022

### Load packages and data

``` r
library(tidyverse) 
library(tidymodels)
library(openintro)
```

``` r
evals <- evals
```

### Exercise 1

> Fit a linear model (one you have fit before): m\_bty, predicting
> average professor evaluation score based on average beauty rating
> (bty\_avg) only. Write the linear model, and note the R2 and the
> adjusted R2.

``` r
m_bty <- lm(score ~ bty_avg, data=evals)

print(m_bty)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg, data = evals)
    ## 
    ## Coefficients:
    ## (Intercept)      bty_avg  
    ##     3.88034      0.06664

``` r
summary(m_bty)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.9246 -0.3690  0.1420  0.3977  0.9309 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  3.88034    0.07614   50.96  < 2e-16 ***
    ## bty_avg      0.06664    0.01629    4.09 5.08e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5348 on 461 degrees of freedom
    ## Multiple R-squared:  0.03502,    Adjusted R-squared:  0.03293 
    ## F-statistic: 16.73 on 1 and 461 DF,  p-value: 5.083e-05

score = 3.88 + (x\*.0666)

r-squared= .035

adjusted r-squared= .033

### Exercise 2

> Fit a linear model (one you have fit before): m\_bty\_gen, predicting
> average professor evaluation score based on average beauty rating
> (bty\_avg) and gender. Write the linear model, and note the R2 and the
> adjusted R2.

``` r
m_bty_gen <- lm(score ~ bty_avg + gender, data=evals)

print(m_bty_gen)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + gender, data = evals)
    ## 
    ## Coefficients:
    ## (Intercept)      bty_avg   gendermale  
    ##     3.74734      0.07416      0.17239

``` r
summary(m_bty_gen)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + gender, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8305 -0.3625  0.1055  0.4213  0.9314 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  3.74734    0.08466  44.266  < 2e-16 ***
    ## bty_avg      0.07416    0.01625   4.563 6.48e-06 ***
    ## gendermale   0.17239    0.05022   3.433 0.000652 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5287 on 460 degrees of freedom
    ## Multiple R-squared:  0.05912,    Adjusted R-squared:  0.05503 
    ## F-statistic: 14.45 on 2 and 460 DF,  p-value: 8.177e-07

score = 3.74 + (bty\* .074) + (gen\*.1724)

R squared = .059

Adjusted R squared = .055

### Exercise 3

> Interpret the slope and intercept of m\_bty\_gen in context of the
> data.

The intercept is the average score for female professors with a beauty
score of 0, who obviously don’t exist (what is a score of 0?)

The first slope (.074) is how much a rating will increase with a 1 point
increase in attractiveness.

The second slope (.1724) is how much a rating will increase by being a
male (rather than female) professor.

### Exercise 4

> What percent of the variability in score is explained by the model
> m\_bty\_gen.

5.5% of the variance has been explained (adjust r-square= .055)

### Exercise 5

> What is the equation of the line corresponding to just male
> professors?

male= 3.74 + (x \* .074) + (1 \* .1724)

### Exercise 6

> For two professors who received the same beauty rating, which gender
> tends to have the higher course evaluation score?

Men tend to have the higher course evaluation score.

### Exercise 7

> How does the relationship between beauty and evaluation score vary
> between male and female professors?

I believe that beauty is more important for one gender than the other,
but based on the analyses I can’t say which. But the increase is larger
when gender is included, so it must be. Based on the way the world
works, it’s probably women for whom it is more impactful.

### Exercise 8

> How do the adjusted R2 values of m\_bty\_gen and m\_bty compare? What
> does this tell us about how useful gender is in explaining the
> variability in evaluation scores when we already have information on
> the beauty score of the professor.

Gender adds nearly .02 to the predictive power of the model, so it’s at
least as important of a predictor as beauty score.

### Exercise 9

> Compare the slopes of bty\_avg under the two models (m\_bty and
> m\_bty\_gen). Has the addition of gender to the model changed the
> parameter estimate (slope) for bty\_avg?

Yes, the slope got larger for bty\_avg when we included gender.

bty=.0666

bty\_gen=.074

### Exercise 10

> Create a new model called m\_bty\_rank with gender removed and rank
> added in. Write the equation of the linear model and interpret the
> slopes and intercept in context of the data.

``` r
m_bty_rank <- lm(score ~ bty_avg + rank, data=evals)

print(m_bty_rank)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + rank, data = evals)
    ## 
    ## Coefficients:
    ##      (Intercept)           bty_avg  ranktenure track       ranktenured  
    ##          3.98155           0.06783          -0.16070          -0.12623

``` r
summary(m_bty_rank)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + rank, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8713 -0.3642  0.1489  0.4103  0.9525 
    ## 
    ## Coefficients:
    ##                  Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)       3.98155    0.09078  43.860  < 2e-16 ***
    ## bty_avg           0.06783    0.01655   4.098 4.92e-05 ***
    ## ranktenure track -0.16070    0.07395  -2.173   0.0303 *  
    ## ranktenured      -0.12623    0.06266  -2.014   0.0445 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5328 on 459 degrees of freedom
    ## Multiple R-squared:  0.04652,    Adjusted R-squared:  0.04029 
    ## F-statistic: 7.465 on 3 and 459 DF,  p-value: 6.88e-05

Teaching:

score= 3.98 + (0) + (0)

Tenure track:

score = 3.98 + (1\*-.1607)

Tenured:

score = 3.98 + (1\*-.1262)

The intercept (3.98) is the score for teaching track professors, as they
are the reference class.

The first slope (-.1607) is how much a rating will decrease on average
by being a tenure track professor

The second slope (-.1262) is how much a rating will decrease on average
by being a tenured professor.

### Exercise 11

> Which variable, on its own, would you expect to be the worst predictor
> of evaluation scores? Why? Hint: Think about which variable would you
> expect to not have any association with the professor’s score.

I think pic color, because I really, really doubt students care about
that.

### Exercise 12

> Check your suspicions from the previous exercise. Include the model
> output for that variable in your response.

``` r
m_pic_color <- lm(score ~ pic_color, data=evals)

print(m_pic_color)
```

    ## 
    ## Call:
    ## lm(formula = score ~ pic_color, data = evals)
    ## 
    ## Coefficients:
    ##    (Intercept)  pic_colorcolor  
    ##         4.3615         -0.2247

``` r
summary(m_pic_color)
```

    ## 
    ## Call:
    ## lm(formula = score ~ pic_color, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8369 -0.3615  0.1385  0.4385  0.8631 
    ## 
    ## Coefficients:
    ##                Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)     4.36154    0.06090  71.613  < 2e-16 ***
    ## pic_colorcolor -0.22466    0.06679  -3.364 0.000833 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5379 on 461 degrees of freedom
    ## Multiple R-squared:  0.02395,    Adjusted R-squared:  0.02184 
    ## F-statistic: 11.31 on 1 and 461 DF,  p-value: 0.0008334

Surprisingly, picture color was a significantly negative predictor!
Professors with black and white photos get lower ratings.

score= 4.36 + (1\*-.2247)

### Exercise 13

> Suppose you wanted to fit a full model with the variables listed
> above. If you are already going to include cls\_perc\_eval and
> cls\_students, which variable should you not include as an additional
> predictor? Why?

cls\_did\_eval would be redundant with cls\_perc\_eval, and less useful
than the percentage because the class sizes are different.

### Exercise 14

> Fit a full model with all predictors listed above (except for the one
> you decided to exclude) in the previous question.

``` r
m_full_model <- lm(score ~ bty_avg + rank + ethnicity + gender + age + language +
            cls_perc_eval + cls_students + cls_level + cls_profs + cls_credits, data=evals)

print(m_full_model)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + rank + ethnicity + gender + age + 
    ##     language + cls_perc_eval + cls_students + cls_level + cls_profs + 
    ##     cls_credits, data = evals)
    ## 
    ## Coefficients:
    ##           (Intercept)                bty_avg       ranktenure track  
    ##             3.5305036              0.0612651             -0.1070121  
    ##           ranktenured  ethnicitynot minority             gendermale  
    ##            -0.0450371              0.1869649              0.1786166  
    ##                   age    languagenon-english          cls_perc_eval  
    ##            -0.0066498             -0.1268254              0.0056996  
    ##          cls_students         cls_levelupper        cls_profssingle  
    ##             0.0004455              0.0187105             -0.0085751  
    ## cls_creditsone credit  
    ##             0.5087427

``` r
summary(m_full_model)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + rank + ethnicity + gender + age + 
    ##     language + cls_perc_eval + cls_students + cls_level + cls_profs + 
    ##     cls_credits, data = evals)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.84482 -0.31367  0.08559  0.35732  1.10105 
    ## 
    ## Coefficients:
    ##                         Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            3.5305036  0.2408200  14.660  < 2e-16 ***
    ## bty_avg                0.0612651  0.0166755   3.674 0.000268 ***
    ## ranktenure track      -0.1070121  0.0820250  -1.305 0.192687    
    ## ranktenured           -0.0450371  0.0652185  -0.691 0.490199    
    ## ethnicitynot minority  0.1869649  0.0775329   2.411 0.016290 *  
    ## gendermale             0.1786166  0.0515346   3.466 0.000579 ***
    ## age                   -0.0066498  0.0030830  -2.157 0.031542 *  
    ## languagenon-english   -0.1268254  0.1080358  -1.174 0.241048    
    ## cls_perc_eval          0.0056996  0.0015514   3.674 0.000268 ***
    ## cls_students           0.0004455  0.0003585   1.243 0.214596    
    ## cls_levelupper         0.0187105  0.0555833   0.337 0.736560    
    ## cls_profssingle       -0.0085751  0.0513527  -0.167 0.867458    
    ## cls_creditsone credit  0.5087427  0.1170130   4.348  1.7e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.504 on 450 degrees of freedom
    ## Multiple R-squared:  0.1635, Adjusted R-squared:  0.1412 
    ## F-statistic: 7.331 on 12 and 450 DF,  p-value: 2.406e-12

### Exercise 15

> Using backward-selection with adjusted R-squared as the selection
> criterion, determine the best model. You do not need to show all steps
> in your answer, just the output for the final model. Also, write out
> the linear model for predicting score based on the final model you
> settle on.

``` r
m_full_model <- lm(score ~  bty_avg + ethnicity + gender  + age + cls_perc_eval + cls_level + cls_credits, data=evals)
print(m_full_model)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + ethnicity + gender + age + cls_perc_eval + 
    ##     cls_level + cls_credits, data = evals)
    ## 
    ## Coefficients:
    ##           (Intercept)                bty_avg  ethnicitynot minority  
    ##              3.414586               0.064639               0.242287  
    ##            gendermale                    age          cls_perc_eval  
    ##              0.181179              -0.005020               0.005148  
    ##        cls_levelupper  cls_creditsone credit  
    ##             -0.015052               0.522498

``` r
summary(m_full_model)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + ethnicity + gender + age + cls_perc_eval + 
    ##     cls_level + cls_credits, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8990 -0.3190  0.0892  0.3728  1.0741 
    ## 
    ## Coefficients:
    ##                        Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            3.414586   0.203019  16.819  < 2e-16 ***
    ## bty_avg                0.064639   0.016394   3.943 9.32e-05 ***
    ## ethnicitynot minority  0.242287   0.071392   3.394 0.000750 ***
    ## gendermale             0.181179   0.050138   3.614 0.000336 ***
    ## age                   -0.005020   0.002623  -1.914 0.056252 .  
    ## cls_perc_eval          0.005148   0.001449   3.554 0.000420 ***
    ## cls_levelupper        -0.015052   0.053163  -0.283 0.777199    
    ## cls_creditsone credit  0.522498   0.110098   4.746 2.79e-06 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5043 on 455 degrees of freedom
    ## Multiple R-squared:  0.1532, Adjusted R-squared:  0.1401 
    ## F-statistic: 11.76 on 7 and 455 DF,  p-value: 8.752e-14

This reduced model accounts for the data the best.

score= 3.41 + (bty\_avg \* .0646) + (ethnicitity \* .2423) + (gender \*
.1811) + (age \* -0.0050) (cls\_perc\_eval \* .0051) + (cls\_level \*
-.0151) + (cls\_credit \* .5225)

### Exercise 16

> Interpret the slopes of one numerical and one categorical predictor
> based on your final model.

cls\_level (-.0151) tells us that the higher level the course is, the
lower the eval is likely to be.

age (=.0050) tells us that the older a professor is, the lower their
eval is likely to be.

### Exercise 17

> Based on your final model, describe the characteristics of a professor
> and course at University of Texas at Austin that would be associated
> with a high evaluation score.

An attractive, young, white male professor teaching a multiple credit
freshman course.

### Exercise 18

> Would you be comfortable generalizing your conclusions to apply to
> professors generally (at any university)? Why or why not?

Not remotely, as this is only a single university and we don’t know how
it might change on a different campus, in a different city, in a
different state, in a different country. This could be entirely
idiosyncratic to UT Austin.

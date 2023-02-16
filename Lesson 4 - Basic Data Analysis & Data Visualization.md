# Index
- [Lesson 0 - Introduction to R](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%200%20-%20Introduction%20to%20R.md) 
- [Lesson 1 - Basic Data Types & Structures](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%201%20-%20%20Basic%20Data%20Types%20%26%20Structures.md) 
- [Lesson 2 - Importing & Exporting Data in R](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%202%20-%20Importing%20&%20Exporting%20Data%20in%20R.md) 
- [Lesson 3 - Manipulating Dataframes using the Tidyverse & Conditional and Iterative Statements](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%203%20-%20Manipulating%20Dataframes%20using%20the%20Tidyverse%20%26%20Conditional%20and%20Iterative%20Statements.md) 
- [Lesson 3.1 - Conditional & Iterative Statements](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%203.1%20-%20Conditional%20%26%20Iterative%20Statements.md) 
# Lesson 4 - Basic Data Analysis & Data Visualization

---
title: "Lesson 4 - Basic Data Analysis & Data Visualization"
---
In this lesson, we cover ways to conduct basic linear regression, anova, and  plotting. Additionally, we also cover how to use user-defined functions.

## Data Analysis & Plotting
----
#### **R Code:**
```R
data <- read.csv("C:/Users/donis/Documents/R Workshop/iris.csv")
```
----

`R` has base functions to conduct regression and ANOVA analyses.

For linear regression you can use `R`'s built-in `lm()` function. The form for the regression equation is `Dependent Variable ~ Independent Variable`. Also, you need to use the `data =` argument so that `lm()` knows that you are referring to variable names inside your data frame. You can see the results of the regression model using `R`'s built-in `summary()`function. 

`Pr(>|t|)` is the p-value if you see an asterisk(`*`) next to the number, your variable is significant.

----
#### **R Code:**
```R
#`lm()` outputs an `lm` object that you can save inside a variable
mod <-  lm(formula = Sepal.Length ~ Petal.Width, data = data)

summary(mod)
```
#### **Output:**

![Screenshot (47)](https://user-images.githubusercontent.com/112973674/219263921-c68d332a-43f6-4661-ae90-9ff6cd3f4146.png)

----
`R` also has a built-in `glm()` function that can also be used for linear regression; however `glm()` includes an argument (`family =`), which allows you to change the error distribution and link function used in your model. This allows you to perform different types of regression analysis such as binomial regression (`family = binomial`) and poisson regression (`family = binomial`).

----
#### **R Code:**
```R
#Linear regression using glm gives the same results as lm
mod_glm <- glm(formula = Sepal.Length ~ Petal.Width, data = data, family = "gaussian")
summary(mod_glm)
```
#### **Output:**
![Screenshot (48)](https://user-images.githubusercontent.com/112973674/219264050-4bb64fb0-191d-4ea0-b4c3-5035a887625e.png)

----

Here, we add an additional variable to the model.

----
#### **R Code:**
```R
mod_extended <-  lm(Sepal.Length ~ Petal.Width + Petal.Length, data = data)

summary(mod_extended)
```
#### **Output:**

![Screenshot (49)](https://user-images.githubusercontent.com/112973674/219264151-5612dcfc-0b24-427b-94e2-cb7a7af966bc.png)

----
We can use `R`'s built-in `anova()` function to see which model is better (reduces the residuals).

----
#### **R Code:**
```R
anova(mod,mod_extended)
```
#### **Output:**
![Screenshot (50)](https://user-images.githubusercontent.com/112973674/219264229-a7328cdb-3804-4bcf-b9c3-36b83f1804d0.png)


----
The `plot()` function can be used to conduct regression diagnostics pertaining to normality of residuals, heteroscedasticity, and leverage. 

----
#### **R Code:**
```R
plot(mod)
```
----

The `hist()` function can be used to create histograms. Here, we create a histogram the residuals from our model, which is extracted using `resid()`. The `main =` argument is used to title the histogram and the `xlab =` argument is used to title the x-axis of the histogram.

----
#### **R Code:**
```R
hist(resid(mod),main = "Histogram", xlab = "Residuals")
```
#### **Output:**
![Screenshot (51)](https://user-images.githubusercontent.com/112973674/219264307-eb9e0482-bdf5-4e4f-b831-95ff0ae354b7.png)


----
`R`'s built-in `aov()` function can be used to perform an ANOVA. Here we regress a continuous variable "Sepal.Length" onto a categorical variable "Species". The same structure for the equation that was used for `lm()` and `glm()` is used for `aov()`.

----
#### **R Code:**
```R
aov_model <- aov(Sepal.Length ~ Species, data = data)

summary(aov_model)
```
#### **Output:**

![Screenshot (52)](https://user-images.githubusercontent.com/112973674/219264418-766b376a-f220-4de7-97de-40bb9a9ccbf0.png)

----

The ANOVA above shows that the sepal length is different among the species of flowers; however, we don't know which species, if not all, are significantly different. We can do two things:

- We can conduct a post-hoc analysis such as a Tukey test (`TukeyHSD()`) or pairwise t-test (`pairwise.t.test()`) using bonferonni's correction to determine which contrasts are significantly different while accounting for multiple comparisons.

----
#### **R Code:**
```R
TukeyHSD(aov_model)
```
#### **Output:**
![Screenshot (53)](https://user-images.githubusercontent.com/112973674/219264503-23c17ac0-c602-4f65-b4a1-9aac6877b8e4.png)


----
#### **R Code:**
```R
pairwise.t.test(x = data$Sepal.Length, g = data$Species, p.adjust.method = "bonferroni")
```
#### **Output:**

![Screenshot (54)](https://user-images.githubusercontent.com/112973674/219264589-1fda8e90-b309-499a-b1de-c28c25fccfb1.png)

----
- We can use `lm()` or `glm()` for linear regression with categorical predictors if we are only interested in seeing the difference in means between a specific reference group and all other groups. The mean of the reference group is the intercept and the beta coefficient for the other groups are the difference in mean between that group and the reference group. This analysis can be used to determine which groups significantly differ from the reference group.

----
#### **R Code:**
```R
mod <- lm(Sepal.Length ~ Species, data = data)

summary(mod)
```
#### **Output:**
![Screenshot (55)](https://user-images.githubusercontent.com/112973674/219264677-3efc8188-d370-4ece-850d-399a430962e1.png)

----
To prove that the intercept is the mean sepal length of the setosa species, we will use `which()` to get the indices of data$Species that is equal to setosa. The `which()` function is useful for obtaining the indices of values in a vector that meet a logical condition. The individual columns in a data frame can be treated as a vector since it is a one dimensional object.

----
#### **R Code:**
```R
which(data$Species == "setosa")
```

#### **Output:**

<p>
     
```
   [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
   [30] 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50
```
<p>
     
----
We can use these indices to get the rows of the "Sepal Length" column for only the "setosa" species. Then obtain the mean.

----
#### **R Code:**
```R
mean(data[which(data$Species == "setosa"),"Sepal.Length"])
```
#### **Output:**

<p>
     
```
   [1] 5.006
```
<p>     
     
----
     
We can also get the difference in the means of the other species and the "setosa" species.
     
----
#### **R Code:**
```R
mean(data[which(data$Species == "versicolor"),"Sepal.Length"]) - mean(data[which(data$Species == "setosa"),"Sepal.Length"]) 
```
#### **Output:**

<p>
     
```
   [1] 0.93
```
<p>     
     
  
----
#### **R Code:**
```R
mean(data[which(data$Species == "virginica"),"Sepal.Length"]) - mean(data[which(data$Species == "setosa"),"Sepal.Length"]) 
```
#### **Output:**

<p>
     
```
   [1] 1.582
```
<p>     
     
  
----

We can use `R`'s built-in `relevel()` function to change the reference group for our regression model.

```R
#Change to factor
data$Species <- factor(data$Species)

levels(data$Species)

data$Species <- relevel(data$Species, ref = "virginica")

levels(data$Species)

```
#### **Output:**

<p>
     
```
   [1] "setosa"     "versicolor" "virginica" 
   [1] "virginica"  "setosa"     "versicolor"
```
<p>     
     
  
----  
     
Here we can see reference group (intercept) has changed due to reveling.
     
----
#### **R Code:**       
```R

mod <- lm(Sepal.Length ~ Species, data = data)

summary(mod)
```
#### **Output:**

![Screenshot (56)](https://user-images.githubusercontent.com/112973674/219264905-cd91eeb2-a22f-48fc-81c0-c25b5b370fd7.png)

  
----  
       
The `plot()` function can be used to create a scatterplot, the regression line is created using `abline()`.
       
----
#### **R Code:**         
```R
# Plot a scatter plot
plot(data$Petal.Width, data$Sepal.Length,
     xlab = "Independent Variable", ylab = "Dependent Variable", 
     main = "Scatter Plot of Independent vs. Dependent Variable")
mod <- lm(formula = Sepal.Length ~ Petal.Width, data = data)
abline(mod)
```
#### **Output:**

![Screenshot (57)](https://user-images.githubusercontent.com/112973674/219265025-0d1ced8e-3d98-4d4f-85ff-816d846cf07f.png)


----
You can also use the `ggplot()` function the ggplot2 package, which is also installed when you install the Tidyverse. With ggplot, the plus sign is used to add additional features to your plot `+` . Overall, ggplot allows for more customization of your plots.

----
#### **R Code:**       
```R

# Plot a scatter plot using ggplot2
ggplot(data, aes(x = Petal.Width, y = Sepal.Length)) +
  geom_point() + 
  #method = lm creates the regression line
  geom_smooth(method = "lm", se = FALSE) +
  labs(title = "Petal Width vs. Sepal Length", x = "Petal Width" , y = "Sepal Length")
```
#### **Output:**


![Screenshot (58)](https://user-images.githubusercontent.com/112973674/219265139-dbd67149-b4a2-4041-8f88-3fb23a7e14f0.png)


----

## User-defined Functions

In `R`, you have the ability to create your own functions using `function()`. If there is a specific set of operations that needs to be repeated, instead of rewriting the code, you can assign that code to a variable and use that variable as a function, similar to how you use `R`'s built-in function. Additionally, in you function, you can create your own names for your own arguments and have as many arguments that you need. Furthermore, functions are insulated. All variables have a scope, which is the region in your program where the variable is declared. This scope, determines where your variable can be accessed accessed in your code. For instance, all variables that are declared outside functions are global variables, they can be accessed outside of functions or inside of functions. Variables declared inside functions are local and cannot be accessed outside of functions. This is why `return()` or the super assignment operator `<<-` needs to be used to access the outputs of a function.

General structure of a function:
```
variable <- function(argument1,argument2,...){
Code 1
Code 2
}
```
Let's say you are conducting multiple regression analysis, where you need to find the Residual Sum of Squares (RSS) of multiple different models, you can create a reusable function to do so. 
```R
#Creating a variable named rss, the same name will be used in the functions.
rss <- 0
# `predict` allows you to use the model parameters to get the predicted response for each of your participants 
# and `sum` is used to add the squared difference of the predicted and actual response

rss_v1 <- function(model){
  rss <- sum((data$Sepal.Length - predict(model))^2)
  return(rss)
}

rss_v2 <- function(model){
  rss <<- sum((data$Sepal.Length - predict(model))^2)
}
```


Notice how despite the same variable name being used in the function, the "rss" variable declared outside the function has not changed.

----
#### **R Code:**     
```R
rss_v1(mod_1)

rss
```
#### **Output:**

<p>
     
```
   [1] 33.81489
   [1] 33.81489
```
<p>     
     
  
----     
     
Here, `rss_v2()` uses the super assignment operator (`<<-`), which overwrites the original value assigned to rss. Even if we didn't create a variable named "rss", the super assignment operator would have created a global variable named "rss". 
         
----
#### **R Code:**           
```R
rss_v2(mod_1)

rss
```
#### **Output:**

<p>
     
```
   [1] 33.81489

```
<p>     
     
  
----

[Previous Lesson](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%203.1%20-%20Conditional%20%26%20Iterative%20Statements.md) 

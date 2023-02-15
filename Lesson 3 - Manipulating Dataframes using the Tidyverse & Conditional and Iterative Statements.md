
# Index
- [Lesson 0 - Introduction to R](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%200%20-%20Introduction%20to%20R.md) 
- [Lesson 1 - Basic Data Types & Structures](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%201%20-%20%20Basic%20Data%20Types%20%26%20Structures.md) 
- [Lesson 2 - Importing & Exporting Data in R](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%202%20-%20Importing%20&%20Exporting%20Data%20in%20R.md) 
- [Lesson 3.1 - Conditional & Iterative Statements](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%203.1%20-%20Conditional%20%26%20Iterative%20Statements.md) 
- [Lesson 4 - Basic Data Analysis & Data Visualisation](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%204%20-%20Basic%20Data%20Analysis%20%26%20Data%20Visualization.md) 


# Lesson 3 - Manipulating Data Frames using the Tidyverse & Conditional and Iterative Statements


In this lesson, we will cover data manipulation using base `R` functions, conditional and iterative statements, and functions from popular packages in the Tidyverse such as tidyr & dplyr.

## Tidyverse

The [Tidyverse](https://www.tidyverse.org/) is collection of several `R` packages that offers functions that makes completing data science related tasks, such as manipulation of data frames, easier to complete in `R`.

Sometimes, before you conduct an analysis, you may need to log transform your data, scale your data, filter out certain participants, etc.

The tidyverse must be installed and the specific packages in the tidyverse must be loaded in.

----
#### **R Code:**
```R
install.packages("tidyverse")

library(tidyr)

library(dplyr)
```
----

**Note: During some sessions, you may need to load in multiple packages in your current `R` session, there is a great `R` package named pacman, which allows you to easily load in multiple packages at once.**

----
#### **R Code:**
```R
install.packages("pacman")

pacman::p_load(dplyr,tidyr)
```
----

#### **R Code:**
```R
data <- read.csv("C:/Users/donis/Documents/R Workshop/iris.csv")

#The `head()` function shows the first few rows of your data frame
head(data)
```

#### **Output:**
![Screenshot (32)](https://user-images.githubusercontent.com/112973674/219190086-b7a1f1d2-b6b7-41b8-be84-b79b8eda5005.png)



----

When you load in dplyr or tidyr, you have access to a new operator - the pipe operator `%>%`. This operator is useful when you need to pass the outputs of one function into another or chain multiple operations together. `dataframe %>% ` allows you to use column names from your dataframe in the next operation or allows you to filter contents in a dataframe. Think of the pipe operator as an assembly line that gives the output of its task to the next person in line.

----

#### **R Code:**
```R
#The dataframe is used as the input for colnames. This is the same as colnames(data)
data %>% colnames()
```
#### **Output:**

<p>

```
  [1] "X" "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width" 
  [6] "Species" 
  
```

----

### Mutating columns
  
----
Using the `mutate()` function you can create a simultaneously assign a transformed column to a new column while retaining the old column or transform a column and assign the transformed column back to itself (overwriting).

----

#### **R Code:**
```R
# Assigning the outputs of these operations back into data.
data <- data %>% mutate(Sepal.Length_Log = log(Sepal.Length))

data <- data %>% mutate(Sepal.Length = scale(Sepal.Length))
  
head(data)
```
#### **Output:**

![Screenshot (31)](https://user-images.githubusercontent.com/112973674/219188302-7c00ddaf-3518-4473-8a4e-a7e698fe0fd7.png)

----

### Summarising groups

----
In some instances, you may need a summary of descriptive statistics of certain groups of participants in your data frame. You can use `group_by()`, which is a function that allows you to perform operations based on groups that are defined by the variables in the column that you are grouping by. Here, we group our data based on species and use some of `R`'s built-in functions for basic descriptive statistics on each species sepal width. Our new data will summarize each species mean (`mean()`), variance (`var()`), standard deviation (`sd()`), max (`max()`), and min (`min()`) sepal width.

----
#### **R Code:**
```R
# Summarize data
summary_data <- data %>%
  group_by(Species) %>%
  summarize(mean = mean(Sepal.Width),
            variance = var(Sepal.Width),
            std_dev = sd(Sepal.Width),
            max = max(Sepal.Width),
            min = min(Sepal.Width))

head(summary_data)
```
  
#### **Output:**

![Screenshot (34)](https://user-images.githubusercontent.com/112973674/219195159-54012ea0-cfb9-41cd-8663-372dd3b66e66.png)



----

### Filtering rows

----
Sometimes you may need to remove particular groups from your data frame in preparation for an analysis. Combining dplyr's `group_by()` and `filter()` can remove or retain particular groups of interest. Here we use the 'not equal to' operator (`!=`) to exclude the setosa species from our data frame and assign this output to a new data frame.
  
----
#### **R Code:**

```R
reduced_data <- data %>% group_by(Species) %>% filter(Species != "setosa") 
```

----
Here, we accomplish the same task as above, instead, we use the `%in%` logical operator to retain the names of the species inside of a vector. Any species not inside the vector (setosa) will be excluded.
#### **R Code:**
```R
reduced_data <- data %>% group_by(Species) %>% 
  filter(Species %in% c("versicolor", "virginica"))
```
----
#### **R Code:**
```R
reduced_data <- data %>% filter(!is.na(Sepal.Length) & !is.na(Sepal.Width)) 
```
---- 
We can use one of `R`'s built-in `factor()` function, which is used to categorical data and use summary `R`'s built-in `summary()` function to summarize the Species column of our old and new data frame. Our new data frame no longer includes the rows associated with the setosa species. 

----
#### **R Code:**
```R
#Result of using summary() on a column that is not a factor
summary(data$Species)

#Factor species in our new and old data frame

data$Species <- factor(data$Species)
reduced_data$Species <- factor(reduced_data$Species)

#Summary and use nrow() to see the number of rows each data frame has
summary(data$Species)
nrow(data)
summary(reduced_data$Species)
nrow(reduced_data)


```
 #### **Output:** 
  
 <p>
 
 ```
    Length     Class      Mode 
      150 character character 
   
    setosa versicolor  virginica 
        50         50         50 
   
   [1] 150
   
    versicolor  virginica 
        50         50 
   
   [1] 100
 ```
   
 <p>
   
----
   
#### Complete Cases

----
   

Some instances, you may only want complete data, you can use `R`'s built-in `complete.cases()` function to get the participants with complete data.

The `.` is a shortcut to the output of the previous step. In this case, `.` is just `data`. Each function that receives the output from the pipe operator has an implicit dot.

----
#### **R Code:**
```R
#All work
complete_data <- data %>% filter(complete.cases(.))

complete_data <- data %>% filter(.,complete.cases(.))

complete_data <- data %>% complete.cases(.)

complete_data <- data %>% complete.cases()
```
----
In certain cases, such as having a function inside a function `filter(complete.cases(.))`. If you need the output of the previous operation as the input for the outermost and innermost function, you need to add an explicit dot for the input of the inner function because the outermost function already used the implicit dot (`filter(complete.cases(.))` is actually `filter(.,complete.cases(.))` which translates to `filter(data,complete.cases(data))` since the previous operation is just the entire dataframe).

----
### Selecting columns

----
We can use dplyr's `select()` function to select specific columns of a data frame.
#### **R Code:**
```R
sepal_data <- data %>% select(c("Sepal.Length","Sepal.Width"))

colnames(sepal_data)

dim(sepal_data)
```
   
#### **Output:** 
  
 <p>
 
 ```
    [1] "Sepal.Length" "Sepal.Width" 
    [1] 150   2
 ```
   
 <p>
 
----
This code produces the same as above but uses dplyr's `matches()` function to get all column names that have "Sepal" or "sepal" in the name (`matches()` is not case sensitive).

----
#### **R Code:**
```R
sepal_data <- data %>% select(matches("Sepal"))

colnames(sepal_data)

dim(sepal_data)
```
 #### **Output:** 
  
 <p>
 
 ```
    [1] "Sepal.Length" "Sepal.Width" 
    [1] 150   2
 ```
   
 <p>
   
----

## Conditional & Iterative Statements

Data manipulation can be a repetitive task if you need to perform the same or multiple operations on several columns of a data frame. Conditional and iterative statements can be combined to automate this task.

### Logical expressions

Logical expressions returns a `TRUE` or `FALSE` value. Logical expressions are made using logical operators. 

`R` has a few logical operators that can return a `TRUE` or `FALSE` value:

- `>` : Greater than operator, evaluates if a **numeric** object on the left of the operator is greater than the numeric object to the right of the operator.

- `<`: Less than operator, evaluates if the **numeric** object on the left of the sign is less than the numeric object to the right of the operator.

- `=>` : Greater than operator or equal operator, evaluates if a **numeric** object on the left of the operator is greater than or equal to the numeric object to the right of the operator.

- `=<`: Less than operator, evaluates if the **numeric** object on the left of the sign is less than or equal to the numeric object to the right of the operator.

- `==`: Equal to operator, evaluates if two objects (logical, numeric, character) are equal to each other.

- `!=` : Not equal operator, evaluates of the object to the left does not equal the object to the right.

----
#### **R Code:**
```R
5 > 2
6 != 6
```
   
#### **Output:** 
  
 <p>
 
 ```
    [1] TRUE
    [1] FALSE
 ```
   
 <p>
 
----

### Conditional Statements

----
   
Conditional Statements (if-else statements) execute a block of code when a certain condition, specified by the user, has been met.

The returned `TRUE` or `FALSE` value from a logical expression such as `5 > 2` is used by the the conditional statements to determine if a code block should be run. If the returned value is `TRUE` then the code block will run, if it is `FALSE` the code block will not be ran.

The conditional statements in `R`:

- `if()` statements: evaluates if a certain condition returns as `TRUE`. If `TRUE` is returned, then the code block is executed.

The structure of if statements (most conditional and iterative statements in `R`).

The expression goes inside the parenthesis, and the code block goes inside the curly braces. 

```
if(logical expression){
  Code 1
  Code 2
}
```

- `else if()` statements: Only used after an `if()` statement if you want to evaluate another condition and activate an alternative block of code if that alternative condition is met. The code under this statement will activate if the logical expression in the first `if()` statement returns `FALSE` and the logical expression in `else if()` returns `TRUE`.


```
if(logical expression){
  Code 1
  Code 2
} else if {
  Code 1
  Code 2
}
```

- `else{}` statements: Only used after an `if()` or `else if()` statement if you want to activate another block of code in the event the logical expressions in  `if()` or `else if()` returns as `FALSE`. This statement does not evaluate a logical condition which is why it does not have open parenthesis. 


```
if(logical expression){
  Code 1
  Code 2
} else if {
  Code 1
  Code 2
} else{
  Code 1
  Code 2
}
```


```
if(logical expression){
  Code 1
  Code 2
} else{
  Code 1
  Code 2
}
```
----
### Iterative Statements

Iterative statements (loops) are used to execute the same block of code several times. 

There are two common iterative statements:

- `for()`: iterates over (loops through) multiple values in a vector, list, etc, and executes a block of code. 

General structure:

```
for(iteration variable in vector){
  statement 1 
  statement 2
}
```
The **iteration variable** is a random variable that you choose. It is used to keep track of the current iteration of the loop, and its value changes with each iteration.


- `while(){}`: repeatedly executes a block of code as long as a certain condition is met. You can think of it as combining the evaluative aspect of an `if` statement and the repetitive/looping aspect of a `for` statement. If the logical expression returns TRUE, the block of code will keep executing. The looping stops when the logical expression returns `FALSE`.

General structure:

```
while(logical expression){
  statement 1 
  statement 2
}
```

```R
#Multi-assignment; assigning the same dataframe to 3 variables
data <- data_2 <- data_3 <- read.csv("C:/Users/donis/Documents/R Workshop/iris.csv")

```

Here we can use a for loop to mean-center all columns that are numeric and factor all columns that are not numeric.

`ncol()` returns the total number of columns that dataframe has. The iris dataframe has 6 columns, `2:ncol(data)` is the same as `2:6`. In this first for loop, `i` will take on a new value in `2:6` for each iteration, in the first iteration, `i` will equal 2, in the second iteration `i` will equal 3 and in the last iteration, it will equal six. The looping will stop was `i` is equal to last element in the vector and the code for the last element has been executed. Since `i` takes on a number, we will be using `i` to index our dataframe.

Within the for loop is an if-else statement, `is.numeric()` returns either a `TRUE` or `FALSE` value, it is `TRUE` is the data type within a vector is numeric and `FALSE` if it is not. When, `is.numeric()` returns a `TRUE` value, the code under the if statement will be executed, in this case, the data will be scaled using `R`'s built in `scale()`. To mean-center with `scale` we set `center = TRUE` and `scale = FALSE`. If we wanted to z-score we would set `center = TRUE` and `scale = TRUE`.

**Note: In `R`, you can use `T` in place of `TRUE` and `F` in place of `FALSE`.**

If `is.numeric()` returns `FALSE`, instead of mean-centering the column, the `else` statement will activate and the column will be factored using `R`'s built in `factor()` function.

----
#### **R Code:**
```R

for(i in 2:ncol(data)){
  if(is.numeric(data[,i])){
    print(i)
    print(is.numeric(data[,i]))
    print("Mean-center")
    scale(data[,i], center = T, scale = F)
  } else{
    print(i)
    print(is.numeric(data[,i]))
    print("Factor")
    factor(data[,i])
  }
}

#Note how iteration variable gets reassigned every iteration and for the final iteration, the else statement was activated because `is.numeric()` returned `FALSE`.
```
#### **Output:**

<p>

```
  [1] 2
  [1] TRUE
  [1] "Mean-center"
  [1] 3
  [1] TRUE
  [1] "Mean-center"
  [1] 4
  [1] TRUE
  [1] "Mean-center"
  [1] 5
  [1] TRUE
  [1] "Mean-center"
  [1] 6
  [1] FALSE
  [1] "Factor"
  
```

----
The for loop above executes this block of code six times.

For the first iteration, `i = 2`. The else statement is not activated.

```
for(i in 2:ncol(data)){
  if(is.numeric(data[,2])){
    print(2)
    print(is.numeric(data[,2]))
    print("Mean-center")
    scale(data[,2], center = T, scale = F)
  } else{
    print(2)
    print(is.numeric(data[,2]))
    print("Factor")
    factor(data[,2])
  }
}
```

For the second iteration, `i = 3`. The else statement is not activated.
```
for(i in 2:ncol(data)){
  if(is.numeric(data[,3])){
    print(3)
    print(is.numeric(data[,3]))
    print("Mean-center")
    scale(data[,3], center = T, scale = F)
  } else{
    print(3)
    print(is.numeric(data[,3]))
    print("Factor")
    factor(data[,3])
  }
}
```
For the last iteration, `i = 6`. The else statement is activated.
```
for(i in 2:ncol(data)){
  if(is.numeric(data[,6])){
    print(6)
    print(is.numeric(data[,6]))
    print("Mean-center")
    scale(data[,6], center = T, scale = F)
  } else{
    print(6)
    print(is.numeric(data[,6]))
    print("Factor")
    factor(data[,6])
  }
}
```


This for loop does the same as the above for loop; however instead instead of using numbers for indexing, we use the names of the columns for indexing. 

----
#### **R Code:**
```R
#Printing the column names
for(name in colnames(data_2[,2:ncol(data_2)])){
  if(name != "Species"){
    print(name)
    print(name != "Species")
    print("Mean-center")
    scale(data_2[,name], center = T, scale = T)
  }
  else{
    print(name)
    print(name != "Species")
    print("Factor")
    factor(data_2[,name])
  }
}

```
#### **Output:**

<p>

```
  [1] "Sepal.Length"
  [1] TRUE
  [1] "Mean-center"
  [1] "Sepal.Width"
  [1] TRUE
  [1] "Mean-center"
  [1] "Petal.Length"
  [1] TRUE
  [1] "Mean-center"
  [1] "Petal.Width"
  [1] TRUE
  [1] "Mean-center"
  [1] "Species"
  [1] FALSE
  [1] "Factor"
  
```
----
  
Here, we use a `while` loop. We create a variable `count <- 1` and assign `1` to it, The logical expression in the while loop returns `TRUE` if the count is less.

----
#### **R Code:**
```R
count <- 1

while(count <= ncol(data_3)){
  if(is.numeric(data_3[,i])){
    scale(data_3[,i], center = T, scale = T)
  }
  else{
    factor(data_3[,i])
  }
  count <- count + 1
  print(count)
  print(count <= ncol(data_3))
}
```
#### **Output:**

<p>

```
  [1] 2
  [1] TRUE
  [1] 3
  [1] TRUE
  [1] 4
  [1] TRUE
  [1] 5
  [1] TRUE
  [1] 6
  [1] TRUE
  [1] 7
  [1] FALSE
  
```
----                             
Be very cautious with `while` statements, if you have a logical condition that always returns `TRUE`, the while statement will run indefinitely (infinite loop) unless it encounters an error (such as an index going out of bounds) or program  becomes unresponsive and crashes. In the above `while` loop, if we do not add 1 to count for each iteration of the loop, then count would always be 1 and the logical expression `count <= ncol(data_3)`, which is essentially `1 <= 6` would always return `TRUE`. Just make sure that the logical condition in your while loop eventually returns `FALSE` or you use an `if` statement with `break` to stop the while loop if a certain condition is met.

----
#### **R Code:**
```R
x <- 1
while(TRUE) {
  if (x > 10) {
    #without `break` this loop would be infinite since the logical expression that is returned in the while loop is `TRUE`
    break
  }
  print(x)
  x <- x + 1
}
```
#### **Output:**

<p>

```
  [1] 1
  [1] 2
  [1] 3
  [1] 4
  [1] 5
  [1] 6
  [1] 7
  [1] 8
  [1] 9
  [1] 10
  
```
----  
[Next Topic: Lesson 3.1 - Conditional & Iterative Statements](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%203.1%20-%20Conditional%20%26%20Iterative%20Statements.md) 
  

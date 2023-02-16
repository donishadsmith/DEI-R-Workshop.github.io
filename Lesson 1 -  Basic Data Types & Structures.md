# Index
- [Lesson 0 - Introduction to R](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%200%20-%20Introduction%20to%20R.md) 
- [Lesson 1 - Basic Data Types & Structures](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%201%20-%20%20Basic%20Data%20Types%20%26%20Structures.md) 
- [Lesson 2 - Importing & Exporting Data in R](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%202%20-%20Importing%20&%20Exporting%20Data%20in%20R.md) 
- [Lesson 3 - Manipulating Dataframes using the Tidyverse & Conditional and Iterative Statements](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%203%20-%20Manipulating%20Dataframes%20using%20the%20Tidyverse%20%26%20Conditional%20and%20Iterative%20Statements.md) 
- [Lesson 4 - Basic Data Analysis & Data Visualisation](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%204%20-%20Basic%20Data%20Analysis%20%26%20Data%20Visualization.md) 

# Lesson 1 -  Basic Data Types & Structures

## Data Types

Data types are essentially classifications/grouping of data values that only permit certain operations to be performed on it.

`R` has several basic data types classes.

Some common classes of data types includes:

- Character: Anything inside a single (`''`) or double (`""`) quotes. The contents Within the string are irrelevant (ex. `'a'`,`"..2567, TRUE"`).
- Numeric: Any real number or rational numbers (ex. `4`, `9.01`).
- Integer: Whole numbers that include the `L` notation after it (ex. `4L`,`3L`);
- Logical: `TRUE` and `FALSE`.
- Complex: Numbers with a real and imaginary part (ex. `2i`, `4i`). The imaginary part uses the `i` notation.

## Variables and Basic Arithmatic

Variables are objects that can store data. Data is assigned to a variable via an assignment operator. R has two standard assignment operator: the equal sign (`=`) and the single headed arrow (`<-`).

*Note: The first character of a variable needs to start with a letter `a-z`or `A-Z`. In R, the symbols that variables can contain are the underscore (`_`) and the period (`.`).*

----
#### **R Code:**
```R
#Note how the result of each operation is stored in the variable
addition = 1 + 1
subtraction <- 2 - 1  
multiplication = 4 * 2
division <- 20/2
modulus = 5 %% 2
exponentiate <- 2^3

#Showing the results of these operations
addition
subtraction
multiplication
division
modulus
exponentiate 
```
#### **Output:**

<p>
  
```
  [1] 2
  [1] 1
  [1] 8
  [1] 10
  [1] 1
  [1] 8
```
  
<p>

----

Variables also adapt the properties of a datatype. To demonstrate this, we will use one of `R`'s base functions `class()`, which will tell you the class a data type belongs to. `R` like any other programming languages includes base functions that are automatically available once the `R` console is open. Functions are blocks of code that are assigned to a variable and take on the form `function_name()`. The open parenthesis are due to functions accepting an input/argument, to perform an operation on and produce an output. If you want to see the arguments that a function contains, you can use `?function_name` or `?function_name()` (ex. `?class` or `?class()`). You will be presented with a documentation page informing you of all the parameters the function has.

----
  
#### **R Code:**
  
```R
#This variable stored the output of a mathematical expression between two numeric data types. 

addition

class(addition)

#Variable used for addition
addition <- addition + 2
```
#### **Output:**

<p>
  
```
  [1] 2
  [1] "numeric"
```
  
<p>

----
            
            
#### What's the difference between the assignment operators?
Unlike the equal sign operator (`=`), the single arrow head operator (`<-`) can assign variables inside functions.

----
                                                                            
#### **R Code:**

```R
print(variable_1 <- "This sentence will print.")
print(variable_2 = "This sentence won't print.")
```
#### **Output:**

<p>
  
```
  [1] "This sentence will print."
  Error in print.default(variable_2 = "This sentence won't print.") :
  argument "x" is missing, with no default
```
  
<p>

----
  
## Data Structures

Data structures allow you to store multiple data types into a single variable. 

`R` has a few data types, some of the most commonly used ones are:

- vectors: one-dimensional object created using the `c()` function, where each data type is separated by a comma. In `R` vectors must be homogeneous (have the same data type). If a vector has different data types, `R` will try to coerce the entire vector to be the same. For instance, if a vector has a character data type and a numeric data type, `R` will turn the numeric data type into a character.

- lists: one-dimensional objects created using the `list()` function. In `R` lists can be heterogeneous (contain different data types).

- matrix: two-dimensional objects created using the `matrix()` function. 

- data frame; two-dimensional objects created using the `data.frame()` function.

- arrays: three-dimensional objects created using `array()`. Arrays will not be covered in this workshop.

----
#### **R Code:**

```R
#Note how the `TRUE` turns into 1 for the vector but not the list
my_vector <- c(1,2,4,TRUE)

my_list <- list(1,2,3,TRUE)

#Turning vector into matrix
my.matrix <- matrix(c(1,2,3,4),nrow = 2, ncol = 2) 

my_dataframe <- data.frame("Col_1" = c(1,2,3), "Col_2" = c(4,5,6), "Col3" = c(7,8,9))

my_vector
my_list
my.matrix
my_dataframe

```
#### **Output:**

<p>
  
```
   [1] 1 2 4 1
  
   [[1]]
   [1] 1

   [[2]]
   [1] 2

   [[3]]
   [1] 3

   [[4]]
   [1] TRUE

        [,1] [,2]
   [1,]    1    3
   [2,]    2    4
  
        Col_1 Col_2 Col3
   [1]   1     4    7
   [1]   2     5    8
   [1]   3     6    9
```
  
<p>
 
----
#### **R Code:**

```R
#`class()` will tell you the data structure a variable is too.
class(my_dataframe)
```

#### **Output:**

<p>
  
```
  [1] "data.frame"
```
  
<p>

---- 
  
In `R` if you want to generate a sequence of numbers for a vector you can use the colon (`:`) operator.

----
  
#### **R Code:**
  
```R
my_vector_1 <- 0:10

my_vector_2 <- c(0:7,50:60,100)

my_vector_1

my_vector_2

```
#### **Output:**

<p>
  
```
  [1]  0  1  2  3  4  5  6  7  8  9 10
  [1]  0   1   2   3   4   5   6   7  50  51  52  53  54  55  56  57  58  59
  [19]  60 100
```
  
<p>

----
  
`R` has built in vectorization where you can perform operations on each element of the vector.
  
----

#### **R Code:**
  
```R

new_my_vector_1 <- my_vector_1 * 10

new_my_vector_1
```
#### **Output:**

<p>
  
```
  [1]   0  10  20  30  40  50  60  70  80  90 100
```
  
<p>

----                   
                                  
If you need you need to generate a sequence of numbers with certain step sizes, you can use `seq()`, where the first argument is the starting number, the second is the ending number, and the third argument is the step size. 

**The order of the inputs for functions matter.** If you look at the documentation for seq using `?seq()` the first three arguments are from, to, and by (`seq(from, to, by,...)`). So if your inputs are in the correct position, you do not to write the name of the argument. The order of the inputs matter.

----
#### **R Code:**
 
```R
my_vector_3 <- seq(from = 0, to = 10,by = 2)

#Will produce the same as `my_vector_3` above.
my_vector_4 <- seq(0,10,2)

#Including the names of the arguments that you want your inputs to be set equal to allows you to include your inputs in any order.
my_vector_5 <- seq(by = 2, to = 10,from = 0,)

my_vector_3
my_vector_4
my_vector_5

```
#### **Output:**

<p>
  
```
  [1]  0  2  4  6  8 10
  [1]  0  2  4  6  8 10
  [1]  0  2  4  6  8 10
```
  
<p>

----
                             
If you need to perform matrix multiplication on a vector or matrix, use `%*%`. You may need to `t()` to transpose a matrix for the correct result.

----
#### **R Code:**
  
```R
my_vector_1 <- 1:3

my_vector_2 <- 4:6

matrix_multiplication_1 <- my_vector_1 %*% my_vector_2 # 1 * 1 output

matrix_multiplication_1

matrix_multiplication_2 <- my_vector_1 %*% t(my_vector_2) # 3 by 3 matrix

matrix_multiplication_2
```
#### **Output:**

<p>
  
```
          [,1]
   [1,]    32
          [,1] [,2] [,3]
   [1,]    4    5    6
   [2,]    8   10   12
   [3,]   12   15   18
```
  
<p>

----  
  
### Indexing

Indexing is used if you want to access specific values in a data structure. In`R`'s index starts at 1. 

There are two common ways to access contents inside data structures:

- `[]` : Square brackets only indexes with numbers.

- `$`: Dollar sign operator only indexes with names. Commonly used to access a specific column of a dataframe using the name of that column. You can use `colnames()` to determine the names of your columns, those are the names that must be used with the dollar sign operator.

----
#### **R Code:**
  
```R
my_vector
#Access the second value in my vector
my_vector[2]
#Indexing and changing the second value of my_vector
my_vector[2] <- "a"
#Note how everything is coerced into characters
my_vector

```
#### **Output:**

<p>
  
```
   [1] 1 2 4 1
   [1] 2
   [1] "1" "a" "4" "1"
```
  
<p>

----  
                  
                
For two-dimensional objects such as data frames, a comma is used to separate the dimensions. To access a row, the notation is (assuming the name of your dataframe is `data`) `data[row,]` and to access a column, the notation is `data[,column]` or `data$column_name`.

----
#### **R Code:**
  
```R
#Access row 1

my_dataframe[1,]

#Different ways to obtain more than one row, the same can be used for columns.

my_dataframe[1:2,]

my_dataframe[c(1,3),]

my_dataframe[c(1:2,3),]
```
#### **Output:**

<p>
  
```
      Col_1 Col_2 Col3
   [1]  1     4    7
  
       Col_1 Col_2 Col3
   [1]   1     4    7
   [1]   3     6    9
  
       Col_1 Col_2 Col3
   [1]   1     4    7
   [1]   2     5    8
   [1]   3     6    9
```
  
<p>

----  
 
#### **R Code:**  

```R
#Access the first column in my data frame
my_dataframe[,1]
#Print out the name of my columns using `colnames()`, `names()` also does the same thing but is often used for 1D data.
colnames(my_dataframe)
#Access the first column in my data frame using the column name
my_dataframe$Col_1
#You can also use the column name in the brackets
my_dataframe[,"Col_1"]
```
#### **Output:**

<p>
  
```
   [1] 1 2 3
   [1] "Col_1" "Col_2" "Col3" 
   [1] 1 2 3
   [1] 1 2 3
```
  
<p>
  
----
[Previous Lesson](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%200%20-%20Introduction%20to%20R.md)  | [Next Lesson](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%202%20-%20Importing%20%26%20Exporting%20Data%20in%20R.md)
  


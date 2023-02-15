# Index
- [Lesson 1 - Basic Data Types & Structures](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%201%20-%20%20Basic%20Data%20Types%20%26%20Structures.md) 
- [Lesson 2 - Importing & Exporting Data in R](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%202%20-%20Importing%20&%20Exporting%20Data%20in%20R.md) 
- [Lesson 3 - Manipulating Dataframes using the Tidyverse & Conditional and Iterative Statements](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%203%20-%20Manipulating%20Dataframes%20using%20the%20Tidyverse%20%26%20Conditional%20and%20Iterative%20Statements.md) 
- [Lesson 3.1 - Conditional & Iterative Statements](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%203.1%20-%20Conditional%20%26%20Iterative%20Statements.md) 
- [Lesson 4 - Basic Data Analysis & Data Visualisation](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%204%20-%20Basic%20Data%20Analysis%20%26%20Data%20Visualization.md) 
# Lesson 0 - Introduction to R 

In this lesson, we will cover what R and RStudio are.

## What is R?

`R` is a high-level programming language commonly used for data analysis and data visualization. 

Additionally, `R` is also an interpreted language. This means that the `R` interpreter reads a line of the program being executed, checks for incorrect syntax that will produce an error, translates `R` syntax into machine code (0's & 1's) to be executed by the computer, and prints the output of that line before proceeding to the next line. 

----
#### **R Code:**
```R
# In R, comments are created by adding the hashtag before your sentence so that the interpretor knows that they are comments.
print("Hello World!") #Interpreter reads and translates this line first
print("My name is _") #Then the interpreter reads and translates this line next
```
#### **Output:**

<p>
   
```
   [1] "Hello World!"
   [1] "My name is _"
```
   
</p>

----

Because each line is translated and executed one line at a time, if the interpreter detects a syntax error, it will stop executing the program and produce an error. Any code under the line producing the error will not be executed.

----
#### **R Code:**

```R
print("Hello World!") 
# This line will produce an error. Note how the first line is printed but neither the second nor third line are.
print("Incorrect syntax" 
print("My name is _") 
```
**Output:**

<p>

```
   [1] "Hello World!"
   Error: unexpected symbol in:
   "print("Incorrect syntax" 
   print"
```

</p>

----

## What is R Studio?

RStudio is an integrated development environment(IDE), which is a graphical user interface(GUI) that makes `R` easier to use.




[Next Lesson](https://github.com/donishadsmith/FIU-DEI-R-Workshop/blob/main/Lesson%201%20-%20%20Basic%20Data%20Types%20%26%20Structures.md)

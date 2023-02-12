
# Lesson 0 - Introduction to R 

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

## What is R Studio

RStudio is an integrated development environment(IDE), which is a graphical user interface(GUI) that makes R easier to use.



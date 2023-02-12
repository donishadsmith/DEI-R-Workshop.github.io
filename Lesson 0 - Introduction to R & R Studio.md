
# Lesson 0 - Introduction to R 

## What is R?

R is a high-level programming language commonly used for data analysis and data visualization. 

Additionally, R, like Python and Javascript, is an interpreted language. This means that the R interpretor reads each line of the program. Each line is read and checked to ensure that the rules of the language have been followed, translated into machine code (0's and 1's) to be executed by the computer, and the output is produced.

```R
# In R, comments are created by adding the hastag before your sentence so that the interpretor knows that they are comments.
print("Hello World!") #Interpretor reads and translates this line first
print("My name is _") #Then the interpretor reads and translates this line next
```
```R
[1] "Hello World!"
[1] "My name is _"
```
Because each line is translated and executed one line at a time, if the interpretor detects a syntax error, it will stop executing the program and produce an error. Any code under the line producing the error will not be executed.

```R
print("Hello World!") 
# This line will produce an error. Note how the first line is printed but neither the second nor third line are.
print("Incorrect syntax" 
print("My name is _") 
```
```R
[1] "Hello World!"
Error: unexpected symbol in:
"print("Incorrect syntax" 
print"
```

## What is R Studio

R Studio is an integrated development environment(IDE), which is a graphical user interface(GUI) that makes R easier to use.



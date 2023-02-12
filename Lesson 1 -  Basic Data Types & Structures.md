# Lesson 1 -  Basic Data Types & Structures

## Variables

Variables are objects that can contain a data type, multiple data types, a function, or a data structure.

### General rules of variables in R (rules broadly applicable to many other languages):

- The first character of a variable ALWAYS must be a letter from a-z or A-Z. A variable can a single letter (a) or a series of letters names (myvariable). In R, variables can contain numbers, the underscore and the period.Variables cannot contain any other symbols or symbols used for arithmetic operations or logical operations. While a1, my_variable, my.variable_2 are valid names for variables, 1a, my-var, var+1 are invalid variable names.

- As mentioned before, variables are written without quotes. For instance, "my_variable" is a data type from the character class while my_variable is a variable.

- Variables are case sensitive: ```my_variable```, ```My_Variable```, and ```MY_VARIABLE``` are all different and cannot be substituted for one another.

#The variable adopts the properties/attributes of the data type (or data structure) assigned to it. If you assign 1 into a variable called my_variable, then my_variable becomes a object that is treated like a numeric data type. Any valid operation that can be done to a numeric data type can be done to my_variable. Just as the interpreter, will see 1 + 1 as the addition of two numeric data types that equals 2, it will see my_variable + 1 as the addition of 1 and an object that contains the numeric data,1, that equals 2

#You can assign a variable that has been defined to an undefined variable. If I assign 1 to a variable named my_variable_1, this is a defined variable. I can then assign my_variable_1 to a new variable named my_variable 2. In this case, my_variable_1 and my_variable_2 are objects that contain the numeric data type, 1.

#It is possible to initialize a variable, which means you can create an "empty" variable, so that the interpreter knows that the variable does exist when you call that variable later in your script. There is a syntactically valid way to create these empty variables. 

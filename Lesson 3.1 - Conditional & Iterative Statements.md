
# Lesson 3.1 - Conditional & Iterative Statements


In this lesson will cover conditional and iterative statements in `R` more deeply. 

## Logical expressions

Logical expressions returns a `TRUE` or `FALSE` value. Logical expressions are made using logical operators.

`R` has a few logical operators that can return a `TRUE` or `FALSE` value.

- `>` : Greater than operator, evaluates if a **numeric** object on the left of the operator is greater than the numeric object to the right of the operator.

- `<`: Less than operator, evaluates if the **numeric** object on the left of the sign is less than the numeric object to the right of the operator.

- `=>` : Greater than operator or equal operator, evaluates if a **numeric** object on the left of the operator is greater than or equal to the numeric object to the right of the operator.

- `=<`: Less than operator, evaluates if the **numeric** object on the left of the sign is less than or equal to the numeric object to the right of the operator.

- `==`: Equal to operator, evaluates if two objects (logical, numeric, character) are equal to each other.

- `!=` : Not equal operator, evaluates of the object to the left does not equal the object to the right.

- `!()`: Logical negation operator, negates a logical expression within the parenthesis. If the statement inside the parenthesis returns `TRUE`, it will be reversed to `FALSE`, if the statement inside the parenthesis returns as `FALSE`, then it will be reversed to `TRUE`.

- `%in%`: Evaluates if the object to the left of the operator is inside the object to the right of the operator. Often used to assess of an object is in a list, vector, etc.

**All of these operators will return a `TRUE` or `FALSE` value**

----
#### **R Code:**
```R
5 > 2

5 < 2

5 <= 2

5 >= 2
```
#### **Output:**

<p>
  
```
  [1] TRUE
  [1] FALSE
  [1] FALSE
  [1] TRUE
```
<p>
----

```R
TRUE == FALSE

5 == 2

"a" == "a"

#Note how this expression returns TRUE, TRUE, FALSE
c(1,2,3) == c(1,2,5)

```



```R
5 != 2

5 !=5

```


*Note: how the logical values returned are reversed.*


```R
!(5 != 2 )

!(5 !=5 )
```



```R
5 %in% c(1:5)

"a" %in% list("a","b","c")

FALSE %in% c(TRUE,1,1)

```



```R
#Adding c() can turn c(1,2,3) == c(1,2,5) into a logical vector, which can be evaluated to return a single `TRUE` or `FALSE` value.

a <- c(1,2,3) == c(1,2,5)

#Checking the class of `a`

class(a)

#print `a`, you don't have to use `print()`
a

FALSE %in% c(c(1,2,3) == c(1,2,5)) 
FALSE %in% a
```


## Evaluating multiple logical expressions

There are two base `R` functions that can be used to evaluate multiple logical expressions. These functions can be used to evaluate a vector of logical expressions. A vector of logical statements will return a vector of logical values; however, there are two useful function and two useful notations to evaluate multiple logical expressions. :

- `any()`: If any of the logical statements in the vector returns TRUE, then this function will return TRUE for the entire vector.`any()` will only return `FALSE` if all logical statements in the vector are `FALSE`.


```R
c(3 > 2,5 < 5, 1 %in% c(0:5))
#Despite one statement returning `FALSE`, `any()` returns `TRUE`
any(3 > 2,5 < 5, 1 %in% c(0:5))

```



```R
a <- c(3 < 2,5 < 5, 1 %in% c(2:5))
a
any(a)
```



```R
c(3 > 2,5 == 5, 1 %in% c(1:5))

any(c(3 > 2,5 == 5, 1 %in% c(1:5)))
```

- `all()`: Evaluates a logical vector and returns `TRUE` if **ALL** logical expressions in the vector returns `TRUE`.


```R
#No expression returns `TRUE` so `all()` returns `FALSE`
a <- c(1 > 2, 5 < 5, "b" == c("v","n"))

a 

all(a)
```



```R
#All expressions returns `TRUE` so `all()` returns `TRUE`

a <- c(1 < 2, 5 == 5, "b" != "v")

a 

all(a)

```



```R
a <- c(1 < 2, 5 != 5, TRUE != FALSE)

a 

all(a)
```

- `&` : logical AND evaluates if two or more statements are TRUE, Like `all()` it will only return `TRUE` if all logical expressions return `TRUE`. Can also be used for indexing.
```R

4 < 6 & 5 == 5 & 7 > 6
4 < 6 & 5 != 5 & 7 > 6

my_vector  <- 1:10

my_vector[my_vector > 1 & my_vector < 6]

```


- `|` : logical AND evaluates if two or more statements are TRUE, Like `any()` it will return `TRUE` if any logical expressions return `TRUE`. Can also be used for indexing.


```R
4 < 6 | 5 == 5 | 7 > 6
4 < 6 | 5 != 5 | 7 > 6

my_vector[my_vector <= 3 | my_vector == 6]
```


##Conditional Statements

Conditional Statements (if-else statements) execute a block of code when a certain condition, specified by the user, has been met.

### If Statements

- `if()` statements: evaluates if a certain condition returns as `TRUE`. If `TRUE` is returned, then the code block is executed.

The structure of if statements (most conditional and iterative statements in R).

The expression goes inside the parenthesis, and the code block goes inside the curly braces. 
```
if(logical expression){
  Code 
  More code
}
```

```R
if(TRUE){
  print("When the expression is TRUE, this block is executed.")
}

#Note how only the sentence above is printed.

if(FALSE){
  print("When the expression is FALSE, this block is not executed.")
}
```


There may be instances, when you want to evaluate multiple expressions to activate a code block. For instance, you may want to know is  However, conditional statements only work if a single logical value (`TRUE` or `FALSE`) is returned. 


```R
if(c(TRUE,TRUE,TRUE)){
  print("This will produce an error.")
}
```

This is where `any()` and `all()` come in.

```R
a <- c(TRUE,TRUE,TRUE)

if(any(a)){
  print("When the expression is TRUE, this block is executed.")
}

if(all(a)){
  print("When the expression is TRUE, this block is executed.")
}
```



```R
x <- 5

y <- c(2 > 1, 5 %in% c(1:6), !(4 == 5))

#Note how the logical  
if(x > 2){
  print("This statement returns TRUE and will be printed.")
}

if(any(y)){
  print("This statement returns TRUE and will be printed.")
}

if(all(y)){
  print("This statement returns TRUE and will be printed.")
}
```

### Else statements

`else{}` statements do not evaluate expressions, they are only used to activate an alternative block of code if the `if()` statement above it returns `FALSE`. Since they do not accept an expression, not hoe `else{}` is followed by curly braces instead of parenthesis and curly braces.

General structure:

```
if(expression){
  statement 1
  statement 2
} else{
  statement 1
}
```

```R
a <- 10
b <- 20

if(a  >  b){
  #sprintf is a function can format, substitute objects in a string.
  # %s is used as a placeholder
  sprintf("%s IS greater than %s",a,b)
  } else {
      sprintf("%s IS NOT greater than %s",a,b)
  }

  
```

### Else statements


`else if(){}` statements do evaluate expressions, they are only used after an if statement to activate an alternative block of code if the `if()` statement above it returns `FALSE`.

General structure:

```
if(expression){
  statement 1
  statement 2
} else{
  statement 1
}
```

```R
a <- 10
b <- 10


if(a > b){
  sprintf("%s IS greater than %s",a,b)
  } else if (a == b){
      sprintf("%s EQUALS than %s",a,b)
  } 
```



```R
a <- 10
b <- 20

if(a > b){
  sprintf("%s IS greater than %s",a,b)
  } else if (a == b){
      sprintf("%s EQUALS than %s",a,b)
  } else{
      sprintf("%s IS NOT greater than %s",a,b)
  }
```



*Note: In these examples, only a single line of code was used; however, you can write multiple lines of code under each conditional statement.*


#Iterative Statements

Iterative statements (loops) are used to execute the same block of code several times. 

There are two common iterative statements:

-`for(){}`: iterates over (loops through) multiple values in a vector, list, etc, and executes a block of code.

General structure:

```
for(iteration variable in vector){
  statement 1 
  statement 2
}
```
The iteration variable is a random variable that you choose. It is used to keep track of the current iteration of the loop, and its value changes with each iteration.


```R
a <- 1:10
for(i in a){
  b <- i + 1
  print(b)
}
```


```R
a <- c("a","b","c")
for(letter in a){
  print(letter)
}
```


-`while(){}`: repeatedly executes a block of code as long as a certain condition is met. You can think of it as combining the evaluative aspect of an `if` statement and the repetitive/looping aspect of a `for` statement. If the logical expression returns TRUE, the block of code will keep executing. The looping stops when the logical expression returns `FALSE`.

General structure:

```
while(logical expression){
  statement 1 
  statement 2
}
```

```R
#Note how it stopped repeating once count < 6 returned as FALSE
count <- 1

while(count < 6){
  #Add 1 to count for each iteration
  count <- count + 1
  #Will stop counting when count equals 6
  print(count)
}
```





# Index

# Lesson 2 - Importing & Exporting Data in R

In this lesson, we will cover how to import and export data with common file extensions `.csv`,`.tsv`, & `.xlsx` into `R`. We will use one of `R`'s most populaular built-in datasets - `iris` as an example. 

## Importing Data

`R` has built-in functions to import export comma-separated values(csv) and tab-separated values(tsv) files. 

To import csv files into `R`, you can use `read.csv()` and to import tsv files, you can use `read.table()`

Both functions have multiple arguments; however, some arguments that are most commonly used are:

- `file =` : To specify the location of the file that you are importing. You can use the absolute path location (full path from the root) to your file or the relative path location (location relative to your current working directory)

- `header =` : This argument only accepts logical arguments (```TRUE``` or ```FALSE```) and defaults to ```header = TRUE```. If set to ```TRUE```, the first line in your will be used as the column names of your data frame. If set to ```FALSE```, `R` will use default column names for your data frame.

- `sep =` : This argument specifies the deliminator, a character that separates the values in your file. For `read.csv()` this argument defaults to `sep = ","` and for read.table() this argument defaults to `sep = ""` (which will recognize values separated by one or two spaces and tabs). You usually won't need to change this parameter, unless the deliminator is not separated by the character in the default argument.

*Note: Each argument must be separated by a comma.*

You can check your current working directory by using `getwd()` if you want to use a relative path to import your data. 

----
**R Code:**
```R
getwd()
```
**Output:**

<p>
  
  ```
  [1] "C:/Users/Documents/R MarkDown Files"
  ``` 
<p>

----
You can change your working directory using, `setwd()`

----
**R Code:**
```R
setwd("C:/Users/Documents/")
getwd()
```
----

#### Importing a csv file:

----
**R Code:**
```R
#Importing from absolute path location
data <- read.csv(file = "C:/Users/Documents/iris.csv", header = T, sep = ",")

#If your file is located in your current working directory, you can simply use the name of your file. 
#This would be the relative path location of your file.
data <- read.csv(file = "iris.csv", header = T, sep = ",")
```
----

#### Importing a tsv file:

----
**R Code:**
```R
data <- read.table(file = "C:/Users/Documents/iris.tsv", header = T, sep = "\t")
```
----
#### Importing an Excel file:

----
R does not have a built-in function to read Excel files. 

In R, you can download and install packages that will allow you to use additional useful functions, using the install.packages().The `install.packages()` function has a `repos =` argument to specify the download location of the package you wish to install. This argument automatically defaults to downloading packages from Comprehensive R Archive Network (CRAN) (`repos = "http://cran.us.r-project.org"`), which is the main repository for R packages. The majority of the R packages that you will need will already be on CRAN. 

`readxl` uses the `path =` as the argument to specify your file's location.
----
**R Code:**
```R
#Name of the package must be in quotes
install.packages("readxl")
```
----
To use the functions in a package, you can either:

- Load it into the `R`'s search path using `library()`.

----
**R Code:**
```R
#Name of the package should not be in quotes
library(readxl)
# The argument to specify your file location `path = `
data <- read_xlsx(path = "C:/Users/Documents/iris.xlsx")
```
----
- Access the contents in a package using the double colon operator(`::`).

----
**R Code:*
```R
data <- readxl::read_xlsx(path = "C:/Users/Documents/iris.xlsx")
```
----
## Exporting Data

R has built-in functions to save csv and tsv files.

To save csv files, you can use `write.csv()`, and the save tsv files you can use `write.tsv()`.

The most common arguments that you will use in these functions are:

- `x = ` : Specify the name of the object (variable) containing the data that you wish to save.
  
- `file = ` : To specify the location that you want your file to be saved and to specify the name of your file.
  
- `sep = ` : Specify what you want the values in you file to be separated by. For `write.csv()`, this argument defaults to `sep = ","` and will ignore any changes to this argument that you attempt make. 

#### Exporting csv file:

----
**R Code:**
```R
write.csv(x = "C:/Users/Documents/iris.csv")
```
----
#### Exporting tsv file:

----
**R Code:**
```R
write.table(x = data, file = "C:/Users/Documents/iris.tsv", sep = "\t")
```
----
#### Exporting Excel file:

----
R does not have a built-in function to export Excel files. A good package to use is `xlsx`. This package requires [Java](https://www.java.com/en/download/) to be installed on your machine to work.

`xlsx` also uses the `x =` and `file =` arguments but does not have a `sep =` argument.
        
----

**R Code:**
```R
install.packages("xlsx")
library(xlsx)

write.xlsx(x = data, file = "C:/Users/Documents/iris.xlsx")
```
----


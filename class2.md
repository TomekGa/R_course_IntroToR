Introduction to R - class 2
================
**Tomek Gaczorek**; <tomek.gaczorek@gmail.com>
11.11.22

<!-- **!!! Description of exercises is in green !!!** -->

### 1. R studio

RStudio is a shell and programming environment for the R language. It
makes working with R much easier and more intuitive by providing a user
interface to R features originally hidden behind R functions. However,
remember that all actions can be also performed within the classical R
console.

**Instalation**

Follow the [link](https://rstudio.com/products/rstudio/download/),
choose the appropriate operating system and install free RStudio
Desktop. Have in mind that R needs to be installed first.

**Appearance**

R Studio has three great advantages over classical R console:

-   saving and editing your code as a text file (.R)  
-   running any piece of previously written code (reanalysis)
-   displaying all R objects and variables saved in your computer memory
    at any given moment

The R Studio window consists of four main panels:

![<https://sfg-ucsb.github.io/fishery-manageR/images/rstudio_ide.png>](/home/tomek/Dropbox/Kurs_R/work_in_progress/rstudio_ide.png)

<!-- ![https://sfg-ucsb.github.io/fishery-manageR/images/rstudio_ide.png](C:\Users\Tomasz\Dropbox\Kurs_R\rstudio_ide.png) -->

1.  **Code editor** - write your code and save it in a text file (.R).
    You can run it anytime by highlighting given piece of code and
    clicking *Run* in right-top corner (also *Ctrl+R*).
2.  **Console** - Exactly the same console as in standard R (see Class
    1). Note that any line of code run from *Code editor* will appear in
    the console. To recall the lastly run line of code use *Arrow-up*
    (it works as a general way of browsing through the history of the
    executed commands).
3.  **Environment / History**
    -   Environment - check all variables and functions present in your
        computer’s memory (RAM). Have in mind they will be lost as soon
        as you close RStudio.
    -   History - access to the entire code run in a given RStudio
        session.
4.  **Files / Plots / Help / Packages**
    -   Files - manage files on your computer.
    -   Plots - preview generated plots before saving them.
    -   Help - access help page (often with examples) for a given
        function.
    -   Packages - manage all additionally installed modules.

**Ex 1. Create new script file (File \>\> New File \>\> R Script) and
save it. Write code for all subsequent exercises using Code editor.
Remember that to obtain any outcome/result you need to execute/run your
code first.**

**An advice**  
If you want to include some comments within a script file or “turn off”
chunk of code, type the hash before it (*\#*). Anything written until
the end of a given line will be ignored by R. To comment several lines
highlight them and use *Ctrl+Shift+c*. Repeat it to uncomment.

### 2. Working directory

Working directory is a folder on your computer where R is operating at
the moment. Think about it as a separate room for a given analysis. R
will look for and save all files in the working directory by default.
You can check current working directory by typing *getwd()*.

To set new working directory use *Session \>\> Set Working Directory
\>\> Choose Directory* or use *setwd()* function with a destination path
provided as an argument.

Unless you continue a previous analysis, ALWAYS set new working
directory.

**Ex 2. Create a new folder and set it as a working directory.**

**Curiosity**  
Although it is usually easier to create folders traditionally, using
your operating system, have in mind that you can also do it through R by
using *dir.create()* function.

### 3. “So it begins” - Théoden, 3019 TE

Before performing any new analysis make sure three things are done:

1.  An appropriate working directory is set.  
2.  New “R script” text file is created (*“File \>\> New File \>\>
    Rscript”*).
3.  Global environment is empty. You can clear it by clicking *broom
    icon* in the Environment panel or by typing *rm(list = ls())*

### 4. Data frame

![](/home/tomek/Dropbox/Kurs_R/work_in_progress/objects.png)

Data frame is something you probably know as a “table”. However it has
some unique characteristics:

1.  It always has a header. It means that each collumn must have its
    unique name. If names are not provided R creates them automatically
    as *V* (as “variable”) followed by the consecutive number.
2.  Table is always complete. It means that each collumn has the same
    number of rows. If some data are missing R puts *NA* (“not
    available”) in a given cell.
3.  An individual collumn of a data frame, similarly to vectors, can
    contain only one type of data, but different columns can be of
    different types.

**Curiosity**  
In R, there is also an object called *matrix* that will not be covered
during this course. It looks and behaves similar to the data frame but
all cells must contains the same type of data (often numbers). It is
usually used in mathematics (matrix operations) and graphics (image
encoding).

**Curiosity**  
Recently, the object called *tibble* is rising in popularity and
possibly will replace *data.frame* in the near future. The differences
between both are rather subtle and do not affect our exercises directly.
If you want to read more, follow the
[link](https://blog.rstudio.com/2016/03/24/tibble-1-0-0/).

### 5. Data import and display

Usually, data imported into R are in the form of text files. Commonly
used extensions:

-   .csv - comma-separated values - rows defined as lines of text,
    columns separated by commas
-   .tsv - tab-separated values - rows defined as lines of text, columns
    separated by tabs

**For Polish speakers**  
Using Polish versions of some software (e.g. Excel) with default
settings of the operating system may generate problems with *.csv* files
as comma is used as decimal delimiter. Excel (in polish) by default
creates *.csv* file with columns separated by semicolon (;). Then,
arguments of importing R functions need to be properly adjusted.

**Ex 3. Copy and execute the command below to download the file
‘CO2.csv’ we are going to work on, to your working directory:**

``` r
download.file(url = "https://dl.dropbox.com/s/41kxqpagkvimsle/CO2.csv?dl=1",
              destfile = paste(getwd(),"/CO2.csv",sep = ""))
```

R provides many training datasets that are built-in into R and can be
called directly by their names. List of them can be obtained by *data()*
function. Also, dataset description can be accessed by typing *?*
followed by its name. “CO2” dataset is one of them, however, we
downloaded it manually to learn how to import external datasets.

**Ex 4. Open dataset description for *CO2* dataset. Check the
description of research and the meaning of collumns’ headers. **

**Ex 5. Import the ‘CO2.csv’ file into R with *read.table()* function
and save it to a variable called *my_data*. Check function’s manual for
the information about arguments’ values. Call *my_data*.**  
First 10 output lines are shown below:

      Plant   Type  Treatment conc uptake
    1   Qn1 Quebec nonchilled   95   16.0
    2   Qn1 Quebec nonchilled  175   30.4
    3   Qn1 Quebec nonchilled  250   34.8
    4   Qn1 Quebec nonchilled  350   37.2
    5   Qn1 Quebec nonchilled  500   35.3
    6   Qn1 Quebec nonchilled  675   39.2
    7   Qn1 Quebec nonchilled 1000   39.7
    8   Qn2 Quebec nonchilled   95   13.6
    9   Qn2 Quebec nonchilled  175   27.3

**An advice**  
While importing any new file, it is a good practice to display it before
in any simple, external text editor (e.g. Notepad) to see its
formatting. It helps to properly adjust *read.table()* arguments.

Displaying tables in a console is often uninformative. Especially when
the number of columns or rows exceeds console capabilities.

**Ex 6. Call built-in dataset called *infert*. Can you see whole table?
If not, what is lacking? Write your answer as a comment within the
script file.**

R Studio provides an easy tool for intuitive visualization of data
frames. It is a *View()* function (note that it starts with a capital
letter). You can call it also by simply clicking on a data frame within
*Environment* panel.

**Ex 7. Display *my_data* with *View()* function. Click on header in the
opened window to sort the data according to the values in a given
column. In what region CO2 uptake is the highest? Write your answer as a
comment within the script file.**

**Curiosity**  
To print the summary of a data frame within a console, use *summary()*
function. It will provide simple statistics for each column separately.
Additionally you can display few rows with the *head()* (first rows) or
*tail()* (last rows) to see a data frame arrangement.

### 6. Types of data

All values inside one column must be of the same data type, but the
columns can be of different types. Type of data within a collumn is
defined by its *class*. The most popular classes are:

-   *character* - strings (remember that numbers surrounded by quotation
    marks are also treated as strings)
-   *factor* - strings with the levels carrying information about the
    number of occurances and order of strings. Factors are commonly used
    when doing statistics in R, where they serve as indicators of the
    [nominal
    scale](https://www.statsdirect.com/help/basics/measurement_scales.htm).
    To read strings as factors set the *stringAsFactors* argument of
    importing function to *TRUE* (for R version \>= 4.0.0).  
-   *numeric* - real numbers
-   *integer* - only integers
-   *logical* - logical values (TRUE or FALSE)

**Curiosity**  
You can convert different data types with the use of *as…* functions
family e.g. *as.character(),as.factor() ect.*. Note, however, that not
all conversions are permitted e.g. a letter cannot be converted into an
integer. To change class of a column you need to replace whole column
with the result of *as…* function.

Class of a column can be checked by displaying data frame with *View()*
function and putting mouse cursor over the column header.

**Ex 8. Check the class of column *uptake*. Write your answer as a
comment within the script file.**

Class of column can be also checked with *class()* function. However, as
it requires a given collumn as an argument we need to learn subsetting
first.

### 7. Subsetting

Data frame can be subsetted with the use of coordinates (indexes)
enclosed within the square brackets. In case of data frames there are
always 2 coordinates: *\[row_number,column_number\]*.  
Note that vectors have only one coordinate, the position, so they can be
called one-dimensional objects. Data frames have two dimensions: rows
and columns.

**Ex 9. Return the value from 49<sup>th</sup> row and 4<sup>th</sup>
column of *my_data*. **

Expected result:

    [1] 1000

You can call for multiple values in the same time. To define range of
coordinates, use colon separating range borders -
*e.g. \[row_number_1:row_number_2, column_number\]*.

**Ex 10. Return first 5 rows for the last 3 collumns of *my_data*.**

Expected result:

       Treatment conc uptake
    1 nonchilled   95   16.0
    2 nonchilled  175   30.4
    3 nonchilled  250   34.8
    4 nonchilled  350   37.2
    5 nonchilled  500   35.3

If you want to call for all rows or columns it is enough to leave blank
space instead of the respective coordinate - *e.g. \[,column_number\]*

**Ex 11. Now, save 5<sup>th</sup> column of *my_data* as a variable
called *my_column_5*. Call call the variable, so its content is
displayed in console.**

Expected result:

     [1] 16.0 30.4 34.8 37.2 35.3 39.2 39.7 13.6 27.3 37.1 41.8 40.6 41.4 44.3 16.2
    [16] 32.4 40.3 42.1 42.9 43.9 45.5 14.2 24.1 30.3 34.6 32.5 35.4 38.7  9.3 27.3
    [31] 35.0 38.8 38.6 37.5 42.4 15.1 21.0 38.1 34.0 38.9 39.6 41.4 10.6 19.2 26.2
    [46] 30.0 30.9 32.4 35.5 12.0 22.0 30.6 31.8 32.4 31.1 31.5 11.3 19.4 25.8 27.9
    [61] 28.5 28.1 27.8 10.5 14.9 18.1 18.9 19.5 22.2 21.9  7.7 11.4 12.3 13.0 12.5
    [76] 13.7 14.4 10.6 18.0 17.9 17.9 17.9 18.9 19.9

Note that the outcome is no longer a table. As we asked for just one
column, a series of numbers (vector) was returned. Let’s recall vector
subsetting.

**Ex 12. Return 3<sup>rd</sup>, 4<sup>th</sup> and 5<sup>th</sup> value
from variable *my_column_5*.**

Expected result:

    [1] 34.8 37.2 35.3

**Curiosity**  
Pulling one row from the data frame will not result in a vector. It is
because a row can contain elements of different types what is not
allowed for vectors.

Table can be also subsetted with the use of columns’ (or rows’) names.

**Ex 13. Return the same column but use column name instead of its
number. Don’t forget about quotation marks.**

One another way to obtain whole collumn is to use dollar sign between
table’s and collumn’s name. Such expression is automatically treated as
a vector, so it can be directly subsetted to get a particular row. -
*e.g. table$collumn_name\[row_number\]*.

**Ex 14. Return values from 15<sup>th</sup> to 30<sup>th</sup> row of
*conc* column from *my_data*. Use dollar sign.**

Expected result:

     [1]   95  175  250  350  500  675 1000   95  175  250  350  500  675 1000   95
    [16]  175

If desired rows (or columns) do not follow each other and the range
option cannot be used, vector of coordinates should be provided.

**Ex 15. Create a vector with values 3, 5, 7, 9 and 12 and save it to a
variable. Call it.**

Expected result:

    [1]  3  5  7  9 12

**Ex 16. Return rows of *uptake* column corresponding to values inside
the vector created before.**

Expected result:

    [1] 34.8 35.3 39.7 27.3 40.6

You can also subset everything except specified columns (or rows). To do
this, put minus (-) before an index or vector of indexes.

**Ex 17. Return all columns except 5<sup>th</sup>.**

First 10 output lines are shown below:

       Plant   Type  Treatment conc
    1    Qn1 Quebec nonchilled   95
    2    Qn1 Quebec nonchilled  175
    3    Qn1 Quebec nonchilled  250
    4    Qn1 Quebec nonchilled  350
    5    Qn1 Quebec nonchilled  500
    6    Qn1 Quebec nonchilled  675
    7    Qn1 Quebec nonchilled 1000
    8    Qn2 Quebec nonchilled   95
    9    Qn2 Quebec nonchilled  175
    10   Qn2 Quebec nonchilled  250

### 8. Simple manipulations

1.  Replacement - assign a given value to specific place in your table
    with the use of an arrow. It works just as with variables
    assignment - *e.g. table\[row_number,collumn_number\] \<- new_value*

**Ex 18. Replace 5<sup>th</sup> value in the column *Type* with the
label ‘Unknown’. Check whether it was indeed replaced.**

2.  Mathematical operations

You can use classical mathematical operators: +, -, \* and /. Remember,
however, that mathematical operations make sense only for *integer* or
*numeric* data type.

**Ex 19. Recalculate and modify *conc* column to include values in L/L
units. Display modified column.**

Expected result:

     [1] 0.095 0.175 0.250 0.350 0.500 0.675 1.000 0.095 0.175 0.250 0.350 0.500
    [13] 0.675 1.000 0.095 0.175 0.250 0.350 0.500 0.675 1.000 0.095 0.175 0.250
    [25] 0.350 0.500 0.675 1.000 0.095 0.175 0.250 0.350 0.500 0.675 1.000 0.095
    [37] 0.175 0.250 0.350 0.500 0.675 1.000 0.095 0.175 0.250 0.350 0.500 0.675
    [49] 1.000 0.095 0.175 0.250 0.350 0.500 0.675 1.000 0.095 0.175 0.250 0.350
    [61] 0.500 0.675 1.000 0.095 0.175 0.250 0.350 0.500 0.675 1.000 0.095 0.175
    [73] 0.250 0.350 0.500 0.675 1.000 0.095 0.175 0.250 0.350 0.500 0.675 1.000

Also, you can use simple summary functions from previous class (see
Class 1).

**Ex 20. Calculate the mean value of the *uptake* collumn.**

Expected result:

    [1] 27.2131

3.  Simple summaries:

-   *nrow()* - number of rows
-   *ncol()* - number of columns

**Ex 21. Return total number of cells within *my_data*.**

Expected result:

    [1] 420

4.  Deleting rows with missing data.

Missing data, as stated before (see point 4), are represented as *NA*
(not-available) in R. Most of the functions will raise an error every
time the *NA* is provided as the argument.

**Ex 22. Choose one cell and replace its value with *NA*. Do not add
quotation marks as *NA* is an iternal R symbol (just as
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi")).
Print whole row.**

Rows with missing data can be removed with *na.omit()* function. To save
changes, the result of *na.omit()* function must be saved as a variable.
**Note that, in practice, deleting missing data must be well justified.
Make sure they do not provide any important information**.

**Ex 23. Remove the row with mising data. Replace variable *my_data*
with modified table. Remember that it cannot be undone.**

### 9. Adding new column or row

1.  Adding new column is relatively simple. All you need to have is a
    vector. However, remember three things:

-   length of vector must equal the number of rows of a data frame
-   order of values within a vector corresponds to the row numbers
-   name of vector will become name of the added column

We are going to add a column with IDs of observations. Note that column
with IDs is often necessary in statistical analysis. It is also inherent
to the data in [long
format](https://www.theanalysisfactor.com/wide-and-long-data/) which is
strongly advised.

**Ex 24. Create a vector with ID numbers starting from 100. Use one of
functions introduced above to obtain the desired length of the vector.
Call the vector *ID*.**

Expected result:

     [1] 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118
    [20] 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137
    [39] 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156
    [58] 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175
    [77] 176 177 178 179 180 181 182

You can combine data frames with the use of *cbind()* function in the
following manner: *cbind(data_frame1,data_frame2)*. Note that a vector
can be seen as a data frame with only one column.

**Ex 25. Place created IDs at the beginning of *my_data* (as first
column). Overwrite *my_data* variable.**

2.  Adding new row is more complicated as you cannot create a vector
    with different types of data. Firstly you need to create a new data
    frame (similar to the old one) consisting of only new row (or rows).
    To do this use *data.frame()* function in the following manner:
    *data.frame(columnName1 = value1, columnName2 = value2,…)*.

**Ex 26. Create data frame with one row and following values:
1,‘Kr1’,‘Krakow’,unknown’,1000,20. Collumns’ names should correspond to
this of *my_data*. Call it *Added_rows*.**

Expected result:

      ID Plant   Type Treatment conc uptake
    1  1   Kr1 Krakow   unknown 1000     20

**Curiosity**  
To combine a data frame with more rows at the same time replace the
values for each collumn with the vectors.

To stick data frames by rows use *rbind()* function in the following
manner: *rbind(data_frame1,data_frame2)*

**Ex 27. Place created row at the end of *my_data*. Overwrite *my_data*
variable.**

### 10. Saving data frame

To save your data frame into a file use *write.table()* function.

**Ex 28. Save modified *my_data* to the *.csv* file. Include your
surname in the file name**

### 11. Next classes

During the next class you will learn about logical expressions,
conditions and loops.

### 12. Homework

**Prepare your homework in the form of a script file (.R) and include
your surname in its name.**

All exercises need to be performed on the built-in *swiss* dataset.
Include all subsequent steps in a script file.  
1. With an R command, return the lowest percentage of catholics.  
2. With an R command, return the median percentage of live births living
more than 1 year.  
3. With an R command, add column with self-chosen ID for each
observation and save the dataset as a *my_data* variable.  
4. With an R command, modify *my_data* by removing its 4 first rows.  
5. Save a modified dataset to a .csv file

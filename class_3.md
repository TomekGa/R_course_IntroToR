Introdution to R - class 3
================
**Tomek Gaczorek**; <tomek.gaczorek@gmail.com>
18.11.22

<!-- **!!! Decription of exercisesis is in green !!!** -->
<!-- **!!! Advanced parts are marked with the red asterixis !!!** -->

### 1. Logical expressions

R as a whole computer architecture (including programming languages) is
based on the binary information, the current either flows (TRUE) or not
(FALSE, capital letters on purpose) depending on the conditions. These
logical values form a distinct type of data and can be, similarly to
other types, combined into vectors.

**Ex 1. Create a logical vector with 3 TRUE and 2 FALSE values and call
it *my_logical*. Note that they are internal R symbols so you should not
use quotation marks.**  
Desired outcome:

    [1]  TRUE  TRUE  TRUE FALSE FALSE

**An advice**  
To make your code shorter you can use T instead of TRUE and F instead of
FALSE.

Formally, logical values correspond to 0 (for FALSE) and 1 (for TRUE)
and behave like them in every mathematical operations.

**Ex 2. Calculate the sum of *my_logical*.**  
Desired outcome:

    [1] 3

However, logical vectors have one important distinctive characteristic:
they can be used for subsetting. To achieve this you need to provide
logical vector with TRUE for the elements you want to keep and FALSE for
for the elements you want to discard. The length of the logical vector
used for subsetting has to be equal to the number of elements (e.g.,
columns) in the object we want to subset.

**Ex 3. Save 6 first rows of built-in *CO2* dataset to a chosen
variable. Then, using logical vectors return its 1<sup>st</sup> and
5<sup>th</sup> collumn.**  
Desired outcome:

      Plant uptake
    1   Qn1   16.0
    2   Qn1   30.4
    3   Qn1   34.8
    4   Qn1   37.2
    5   Qn1   35.3
    6   Qn1   39.2

### 2. Comparisons

Normally, no one creates logical vectors on his/her own. There are
created automatically as the effect of different comparisons. The most
common is *equality*. It is done with double equal sign (*==*).

**Ex 4. Check whether in R: 5 equals 5.00 and whether
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi")
equals 3.14.**  
Desired outcome:

    [1] TRUE

    [1] FALSE

The same stands for all others comparisons but the symbols are
different:

-   **==** - equal
-   **!=** - unequal
-   **\>** - higher
-   **\>=** - higher or equal
-   **\<** - lower
-   **\<=** - lower or equal

**Curiosity**  
Double equal sign is used for equality because single sign is already in
use. It serves as an alternative for the assigning arrow, however, for
code purity the arrow is the one recommended.

Note that while comparing two vectors with the symbols shown above, R
does not consider the action as one comparison. It rather compares them
element by element, recycling shorter vector and resulting in logical
vector of longer one’s length. It is the same rule as for matematical
operations on vectors.

**Ex 5. Manually create two vectors. One of the prime numbers and a
second of even numbers. Both should belong to the range \<0,10\>. Check
if they are equal.**  
Desired outcome:

    [1]  TRUE FALSE FALSE FALSE FALSE

To check whether vectors (as a whole) are identical use *identical()*
function.

**Ex 6. Create two integer vectors from 1 to 10. Call them differently
and compare them with *identical()* function. Then, change one value
within first vector and repeat comparison.**  
Desired outcome:

    [1] TRUE

    [1] FALSE

The other useful tool is the *%in%* operator. It provides information
whether elements of first vector are present in the second one. Note
that it is focused on the first vector only, so there is no recycling.

**Ex 7. Create two character vectors each consisting of a set of
individual characters. The first should contain your name and the second
one the name of other person from the group. Check how many letter your
names have in common. Then, change the order of names and repeat the
comparison.**

### 3. Exclamation mark

Exclamation mark (*!*) works in R as the symbol of negation. Any logical
vector preceded by *!* will result in its reversal - FALSE changed into
TRUE and vice versa.

**Ex 8. Having vector of 3 TRUE values, return its negation.**  
Desired outcome:

    [1] FALSE FALSE FALSE

More typically *!* is used to negate comparisons. Note that the idea is
the same: you negate logical vector by negating action which produces
it. Remember that negated comparison should be enclosed in parentheses
e.g. *!(2 == 2)*.

**Ex 9. Create a sequence of integers from 1 to 100 in which each
subsequent element is larger by 3 than the previous one. Then, create
logical vector indicating which elements are larger than 50. Do not use
‘*\>*’ sign.**  
Desired outcome:

     [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    [13] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
    [25]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE

### 4. Logical operators

The real power of logic in programming is provided by combining
comparisons (use parentheses for clarity). There are two basic
operators:

-   **&** - and - condition is TRUE if both comparison are TRUE
-   **\|** - or - condition is TRUE if at least one comparison is TRUE

**Ex 10. For an integer vector from 1 to 10, create logical vector
indicating which element is smaller or larger than 5.**  
Desired outcome:

     [1]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE

**Ex 11. For an integer vector from 1 to 10, create logical vector
indicating which element is divisible by both 2 and 3.**  
Desired outcome:

     [1] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE

**Curiosity**  
R also uses double version of *&* and *\|* operators. Their outcome is
exactly the same and their role is just related to optimalization. While
using double operators, R checks first condition and if not needed,
ignore the second one (e.g. in the ‘AND’ statement if the first
condition is FALSE, there is no need to check the second one as the
result will always be FALSE). Note that they are often used when
conditions are severly time-consuming.

### 5. *which()* function

Frequently, the question is not about logical vectors themselves but
rather about which element of a vector fulfills given condition. The
answer is provided by *which()* function. It takes comparison as an
argument and return a vector of indexes.

**Ex 12. Construct a vector with first 20 integers divisible by 3. Which
elements of it are larger or equal 21? **  
Desired outcome:

     [1]  7  8  9 10 11 12 13 14 15 16 17 18 19 20

**Ex 13. Having indexes from the previous exercise, return the values
from the vector.**  
Desired outcome:

     [1] 21 24 27 30 33 36 39 42 45 48 51 54 57 60

### 6. Subsetting with the logical expressions

As stated before subsetting can be done directly with logical vectors
(TRUE for each kept element) or indexes generated by *which()* function.
In practice, it is even simpler. All you need to provide is a condition
instead of a coordinate e.g. *vector\[condition\]* will return only the
elements fulfilling given condition.  
The logic behind is as follows: condition generates a logical vector
\>\> coordinates are denoted as a series of TRUEs and FALSEs elements in
this logical vector \>\> returned are elements of the vector you want to
subset, for which coordinate equals TRUE.

**Ex 14. For an integer vector from 1 to 100, return elements higher
than vector’s mean.**  
Desired outcome:

     [1]  51  52  53  54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69
    [20]  70  71  72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88
    [39]  89  90  91  92  93  94  95  96  97  98  99 100

The same pattern applies for subsetting data frames.

**Ex 15. Using built-in dataset *CO2*, return observation for *Qn2*
plant.**  
Desired outcome:

       Plant   Type  Treatment conc uptake
    8    Qn2 Quebec nonchilled   95   13.6
    9    Qn2 Quebec nonchilled  175   27.3
    10   Qn2 Quebec nonchilled  250   37.1
    11   Qn2 Quebec nonchilled  350   41.8
    12   Qn2 Quebec nonchilled  500   40.6
    13   Qn2 Quebec nonchilled  675   41.4
    14   Qn2 Quebec nonchilled 1000   44.3

**An advice**  
Note that to obtain the logical vector with one element for each row,
you need to make comparison based on a collumn
e.g. *my_data\[my_data$my_column != 5,\]* would result in the
observations (including all columns) from *my_data* in which the value
for *my_collumn* does not equal 5.

**Ex 16. Using built-in dataset *CO2*, return observation from
Mississippi chilled plant with an uptake higher than 20
ummol/m<sup>2</sup> x s.**  
Desired outcome:

       Plant        Type Treatment conc uptake
    69   Mc1 Mississippi   chilled  675   22.2
    70   Mc1 Mississippi   chilled 1000   21.9

### 7. IF, ELSE statements

The next important application of conditions is decision making. It is
extremely useful when you want your code to behave differently depending
on conditions. It is done with *if()* and *else()* statements with the
following syntax (note curly brackets):

``` r
if(your_condition){
  # do something if condition is TRUE
} else {
  # do something otherwise
}
```

To perform it properly be aware of 3 things:

-   your condition needs to result in a single TRUE or FALSE (not a
    vector with 2 or more elements). Think about it as real-life
    decision - yes or no.
-   *else()* statement makes sense only when preceded by *if()*
    statement.
-   *else()* statement is optional. If not used, R simply does not
    perform any action when condition is FALSE

**Ex 17. Assume x is a real number. Write piece of code printing
positive number when x is negative and vice versa. Check it for x equals
-1 and 2.**  
Desired outcome:

    [1] 1

    [1] -2

**An advice**  
You can print a value by simply typing it without any function or with
the use of *print()*.

Sometimes two options are not enough. You can introduce more conditions
with *else if()*

``` r
if(condition_1){
  # do something if condition_1 is TRUE
} else if(condition_2){
  # do something if condition_1 if FALSE but condition_2 is TRUE
} else {
  # do something otherwise
}
```

**Ex 18. Assume x is a real number. Write piece of code printing ‘P’ if
the number is positive, ‘N’ if negative and ‘Z’ if it equals 0. Check it
for -1,0 and 2.**  
Desired outcome:

    [1] "N"

    [1] "Z"

    [1] "P"

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*ADVANCED\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
Making a proper choice often require making subsequent decisions based
on previous choices. To do this, nest one *if()* statement into another
(there is no limit of steps).

``` r
if(condition_1){
  # do something if condition_1 is TRUE
  if(condition_2){
    # do something if both conditions are TRUE
  } else {
    # do something if condition_1 is TRUE but condiiton_2 if FALSE
  }
} else {
  # do something if condition_1 is FALSE
}
```

**Curiosity**  
1. Note that R Studio by default intends blocks of code to make reading
easier.  
2. Note that nested *if()* statement behave in the same way as single
one with conditions seperated with *&* operator.

**Ex 19. Assume n is one of the DNA nucleotides. Write piece of code
detecting two things: (1) whether it belongs to [purines or
pyrimidines](https://library.med.utah.edu/NetBiochem/pupyr/pp.htm) and
(2) what is its complementary nucleotide. Check it for all nucleotides
(A,T,C,G).**  
Desired outcome:

    [1] "Purine"

    [1] "T"

    [1] "Pyrimidine"

    [1] "A"

    [1] "Pyrimidine"

    [1] "G"

    [1] "Purine"

    [1] "C"

**Ex 20. Copy and modify previous code to obtain, as a result, the
vector consisting: checked nucleotide, type (purines or pyrimidines) and
complementary nucliotide.**  
Desired outcome:

    [1] "A"      "Purine" "T"     

    [1] "T"          "Pyrimidine" "A"         

    [1] "C"          "Pyrimidine" "G"         

    [1] "G"      "Purine" "C"     

------------------------------------------------------------------------

### 8. Loops

Until now, you should know how to force your code to behave differently
based on conditions. Imagine, however, checking thousands or millions of
values. It does not make sense to do it manually, right? The proper tool
for it is a loop.

The basic one is the *FOR* loop. It executes given lines of code
independently for each element of a given vector, one by one. The syntax
is as follow:

``` r
for(iterator in your_vector){
  # do something for each element (iterator) of your_vector
  # e.g. 'iterator+2' will print each element of your vector enlarged by 2 
}
```

**An advice**  
1. Inside a loop, given element of a vector is represented by an
*iterator* (letter *i* is often used by convention).  
2. Due to the fact that *FOR* loop is often used to iterate over range
of numbers, R let you to ommit *c()* function while creating such
vectors. Then, the syntax is e.g. *for(iterator in 1:1000){…*.

**Ex 21. Create *FOR* loop that will print all numbers from 1 to 2000.**

Unless saved, outcome obtained within a given loop cycle is overwritten
when iterator is replaced with the next value. What is received at the
end is just the result for last element of a vector. To save each
outcome, create an empty vector (just *c()*) and save there your outcome
during each loop cycle. Remember that:

1.  Empty vector needs to be created before the loop. Note that creation
    of a new vector within a loop will result in erasing previously
    saved values.  
2.  Outcomes can be saved in three ways:  

-   you can append a vector by combining previous and new value
    e.g. *outcomes \<- c(outcomes,new_value)*. For the large number of
    values (e.g. millions), however, it becomes extremely
    computationally demanding (rewritting variable).  
-   if your iterator represents subsequent numbers starting from 1, you
    can assign new value to the specific position in a vector, indicated
    by the iterator e.g. *outcomes\[iterator\] \<- new_value*. Note that
    if iterators start from 2 you can use *iterator-1* instead.  
-   you can create a variable that will count loop cycles and serve as
    position indication. To do this, create a variable which equals 0
    and then add one to it with subsequent cycles. Then, use it as
    *outcome\[counter\] \<- new_value*.

**Ex 22. Using *FOR* loop, return modified vector from 1 to 1000 where
every second value will be reduced by 100.**  
First 100 elements of desired vector:

      [1]   1 -98   3 -96   5 -94   7 -92   9 -90  11 -88  13 -86  15 -84  17 -82
     [19]  19 -80  21 -78  23 -76  25 -74  27 -72  29 -70  31 -68  33 -66  35 -64
     [37]  37 -62  39 -60  41 -58  43 -56  45 -54  47 -52  49 -50  51 -48  53 -46
     [55]  55 -44  57 -42  59 -40  61 -38  63 -36  65 -34  67 -32  69 -30  71 -28
     [73]  73 -26  75 -24  77 -22  79 -20  81 -18  83 -16  85 -14  87 -12  89 -10
     [91]  91  -8  93  -6  95  -4  97  -2  99   0

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*ADVANCED\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
The second loop is called *WHILE*. The idea is similar but *WHILE* cycle
as long as the given condition is TRUE. The syntax is as follow:

``` r
while(your_condition){
  # do something as long as your_condition is TRUE
}
```

*WHILE* loop is a little bit dangerous as improperly written can last
forever. There are 2 main techniques used:  
1. In the condition, place some variable that will be changed in each
loop cycle. After desired number of cycles, it should reach a threshold
which falsifies the condition e.g. consequent number addition.  
2. you can use *checker* variable which eqauls TRUE. It needs to be
created before the loop. The initial condition should be *(checker ==
TRUE)*. Then inside the loop you should include *IF* statement changing
*checker* to FALSE if some other condition is fulfilled.

**Ex 23. Using WHILE loop create a vector with [Fibonacci
sequence](https://en.wikipedia.org/wiki/Fibonacci_number) consisting
numbers lower than 1000.**  
Desired outcome:

     [1]   0   1   1   2   3   5   8  13  21  34  55  89 144 233 377 610 987

**An advice**  
Last element of a vector can be obtained by placing its length as a
coordinate.

------------------------------------------------------------------------

### 9. Next classes

**Please, send me the script from today classes.**

During the next class you will learn about function from the *apply*
family, writting your own functions and plotting.

### 10. Homework

**Prepare your homework in a form of script file (.R) and include your
surname in its name.**

Include all subsequent steps in a script file.  
1. Create a vector from 1 to 50. Then, using R only, calculate how many
elements of this vector are higher than the positive square root of
456.  
2. Using built-in *mtcars* dataset, return (in one table) observations
with the lowest and the highest value for the gross horsepower. Don’t
look for the rows’ indexes manually.  
3. Assume x is an integer. Create an *‘if’* statement printing word
“divisible” if x is divisible by 5 and “undivisible” if it is not
divisible by 5.  
4. Using *FOR* loop, create 100, 8-letters “words” created from random
letters drawn without replacement. All 8 letters should be paste
together. Of course, the “words” don’t need to mean anything.  
5. Modify the loop above such as all words contain at least one vowel.  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*ADVANCED\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
6. Imagine you are a gambler and you play a game that randomly draws
(with replacement) 3 letters from the alphabet. If 3 identical letter
are drawn you win 100€ and nothing otherwise. Each game costs 1€ and you
start with 200€. Play until you run out of money. Remember that won
money gets back to pool. Print how many times you played.  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

**An advice**  
1. Positive square root can be calculated with *sqrt()* function  
1. Alphabet can be obtained from built-in vector *LETTERS*.  
2. For sampling use *sample()* function.

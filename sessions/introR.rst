**Intro R** 
-----------

R is a programming environment for statistics and graphics

- Does basically everything, can also be extended
- It’s the default when statisticians implement new methods
- Free, open-source

But

- Steeper learning curve than e.g. Excel, Stata
- Command-line driven (programming, not drop-down menus)
- Gives only what you ask for!

1. Base R vs tidyverse
======================

You know how when you get a new smartphone, it comes with an email and calendar app... but they're not the greatest? I usually download the Google Calendar and Gmail apps on my phone because, even though they technically do the same thing, they do it better. R is similar in this way.

When you downloaded R, it came with capabilities to import, analyze, and export data.  
But since R's creation, users have created ``packages`` which act like plug-ins or addons or apps. These add or improve the functionality of R. We'll be using a suite of packages called the `tidyverse` that tries to make R more straightforward for beginners.

The tidyverse has two main goals:

- Work with tidy (not messy) data
- Make code more human readable

Each package within the tidyverse is meant to do a particular thing, but each ultimately goes back to those two goals. We'll be using two packages in the ``tidyverse``, called ``dplyr`` (for manipulating tidy data in R), and ``ggplot2`` (for visualizing tidy data in R).

2. What is RStudio?
===================

Often, learning a programming language is made worse by an unintuitive and unhelpful user interface. For our workshop, we will be using RStudio, a graphical user interface (front-end) for R that is slightly more user-friendly than ‘Classic’ R’s GUI.

2.1 The console window  
~~~~~~~~~~~~~~~~~~~~~~

There are some useful features available in the console:

- Use the **UP** arrow to see past commands you have typed
- Help window appears as you type to help you complete your thought
- Tab autocomplete
    - When just typing, use tab autocomplete to fill in object names for you
    - When inside quotes ``'  '``, you can press tab to help you spell folder names correctly

2.2 Trying out the Console
~~~~~~~~~~~~~~~~~~~~~~~~~~

We’ll use the ``Console`` window first – as a (fancy!) calculator

.. code-block :: R

    2+2
    # [1] 4

    2^5+7
    # [1] 39

    2^(5+7)
    # [1] 4096

    exp(pi)-pi
    # [1] 19.9991

    log(20+pi)
    # [1] 3.141632

    0.05/1E6 # a comment; note 1E6 = 1,000,000
    # [1] 5e-08

- All common math functions are available; parentheses (round brackets) work as per high school math
- Try to get used to bracket matching. A ``+`` prompt means the line isn’t finished – hit Escape to get out, then try again.

We can also compare things in R using **operators**.

We can see if things are equal by using two equal signs ``==``.  To see if something is NOT equal, we use the exclamation mark ``!``.

.. code-block :: R

    3 == 2
    # [1] FALSE

    3-1 == 2
    # [1] TRUE

    TRUE == TRUE
    # [1] TRUE

    TRUE == FALSE
    #[1] FALSE

    'a' == 'a'
    # [1] TRUE

    'abc' != 'ABC'
    # [1] TRUE

    !is.na(NA)
    # [1] FALSE

.. Note :: 

  We can represent missing data with ``NA``, and use a function/command called ``is.na()`` to ask if data is missing. More on this later.

We can use greater than ``>`` or less than ``<`` signs as you would expect.

.. code-block :: R

    300 > 200
    # [1] TRUE

    0 > 999
    # [1] FALSE

- MULTIPLE CHOICE QUESTION - 1

Which of the following will **NOT** return **TRUE**? 

  A. FALSE == FALSE  
  B. 10-5 == sqrt(25)  
  C. TRUE > FALSE  
  D. 'a' > 'b'  

2.3 Storing Data
~~~~~~~~~~~~~~~~

We can quickly make comparisons, but we usually want to do things more sophisticated than that. For example, instead of typing "This is an important string that we want to do analysis on" into the console over and over again, we might want to give it a shorter name and then reference it later.

.. code-block :: R

  x <- "This is an important string that we want to do analysis on"

This shows up in the Environment tab in R Studio. This is very useful, because now when we want to print out this string, we can just type ``x`` into the Console.

.. code-block :: R

  x
  # [1] "This is an important string that we want to do analysis on"

The console is most useful for quick calculations or code chunks. But what happens when you want to remember what you coded yesterday, a year ago, or a decade ago? R won't necessarily save everything you've done forever in the Environment tab (and we wouldn't want it to!).

R stores data (and everything else) as objects. New objects are created when we assign them values;

.. code-block :: R

  x <- 3
  y <- 2 # now check the Environment window
  x+y
  # [1] 5

2.4 Using the script window
~~~~~~~~~~~~~~~~~~~~~~~~~~~

While fine for occasional use, entering every command by hand is error-prone, and quickly gets tedious. A much better approach is to use a Script window 

– open one with Ctrl-Shift-N, or the drop-down menus
- Opens a nice editor, enables saving code (.R extension)
- Run current line (or selected lines) with Ctrl-Enter, or Ctrl-R

.. important::

  From now on, we assume you are using a script editor.

- First-time users tend to be reluctant to switch! – but it’s worth it, ask any experienced user
- Scripts make it easy to run slightly modified code, without re-typing everything – remember to save them as you work
- Also remember the Escape key, if e.g. your bracket-matching goes wrong

For a very few jobs, e.g. changing directories, we’ll still use drop-down menus. But commands are available, for all tasks.

We can save our scripts wherever we want, but it makes it easier if we set a working directory in R. This makes it easier to find files, and also can make research more reproducible because it gives you the ability to share data structure with a collaborator.

Before we can set the working directory, we need to know where we are on our computer right now.  Just like the command line's ``pwd`` command, R has a command called ``getwd()``.  Notice that it returns the absolute path to your home directory.

.. code-block :: R

  getwd()
  # [1] "C:/Users/gaugustus/Documents/Rdocs/"

You can point to files from anywhere on the computer RELATIVE to your current position.  If you need to change this working directory, such as to go into the new folder, you can do so with ``setwd()``.  Let's try this. Make sure you put the path in quotes.

You can use tab complete in R Studio, so once you open the quotes, press tab to see all the files and directories listed for you.  If you type a letter, that list will shorten. 

.. Note :: 

  You can also use the Files tab in R Studio. Your home directory can be found by clicking the ``Home`` button.

.. code-block :: R

  setwd("~/")
  getwd()
  # [1] "C:/Users/gaugustus/Documents/Rdocs/r-intro-20170825-master"

- MULTIPLE CHOICE QUESTION - 2

What is the output when we execute the following code?

.. code-block :: R

  x <- 3   
  y <- 2   
  y <- 17.4   
  x+y   

  A. [1] 3  2  17.4  
  B. [1] 22.4    
  C. [1] 20.4   
  D. [1] 5    

.. warning ::

  Assigning new values to existing objects over-writes the old version – and be aware there is no Ctrl-Z ‘undo’

.. code-block :: R

  y <- 17.4 # check the Environment window again

  x+y
  # [1] 20.4

.. Note ::
  
  - Anything after a hash (#) is ignored – e.g. comments
  - Spaces don’t matter outside of quotes (except for the `<-` symbol)
  - Capital letters do matter

.. tip ::

  What’s a good name for my new object?

  - Something memorable (!) and not easily-confused with other objects, e.g. X isn’t a good choice if you already have x
  - Names must start with a letter or period (”.”), after that any letter, number or period is okay
  - Avoid other characters; they get interpreted as math (”-”,”*”) or are hard to read (” ”) so should not be used in names
  - Avoid names of existing functions – e.g. summary. Some oneletter choices (c, C, F, t, T and S) are already used by R as names of functions, it’s best to avoid these too

3. Data Types
=============
There are 6 main types: `double (numeric)`, `integer`, `complex`, `logical` and `character`. The sixth one "raw" will not be discussed in this workshop.

R provides many functions to examine features of vectors and other objects, for example

 - ``class()`` - what kind of object is it (high-level)?
 - ``typeof()`` - what is the object’s data type (low-level)?
 - ``length()`` - how long is it? What about two dimensional objects?
 - ``attributes()`` - does it have any metadata?


3.1 Character
~~~~~~~~~~~~~

Surround with quotes, can be any keyboard character

.. code-block :: R

  c <- 'Hello world! 123'
  class(c)
  # [1] "character"
  typeof(c)
  # [1] "character"

3.2 Double (numeric)
~~~~~~~~~~~~~~~~~~~~

No quotes, can be any real number, decimal, or whole numbers

.. code-block :: R

  n <- 3.4
  class(n)
  # [1] "numeric"
  typeof(n)
  # [1] "double"

3.3 Integer
~~~~~~~~~~~

No quotes, can be any whole number.  Place an `L` behind it, otherwise R will read it as a numeric

.. code-block :: R

  i <- 2L
  class(i)
  # [1] "integer"

3.4 Complex
~~~~~~~~~~~

Can use notation like ``+`` ``-``, and values like ``i`` for imaginary units in complex numbers.

.. code-block :: R

  comp <- 1+4i
  class(comp)
  # [1] "complex"

3.5 Logical
~~~~~~~~~~~

Are equal to either ``TRUE`` or ``FALSE`` in all caps

.. code-block :: R

  l <- TRUE
  l <- FALSE
  class(l)
  # [1] "logical"


4 Data Structures
=================

4.1 Atomic Vector
~~~~~~~~~~~~~~~~~

Use ``c()`` notation (stands for combine).  All elements of a vector have to be of the same data type.

.. code-block :: R

  log_vector <- c(TRUE, TRUE, FALSE, TRUE)
  char_vector <- c("Uwe", "Gaius", "Liz")
  char_vector <- c(char_vector, "Helper1", NA) #NA represents empty data
  char_vector
  # [1] "Uwe"     "Gaius"   "Liz"     "Helper1" NA       
  length(char_vector)
  # [1] 5
  class(char_vector)
  # [1] "character"
  anyNA(char_vector)
  # [1] TRUE

Given that atomic vectors *must* be of all one data type, what will happen when data is mixed?

.. code-block :: R

  mixed <- c("True", TRUE)
  mixed 
  # [1] "True" "TRUE"
  typeof(mixed)
  # [1] "character"
  #It has converted the logical to a character

R will create a resulting vector with a mode that can most easily accommodate all the elements it contains. This is something called type coercion, and it is the source of many surprises and the reason why we need to be aware of the basic data types and how R will interpret them.

- EXERCISE - 1

Uncover the heirarchy of the data types using the elements in this vector "anothermixed".

.. code-block :: R

    anothermixed <- c("Stanford",FALSE, 2L, 3.14)
   
    test_c_i <- c("Stanford", 2L)
    typeof(test_c_i)
    # [1] "character"
    
    test_c_d <- c("Stanford", 3.14)
    typeof(test_c_d)
    # [1] "character"
    
    test_l_i <- c(FALSE, 2L)
    typeof(test_l_i)
    # [1] "integer"
    
    test_l_d <- c(FALSE, 3.14)
    typeof(test_l_d)
    # [1] "double"
    
    test_i_d <- c(2L, 3.14)
    typeof(test_i_d)
    [1] "double"
    
Using ``as.datatype`` (``as.logical``, ``as.character``, ``as.factor``, etc) will make R try to force it to be the this data type.

.. code-block :: R

  as.logical(mixed) 
  # [1] TRUE TRUE

4.2 List
~~~~~~~~

Holds multiple of the above data types, including other lists.  surround with `list()`

.. code-block :: R

  mylist <- list(chars = 'c', nums = 1.4, logicals=TRUE, anotherList = list(a = 'a', b = 2))
  class(mylist)
  # [1] "list"

.. warning :: 

  Don't forget that the command ``str()`` also lists the class of each column within a data frame. It is good to use to make sure all of your data was imported correctly.
Lists are like vectors except that you can use multiple data types.  Make a list using the ``list()`` function.

.. code-block :: R

  my_list <- list(1, "A", TRUE)
  my_list
  # [[1]]
  # [1] 1
  # 
  # [[2]]
  # [1] "A"
  # 
  # [[3]]
  # [1] TRUE

We can access a value of a list by referencing the index or by using the label.

.. code-block :: R

  my_list[1]
  # [[1]]
  # [1] 1

.. code-block :: R

  phonebook <- list(name="Upendra", phone="111-1111", age=27)
  phonebook["name"]
  # $name
  # [1] "Gaius"


4.3 Matrices
~~~~~~~~~~~~

Matrices are 2 dimensional structures that hold only one data type.  Using ``ncol`` and ``nrow``, you can define its shape. You can fill in the matrix by assigning to ``data``.  By default, it fills in by column, but you can change this using the ``byrow`` argument.

.. code-block :: R

  m <- matrix(nrow=2, ncol=3)
  m
  #      [,1] [,2] [,3]
  # [1,]   NA   NA   NA
  # [2,]   NA   NA   NA
  m <- matrix(data=1:6, nrow=2, ncol=3)
  m
  #      [,1] [,2] [,3]
  # [1,]    1    3    5
  # [2,]    2    4    6
  m <- matrix(data=1:6, nrow=2, ncol=3, byrow=TRUE)
  m
  #      [,1] [,2] [,3]
  # [1,]    1    2    3
  # [2,]    4    5    6

.. Note :: 

  You can also have multi-dimensional structures called arrays. You can create this using the ``array()`` function, but it is outside the scope of this course.

4.4 Data Frames 
~~~~~~~~~~~~~~~

Data Frames are like matrices, but can hold multiple data types.  

**Vectors** are to **Lists** as **Matrices** are to **Data Frames**

.. code-block :: R

  df <- data.frame(id=letters[1:10], x=1:10, y=11:20)
  df
  #    id  x  y
  # 1   a  1 11
  # 2   b  2 12
  # 3   c  3 13
  # 4   d  4 14
  # 5   e  5 15
  # 6   f  6 16
  # 7   g  7 17
  # 8   h  8 18
  # 9   i  9 19
  # 10  j 10 20

  class(df)
  # [1] "data.frame"

  typeof(df)
  # [1] "list"

  head(df)
  #   id x  y
  # 1  a 1 11
  # 2  b 2 12
  # 3  c 3 13
  # 4  d 4 14
  # 5  e 5 15
  # 6  f 6 16

  tail(df)
  #    id  x  y
  # 5   e  5 15
  # 6   f  6 16
  # 7   g  7 17
  # 8   h  8 18
  # 9   i  9 19
  # 10  j 10 20

  nrow(df)
  # [1] 10

  ncol(df)
  # [1] 3

  str(df)
  # 'data.frame': 10 obs. of  3 variables:
  #  $ id: Factor w/ 10 levels "a","b","c","d",..: 1 2 3 4 5 6 7 8 9 10
  #  $ x : int  1 2 3 4 5 6 7 8 9 10
  #  $ y : int  11 12 13 14 15 16 17 18 19 20

  summary(df)
   #       id          x               y        
   # a      :1   Min.   : 1.00   Min.   :11.00  
   # b      :1   1st Qu.: 3.25   1st Qu.:13.25  
   # c      :1   Median : 5.50   Median :15.50  
   # d      :1   Mean   : 5.50   Mean   :15.50  
   # e      :1   3rd Qu.: 7.75   3rd Qu.:17.75  
   # f      :1   Max.   :10.00   Max.   :20.00  
   # (Other):4                                  

  names(df)
  # [1] "id" "x"  "y" 

4.5 Factors
~~~~~~~~~~~~

Factors are very useful when running statistics, and also clog up memory less than character vectors.

They do this by storing each unique value as an integer, which takes up less space in memory than characters in a string.  Then it references that integer to the corresponding string so that it is human readable.

.. code-block :: R

  state <- factor(c("Arizona", "Colorado", "Arizona"))
  state
  # [1] Arizona  Colorado Arizona 
  # Levels: Arizona Colorado

  nlevels(state)
  # [1] 2

  levels(state)
  # [1] "Arizona"  "Colorado"

Factors by default don't actually have hierarchy.  That is to say, Arizona is not more or less than Colorado.  But sometimes we want factors to have hierarchy (e.g. low comes before medium comes before high).

.. code-block :: R

  ratings <- factor(c("low", "high", "medium", "low"))
  ratings
  # [1] low    high   medium low   
  # Levels: high low medium

If we look for the minimum of the factors, we get an error because they are not ordered

.. code-block :: R

  min(ratings) 
  # Error in Summary.factor(c(2L, 1L, 3L, 2L), na.rm = FALSE) : 
    # ‘min’ not meaningful for fact
  levels(ratings)
  # [1] "high"   "low"    "medium"

We can add an order by putting ``ordered=TRUE`` into the arguments of the ``factor()`` function.  Then when we run ``min()``, it understands that "low" is the minimum value. Notice that the Levels change to less than symbols, showing there is a hierarchy.

.. code-block :: R

  ratings <- factor(ratings, levels=c("low", "medium", "high"), ordered=TRUE)
  levels(ratings)
  # [1] "low"    "medium" "high"  

  min(ratings)
  # [1] low
  # Levels: low < medium < high

When we run the ``str()`` function on a dataframe with factors, notice that it lists the type as a Factor and tells us how many levels it has. ``summary`` lists each factor level and tells us how many are in each group.

.. code-block :: R

  survey <- data.frame(number=c(1,2,2, 1, 2), group=c("A", "B","A", "A", "B"))
  str(survey)
  # 'data.frame': 5 obs. of  2 variables:
  #  $ number: num  1 2 2 1 2
  #  $ group : Factor w/ 2 levels "A","B": 1 2 1 1 2

  summary(survey)
   #     number    group
   # Min.   :1.0   A:3  
   # 1st Qu.:1.0   B:2  
   # Median :2.0        
   # Mean   :1.6        
   # 3rd Qu.:2.0        
   # Max.   :2.0        

A useful command to count how many values overlap is the ``table()`` function.  Here we see that 2 rows in the table have a ``1`` in the ``number`` column and an ``A`` in the `group` column, but there are 0 rows that have a ``B`` and a ``1``.

.. code-block :: R

  table(survey$number, survey$group)
    #   A B
    # 1 2 0
    # 2 1 2

- EXERCISE - 2

1. Create the following data frame in R:

+-----+---------------+-------------+
| Day | Magnification | Observation |
+=====+===============+=============+ 
|  1  |      2        |   Growth    |
+-----+---------------+-------------+ 
|  2  |      10       |    Death    |
+-----+---------------+-------------+
|  3  |      5        |  No Change  |
+-----+---------------+-------------+
|  4  |      2        |    Death    |
+-----+---------------+-------------+
|  5  |      5        |   Growth    |
+-----+---------------+-------------+

5. Reading in Data
==================

First, let's see how we can read in data using base R, using the ``read.csv()`` command:

.. code-block :: R

  gapminder.base <- read.csv(file = "datasets/gapminder.txt", header=TRUE, sep = "\t", stringsAsFactors = FALSE)

After successfully reading in the data;

- The environment now includes a ``gapminder.base`` object – or whatever you called the data read from file
- A copy of the data can be examined in the Excel-like data viewer – if it looks weird, find out why & fix it!

**What can I do with my data?**

Well you can several things. To operate on data, type commands in the Console window, just like our earlier calculator-style approach;

.. code-block :: R

  summary(gapminder)
   #   country           continent              year         lifeExp           pop           
   # Length:1704        Length:1704        Min.   :1952   Min.   :23.60   Min.   :6.001e+04  
   # Class :character   Class :character   1st Qu.:1966   1st Qu.:48.20   1st Qu.:2.794e+06  
   # Mode  :character   Mode  :character   Median :1980   Median :60.71   Median :7.024e+06  
   #                                       Mean   :1980   Mean   :59.47   Mean   :2.960e+07  
   #                                       3rd Qu.:1993   3rd Qu.:70.85   3rd Qu.:1.959e+07  
   #                                       Max.   :2007   Max.   :82.60   Max.   :1.319e+09 

.. code-block :: R

  str(gapminder)
  # Classes ‘tbl_df’, ‘tbl’ and 'data.frame':	1704 obs. of  6 variables:
  #  $ country  : chr  "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
  #  $ continent: chr  "Asia" "Asia" "Asia" "Asia" ...
  #  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...

- ``summary()`` summarizes the object and provide basic summary statistics for each column within your data
- ``str()`` tells us the structure of an object (i.e., it's dimensions/size and the class of the each data column)

We can also use these commands on any object – e.g. the single numbers we created earlier (try it!)

There are also commands to get these statistics alone. For this we use the ``$`` symbol to tell R which column we are interested in.

.. code-block :: R

  min(gapminder$lifeExp)
  # [1] 23.599

  median(gapminder$lifeExp)
  # [1] 60.7125

  max(gapminder$lifeExp)
  # [1] 82.603

These are called **FUNCTIONS** (we will more on this later), and are used to do a particular task on a set of data. Here we are accessing columns by using the dollar sign. We are telling R that we are only interested in one column.

We can also do more sophisticated things with these commands. Let's try a simple plot:

.. code-block :: R

  plot(gapminder$lifeExp, gapminder$gdpPercap)

The ``gapminder`` data we just imported is in an object called a Data Frame. A data frame holds data in a table format, like what you might be used to in Excel. A "tidy" data frame has columns that each represent a variable and rows which hold one observation.

As we saw before, individual columns in data frames are identified using the ``$`` symbol – just seen in the ``str()`` output.

Think of $ as ``apostrophe-S``, i.e. gapminder`’S`lifeExp

New columns are created when you assign their values – here containing the life expectancy in months instead of years;

.. code-block :: R

  gapminder$lifeExpMonths <- gapminder$lifeExp*12

  str(gapminder)
  # Classes ‘tbl_df’, ‘tbl’ and 'data.frame':	1704 obs. of  7 variables:
  #  $ country      : chr  "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
  #  $ continent    : chr  "Asia" "Asia" "Asia" "Asia" ...
  #  $ year         : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
  #  $ lifeExp      : num  28.8 30.3 32 34 36.1 ...
  #  $ pop          : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
  #  $ gdpPercap    : num  779 821 853 836 740 ...
  #  $ lifeExpMonths: num  346 364 384 408 433 ...

  summary(gapminder$lifeExpMonths)
  #  Min.   1st Qu.  Median    Mean    3rd Qu.    Max. 
  #  283.2  578.4    728.5     713.7   850.1      991.2 

- Assigning values to existing columns over-writes existing values – again, with no warning
- With e.g. gapminder$newcolumn <- 0, the new column has every entry zero; R recycles this single value, for every entry
- It’s unusual to delete columns... but if you must; use ``gapminder$lifeExpMonths <- NULL``

Other functions useful for summarizing data frames, and their columns;

.. code-block :: R

  names(gapminder)
  # [1] "country"       "continent"     "year"          "lifeExp"       "pop"           "gdpPercap"    
  # [7] "lifeExpMonths"

  dim(gapminder) # dim is short for dimension
  # [1] 1704 7

  length(gapminder$lifeExp) # how many rows in our dataset?
  # [1] 1704

  min(gapminder$lifeExp)
  # [1] 23.599

  max(gapminder$lifeExp)
  # [1] 82.603

  range(gapminder$lifeExp)
  # [1] 23.599 82.603

  mean(gapminder$lifeExp)
  # [1] 59.47444

  sd(gapminder$lifeExp) # sd is short for standard deviation
  # [1] 12.91711

  median(gapminder$lifeExp)
  # [1] 60.7125

  median(gapminder$li) # uses pattern-matching (but hard to debug later)
  # [1] 60.7125

- EXERCISE

Import the gapminder data frame again.

Use ``str()`` to look at the structure of the dataframe and ``summary()`` to get information about the variables.

- What are its columns?
- How many rows and columns are there?
- What is the earliest year in the `year` column?
- What is the average life expectancy?
- What is the largest population?

.. code-block :: R

  gapminder <- read_delim("datasets/02_gapminder.txt", 
      "\t", escape_double = FALSE, trim_ws = TRUE)

  str(gapminder)
  # Classes ‘tbl_df’, ‘tbl’ and 'data.frame':	1704 obs. of  6 variables:
  # $ country  : chr  "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
  # $ continent: chr  "Asia" "Asia" "Asia" "Asia" ...
  # $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
  # $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
  # $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
  # $ gdpPercap: num  779 821 853 836 740 ...

  dim(gapminder)

5.1 Subsetting
~~~~~~~~~~~~~~

5.1.1 Base R
^^^^^^^^^^^^^

Suppose we were interested in the life expectancy (i.e. 4th column) for 1957 for Afganistan in the years 1952, 1962, and 1977 (i.e. rows 1, 3, and 5). How to select these multiple elements?

.. code-block :: R

  gapminder[c(1, 3, 5), 4]
  # A tibble: 3 × 1
  #   lifeExp
  #     <dbl>
  # 1  28.801
  # 2  31.997
  # 3  36.088 # check these against data view

But what is ``c(1,3,5)``? It’s a vector of numbers – ``c()`` is for combine;

.. code-block :: R

  length(c(1, 3, 5))
  # [1] 3

  str(c(1, 3, 5))
  # num [1:3] 1 3 5

We can select these rows and all the columns;

.. code-block :: R

  gapminder[c(1, 3, 5),]
  # A tibble: 3 × 6
  #       country continent  year lifeExp      pop gdpPercap
  #         <chr>     <chr> <int>   <dbl>    <int>     <dbl>
  # 1 Afghanistan      Asia  1952  28.801  8425333  779.4453
  # 2 Afghanistan      Asia  1962  31.997 10267083  853.1007
  # 3 Afghanistan      Asia  1972  36.088 13079460  739.9811

A very useful special form of vector;

.. code-block :: R

  1:10
  # [1] 1 2 3 4 5 6 7 8 9 10

  6:2
  # [1] 6 5 4 3 2

  -1:-3
  # [1] -1 -2 -3


R expects you to know this shorthand – see e.g. its use of `1:3` in the output from `str()`, on the previous slide. For a ‘rectangular’ selection of rows and columns;

.. code-block :: R

  gapminder[20:22, 3:4]
  # A tibble: 3 x 2
  #    year lifeExp
  #   <int>   <dbl>
  # 1  1987  72.000
  # 2  1992  71.581
  # 3  1997  72.950

Negative values correspond to dropping those rows/columns;

.. code-block :: R

  gapminder[-3:-1704,] # everything but the first two rows will be dropped
  # A tibble: 2 x 6
  #       country continent  year lifeExp     pop gdpPercap 
  #         <chr>     <chr> <int>   <dbl>   <int>     <dbl>         
  # 1 Afghanistan      Asia  1952  28.801 8425333  779.4453       
  # 2 Afghanistan      Asia  1957  30.332 9240934  820.8530       

As well as storing numbers and character strings (like "United States", "Canada") R can also store logicals – `TRUE` and `FALSE`.
To make a new vector, with elements that are `TRUE` if life expectancy is above 71.5 and FALSE otherwise;

.. code-block :: R

  is.above.avg <- gapminder$lifeExp > 71.5

Let's see how many of the total were TRUE and how many were FALSE using the table() function.
The table() function will create a count table from a vector of categorical data.

.. code-block :: R

  table(is.above.avg)
  # is.above.avg
  # FALSE  TRUE 
  #  1329   375 

Which countries and during what years were these? (And what was the avg. life expectancy?)

.. code-block :: R

  gapminder[is.above.avg,] # just the rows for which is.above.avg is TRUE
  # A tibble: 375 x 6
  #      country continent  year lifeExp      pop gdpPercap 
  #        <chr>     <chr> <int>   <dbl>    <int>     <dbl>         
  #  1   Albania    Europe  1987  72.000  3075321  3738.933       
  #  2   Albania    Europe  1992  71.581  3326498  2497.438       
  #  3   Albania    Europe  1997  72.950  3428038  3193.055       
  #  4   Albania    Europe  2002  75.651  3508512  4604.212       
  #  5   Albania    Europe  2007  76.423  3600523  5937.030       
  #  6   Algeria    Africa  2007  72.301 33333216  6223.367       
  #  7 Argentina  Americas  1992  71.868 33958947  9308.419       
  #  8 Argentina  Americas  1997  73.275 36203463 10967.282       
  #  9 Argentina  Americas  2002  74.340 38331121  8797.641       
  # 10 Argentina  Americas  2007  75.320 40301927 12779.380       

  > gapminder[is.above.avg,4] # combining TRUE/FALSE (rows) and numbers (columns)
  # A tibble: 375 x 1
  #    lifeExp
  #      <dbl>
  #  1  72.000
  #  2  71.581
  #  3  72.950
  #  4  75.651
  #  5  76.423
  #  6  72.301
  #  7  71.868
  #  8  73.275
  #  9  74.340
  # 10  75.320

One final method... for now!

Instead of specifying rows/columns of interest by number, or through vectors of `TRUE`s/`FALSE`s, we can also just give the names – as character strings, or vectors of character strings.

.. code-block :: R

  gapminder[,'lifeExp']
  # A tibble: 1,704 x 1
  #    lifeExp
  #      <dbl>
  #  1  28.801
  #  2  30.332
  #  3  31.997
  #  4  34.020
  #  5  36.088
  #  6  38.438
  #  7  39.854
  #  8  40.822
  #  9  41.674
  # 10  41.763
  # # ... with 1,694 more rows

  gapminder[gapminder$country == 'Gabon',c("lifeExp","gdpPercap")]
  # A tibble: 12 x 2
  #    lifeExp gdpPercap
  #      <dbl>     <dbl>
  #  1  37.003  4293.476
  #  2  38.999  4976.198
  #  3  40.489  6631.459
  #  4  44.598  8358.762
  #  5  48.690 11401.948
  #  6  52.790 21745.573
  #  7  56.564 15113.362
  #  8  60.190 11864.408
  #  9  61.366 13522.158
  # 10  60.461 14722.842
  # 11  56.761 12521.714
  # 12  56.735 13206.485

  gapminder[gapminder$country == 'Gabon',4] # okay to mix & match
  # A tibble: 12 x 1
  #    lifeExp
  #      <dbl>
  #  1  37.003
  #  2  38.999
  #  3  40.489
  #  4  44.598
  #  5  48.690
  #  6  52.790
  #  7  56.564
  #  8  60.190
  #  9  61.366
  # 10  60.461
  # 11  56.761
  # 12  56.735

This is more typing than the other options, but is much easier to debug/reuse.

5.1.2 Dplyr
^^^^^^^^^^^

Remember how we mentioned earlier that data should be "tidy", that is each variable should be represented in one column and each row represents one observation.  The `tidyverse` has a package to help us work with data in a tidy way.  We are now going to discuss a package that helps you to manipulate your data, `dplyr`.

If you haven't already, install dplyr and load the package so we can use its functionality

.. code-block :: R

  install.packages('dplyr')
  library(dplyr)


dplyr works by piping commands, like you learned to do in the command line.  Instead of the pipe `|`, we use `%>%`.

Subsetting in dplyr uses two functions:
- ``select()``
- ``filter()``

Using select()

If, for example, we wanted to move forward with only a few of the variables in our dataframe we could use the `select()` function. This will subset the dataframe by columns.

.. code-block :: R

  # without pipes
  select(gapminder,year,country,gdpPercap)
  
  # with pipes
  gaminder %>% select(year,country,gdpPercap)
  
To help you understand why we wrote that in that way, let's walk through it step by step. 
First we summon the gapminder dataframe and pass it on, using the pipe symbol ``%>%``, to the next step, which is the ``select()`` function. 
In this case we don't specify which data object we use in the ``select()`` function since in gets that from the previous pipe.

.. important ::

  An important difference between `dplyr` and base R is when use character strings we don't need to enclose them in quotation marks as we did above (i.e. gapminder[,'year'])

Using filter()

Now what about subsetting rows?  For this we use the `filter` command:

.. code-block :: R

  gapminder %>% filter(lifeExp > 71.5)
  # A tibble: 375 x 7
  #      country continent  year lifeExp      pop gdpPercap lifeExpMonths
  #        <chr>     <chr> <int>   <dbl>    <int>     <dbl>         <dbl>
  #  1   Albania    Europe  1987  72.000  3075321  3738.933       864.000
  #  2   Albania    Europe  1992  71.581  3326498  2497.438       858.972
  #  3   Albania    Europe  1997  72.950  3428038  3193.055       875.400
  #  4   Albania    Europe  2002  75.651  3508512  4604.212       907.812
  #  5   Albania    Europe  2007  76.423  3600523  5937.030       917.076
  #  6   Algeria    Africa  2007  72.301 33333216  6223.367       867.612
  #  7 Argentina  Americas  1992  71.868 33958947  9308.419       862.416
  #  8 Argentina  Americas  1997  73.275 36203463 10967.282       879.300
  #  9 Argentina  Americas  2002  74.340 38331121  8797.641       892.080
  # 10 Argentina  Americas  2007  75.320 40301927 12779.380       903.840
  # ... with 365 more rows


If we now wanted to subset by columns and rows,  we can combine `select` and `filter`

.. code-block :: R

    year_country_gdp_mex <- gapminder %>%
        select(year,country,gdpPercap) %>% 
        filter(country=="Mexico")
    # A tibble: 12 x 3
    #    year country gdpPercap
    #   <int> <fct>       <dbl>
    # 1  1952 Mexico       3478
    # 2  1957 Mexico       4132
    # 3  1962 Mexico       4582
    # 4  1967 Mexico       5755
    # 5  1972 Mexico       6809
    # 6  1977 Mexico       7675
    # 7  1982 Mexico       9611
    # 8  1987 Mexico       8688
    # 9  1992 Mexico       9472
    #10  1997 Mexico       9767
    #11  2002 Mexico      10742
    #12  2007 Mexico      11978
     
- Challenge 1

Write a single command (which can span multiple lines and includes pipes) that will produce a dataframe that has the African values for ``lifeExp``, ``country`` and ``year``, but not for other Continents. How many rows does your dataframe have and why?

If we want to select all columns except 1, we can do that with the ``-`` operator.  

.. code-block :: R

  gapminder %>% select(-gdpPercap)
  
  # A tibble: 1,704 x 5
  #        country continent  year lifeExp      pop 
  #          <chr>     <chr> <int>   <dbl>    <int>              
  #  1 Afghanistan      Asia  1952  28.801  8425333         
  #  2 Afghanistan      Asia  1957  30.332  9240934         
  #  3 Afghanistan      Asia  1962  31.997 10267083        
  #  4 Afghanistan      Asia  1967  34.020 11537966         
  #  5 Afghanistan      Asia  1972  36.088 13079460         
  #  6 Afghanistan      Asia  1977  38.438 14880372         
  #  7 Afghanistan      Asia  1982  39.854 12881816         
  #  8 Afghanistan      Asia  1987  40.822 13867957         
  #  9 Afghanistan      Asia  1992  41.674 16317921         
  # 10 Afghanistan      Asia  1997  41.763 22227415         
  # ... with 1,694 more rows

If we want to make a new column, use ``mutate``.  Don't forget we have to assign it if we want to keep the changes

.. code-block :: R

  gapminder <- gapminder %>% mutate(lifeExpMonths= lifeExp*12)
  gapminder

  # A tibble: 1,704 x 7
  #        country continent  year lifeExp      pop gdpPercap lifeExpMonths 
  #          <chr>     <chr> <int>   <dbl>    <int>     <dbl>         <dbl>     
  #  1 Afghanistan      Asia  1952  28.801  8425333  779.4453       345.612   
  #  2 Afghanistan      Asia  1957  30.332  9240934  820.8530       363.984   
  #  3 Afghanistan      Asia  1962  31.997 10267083  853.1007       383.964   
  #  4 Afghanistan      Asia  1967  34.020 11537966  836.1971       408.240   
  #  5 Afghanistan      Asia  1972  36.088 13079460  739.9811       433.056   
  #  6 Afghanistan      Asia  1977  38.438 14880372  786.1134       461.256   
  #  7 Afghanistan      Asia  1982  39.854 12881816  978.0114       478.248   
  #  8 Afghanistan      Asia  1987  40.822 13867957  852.3959       489.864   
  #  9 Afghanistan      Asia  1992  41.674 16317921  649.3414       500.088   
  # 10 Afghanistan      Asia  1997  41.763 22227415  635.3414       501.156   
  # ... with 1,694 more rows
  
We can pipe several commands, just like with the command line:

.. code-block :: R

  gapminder %>% select(lifeExp, country) %>% filter(lifeExp > 71.5) %>% mutate(lifeExpdays = lifeExp * 365)
  # A tibble: 375 x 3
  #    lifeExp   country lifeExpdays
  #      <dbl>     <chr>       <dbl>
  #  1  72.000   Albania    26280.00
  #  2  71.581   Albania    26127.07
  #  3  72.950   Albania    26626.75
  #  4  75.651   Albania    27612.61
  #  5  76.423   Albania    27894.40
  #  6  72.301   Algeria    26389.87
  #  7  71.868 Argentina    26231.82
  #  8  73.275 Argentina    26745.38
  #  9  74.340 Argentina    27134.10
  # 10  75.320 Argentina    27491.80
  # ... with 365 more rows

We can also use outside information to help subset data.

.. code-block :: R

  two.countries <- c('Kenya', 'Gibon')

  gapminder %>% filter(country %in% two.countries)
  # A tibble: 12 x 7
  #    country continent  year lifeExp      pop gdpPercap lifeExpMonths
  #      <chr>     <chr> <int>   <dbl>    <int>     <dbl>         <dbl>
  #  1   Kenya    Africa  1952  42.270  6464046  853.5409       507.240
  #  2   Kenya    Africa  1957  44.686  7454779  944.4383       536.232
  #  3   Kenya    Africa  1962  47.949  8678557  896.9664       575.388
  #  4   Kenya    Africa  1967  50.654 10191512 1056.7365       607.848
  #  5   Kenya    Africa  1972  53.559 12044785 1222.3600       642.708
  #  6   Kenya    Africa  1977  56.155 14500404 1267.6132       673.860
  #  7   Kenya    Africa  1982  58.766 17661452 1348.2258       705.192
  #  8   Kenya    Africa  1987  59.339 21198082 1361.9369       712.068
  #  9   Kenya    Africa  1992  59.285 25020539 1341.9217       711.420
  # 10   Kenya    Africa  1997  54.407 28263827 1360.4850       652.884
  # 11   Kenya    Africa  2002  50.992 31386842 1287.5147       611.904
  # 12   Kenya    Africa  2007  54.110 35610177 1463.2493       649.320

``%in%`` will enable you to search all lines in the column country for all character strings in the two.countries file and will return a TRUE if it finds an one of them.

- EXERCISE - 3

Create a new dataframe that contains only country names, years, and life expectancies of the ``gapminder`` dataset. Use this new dataframe to calculate minimum & maximum life expectancies.

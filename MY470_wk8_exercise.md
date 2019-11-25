``` r
knitr::opts_chunk$set(fig.path = 'Figs/')
```

The goal of this exercise is to practice writing code in R. You will
have to use the content from this week’s lecture as well as the required
readings and the R documentation in order to answer the questions below.

We will mark the assignment based on the compiled html file, so please
check that the final version of your submission includes that file.
Submissions without a compiled html file will receive a mark of 0.

### Getting Started: Installing R and RStudio

Try knitting the [`TestRMarkdown.Rmd`](TestRMarkdown.Rmd) document. This
means that you will need to have:

1.  Installed RStudio.
2.  Installed R. (Preferably 3.6.1)
3.  Installed the **knitr** and **rmarkdown** packages. (When you open
    the `TestRMarkdown.Rmd` file, you should see a button for “Knit”.
    When you click on that, if the required packages are not yet
    installed, you should be prompted to install them.)
4.  When this is successful, you will have converted a mixture of
    Markdown and R code into an HTML document. This is am important
    step, since the homework is in Rmarkdown.

For the rest of the exercise, you will need to open the file
`MY470_wk8_exercise.Rmd` and work by modifying and knitting that (this!)
file. Note that in the “YAML” header, you will be using the
[`md_document` output
format](http://rmarkdown.rstudio.com/markdown_document_format.html).
This produces a markdown file that can be viewed nicely on GitHub.

### 1. R basics

Open RStudio and explore the programme. Make sure you can identify the
`console`, the script editor, the `environment` window, the `packages`
window and the `help` window!

1.  Use the code below to create a vector of the integers 1 through 5.
    Examine the
    [RMarkdown](https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf)
    code block below. This is the R equivalent of a Jupyter notebook
    “cell”.

It is entered as follows:

    ```{r eval=TRUE}
    my_vec <- c(1, 2, 3, 4, 5)
    ```

And when knitted, produces this output:

``` r
my_vec <- c(1, 2, 3, 4, 5)
```

In RStudio, you can insert code blocks in R (or Python) using the
“Insert” button in the Source pane, or by typing the code fence triple
backticks and the the `{r}` manually.

b Multiply each element of your vector by 3, and assign the output to a
new object. `print` the values of your new object. Here, we have given
the answer to you for free.

``` r
my_new_vec <- my_vec * 3
print(my_new_vec)
```

    ## [1]  3  6  9 12 15

c Add together the two objects that you have created to far,
`print()`ing the result. Note that R operates on vectors element-wise.

``` r
print(my_new_vec + my_vec)
```

    ## [1]  4  8 12 16 20

1.  Create a logical vector of length five, again using the `c()`
    function. Make sure that you have a mix of `TRUE` and `FALSE` values
    in the vector. Use the logical vector to subset the numeric vector
    that you created in question 2 and `print` the result.

``` r
log_vec <- c(TRUE, FALSE, FALSE, TRUE, FALSE)
#subset my_new_vec using log_vec
print(my_new_vec[log_vec])
```

    ## [1]  3 12

### 2. Working with text

Here, we revisit some of the same issues as in [Week
2](https://github.com/lse-my470/assignment-2/blob/master/MY470_wk2_assign.ipynb).

We will use the same text:

``` r
txt <- "Someone must have been telling lies about Josef K., he knew he had
done nothing wrong but, one morning, he was arrested.  Every day at
eight in the morning he was brought his breakfast by  Mrs. Grubach's
cook - Mrs. Grubach was his landlady - but today she didn't come.  That
had never happened before.  K. waited a little while, looked from his
pillow at the old woman who lived opposite and who was watching him with
an inquisitiveness quite unusual for her, and finally, both hungry and
disconcert"

# this splits the text by whitespace
toks <- unlist(strsplit(txt, "\\s"))
```

Answer the questions below by creating your own chunks of code to find
the right answer:

1.  What is the type of the object `toks`? (Hint: Examine it using the
    same tools as from the lecture notes.)

``` r
typeof(toks)
```

    ## [1] "character"

1.  How many elements are in `toks`? And how many *unique* elements?

``` r
# the number of elements in `toks`:
length(toks)
```

    ## [1] 93

``` r
#the number of unique elements in `toks`:
length(unique(toks))
```

    ## [1] 74

1.  What are the most common three words? Hint: See `?table`.

``` r
#"words" here should mean actual words, not punctuation, spaces, or other characters. As required,we do not need to remove them (necessarily) but you should not count them in the answer to this question.
word_frequency <- tail(sort(table(toks)))
#after result print, we could see the one of the top three common words is a space, therefore we shoul eliminate it
#and also have the same frequency with "his", therefore I add "and" here
top_three_word <- tail(word_frequency)[-4][2:5]
# the most common three words in a decendig order are:
sort(names(top_three_word), decreasing = TRUE)
```

    ## [1] "was" "his" "he"  "and"

### 3. Working with a dataset.

This exercise relates to the `College` data set, which comes from [An
Introduction to Statistical
Learning](http://www-bcf.usc.edu/~gareth/ISL/data.html) by James et al
2013. It contains a number of variables for 777 different universities
and colleges in the US.

For convenience, we have placed the `.csv` file in this repository.

Use the `read.csv()` function to read the data into `R`. Call the loaded
data `college`. Make sure that you have the directory set to the correct
location for the data. You can load this in R directly from the website,
using:

``` r
college <- read.csv("http://www-bcf.usc.edu/~gareth/ISL/College.csv")
```

Or you can load it from a saved file, using (you might need to modify
the path):

``` r
college <- read.csv("/Users/YSR/Desktop/MY470/assignment-8-betoriay-master/College.csv")
```

1.  Look at the data using the `View()` function. Create a code block
    and output the results of printing the first 6 rows of the dataset,
    using the `head()` function.

``` r
View(college)
head(college)
```

    ##                              X Private Apps Accept Enroll Top10perc Top25perc
    ## 1 Abilene Christian University     Yes 1660   1232    721        23        52
    ## 2           Adelphi University     Yes 2186   1924    512        16        29
    ## 3               Adrian College     Yes 1428   1097    336        22        50
    ## 4          Agnes Scott College     Yes  417    349    137        60        89
    ## 5    Alaska Pacific University     Yes  193    146     55        16        44
    ## 6            Albertson College     Yes  587    479    158        38        62
    ##   F.Undergrad P.Undergrad Outstate Room.Board Books Personal PhD Terminal
    ## 1        2885         537     7440       3300   450     2200  70       78
    ## 2        2683        1227    12280       6450   750     1500  29       30
    ## 3        1036          99    11250       3750   400     1165  53       66
    ## 4         510          63    12960       5450   450      875  92       97
    ## 5         249         869     7560       4120   800     1500  76       72
    ## 6         678          41    13500       3335   500      675  67       73
    ##   S.F.Ratio perc.alumni Expend Grad.Rate
    ## 1      18.1          12   7041        60
    ## 2      12.2          16  10527        56
    ## 3      12.9          30   8735        54
    ## 4       7.7          37  19016        59
    ## 5      11.9           2  10922        15
    ## 6       9.4          11   9727        55

1.  Use the `str()` function to look at the structure of the data. Which
    of the variables are numeric? Which are integer? Which are factors?

``` r
str(college)
```

    ## 'data.frame':    777 obs. of  19 variables:
    ##  $ X          : Factor w/ 777 levels "Abilene Christian University",..: 1 2 3 4 5 6 7 8 9 10 ...
    ##  $ Private    : Factor w/ 2 levels "No","Yes": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ Apps       : int  1660 2186 1428 417 193 587 353 1899 1038 582 ...
    ##  $ Accept     : int  1232 1924 1097 349 146 479 340 1720 839 498 ...
    ##  $ Enroll     : int  721 512 336 137 55 158 103 489 227 172 ...
    ##  $ Top10perc  : int  23 16 22 60 16 38 17 37 30 21 ...
    ##  $ Top25perc  : int  52 29 50 89 44 62 45 68 63 44 ...
    ##  $ F.Undergrad: int  2885 2683 1036 510 249 678 416 1594 973 799 ...
    ##  $ P.Undergrad: int  537 1227 99 63 869 41 230 32 306 78 ...
    ##  $ Outstate   : int  7440 12280 11250 12960 7560 13500 13290 13868 15595 10468 ...
    ##  $ Room.Board : int  3300 6450 3750 5450 4120 3335 5720 4826 4400 3380 ...
    ##  $ Books      : int  450 750 400 450 800 500 500 450 300 660 ...
    ##  $ Personal   : int  2200 1500 1165 875 1500 675 1500 850 500 1800 ...
    ##  $ PhD        : int  70 29 53 92 76 67 90 89 79 40 ...
    ##  $ Terminal   : int  78 30 66 97 72 73 93 100 84 41 ...
    ##  $ S.F.Ratio  : num  18.1 12.2 12.9 7.7 11.9 9.4 11.5 13.7 11.3 11.5 ...
    ##  $ perc.alumni: int  12 16 30 37 2 11 26 37 23 15 ...
    ##  $ Expend     : int  7041 10527 8735 19016 10922 9727 8861 11487 11644 8991 ...
    ##  $ Grad.Rate  : int  60 56 54 59 15 55 63 73 80 52 ...

**Numeric variables are S.F.Ratio; Integer variables are Apps, Accept,
Enroll, Top10perc, Top25perc, F.Undergrad, P.Undergrad, Outstate,
Room.Board, Books, Personal, PhD, Terminal, perc.alumni, Expend,
Grad.Rate; Factors variables are Private, and X(which actually refers to
college name )**

1.  Use the `summary()` function to produce a numerical summary of the
    variables in the data set.

``` r
summary(college)
```

    ##                             X       Private        Apps           Accept     
    ##  Abilene Christian University:  1   No :212   Min.   :   81   Min.   :   72  
    ##  Adelphi University          :  1   Yes:565   1st Qu.:  776   1st Qu.:  604  
    ##  Adrian College              :  1             Median : 1558   Median : 1110  
    ##  Agnes Scott College         :  1             Mean   : 3002   Mean   : 2019  
    ##  Alaska Pacific University   :  1             3rd Qu.: 3624   3rd Qu.: 2424  
    ##  Albertson College           :  1             Max.   :48094   Max.   :26330  
    ##  (Other)                     :771                                            
    ##      Enroll       Top10perc       Top25perc      F.Undergrad   
    ##  Min.   :  35   Min.   : 1.00   Min.   :  9.0   Min.   :  139  
    ##  1st Qu.: 242   1st Qu.:15.00   1st Qu.: 41.0   1st Qu.:  992  
    ##  Median : 434   Median :23.00   Median : 54.0   Median : 1707  
    ##  Mean   : 780   Mean   :27.56   Mean   : 55.8   Mean   : 3700  
    ##  3rd Qu.: 902   3rd Qu.:35.00   3rd Qu.: 69.0   3rd Qu.: 4005  
    ##  Max.   :6392   Max.   :96.00   Max.   :100.0   Max.   :31643  
    ##                                                                
    ##   P.Undergrad         Outstate       Room.Board       Books       
    ##  Min.   :    1.0   Min.   : 2340   Min.   :1780   Min.   :  96.0  
    ##  1st Qu.:   95.0   1st Qu.: 7320   1st Qu.:3597   1st Qu.: 470.0  
    ##  Median :  353.0   Median : 9990   Median :4200   Median : 500.0  
    ##  Mean   :  855.3   Mean   :10441   Mean   :4358   Mean   : 549.4  
    ##  3rd Qu.:  967.0   3rd Qu.:12925   3rd Qu.:5050   3rd Qu.: 600.0  
    ##  Max.   :21836.0   Max.   :21700   Max.   :8124   Max.   :2340.0  
    ##                                                                   
    ##     Personal         PhD            Terminal       S.F.Ratio    
    ##  Min.   : 250   Min.   :  8.00   Min.   : 24.0   Min.   : 2.50  
    ##  1st Qu.: 850   1st Qu.: 62.00   1st Qu.: 71.0   1st Qu.:11.50  
    ##  Median :1200   Median : 75.00   Median : 82.0   Median :13.60  
    ##  Mean   :1341   Mean   : 72.66   Mean   : 79.7   Mean   :14.09  
    ##  3rd Qu.:1700   3rd Qu.: 85.00   3rd Qu.: 92.0   3rd Qu.:16.50  
    ##  Max.   :6800   Max.   :103.00   Max.   :100.0   Max.   :39.80  
    ##                                                                 
    ##   perc.alumni        Expend        Grad.Rate     
    ##  Min.   : 0.00   Min.   : 3186   Min.   : 10.00  
    ##  1st Qu.:13.00   1st Qu.: 6751   1st Qu.: 53.00  
    ##  Median :21.00   Median : 8377   Median : 65.00  
    ##  Mean   :22.74   Mean   : 9660   Mean   : 65.46  
    ##  3rd Qu.:31.00   3rd Qu.:10830   3rd Qu.: 78.00  
    ##  Max.   :64.00   Max.   :56233   Max.   :118.00  
    ## 

1.  What is the mean and standard deviation of the `Enroll` and
    `Top10Perc` variables? You should use the functions `mean()` and
    `sd()` for the answer.

``` r
mean(college$Enroll)
```

    ## [1] 779.973

``` r
sd(college$Enroll)
```

    ## [1] 929.1762

``` r
mean(college$Top10perc)
```

    ## [1] 27.55856

``` r
sd(college$Top10perc) 
```

    ## [1] 17.64036

1.  Now remove the 10th through 85th observations. This will involve
    slicing the data, similar to in Python, but for the row element.
    What is the mean and standard deviation of the `Enroll` and
    `Top10perc` variables in the subset of the data that remains?

``` r
new_college <- college[c(-85:-10), ]
mean(new_college$Enroll)
```

    ## [1] 787.913

``` r
sd(new_college$Enroll)
```

    ## [1] 931.2228

``` r
mean(new_college$Top10perc)
```

    ## [1] 27.45221

``` r
sd(new_college$Top10perc)
```

    ## [1] 17.64522

1.  What is the range of the `Books` variable? Hint: Use `range()`.

``` r
range(college$Books, na.rm = TRUE)
```

    ## [1]   96 2340

1.  Produce a scatterplot matrix of the first five numeric variables of
    the dataset.

``` r
#Use Filter Function to select all numeric type of variable
my_df<- Filter(is.numeric, college)

#Select the first five numeric variables to draw a scatterplot matrix
pairs(my_df[1:5], pch = 19, cex = 0.5)
```

![](Figs/unnamed-chunk-17-1.png)

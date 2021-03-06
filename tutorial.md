[![](https://res.cloudinary.com/dchysltjf/image/upload/f_auto,q_auto:best/v1574281173/Signal_Banner_2.png)](https://www.datacamp.com/signal)

Loading data into R can be quite frustrating. Almost every single type
of file that you want to get into R seems to require its own function,
and even then you might get lost in the functionsâ€™ arguments. In short,
it can be fairly easy to mix up things from time to time, whether you
are a beginner or a more advanced R user.

To cover these needs, DataCamp decided to publish a comprehensive, yet
easy tutorial to quickly import data into R, going from simple text
files to the more advanced SPSS and SAS files. Continue to read this
tutorial to find out how you easily import your files into R!

(Try this interactive course: [Importing Data in R (Part
1)](https://www.datacamp.com/courses/importing-data-in-r-part-1/), to
work with CSV and Excel files in R.)

**Contents**

-   [Read CSV, TXT, HTML, and Other Common Files into R](#Getting)
    -   [Read TXT files with read.table()](#txt)
    -   [Read CSV Files into R](#csv)
    -   [read.delim() for Delimited Files](#files)
    -   [XLConnect Package for Reading Excel Files](#excel)
    -   [Read JSON Files](#javascript)
    -   [Read XML Files](#xml)
    -   [Read HTML Tables](#data)
-   [Read SAS, SPSS, and Other Datasets into R](#Getting_Statistical)
    -   [SPSS Files](#spss)
    -   [Read Stata Files](#stata)
    -   [Read Systat Files](#systat)
    -   [Read SAS Files](#sas)
    -   [Read Minitab Files](#minitab)
    -   [Read RDA or RData Files](#rda)
-   [Read Databases and Other Sources Into R](#Getting_Other)
    -   [Read Relational and Non-Relational Databases into R](#data1)
    -   [Through Webscraping](#data2)
    -   [Through The TM Package](#data3)

\

Checking Your Data {#Your}
------------------

To start, you first need to have data. The data can be saved in a file
onto your computer in an Excel, SPSS, or some other file type. When your
data is saved locally, you can go back to it later to edit, to add more
data or to change them, preserving the formulas that you maybe used to
calculate the data, etc.

However, data can also be found on the Internet or can be obtained
through other sources.

Where to find these data are out of the scope of this tutorial, so for
now itâ€™s enough to mention this [list of data
sets](http://www.kdnuggets.com/datasets/index.html), and DataCampâ€™s
[interactive
tutorial](https://www.datacamp.com/courses/quandl-r-tutorial/), which
deals with how to import and manipulate Quandl data sets.

Before you move on and discover how to load your data into R, it might
be useful to go over the following checklist that will make it easier to
import the data correctly into R:

-   If you work with spreadsheets, the first row is usually reserved for
    the header, while the first column is used to identify the sampling
    unit;
-   Avoid names, values or fields with blank spaces, otherwise each word
    will be interpreted as a separate variable, resulting in errors that
    are related to the number of elements per line in your data set;
-   If you want to concatenate words, inserting a . in between to words
    instead of a space;
-   Short names are prefered over longer names;
-   Try to avoid using names that contain symbols such as `?`, `$`,`%`,
    `^`, `&`, `*`, `(`, `)`,`-`,`#`, `?`,`,`,`<`,`>`, `/`, `|`, `\`, `[`
    ,`]` ,`{`, and `}`;
-   Delete any comments that you have made in your Excel file to avoid
    extra columns or NAâ€™s to be added to your file; and
-   Make sure that any missing values in your data set are indicated
    with `NA`.

\

Preparing Your R Workspace {#Preparing}
--------------------------

Make sure to go into RStudio and see what needs to be done before you
start your work there. You might have an environment that is still
filled with data and values, which you can all delete using the
following line of code:

        rm(list=ls())

The `rm()` function allows you to â€śremove objects from a specified
environmentâ€ť. In this case, you specify that you want to consider a list
for this function, which is the outcome of the `ls()` function. This
last function returns you a vector of character strings that gives the
names of the objects in the specified environment. Since this function
has no argument, it is assumed that you mean the data sets and functions
that you as a user have defined.

Next, you might also find it handy to know where your working directory
is set at the moment:

eyJsYW5ndWFnZSI6InIiLCJzYW1wbGUiOiJnZXR3ZCgpIn0=

\
\

And you might consider changing the path that you get as a result of
this function, maybe to the folder in which you have stored your data
set:

        setwd("<location of your dataset>")

Read CSV, TXT, HTML, and Other Common Files into R {#Getting}
--------------------------------------------------

You will notice that the following basic R functions focus on getting
spreadsheets into R, rather than Excel or other type of files. If you
are more interested in the latter, scroll a bit further to discover the
ways of importing other files into R.

### Read TXT files with read.table() {#txt}

If you have a `.txt` or a tab-delimited text file, you can easily import
it with the basic R function `read.table()`. In other words, the
contents of your file will look similar to this

        1   6   a
        2   7   b
        3   8   c
        4   9   d
        5   10  e

and can be imported as follows:

eyJsYW5ndWFnZSI6InIiLCJzYW1wbGUiOiJkZiA8LSByZWFkLnRhYmxlKFwiaHR0cHM6Ly9zMy5hbWF6b25hd3MuY29tL2Fzc2V0cy5kYXRhY2FtcC5jb20vYmxvZ19hc3NldHMvdGVzdC50eHRcIiwgXG4gICAgICAgICAgICAgICAgIGhlYWRlciA9IEZBTFNFKVxuZGYifQ==

\
\

**Note** that ideally, you should just pass in the file name and the
extension because you have set your working directory to the folder in
which your data set is located. Youâ€™ll have seen in the code chunk above
that the first argument isnâ€™t always a filename, but could possibly also
be a webpage that contains data. The `header` argument specifies whether
or not you have specified column names in your data file. Lastly, youâ€™ll
see that, by using this function, your data from the file will become a
`data.frame` object.

Inspect the final result of your importing in the DataCamp Light chunk!

Itâ€™s good to know that the `read.table()` function is the most important
and commonly used function to import simple data files into R. It is
easy and flexible. That is why you should check out our previous
tutorial on [reading and importing Excel files into
R](https://www.datacamp.com/community/tutorials/r-tutorial-read-excel-into-r/),
which explains in great detail how to use the `read.table()` function
optimally.

For files that are not delimited by tabs, like `.csv` and other
delimited files, you actually use variants of this basic function.

These variants are almost identical to the `read.table()` function and
differ from it in three aspects only:

-   The separator symbol;
-   The `header` argument is always set at TRUE, which indicates that
    the first line of the file being read contains the header with the
    variable names;
-   The `fill` argument is also set as TRUE, which means that if rows
    have unequal length, blank fields will be added implicitly.

\
\

[![Learn Python for Data Science With
DataCamp](http://community.datacamp.com.s3.amazonaws.com/community/production/ckeditor_assets/pictures/293/content_blog_banner.png)](https://www.datacamp.com/courses/)

\

### Read CSV Files into R {#csv}

If your separates the values with a `,` or `;`, you usually are working
with a `.csv` file. Its contents will look similar to this:

        Col1,Col2,Col3
        1,2,3
        4,5,6
        7,8,9
        a,b,c

Make sure that you have saved the file as a regular csv file without a
Byte Order Mark (BOM). If you have done this, youâ€™ll see weird
characters appearing at the beginning of your imported data if you donâ€™t
add the extra argument `fileEncoding = "UTF-8-BOM"` to your importing
function!

To successfully load this file into R, you can use the `read.table()`
function in which you specify the separator character, or you can use
the `read.csv()` or `read.csv2()` functions. The former function is used
if the separator is a `,`, the latter if `;` is used to separate the
values in your data file.

Remember that the `read.csv()` as well as the `read.csv2()` function are
almost identical to the `read.table()` function, with the sole
difference that they have the `header` and `fill` arguments set as
`TRUE` by default.

eyJsYW5ndWFnZSI6InIiLCJzYW1wbGUiOiIjIFJlYWQgaW4gY3N2IGZpbGVzXG5kZiA8LSByZWFkLnRhYmxlKFwiaHR0cHM6Ly9zMy5hbWF6b25hd3MuY29tL2Fzc2V0cy5kYXRhY2FtcC5jb20vYmxvZ19hc3NldHMvdGVzdC5jc3ZcIiwgXG4gICAgICAgICAgICAgICAgIGhlYWRlciA9IEZBTFNFLFxuICAgICAgICAgICAgICAgICBzZXAgPSBcIixcIilcblxuZGYgPC0gcmVhZC5jc3YoXCJodHRwczovL3MzLmFtYXpvbmF3cy5jb20vYXNzZXRzLmRhdGFjYW1wLmNvbS9ibG9nX2Fzc2V0cy90ZXN0LmNzdlwiLFxuICAgICAgICAgICAgICAgaGVhZGVyID0gRkFMU0UpXG5cbmRmIDwtIHJlYWQuY3N2MihcImh0dHBzOi8vczMuYW1hem9uYXdzLmNvbS9hc3NldHMuZGF0YWNhbXAuY29tL2Jsb2dfYXNzZXRzL3Rlc3QuY3N2XCIsIFxuICAgICAgICAgICAgICAgaGVhZGVyPSBGQUxTRSlcblxuIyBJbnNwZWN0IHRoZSByZXN1bHRcbmRmIn0=

\
\

Tip: if you want to learn more about the arguments that you can use in
the `read.table()`, `read.csv()` or `read.csv2()` functions, you can
always check out our [reading and importing Excel files into
R](https://www.datacamp.com/community/tutorials/r-tutorial-read-excel-into-r/)
tutorial, which explains in great detail how to use the `read.table()`,
`read.csv()` or `read.csv2()` functions.

Note that if you get a warning message that reads like â€śincomplete final
line found by readTableHeaderâ€ť, you can try to go and â€śstandâ€ť on the
cell that contains the last value (`c` in this case) and press ENTER.
This will normally fix the warning because the message indicates that
the last line of the file doesnâ€™t end with an End Of Line (EOL)
character, which can be a linefeed or a carriage return and linefeed.
Donâ€™t forget to save the file to make sure that your changes are saved!

**Pro-Tip**: use a text editor like NotePad to make sure that you add an
EOL character without adding new rows or columns to your data.

Also note that if you have initialized other cells than the ones that
your data contains, youâ€™ll see some rows or columns with `NA` values
appear. The best case is then to remove those rows and columns!

### read.delim() for Delimited Files {#files}

In case you have a file with a separator character that is different
from a tab, a comma or a semicolon, you can always use the
`read.delim()` and `read.delim2()` functions. These are variants of the
`read.table()` function, just like the `read.csv()` function.

Consequently, they have much in common with the `read.table()` function,
except for the fact that they assume that the first line that is being
read in is a header with the attribute names, while they use a tab as a
separator instead of a whitespace, comma or semicolon. They also have
the `fill` argument set to `TRUE`, which means that blank field will be
added to rows of unequal length.

You can use the `read.delim()` and `read.delim2()` functions as follows:

eyJsYW5ndWFnZSI6InIiLCJzYW1wbGUiOiIjIFJlYWQgYSBkZWxpbWl0ZWQgZmlsZVxuZGYgPC0gcmVhZC5kZWxpbShcImh0dHBzOi8vczMuYW1hem9uYXdzLmNvbS9hc3NldHMuZGF0YWNhbXAuY29tL2Jsb2dfYXNzZXRzL3Rlc3RfZGVsaW0udHh0XCIsIHNlcD1cIiRcIikgXG5kZiA8LSByZWFkLmRlbGltMihcImh0dHBzOi8vczMuYW1hem9uYXdzLmNvbS9hc3NldHMuZGF0YWNhbXAuY29tL2Jsb2dfYXNzZXRzL3Rlc3RfZGVsaW0udHh0XCIsIHNlcD1cIiRcIilcblxuIyBJbnNwZWN0IHRoZSByZXN1bHRcbmRmIn0=

\
\

### XLConnect Package for Reading Excel Files {#excel}

To load Excel files into R, you first need to do some further prepping
of your workspace in the sense that you need to install packages.

Simply run the following piece of code to accomplish this:

        install.packages("<name of the package>")

When you have installed the package, you can just type in the following
to activate it in your workspace:

eyJsYW5ndWFnZSI6InIiLCJzYW1wbGUiOiIjIEZpbGwgaW4gYSBwYWNrYWdlIG5hbWVcbmxpYnJhcnkoXCI8bmFtZSBvZiB0aGUgcGFja2FnZT5cIilcblxuIyBDaGVjayBpZiB5b3UgYWxyZWFkeSBpbnN0YWxsZWQgdGhlIHBhY2thZ2VcbmFueShncmVwbChcIjxuYW1lIG9mIHlvdXIgcGFja2FnZT5cIiwgXG4gICAgICAgICAgaW5zdGFsbGVkLnBhY2thZ2VzKCkpKSIsInNvbHV0aW9uIjoiIyBGaWxsIGluIGEgcGFja2FnZSBuYW1lXG5saWJyYXJ5KFwiZGF0YS50YWJsZVwiKVxuXG4jIENoZWNrIGlmIHlvdSBhbHJlYWR5IGluc3RhbGxlZCB0aGUgcGFja2FnZVxuYW55KGdyZXBsKFwiZGF0YS50YWJsZVwiLCBcbiAgICAgICAgICBpbnN0YWxsZWQucGFja2FnZXMoKSkpIn0=

\
\

#### Importing Excel Files With The XLConnect Package

The first way to get Excel files directly into R is by using the
`XLConnect` package. Install the package and if youâ€™re not sure whether
or not you already have it, check if it is already there.

Next, you can start using the `readWorksheetFromFile()` function, just
like shown here below:

        library(XLConnect)
        df <- readWorksheetFromFile("<file name and extension>",
                                    sheet = 1)

**Note** that you need to add the `sheet` argument to specify which
sheet you want to load into R. You can also add more specifications. You
can find these explained in our tutorial on [reading and importing Excel
files into
R](https://www.datacamp.com/community/tutorials/r-tutorial-read-excel-into-r/).

You can also load in a whole workbook with the `loadWorkbook()`
function, to then read in worksheets that you desire to appear as data
frames in R through `readWorksheet()`:

        wb <- loadWorkbook("<name and extension of your file>")
        df <- readWorksheet(wb,
                            sheet=1) 

**Note** again that the `sheet` argument is not the only argument that
you can use in `readWorkSheetFromFile()` . If you want more information
about the package or about all the arguments that you can pass to the
`readWorkSheetFromFile()` function or to the two alternative functions
that were mentioned, you can visit the packageâ€™s
[RDocumentation](http://www.rdocumentation.org/packages/XLConnect) page.

#### Importing Excel Files With The Readxl Package

The `readxl` package allows R users to easily read in Excel files, just
like this:

        library(readxl)
        df <- read_excel("<name and extension of your file>")

**Note** that the first argument specifies the path to your `.xls` or
`.xlsx` file, which you can set by using the `getwd()` and `setwd()`
functions. You can also add a `sheet` argument, just like with the
XLConnect package, and many more arguments on which you can read up
[here](https://github.com/hadley/readxl) or in this [blog
post](http://blog.rstudio.org/2015/04/15/readxl-0-1-0/).

### Read JSON Files Into R {#javascript}

To get [JSON](http://json.org/) files into R, you first need to install
or load the [rjson](http://www.rdocumentation.org/packages/rjson)
package. If you want to know how to install packages or how to check if
packages are already installed, scroll a bit up to the section of
importing Excel files into R :)

Once this is done, you can use the `fromJSON()` function. Here, you have
two options:

1.  Your JSON file is stored in your working directory:

\

        # Activate `rjson`
        library(rjson)
        
        # Import data from json file
        JsonData <- fromJSON(file= "<filename.json>" )

2.  Your JSON file is available through a URL:

\

        # Activate `rjson`
        library(rjson)
        
        # Import data from json file
        JsonData <- fromJSON(file= "<URL to your JSON file>" )

### Read XML Data Into R {#xml}

If you want to get XML data into R, one of the easiest ways is through
the usage of the [XML](http://www.rdocumentation.org/packages/XML)
package. First, you make sure you install and load the XML package in
your workspace, just like demonstrated above. Then, you can use the
`xmlTreeParse()` function to parse the XML file directly from the web:

        # Activate the `XML` library
        library(XML)
        
        # Parse the XML file
        xmlfile <- xmlTreeParse("<Your URL to the XML data>")

Next, you can check whether R knows that `xmlfile` is in XML by
entering:

        # Result is usually similar to this: [1] "XMLDocument"         "XMLAbstractDocument"
        class(xmlfile)

**Tip**: you can use the `xmlRoot()` function to access the top node:

        topxml <- xmlRoot(xmlfile)

You will notice the data is presented kind of weirdly when printing out
the `xmlfile` vector. That is because the XML file is still a real XML
document in R at this point. To put the data in a data frame, you first
need to extract the XML values. You can use the `xmlSApply()` function
to do this:

        topxml <- xmlSApply(topxml,
                            function(x) xmlSApply(x, xmlValue))

The first argument of this function will be `topxml`, since it is the
top node on whose children you want to perform a certain function. Then,
you list the function that you want to apply to each child node. In this
case, you want to extract the contents of a leaf XML node. This, in
combination with the first argument `topxml`, will make sure that you
will do this for each leaf XML node.

Finally, you put the values in a dataframe!

You use the `data.frame()` function in combination with the matrix
transpostition function `t()` to do this. Additionally you also specify
that no row names should be included:

        xml_df <- data.frame(t(topxml),
                             row.names=NULL)

If you think the previous steps are a bit too complicated, just do the
following:

        url <- "<a URL with XML data>"
        data_df <- xmlToDataFrame(url)

### Importing Data From HTML Tables Into R {#data}

From HTML tables into R is pretty straightforward:

        # Assign your URL to `url`
        url <- "<a URL>"
        
        # Read the HTML table
        data_df <- readHTMLTable(url,
                                 which=3)

**Note** that the `which` argument allows you to specify which tables to
return from within the document.

If this gives you an error in the nature of â€śfailed to load external
entityâ€ť, donâ€™t be confused: this error has been signaled by many people
and has been confirmed by the packageâ€™s author
[here](http://comments.gmane.org/gmane.comp.lang.r.mac/2284).

You can work around this by using the `RCurl` package in combination
with the `XML` package to read in your data:

        # Activate the libraries
        library(XML)
        library(RCurl)
        
        # Assign your URL to `url`
        url <- "YourURL"
        
        # Get the data
        urldata <- getURL(url)
        
        # Read the HTML table
        data <- readHTMLTable(urldata,
                              stringsAsFactors = FALSE)

**Note** that you donâ€™t want the strings to be registered as factors or
categorical variables! You can also use the httr package to accomplish
exactly the same thing, except for the fact that you will want to
convert the raw objects of the URLâ€™s content to characters by using the
`rawToChar` argument:

        # Activate `httr`
        library(httr)
        
        # Get the URL data
        urldata <- GET(url)
        
        # Read the HTML table
        data <- readHTMLTable(rawToChar(urldata$content),
                              stringsAsFactors = FALSE)

\

[![import data in
R](http://community.datacamp.com.s3.amazonaws.com/community/production/ckeditor_assets/pictures/293/content_blog_banner.png)](https://www.datacamp.com/courses/)

\

Read SAS, SPSS, and Other Datasets into R {#Getting_Statistical}
-----------------------------------------

As you already know, R is a programming language and software
environment for statistical computing. Thatâ€™s why it probably wonâ€™t come
as a surprise when I say that many people use R as an open-source
alternative to commercial statistical programs, such as SPSS, SAS, etc.

In this section, youâ€™ll see how you can import data from advanced
statistical software programs: youâ€™ll see which packages that you need
to install to read your data files into R, just like you have done with
data that was stored in Excel or JSON files.

### Read SPSS Files into R {#spss}

If youâ€™re a user of SPSS software and you are looking to import your
SPSS files into R, firstly install the
[foreign](https://cran.r-project.org/web/packages/foreign/foreign.pdf)
package. After loading the package, run the `read.spss()` function that
is contained within it and you should be good to go!

        # Activate the `foreign` library
        library(foreign)
        
        # Read the SPSS data
        mySPSSData <- read.spss("example.sav")

**Tip** if you wish the result to be displayed in a data frame, make
sure to set the `to.data.frame` argument of the `read.spss()` function
to `TRUE`. Furthermore, if you do NOT want the variables with value
labels to be converted into R factors with corresponding levels, you
should set the `use.value.labels` argument to `FALSE`:

        # Activate the `foreign` library
        library(foreign)
        
        # Read the SPSS data
        mySPSSData <- read.spss("example.sav",
                               to.data.frame=TRUE,
                               use.value.labels=FALSE)

**Remember** that factors are variables that can only contain a limited
number of different values. As such, they are often called â€ścategorical
variablesâ€ť. The different values of factors can be labeled and are
therefore often called â€śvalue labelsâ€ť

### Read Stata Files into R {#stata}

To import Stata files, you keep on using the `foreign` package. Use the
`read.dta()` function to get your data into R:

        # Activate the `foreign` library
        library(foreign)
        
        # Read Stata data into R
        mydata <- read.dta("<Path to file>") 

### Read Systat Files into R {#systat}

If you want to get Systat files into R, you also want to use the
[`foreign`](https://www.rdocumentation.org/packages/foreign/versions/0.8-67)
package, just like shown below:

        # Activate the `foreign` library
        library(foreign)
        
        # Read Systat data
        mydata <- read.systat("<Path to file>") 

### Read SAS Files into R {#sas}

For users that also want to import SAS files into R, itâ€™s quite simple!
For starters, install the `sas7bdat` package. Load it, and then invoke
the `read.sas7bdat()` function contained within the package and you are
good to go!

        # Activate the `sas7bdat` library
        library(sas7bdat)
        
        # Read in the SAS data
        mySASData <- read.sas7bdat("example.sas7bdat")

Does this function interest you and do you want to know more? Visit the
[Rdocumentation](http://www.rdocumentation.org/packages/sas7bdat/functions/read.sas7bdat)
page.

Note that you can also use the `foreign` library to load in SAS data in
R. In such cases, youâ€™ll start from a SAS Permanent Dataset or a SAS
XPORT Format Library with the `read.ssd()` and `read.xport()` functions,
respectively. For more information, click
[here](https://www.rdocumentation.org/packages/foreign/versions/0.8-67).

### Read Minitab Files into R {#minitab}

Is your software of choice for statistical purposes Minitab? Look no
further if you want to use Minitab data in R!

Importing `.mtp` files into R is pretty straightforward. It wonâ€™t come
as a surprise any more that youâ€™ll need to install the
[foreign](https://cran.r-project.org/web/packages/foreign/foreign.pdf)
package and load it. Then simply use the `read.mtp()` function from that
package:

        # Activate the `foreign` library
        library(foreign)
        
        # Read the Minitab data
        myMTPData <- read.mtp("example2.mtp")

### Read RDA or RData Files into R {#rda}

If your data file is one that you have saved in R as an `.rdata` file,
you can read it in as follows:

        load("<FileName>.RDA")

Read Databases and Other Sources Into R {#Getting_Other}
---------------------------------------

Since this tutorial focuses on importing data from different types of
sources, it is only right to also briefly mention that you can import
data into R that comes from databases, webscraping, etc.

### Read Relational and Non-Relational Databases into R {#data1}

#### Importing Data From Relational Databases

For more information on getting data from relational databases into R,
check out [this
tutorial](https://www.monetdb.org/Documentation/UserGuide/MonetDB-R) for
importing data from **MonetDB**.

If, however, you want to load data from **MySQL** into R, you can follow
this [tutorial](https://www.r-bloggers.com/accessing-mysql-through-r/),
which uses the dplyr package to import the data into R.

If you are interested in knowing more about this last package, make sure
to check out DataCampâ€™s [interactive
course](https://www.datacamp.com/courses/dplyr-data-manipulation-r-tutorial/),
which is definitely a must for everyone that wants to use dplyr to
access data stored outside of R in a database. Furthermore, the course
also teaches you how to perform sophisticated data manipulation tasks
using dplyr!

#### Importing Data From Non-Relational Databases

For more information on loading data from non-relational databases into
R, like data from **MongoDB**, you can read this
[blogpost](https://statcompute.wordpress.com/2013/06/08/r-and-mongodb/)
from â€śYet Another Blog in Statistical Computingâ€ť for an overview on how
to load data from MongoDB into R.

### Importing Data Through Webscraping {#data2}

You can read up on how to scrape JavaScript data with R with the use of
PhantomJS and the `rvest` package in this [DataCamp
tutorial](https://www.datacamp.com/community/tutorials/scraping-javascript-generated-data-with-r/).
If you want to use APIs to import your data, you can easily find one
[here](http://www.programmableweb.com/apis/directory).

**Tip**: you can check out [this
set](http://quantifyingmemory.blogspot.co.uk/2014/02/web-scraping-basics.html)
of amazing tutorials which deal with the basics of webscraping.

### Importing Data Through The TM Package {#data3}

For those of you who are interested in importing textual data to start
mining texts, you can read in the text file in the following way after
having installed and activated the
[`tm`](http://www.rdocumentation.org/packages/tm) package:

        text <- readLines("<filePath>")

Then, you have to make sure that you load these data as a corpus in
order to get started correctly:

        docs <- Corpus(VectorSource(text))

You can find an accessible tutorial on text mining with R
[here](http://www.exegetic.biz/blog/2013/09/text-mining-the-complete-works-of-william-shakespeare/).

This Is Just The Beginningâ€¦
---------------------------

Loading your data into R is just a small step in your exciting data
analysis, manipulation and visualization journey. DataCamp is here to
guide you through it!

Continue with our [Importing Data in
R](https://www.datacamp.com/courses/importing-data-in-r-part-1/) course
or go and build models with your data: our [machine
learning](https://www.datacamp.com/community/tutorials/machine-learning-in-r/)
will definitely come in handy, just like our [Introduction to Machine
Learning](https://www.datacamp.com/courses/introduction-to-machine-learning-with-r/).

If you want to continue with data manipulation, go through the DataCamp
tutorial on [15 Easy Solutions To Your Data Frame Problems In
R](https://www.datacamp.com/community/tutorials/15-easy-solutions-data-frame-problems-r/)
or consider taking DataCampâ€™s [data.table
course](https://www.datacamp.com/courses/data-table-data-manipulation-r-tutorial/).

Are you not sure where to start? Check out [DataCampâ€™s course
curriculum](https://www.datacamp.com/courses/) and discover what lies
ahead in your data science journey with DataCamp!

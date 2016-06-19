This is an analysis of GDP by Income Group. The r markdown file will download 2 files (GDP and Educ data) from worldbank.org, tidy the data, and merge the two data sets. The packages required are repmis, plyr, dplyr (must be installed after plyr), and ggplot2.

##**Introduction** 

This is an analysis of GDP from 2014. We will also analyze education statistics from 1970-current. The data sets are provided by worldbank.org. We will download, tidy, and merge the data sets together. Then, we will obtain the average rankings for the "High Income: Organisation for Economic Co-operation and Development (OECD)" and also for the "High Income: nonOECD" groups. Additionally, we will plot the countries by GDP with colors according to their Income Group. Finally, we will separate the countries into 5 quantile groups by GDP; then, out of the top quantile, we will determine the number of countries whose income group is "Lower middle income".

###**Setting environment**

  * Load necessary packages and set directories

###**Loading data**

 1. Downloads GDP file from https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv 
    + Reads file into gdp and checks variable names
    + Variable names don't look normal, so read file into gdp without header
    
 2. Downloads Educ file from  https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv
    + Reads file into educ and checks variable names

###**Tidying data**

 1. educ data
    + Subsets educ into educ.tidy with only CountryCode and Income.Group variables
    + Checks for NA values
 
 2. gdp data
    + Checks number of NA values in entire data frame
    + Checks number of NA values in variables V3, V7, V8, and V9
        + all observations for variables V3, V7, V8, and V9 are NA values
    + Checks variable V6 to see if it contains valid data or all blank values
    + Creates gdp.tidy data with the following tidying
        + removes first 5 rows because they are headers and/or blanks
        + removes variables V3, V7, V8, and V9 as they contain all NA values
        + removes variable V6 as it contains only a few values of a,b,c,d,e,f which after looking at the data set online, it is for footnotes about the various countries
        + Removes observations where variable V1 is blank & where variable V2 is blank
        + Removes double quotes (") and commas from any variable V5
        + Converts variables V2 and V5 to integer
        + Divides variable V5 by 1000 for better visibiliy in plot
        + Sets variable names to "CountryCode", "Rank", "CountryName", "Dollars.in.Billions" respectively

###**Merging data**

  * Merges gdp and educ tidy data frames by variable CountryCode
    + Verifies number of matches during the merge
    + Sorts in descending order by variable rank
    + Checks first 5 observations of the first and second variable to verify sort worked as designed
    + Obtains the 13th observation's country
    + Views table of variable Income.Group to determine values
    + Calculates means of Income.Group = "High income: nonOECD"
    + Calculates means of Income.Group = "High income: OECD"

###**Analyzing data**

 1. Plots Dollars.in.Billions by CountryCode (colored by Income Group), including interpretation of the plot

 2. Creates a table quantile versus income group and determines how many countries are Lower middle income but among the 38 nations with the highest GDP

###**Answers the following questions**
**Question 1. After merging, how many of the country codes matched?**

**Question 2. After sorting, what is the 13th country**

**Question 3. What are the average GDP rankings for the "High income: OECD" and the "High income: nonOECD" groups?**

**Question 4. Plot the GDP for all of the countries. Use ggplot2 to color your plot by income group**

**Question 5. Make a table quantile versus income group. How many countries are Lower middle income but among the 38 nations with the highest GDP?**

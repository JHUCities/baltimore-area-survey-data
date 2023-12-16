2023 Baltimore Area Survey
==========================

Data for the 2023 Baltimore Area Survey may be found in this directory. Data are saved in a comma-delimited-format file and as an `.Rdata` file for use with R software and are documented on the [documentation page](https://jhucities.github.io/baltimore-area-survey-data/bas-2023).

Weighting
---------

The data collected by the Baltimore Area Survey are representative of residents in Baltimore City and Baltimore County. To get results that accurately represent the population of the Baltimore-area, however, __you must apply survey weights to your analysis__. 

### Brief Overview

The survey weights adjust for two ways that the sample may not represent all residents:

1. Some places were sampled at a rate higher than the number of people that lived there (for example, we sampled at a higher rate in Baltimore City than in Baltimore County)
2. The unequal probability that someone receiving the survey would respond (for example, response rates tend to be higher among those with college degrees than those without)

The survey weights account for both of these elements. Therefore, the raw totals from a variable will not accurately represent the true rates of responses among Baltimore-area residents. You can read details about the construction of survey weights in the [BAS 2023 documentation](https://jhucities.github.io/baltimore-area-survey-data/bas-2023/methodology.html#weighting). 


### Applying Weights

The sample weight for each respondent is included in the variable `bas23_svy_fwgt`. 

Using weights will differ based on the software package that you use to analyze the data. To use weights in R, a free and open-source statistical software program, you will need to install the `survey` package, which you only need to do once using the command:

```r
install.packages("survey")
```

To apply the weights you would then use the following commands:

```r
library(survey)
load("data/bas-2023/baltimore-area-survey-2023.Rdata")
bassvy <- svydesign(~1, weights = ~bas23_svy_fwgt, data = bas23)
```

Other statistical packages such as Stata, SAS, SPSS, or Python will require different methods. You should view the documentation for commands in those packages to apply survey weights. 

Citation
--------

Bader, Michael DM, Mac McComas, Alexi Williams, Marin Beal, Raghav Agrawal, and Stephanie Leveron. 2023. “Baltimore Area Survey 2023.” Version 1.0. December 5, 2023. https://github.com/JHUCities/baltimore-area-survey-data/.
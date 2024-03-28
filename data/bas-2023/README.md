2023 Baltimore Area Survey
==========================

Data for the 2023 Baltimore Area Survey may be found in this directory. Documentation of the data, including data collection methods and a codebook, are included on the [documentation page](https://jhucities.github.io/baltimore-area-survey-data/bas-2023).

Data Format
-----------

The canonical version of the data are saved as a comma separated value (.csv) format in the file `baltimore-area-survey-2023.csv`. 

The data are also saved in `.Rdata` format that convert the categorical variables to factor and apply labels. These data are saved to the object `bas23` in the file `baltimore-area-survey-2023.Rdata`. This file is provided for convenience. The canonical CSV data should be used as the primary source of data. 

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

Other statistical packages such as Stata, SAS, SPSS, or Python will require different methods ([examples][] for applying survey weights using other software packages are available from the Office of Advanced Research Computing at UCLA). You should view the documentation for commands in those packages to apply survey weights. 

[examples]: https://stats.oarc.ucla.edu/other/mult-pkg/faq/faq-choosing-the-correct-analysis-for-various-survey-designs/

Citation
--------

Bader, Michael DM, Mac McComas, Alexi Williams, Marin Beal, Raghav Agrawal, and Stephanie Leveron. 2023. “Baltimore Area Survey 2023.” Version 1.0. December 5, 2023. https://github.com/JHUCities/baltimore-area-survey-data/.

Change Log
----------

* 2023-03-28 (version 1.1)
	- Saves values of variables as numeric codes in CSV file
	- Fixes variable `svy_csaid` to use 2020 Census tract crosswalk to BNIA Community Statistical Areas. The data previously used an outdated crosswalk to 2010 Census tract and Community Statistical Area definitions.
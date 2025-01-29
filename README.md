Baltimore Area Survey Data
==========================

This repository contains data for the Baltimore Area Surveys.

The surveys are conducted annually by the [21st Century Cities Initiative (21CC)](https://21cc.jhu.edu/) at Johns Hopkins University. The data are collected from independent samples of adult residents in Baltimore City and Baltimore County every year. The data are organized by year, with documentation for each wave of data contained within the directory for that year. 

More information about the Baltimore Area Survey can be found on the [21CC website](https://21cc.jhu.edu/bas). Questions about the data can be directed to 21cc@jhu.edu.

Data
----

Surveys are organized by year in the `data` directory. 

The canonical version of the data are saved as a comma separated value (.csv) format in the file `baltimore-area-survey-YEAR.csv`, replacing `YEAR` with the four-digit year (e.g., the 2023 data will be saved in the file `baltimore-area-survey-2023.csv`). The canonical CSV data should be used as the primary source of data. 

As a convenience, the data are also saved in `.Rdata` format for use in R, an [open-source statistical software program](https://www.r-project.org/) that can be used for data visualization and analysis. The `.Rdata` format converts variables to the type `factor` that assigns labels to values and analyzes data as categorical by default. In each data file, the data are saved to the object `basYY` replacing `YY` with the two-digit year (e.g., the BAS 2023 data will be loaded in the object `bas23`). 

Variables are prepended with a prefix that indicates the year that the variable was collected. For example, all variable names included in the BAS 2023 will be prepended with the prefix `bas23_`.

Documentation & Codebooks
-------------------------

Documentation for surveys can be found at https://jhucities.github.io/baltimore-area-survey-data/. The data are documented by year and provide documentation for both the methods of data collection and codebooks describing variables. 

Citation
--------

If you use the data, please cite the data that you use. The README.md file in each data directory and the documention include recommended citations. 

Weighting
---------

The data collected by the Baltimore Area Survey are representative of residents in Baltimore City and Baltimore County. To get results that accurately represent the population of the Baltimore-area, however, __you must apply survey weights to your analysis__. 

### Brief Overview

The survey weights adjust for two ways that the sample may not represent all residents:

1. Some places were sampled at a rate higher than the number of people that lived there (for example, we sampled at a higher rate in Baltimore City than in Baltimore County)
2. The unequal probability that someone receiving the survey would respond (for example, response rates tend to be higher among those with college degrees than those without)

The survey weights account for both of these elements. Therefore, the raw totals from a variable will not accurately represent the true rates of responses among Baltimore-area residents. You can read details about the construction of survey weights in the [BAS 2023 documentation](https://jhucities.github.io/baltimore-area-survey-data/bas-2023/methodology.html#weighting). 


### Applying Weights

The sample weight for each respondent is included in the variable `<svy>_svy_fwgt` where `<svy>` will be the prefix `basYY` where `YY` is the two-digit year. 

Using weights will differ based on the software package that you use to analyze the data. To use weights in R, a free and open-source statistical software program, you will need to install the `survey` package, which you only need to do once using the command:

```r
install.packages("survey")
```

To apply the weights for the BAS 2023 you would then use the following commands:

```r
library(survey)
load("data/bas-2023/baltimore-area-survey-2023.Rdata")
bassvy <- svydesign(~1, weights = ~bas23_svy_fwgt, data = bas23)
```

Other statistical packages such as Stata, SAS, SPSS, or Python will require different methods ([examples][] for applying survey weights using other software packages are available from the Office of Advanced Research Computing at UCLA). You should view the documentation for commands in those packages to apply survey weights. 

[examples]: https://stats.oarc.ucla.edu/other/mult-pkg/faq/faq-choosing-the-correct-analysis-for-various-survey-designs/

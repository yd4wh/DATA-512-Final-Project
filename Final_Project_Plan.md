# Final-Project-Plan
Project Plan for DATA 512, Autumn 2018

Name: Yumeng Ding	

Date: November 22nd, 2018


## Introduction

This project uses [College Scorecard Data](https://collegescorecard.ed.gov/data/) published by the U.S. Department of Education to understand the landscape of higher education from the perspectives of demographic composition, ownership of the institution versus availability of federal student loan, and cost of enrollment versus post-school earnings. The goal of this project is to provide a high-level composition analysis and comparison of different types of college and the return on investments on higher education.


## Background

During the Obama administration, one of his [initiatives](https://obamawhitehouse.archives.gov/issues/education/higher-education) was to provide more transparency to higher education. One of the goals of this initiative was to link federal funding to performance after graduation. A by-product of this initiative was the release of previously unavailable information like average family income of students, completion metrics and student earnings data through the U.S. Department of Education of a dataset called [College Scorecard Data](https://collegescorecard.ed.gov/data/). 

The release of this dataset enabled us to compare the outcomes of colleges across states and regions, across types of ownerships, and across different admissions criteria. It also enabled us to analyze different aspects of diversity among colleges, such as racial diversity and programs offered diversity. 

Therefore, I plan to clean the rich dataset into a smaller subset of data that will include four-year degree granting institutions with variables related to regions, states, racial composition, admissions information, federal funding information, and post-graduation earnings. I will then use the smaller subset to explore racial diversity in US colleges, and correlation among admissions criteria, enrollment costs and return on education investments.


## Data 

### Data Description

The data used for this project consists two main static csv files and one data dictionary file for lookup purposes:

* [2017 College Scorecard Data](https://ed-public-download.app.cloud.gov/downloads/Most-Recent-Cohorts-All-Data-Elements.csv): Full dataset on 7175 US higher education institutions in 2016-2017 year, including 7175 rows and 1899 columns

* [2017 Post-school Earnings](https://ed-public-download.app.cloud.gov/downloads/Most-Recent-Cohorts-Treasury-Elements.csv): Comprehensive earnings data on 7175 US higher education institutions in 2016-2017 year, including 7175 rows and 92 columns

* [Data Dictionary](https://collegescorecard.ed.gov/assets/CollegeScorecardDataDictionary.xlsx): dictionary file for understanding different measurements and column variables in all College Scorecard Data (this dataset will not be used for the analysis, it is mainly for lookup and understanding purposes)

All datasets used for this projects are publicly available and accessible under [CC0 1.0 Universal (CC0 1.0) Public Domain Dedication](https://creativecommons.org/publicdomain/zero/1.0/) within the United States. 


Due to the large amount of variables in both datasets, below are descriptions of subsets of both datasets that will later be used for analysis:

#### 2017 College Scorecard Data

The college scorecard data consists of ten main categories of information according to its [documentation](https://collegescorecard.ed.gov/data/documentation/): Root, School, Academics, Admissions, Student, Cost, Aid, Repayment, Completion, and Earnings. 

The project will focus on:

	School: Name, Location, Degree Type, Public/Private Nonprofit/Private For-Profit
	Admissions: Acceptance Rate, SAT scores
	Student: Number of Undergraduate Students, Undergraduate Student Body by Race/Ethnicity
	Cost: Average Cost of Attendance, Tuition and Fees, Average Faculty Salary
	Aid: Percent of Undergraduates Receiving Federal Loans

Cleaned version of College Scorecard Data will include the following schema:

| VARIABLE NAME  | DATA TYPE | CATEGORY   | DESCRIPTION                                                                               |
|----------------|-----------|------------|-------------------------------------------------------------------------------------------|
| INSTNM         | string    | school     | Institution name                                                                          |
| CITY           | string    | school     | City                                                                                      |
| STABBR         | string    | school     | State postcode                                                                            |
| ZIP            | string    | school     | ZIP code                                                                                  |
| SCH_DEG        | integer   | school     | Predominant degree awarded (recoded 0s and 4s)                                            |
| PREDDEG        | integer   | school     | Predominant undergraduate degree awarded                                                  |
| CONTROL        | integer   | school     | Control of institution                                                                    |
| REGION         | integer   | school     | 10 regions of US including Outlying Areas                                                 |
| ADM_RATE       | float     | admissions | Admission rate                                                                            |
| SATVRMID       | float     | admissions | Midpoint of SAT scores at the institution (critical reading)                              |
| SATMTMID       | float     | admissions | Midpoint of SAT scores at the institution (math)                                          |
| SATWRMID       | float     | admissions | Midpoint of SAT scores at the institution (writing)                                       |
| UG             | integer   | student    | Enrollment of all undergraduate students                                                  |
| UG_NRA         | float     | student    | Total share of enrollment of undergraduate students who are non-resident aliens           |
| UG_UNKN        | float     | student    | Total share of enrollment of undergraduate students whose race is unknown                 |
| UG_WHITENH     | float     | student    | Total share of enrollment of undergraduate students who are white non-Hispanic            |
| UG_BLACKNH     | float     | student    | Total share of enrollment of undergraduate students who are black non-Hispanic            |
| UG_API         | float     | student    | Total share of enrollment of undergraduate students who are Asian/Pacific Islander        |
| UG_AIANOLD     | float     | student    | Total share of enrollment of undergraduate students who are American Indian/Alaska Native |
| UG_HISPOLD     | float     | student    | Total share of enrollment of undergraduate students who are Hispanic                      |
| COSTT4_A       | integer   | cost       | Average cost of attendance (academic year institutions)                                   |
| TUITIONFEE_IN  | integer   | cost       | In-state tuition and fees                                                                 |
| TUITIONFEE_OUT | integer   | cost       | Out-of-state tuition and fees                                                             |
| AVGFACSAL      | integer   | cost       | Average faculty salary                                                                    |
| PCTFLOAN       | float     | aid        | Percent of all undergraduate students receiving a federal student loan                    |


#### 2017 Post-school Earnings

The post-school earnings dataset include comprehensive measures of employment and earnings data subgrouped into 10, 8, 7 and 6 years after entry into the insititution, for this analysis, we will keep 10 years and 6 years after entry for a time length comparison.

Cleaned version of Post-school Earnings Data will include the following schema:

| VARIABLE NAME      | DATA TYPE | CATEGORY | DESCRIPTION                                                                              |
|--------------------|-----------|----------|------------------------------------------------------------------------------------------|
| INSTNM             | string    | earnings | Institution name                                                                         |
| UNEMP_RATE         | float     | earnings | unemployment rate                                                                        |
| COUNT_NWNE_P10     | integer   | earnings | Number of students not working and not enrolled 10 years after entry                     |
| COUNT_WNE_P10      | integer   | earnings | Number of students working and not enrolled 10 years after entry                         |
| MN_EARN_WNE_P10    | integer   | earnings | Mean earnings of students working and not enrolled 10 years after entry                  |
| MD_EARN_WNE_P10    | integer   | earnings | Median earnings of students working and not enrolled 10 years after entry                |
| PCT10_EARN_WNE_P10 | integer   | earnings | 10th percentile of earnings of students working and not enrolled 10 years after entry    |
| PCT25_EARN_WNE_P10 | integer   | earnings | 25th percentile of earnings of students working and not enrolled 10 years after entry    |
| PCT75_EARN_WNE_P10 | integer   | earnings | 75th percentile of earnings of students working and not enrolled 10 years after entry    |
| PCT90_EARN_WNE_P10 | integer   | earnings | 90th percentile of earnings of students working and not enrolled 10 years after entry    |
| SD_EARN_WNE_P10    | integer   | earnings | Standard deviation of earnings of students working and not enrolled 10 years after entry |
| COUNT_NWNE_P6      | integer   | earnings | Number of students not working and not enrolled 6 years after entry                      |
| COUNT_WNE_P6       | integer   | earnings | Number of students working and not enrolled 6 years after entry                          |
| MN_EARN_WNE_P6     | integer   | earnings | Mean earnings of students working and not enrolled 6 years after entry                   |
| MD_EARN_WNE_P6     | integer   | earnings | Median earnings of students working and not enrolled 6 years after entry                 |
| PCT10_EARN_WNE_P6  | integer   | earnings | 10th percentile of earnings of students working and not enrolled 6 years after entry     |
| PCT25_EARN_WNE_P6  | integer   | earnings | 25th percentile of earnings of students working and not enrolled 6 years after entry     |
| PCT75_EARN_WNE_P6  | integer   | earnings | 75th percentile of earnings of students working and not enrolled 6 years after entry     |
| PCT90_EARN_WNE_P6  | integer   | earnings | 90th percentile of earnings of students working and not enrolled 6 years after entry     |
| SD_EARN_WNE_P6     | integer   | earnings | Standard deviation of earnings of students working and not enrolled 6 years after entry  |


### Potential Data Limitation

After initial exploratory analysis of the data, I decided to only include the most recent year's data into my analysis. However, in the [main data download page](https://collegescorecard.ed.gov/data/), users can download raw data as far back as 1997. Since this analysis will not be focusing on time series trend change of College Scorecard data, I will not be including historical data, but the same analysis can be applied to previous years as well. 

Due to the maintenance nature of these datasets, some colleges no longer have all the information listed above, therefore, some institutions will be removed during the data cleaning step due to NULL data values.


### Repoducibility

All datasets used for this analysis are static datasets hosted on the U.S. Department of Education website(retrivable via links provided above). Developers can also use API calls to retrieve the same datasets.

	The College Scorecard API is a GET API that lives at http://api.data.gov/ed/collegescorecard/
	The endpoint for querying all data is /v1/schools
	The basic structure of an API call is year.dev-category.dev-friendly-variable-name.
		* The year may be any year of data available (for this analysis: 2017), or use the word latest to get the most recent data available from the API. Using the "latest" key will allow your application to access the new data as soon as it is released.
		* The school category has no year.
		* id, ope6_id, ope8_id and location have no category or year.


## Project Plan

### Research Questions


### Anticipated Results


### Human Centered Design Considerations


### Unknowns and Dependencies

The understanding and interpretation of correlation between tuition and earnings is very complex and sometimes subjective, there are factors like high cost of living that could cause both variables to increase or decrease simultanously. We will not be incorporating living expense and regional dependencies in the analysis, and these factors will remain unknowns to this particular project scope.





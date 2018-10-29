## 311 Service Request
[3-1-1](https://en.wikipedia.org/wiki/3-1-1) is a phone number in the United States that provides access to non-emergency municipal services. This analysis will look into all 311 Service Requests from 2010 to 2018 and try to answer the following questions.
1. Consider only the 10 most common overall complaint types. For each borough, how many of each of those 10 types were there in 2017?
2. Consider only the 10 most common overall complaint types.  For the 10 most populous zip codes, how many of each of those 10 types were there in 2017?
3. Considering all complaint types. Which boroughs are the biggest "complainers" relative to the size of the population in 2017? Meaning, calculate a complaint-index that adjusts for population of the borough.

To answer the questions, following 3 data source are used as input.
* All 311 Service Requests from 2010 to 2018 (https://nycopendata.socrata.com/Social-Services/311-Service-Requests-from-2010-to-Present/erm2-nwe9)
* The 2010 US Census Population By Zip Code (https://blog.splitwise.com/2013/09/18/the-2010-us-census-population-by-zip-code-totally-free/)
* ZIP Code Definitions of New York City Boroughs (https://www.health.ny.gov/statistics/cancer/registry/appendix/neighborhoods.htm)

The latter is saved as [borough_zip.txt](borough_zip.txt) and available in repository.

## Data Analysis
Jupyter Notebook [service_request.ipynb](service_request.ipynb) used for this data analysis and consists of following main steps.
1. Data ingestion into pandas dataframe for the above-mentioned data sources (cells 2, 7, 12 respectively)
2. Preprocessing
    1. Exclude service request data columns that are not required for this analysis (cell 2)
    2. Extract year from Created Date column (cell 4)
    3. Validate extracted years (cell 6)
    4. Lookup zip codes' populations and boroughs (cells 9, 13)
    5. Validate zip code and population (cell 8)
    6. Create subset of service request dataframe for year 2017 (cell 15)
    7. Exclude missing population and validate (cells 9, 11)
3. Processing and aggregations for each question
    1. Cell 16, question 1
    2. Cell 22, question 2
    3. Cells 23, 24 and 25, question 3

## Assumptions
Only one assumption was made prior to this data analysis. The main concern is to have valid input data 
1. In case a zip code does not belong to the borough column value in service request data, it is assumed that the zip code is correct and the borough will be replaced with correct one.
Assuming otherwise will leave the record without zip code, hence population which is a required input for answering questions 2 and 3. A workaround would be to impute the missing population with average borough population which is another approach but will exclude those records from answer to question 3.
If the zip code does not belong to New York City, the record will be dropped with validation introduced in cell 13.

## References
1. Style: [PEP 8](https://www.python.org/dev/peps/pep-0008)


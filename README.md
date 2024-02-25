# Analyzing the Effect of School-level Sociodemographic Factors on State Math Assessment Results in NYC Public Schools

## Contributors
- Lara Karacasu

## I. Introduction

This project aims to analyze the effect of school-level sociodemographic indicators on the percentage of NYC public school students passing the NY State Math assessment, accounting for variability at borough levels. The novelty in this project lies in its merging of two distinct NYC public school datasets to derive new insights into indicators for math exam performance via a multi-level model. While some basic summary statistics are publicly available, analyses on both datasets in tandem do not exist online to my knowledge, and neither do analyses that leverage this data to account the multi-level nature of the research question.

### i. Problem Context

Each year, New York public school students in grades 3-8 take a state-wide math exam known as the NY State Math Test. The assessment contains several different mathematics multiple choice and open-ended questions. Exams are specific to the grade and year, meaning that all NY public school students within the same grade, and within the same year, take the same exam. The exam results are aggregated at the school-level for each grade and year, then released by the Department of Education. There are 4 levels of achievement: 1, 2, 3, and 4. Achieving a 3 or 4 on the exam qualifies as 'passing' the exam.

Additionally, demographic data is collected yearly on these same public schools. This data will be described further in the 'Data' section, but it generally includes school data on socioeconomic variables, ethnicity, gender, English-language learners, and special education rates. I use the term 'sociodemographic' factors to encompass both economic demographics (like the percentage of student on free lunch program) and social demographics (percent of students belonging to different races, percentage of male/female students, etc.). This term is used to concisely describe a broad range of social and economic variables.

### ii. Data Context

The exam data itself is used so that NY state can determine school-level mathematics performance. Schools with lower pass rates may receive additional state support, as lower pass rates indicate that the schools may not currently be meeting state-wide mathematics standards for grades 3 - 8. The data itself is released for public use, to inform the public of general school performance in the NY State Math Test. The school-level demographic information is used for similar reasons, as the state often makes financial and political decisions based on school demographics. I will use this data to understand how school-level socioeconomic factors are linked to school pass rates, while controlling for borough-level differences.

## II. Data

The data needed to accomplish this project includes school-level information about sociodemographic factors as well as information about each borough in which each school is located. Such features were not present in a singular dataset, so I decided to merge two different datasets over the 2006 - 2012 time period from NYC Open Data, Department of Education. The datasets are as follows: “2006 - 2012 School Demographics and Accountability Snapshot” and “2006 - 2012 Math Test Results - All Students."

## III. Priors and Model Adjustments

A multilevel beta regression model was selected due to the response variable being a proportion (percentage of students who passed the exam). Adjustments were made to accommodate the hierarchical structure of schools within districts within boroughs, and to handle boundary values in the dataset.

## Analysis

### Model Convergence and Selection

Six models were assessed for convergence, with a non-nested hierarchical model showing proper convergence. This model, incorporating informative priors, was selected as the most reliable for interpreting the effect of sociodemographic factors.

## V. Conclusions

### Comparisons and Model Performance

Out of the six models, the model with the uninformative priors and the nesting structure has the lowest WAIC. This would suggest that model_uninformative_12 fits the data best. However, we should keep in mind that only the two non-nested model properly converged. Out of those two converged models, m_informative_2 performed the best.

### Summary and Implications

The analysis highlights the importance of economic indicators, particularly the eligibility for free lunch, as the primary sociodemographic factor affecting academic performance. This underscores the need for policies aimed at reducing income inequality to improve educational outcomes.

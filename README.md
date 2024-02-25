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

The distribution of each variable is summarized below:

![Variable Distributions](https://github.com/larakaracasu/Bayesian-Multilevel-Model/blob/main/images/bayesian-1.png)

It seems that some of the predictors quite widely in their distributions. For example, looking at the third
quantile racial composition predictors, it seems like Asian and white students seem to have lower enrollment
rates at the schools within the dataset than Black and Hispanic students. Additionally, the percent of
students eligible for free lunch is also skewed toward larger percentages, while the opposite is true for the
proportion of English-language learners. Finally, inspecting the response variable, we see that pass_rates are
better than chance, as the median pass_rate is around 0.6, and the distribution also seems to be bimodal.

## III. Priors and Model Adjustments

A multilevel beta regression model was selected due to the response variable being a proportion (percentage of students who passed the exam). Adjustments were made to accommodate the hierarchical structure of schools within districts within boroughs, and to handle boundary values in the dataset.

## Analysis

### Model Convergence and Selection

Six models were assessed for convergence. They can be summarized as follows:

- Model 1.1: Nested Hierarchical Model, Uninformative Priors
- Model 1.1.2: Nested Hierarchical Model, Uninformative Priors (Convergence-Adjusted)
- Model 1.2: Non-Nested Hierarchical Model, Uninformative Priors
- Model 2.1: Nested Hierarchical Model, Informative Priors
- Model 2.1.2: Nested Hierarchical Model, Informative Priors (Convergence-Adjusted)
- Model 2.2: Non-Nested Hierarchical Model, Informative Priors

Read 'project-report' for details on the parameters and specifications of each of the above models.

The model results are below:

![Summary](https://github.com/larakaracasu/Bayesian-Multilevel-Model/blob/main/images/bayesian-4.png)

Out of the six models, the model with the uninformative priors and hierarchical nesting structure (m_uninformative_12) has the lowest WAIC. This would suggest that m_uninformative_12 fits the data best. However, only the two non-nested model properly converged. Out of those two converged models, m_informative_2 (Model 2.2) performed the best. Thus, we should keep m_informative_2 as our final model.

A non-nested hierarchical model with informative priors was selected as the most reliable for interpreting the effect of sociodemographic factors, as it is the model across all six models. The Markov chain traceplots for Model 2.1 shown below:

![Traceplot](https://github.com/larakaracasu/Bayesian-Multilevel-Model/blob/main/images/bayesian-3.png)

Evidently, the MCMC traceplots are expectedly "fuzzy" with no clear abnormalities.
Thus, we can say that the m_informative_2, the model with informative priors with a non-hierarchical prior set-up, likely converged.

The posterior confidence intervals for the coefficients of m_informative_2 are summarized in the plot below:

![Plot](https://github.com/larakaracasu/Bayesian-Multilevel-Model/blob/main/images/bayesian-2.png)

For the final model, the only significant sociodemographic predictor that was significantly different from
zero, was b_fl. B_fl is the coefficient for the percentage of students within a school who are eligible for free
lunch.

## V. Conclusions

### Implications

The model that fit the data best AND converged was m_informative_2. This is
the non-nested model with priors informed by previous literature. Interestingly, all models with informed
priors outperformed all models with flat priors in terms of WAIC.

The results align with the previous literature, which found the economic indicators were the primary sociodemo-
graphic factor involved in determining perform on academic assessments. The findings indicate that race
and status as an English-language learner, the other school-level features accounted for, were not significant
predictors of pass rates for the NY State Math Test. Even when accounting for variations at the borough
level, the results suggest that students’ eligibility for free lunch (a direct proxy for socioeconomic status)
was the most important factor of those tested within this project. While keeping in mind that the data
is limited to 2008, the broader implications of these findings are that the state should likely devote more
attention toward bridging gaps in income inequity if they aim to improve eighth graders’ performance on
the NY State Math Exam.

The analysis highlights the importance of economic indicators, particularly the eligibility for free lunch, as the primary sociodemographic factor affecting academic performance. This underscores the need for policies aimed at reducing income inequality to improve educational outcomes.

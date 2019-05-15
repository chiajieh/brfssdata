# brfssdata
Exploratory Data Analysis of the 2013 BRFSS Data
---
View project on https://chiajieh.github.io/brfssdata/
---
### Chinwe Ajieh | chinweajieh@gmail.com

## Setup

### Install Package

We will install `ggpubr` package using `install.packages("ggpubr")` as we need one of its function to merge/arrange more than one ggplots.


### Load Packages

```{r load-packages, message = FALSE}
library(ggplot2)
library(dplyr)
library(ggpubr)
library(DT)
```

### Load Data

```{r load-data}
load("brfss2013.RData")
```
* * *

## Part 1: Data

The [Behavioral Risk Factor Surveillance System (BRFSS)](www.cdc.gov/brfss) is an ongoing surveillance system (hence an observational study) designed to measure behavioral risk factors for the non-institutionalized adult population (18 years of age and older) residing in the US. Surveillance data on risk behaviors are collected through monthly telephone interviews (both landline telephone, from a randomly selected adult in a household and cellular telephone, from an adult who participates by using a cellular telephone and resides in a private residence or college housing) for all 50 states, the District of Columbia, Puerto Rico, Guam and the US Virgin Islands. All 50 states, the District of Columbia, Puerto Rico, and Guam collect data annually, and American Samoa, Federated States of Micronesia, and Palau collect survey data over a limited point-in-time (usually one to three months). 

Data collection is done with a standardized questionnaire following the [BRFSS protocol](https://www.cdc.gov/brfss/data_documentation/pdf/UserguideJune2013.pdf) to ensure a quality report.

The BRFSS uses two samples: one for landline telephone respondents and one for cellular telephone respondents.
Since landline telephones are often shared among persons living within a residence, household sampling is used in the landline sample to collect information on the number of adults living within a residence and then select randomly from all eligible adults. Cellular telephone respondents are weighted as single adult households. 


The method used for the landline telephone sampling is called Disproportionate stratified sampling (DSS). It draws known telephone household numbers from two strata (a large proportion of target numbers, the high-density block and a set that contains a smaller proportion of target numbers, the medium-density block). The BRFSS samples landline telephone numbers based on sub-state geographic regions. Regional sampling is used to target data collection to geographic subpopulations (such as residents within a public health district).

The cellular telephone sample is randomly generated from a sampling frame of the confirmed cellular area code and prefix combinations. Cellular telephone respondents are randomly selected with each having an equal probability of selection.  From 2013, cellular telephone stratification was conducted by the BRFSS, although geographic specificity is less reliable for cellular telephone numbers than for landline numbers. 

Also, appropriate weighting methods (design weighting and iterative proportional fitting) are used in an attempt to remove bias in the sample.

The BRFSS 2013 data is as a result of the retrospective observational study (as the data recorded are as a result of events that have taken place) and not an experimental study, hence no random assignment and as a result, we cannot make causal conclusions from the data (we can only associate). BRFSS uses random sampling as explained above; hence the data is generalizable. We are simply saying that since there is no random assignment, only random sampling, there is no causal relationship, only association and the data is generalizable.

This data is generalizable to the non-institutionalized adult population, aged 18 years or older, who reside in the US (N.B: In this project, the term "state" is used to refer to all areas participating in BRFSS, including the District of Columbia, Guam, and the Commonwealth of Puerto Rico).



* * *

## Part 2: Research Questions

**Research Question 1:** We want to find out the health status of those who sleep 7-9hrs per day and meet the aerobic exercise recommendation and consume at least one or more fruits and vegetable each per day (Case 1). What percentage of adults who meet the above reported good or better health?

*Interest:* To ensure overall good health, the [National Sleep Foundation](http://www.sleepfoundation.org) recommends at least 7 hours of sleep for adults from age 18 years (a recommended range of 7 to 9 hours of sleep per day) and the [American Heart Association](http://www.heart.org) recommends at least 150minutes per week of moderate exercise or 75 minutes per week of vigorous exercise (or a combination of moderate and vigorous activity), to improve overall cardiovascular health. Also for good health, fruits and vegetables should be the main part of a meal.

**Research Question 2:** We want to know the percentage of the population that was ever diagnosed with a heart attack; what percentage of the diagnosed population is above or below 65 years of age, we want to know their sex and also race. We will also do that for those that (were told they) ever had a stroke.

*Interest:* Heart disease and stroke are the world's two leading causes of death, and for all Americans, heart disease is the No. 1 killer and stroke is also a leading cause of death. 

**Research question 3:** We want to compare the health status of several cases (cases 1 to 5); find out if those who fulfill each case were ever diagnosed with a heart attack. We will also compare the percentage that was ever diagnosed with stroke for each case.

*Interest:* Heart diseases can lead to a heart attack and stroke, which can be prevented or treated with healthy lifestyle choices. I am personally interested in preventive health practices, so knowing the effects of different lifestyle choices can aid us in our quest of living healthy/ensuring a healthy lifestyle.

**Research Questions Breakdown**

We are interested in 5 cases of adults in the sample population:

*1.* Those who sleep 7-9hrs per day and meet the aerobic exercise recommendation per week and consume at least one or more fruits and vegetable each per day.

*2.* Those who sleep 7-9hrs per day and those who do any physical activity or exercise and consume at least one or more fruits and vegetable each per day.

*3.*Those who sleep 7-9hrs per day and those who do not do any physical activity or exercise but consume at least one or more fruits and vegetable each per day.

*4.* Those who sleep 7-9hrs per day and meet the aerobic exercise recommendation per week but consume less than one fruits and vegetable each per day.

*5.* Those who sleep 7-9hrs per day and who do not do any physical activity or exercise and consume less than one fruits and vegetable each per day.

*6.* Those who sleep 7-9hrs per day and meet the aerobic exercise recommendation per week.

*7.* Those who meet the aerobic exercise recommendation per week and consume at least one or more fruits and vegetable each per day. We will look at their health based on their sleep time (group by sleepbreaks), then plot a segmented bar plot. With this, we will answer the question: do those who sleep less than 7-9 hours or more report better health considering that they met the aerobic exercise recommendation and consumed at least one or more fruits and vegetable each per day?

For cases (1) to (5), we will look at the percentage of the population that undergo each, then the percentage of each that have good or better health/fair or poor health.

For only case 1, we will analyze the age group that had the most reported good or better health and the health status of case 1 adult within each month.

We will look at the percentage of the general sample population that had good or better health, visualize their health status based on months to know which month the population reported the most good or better health. We will analyze the following and more:

*1.* Number of healthy days (good physical and mental health) and active days a typical adult has.

*2.* The typical sleep time of an adult in the sample population.

In doing the above,  we will answer the following questions and more:

*1.* What is the probability that an adult in the sample population  (who gave a response) have ever had(been told/diagnosed with) a stroke? We will be considering only those who gave a yes or no response to the question.

*2.* What is the probability that an adult age 65 and above reported good or better health given that the adult fulfilled case 1.

*3.* What is the chance that a Black or African American who met case 1 was ever diagnosed with a heart attack?

*4.* What percentage of the population who met case 1 and reported that (s)he had good or better health was also ever diagnosed with a heart attack?

* * *


## Part 3: Exploratory Data Analysis

In this analysis, we will exclude all missing results, those who did not give a response or did not know (all analysis excludes NAs).
**The results of the analysis are generalized to only non-institutionalized adult population, aged 18 years or older in the States (all areas participating in BRFSS)**- *see part 1 for details.* In this analysis, the term "adult" refers to "non-institutionalized adult population, aged 18 years and above in the States".

*Note the term "we" used throughout this analysis simply refers to "me (/I) explaining the concept to my audience."*

Before we begin our analysis, we will select the variables that are of importance to us and create a new dataframe from brfss2013 called "cbrfss" (this is after we have gone through [the code book](https://www.cdc.gov/brfss/annual_data/2013/pdf/CODEBOOK13_LLCP.pdf) and [calculated variables](https://www.cdc.gov/brfss/annual_data/2013/pdf/2013_Calculated_Variables_Version15.pdf) to know the variables we are interested in and their types/structures, keeping in mind our research questions. 

```{r}
cbrfss<-brfss2013%>%select(X_frtlt1,X_veglt1,X_age65yr,X_age_g,X_ageg5yr,fmonth,genhlth,X_rfhlth,physhlth,menthlth,poorhlth,sleptim1,X_totinda,X_paindx1,cvdinfr4,cvdstrk3,X_mrace1,sex)
```

Also, we create a new variable sleepbreaks from sleptim1 to group the amount of time adults sleep into ten groups and add to the data frame, "cbrfss".
```{r}
sleepbreaks<-cut(cbrfss$sleptim1,breaks = c(0,3,5,7,10,13,16,25,451),labels = c("0-2","3-4","5-6","7-9","10-12","13-15","16-24","25+"),right = FALSE)
cbrfss<-cbrfss%>%mutate(sleepbreaks)
table(cbrfss$sleepbreaks,useNA = "ifany")
```


Or you could combine both codes as below:

cbrfss<-cbrfss%>%mutate(sleepbreaks=cut(sleptim1,breaks = c(0,3,5,7,10,13,16,25,451),labels = c("0-2","3-4","5-6","7-9","10-12","13-15","16-24","25+"),right = FALSE))


Use summary(cbrfss) to view the data summary and str(cbrfss) to view the structure of the data. Knowing the values that make up the variables (the type and structure) will ease our analysis. *In order not to take up pages, we will not include the result of summary(cbrfss) in our report.*

```{r}
str(cbrfss) 
```

### Sample Population' Health Status

Before we delve into our research questions, we want to understand the health status of the population as stated earlier (see Part 2 for details)

To get the distribution and percentage of the sample population' health in terms of those that responded if they had Good or Better OR Fair or Poor Health, we tabulate "X_rfhlth" and plot a bar chart.


```{r}
cbrfss%>%filter(!is.na(X_rfhlth))%>%summarise(perc_hg_b=sum(X_rfhlth=="Good or Better Health")/n(),perc_hf_p=sum(X_rfhlth=="Fair or Poor Health")/n())
```

We filter NAs by using !is.na and plot a bar chart of the sample population health status.

```{r}
cbrfss%>%filter(!is.na(X_rfhlth))%>%ggplot(aes(X_rfhlth))+geom_bar()
```

80.67% of the sample population have "good or better health". It can be attributed to good health care, reduced unemployment rates, good general standard of living as expected in First World Countries.


We can tabulate the percentage of the health Status of the sample population, in decimal, across age groups
```{r}
cbrfss%>%filter(!is.na(X_ageg5yr),!is.na(X_rfhlth))%>%group_by(X_ageg5yr)%>%summarise(perc_hg_b=sum(X_rfhlth=="Good or Better Health")/n(),perc_hf_p=sum(X_rfhlth=="Fair or Poor Health")/n())
```

To visualize the above result, we plot a bar chart.To do this, we first create a subset of the data frame "percent_rfhlth" and mutate to include the percentage of health status within age groups, in decimal; then plot.

```{r}
percent_rfhlth<-cbrfss%>%filter(!is.na(X_ageg5yr),!is.na(X_rfhlth))%>%group_by(X_ageg5yr)%>%count(X_rfhlth)%>%mutate(percentage=n/sum(n))
ggplot(percent_rfhlth,aes(x=X_ageg5yr,y=percentage,fill=X_rfhlth))+geom_bar(stat= "identity",position = position_dodge(width = 0.9),width =1)+geom_text(aes(label=round(percentage,2)),vjust=-0.25)+theme(axis.text.x = element_text(angle = 45,hjust = 1))+ggtitle("Plot of Health Status of the Sample Population within Age Groups")+theme(plot.title = element_text(hjust = 0.3))
```



We can use geom_bar (with stat="identity"), or we  plot the bar chart with geom_col in order to indicate the variable in the y-axis. We can decide to flip the plot using "coord_flip" to get a better view.

```{r}
ggplot(percent_rfhlth,aes(x=X_ageg5yr,y=percentage,fill=X_rfhlth))+coord_flip()+geom_col(position = "dodge")+geom_text(aes(label=round(percentage,2)),vjust=-0.25)+ggtitle("Plot of Health Status of the Sample Population within Age Groups")+theme(plot.title = element_text(hjust = 0.4))
```

From the chart, it can be seen that the ratio of "good or better health" to "fair or poor health" reduces as the age of the adult increases, hence we can say that the older one gets, the more likely his/her health deteriorates (having fair or poor health)- slight negative association. Though there are other confounding variables, e.g., healthy lifestyles like regular check-ups,exercise, sleep duration, fruits, and vegetable consumption, we can say younger adults generally have good or better health, due to age.


We want to check if the report of fair or poor health is predominant in a particular season. We will use the variable fmonth (with the assumption that it represents the actual month of the event). We will find the percentage of each health status, in decimal, across each month.

```{r}
cbrfss%>%filter(!is.na(fmonth),!is.na(X_rfhlth))%>%group_by(fmonth)%>%summarise(perc_hg_b=sum(X_rfhlth=="Good or Better Health")/n(),perc_hf_p=sum(X_rfhlth=="Fair or Poor Health")/n())
```

To visualize the above result, we plot a segmented (dodge) bar chart

```{r}
percent_mrfhlth<-cbrfss%>%filter(!is.na(fmonth),!is.na(X_rfhlth))%>%group_by(fmonth)%>%count(X_rfhlth)%>%mutate(percentage=n/sum(n))
ggplot(percent_mrfhlth,aes(x=fmonth,y=percentage,fill=X_rfhlth))+geom_bar(stat= "identity",position = position_dodge(width = 0.9),width =1)+geom_text(aes(label=round(percentage,2)),vjust=-0.25)+theme(axis.text.x = element_text(angle = 45,hjust = 1))+ggtitle("Plot of Health Status of the Sample Population within Months")+theme(plot.title = element_text(hjust = 0.5))
```

From the bar chart and tabular representation above, we can see that the health status of the sample population across months is approximately equal (~81%); so the population health status is not dependent on the month of the year. 



#### Population Case 1: 

**Number of healthy (good physical and mental health) and active days a typical adult has**

Create new variables: gphyshlth (number of days physical health is good), gmenthlth (number of days mental health is good), activedays(number of activedays, assuming it as the number of days you were able to do your usual activities, due to good physical and mental health) and add to the dataframe

```{r}
cbrfss<-cbrfss%>%mutate(gphyshlth=30-physhlth,gmenthlth=30-menthlth,activedays=30-poorhlth)
```

View the first six values of the added variable
```{r}
cbrfss%>%select(gphyshlth,gmenthlth,activedays)%>%head()
```

Plot histogram to determine the shape of the sample population' healthy (physical and mental) and active days

```{r}
cbrfss%>%filter(!is.na(gphyshlth))%>%ggplot(aes(gphyshlth))+geom_histogram()
cbrfss%>%filter(!is.na(gmenthlth))%>%ggplot(aes(gmenthlth))+geom_histogram(binwidth = 15)
cbrfss%>%filter(!is.na(activedays))%>%ggplot(aes(activedays))+geom_histogram(binwidth = 15)
```

From the above plots, we can see that the number of healthy (good physical and good mental health) and active days are left-skewed.

We can use the function summary() to find the summary statistics of healthy and active days

```{r}
summary(cbrfss$gphyshlth)
summary(cbrfss$gmenthlth)
summary(cbrfss$activedays)
```

The distributions of gphyshlth, gmenthlth, and activedays of the sampled population are left skewed, so a typical good physical health, good mental health, active days for an adult in the sample population is 30 days each (the median value).



#### Population Case 2:

**The typical sleep time of an adult in the sample population**

Get the  distribution of sleptim1 and summary statistics to know the duration a typical adult in the sample population sleeps per day. Use function: summary() Or

cbrfss%>%filter(!is.na(sleptim1))%>%summarise(median(sleptim1),mean(sleptim1),IQR(sleptim1),sd(sleptim1)) Or

cbrfss%>%summarise(median(sleptim1,na.rm = TRUE),mean(sleptim1,na.rm = TRUE),IQR(sleptim1,na.rm = TRUE),sd(sleptim1,na.rm = TRUE))


Plot a histogram to determine the shape of the sleep time of an adult in the sample population. Note that non-finite values are removed by default.

```{r}
ggplot(data=cbrfss,aes(x=sleptim1))+geom_histogram()

```

The distribution of sleep time is right skewed, so for robust statistics, we find the median and IQR (to determine variability) of the data. We can also include the mean and standard deviation in our summary.

```{r}
cbrfss%>%filter(!is.na(sleptim1))%>%summarise(median(sleptim1),mean(sleptim1),IQR(sleptim1),sd(sleptim1))
```

*A typical adult sleeps 7hours a day*. 


We can decide to see the distribution of sleep time within age groups by plotting a bar chart of "X_age_g and sleepbreaks" or we can plot a side by side box plot using the variable "sleptim1".

```{r}
cbrfss%>%filter(!is.na(sleepbreaks),!is.na(X_age_g))%>%ggplot(aes(x=X_age_g,fill=sleepbreaks))+geom_bar()+ggtitle("Chart Showing Sleep Period Distribution within Age Groups")
```

From the chart, we can see that the typical sleep period across age groups is 7-9hours.

```{r}
cbrfss%>%filter(!is.na(sleptim1),!is.na(X_age_g))%>%ggplot(aes(x=X_age_g,y=sleptim1))+geom_boxplot()+ggtitle("Plot of Sleep Time for different Age Groups")+theme(plot.title = element_text(hjust = 0.5))
```

This plot confirms the typical sleep time of 7 hours for adults across all age groups.



### Case 1 

*Research Question 1*

**Those who sleep 7-9hrs per day and meet the aerobic exercise recommendation and consume at least one or more fruits and vegetable each per day (tsleepexfrvg)**


We will create a new variable "tsleepexfrvg" for case 1 and add to new dataframe "scbrfss" (created from and same as "cbrfss"- the essence of this is to easily get hold of your original dataframe in a case of wrong computation). First, we create a subset of data frame "cbrfss" and mutate case 1.

```{r}
sleepexfvg<-cbrfss%>%select(sleepbreaks,X_paindx1,X_frtlt1,X_veglt1)%>%mutate(sleep_ex_fr_vg=ifelse(sleepbreaks=="7-9"&X_paindx1=="Met aerobic recommendations"&X_veglt1=="Consumed vegetables one or more times per day"&X_frtlt1=="Consumed fruit one or more times per day","True","False"))
table(sleepexfvg$sleep_ex_fr_vg,useNA = "ifany")
```

Save the variable "sleep_ex_fr_vg" as "tsleepexfrvg" and add to the dataframe scbrfss
```{r}
tsleepexfrvg<-sleepexfvg$sleep_ex_fr_vg
scbrfss<-cbrfss
scbrfss<-scbrfss%>%mutate(tsleepexfrvg)
```


Count and Percentage of the sample population for Case 1
```{r}
scbrfss%>%filter(!is.na(tsleepexfrvg))%>%summarise(count_pop_1=sum(tsleepexfrvg=="True"),perc_pop_1=sum(tsleepexfrvg=="True")/n())
```

Age Group that does Case 1

```{r}
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(X_ageg5yr))%>%group_by(X_ageg5yr)%>%count()%>%ggplot(aes(X_ageg5yr,n))+geom_bar(stat = "identity")+geom_text(aes(label=n),vjust=-0.25)+theme(axis.text.x = element_text(angle = 45,hjust = 1))+ggtitle("Number of Adults across Age Groups that fulfil Case 1")+theme(plot.title = element_text(hjust = 0.5))
```

Out of 20.57% of the sample population that fulfill Case 1,from the bar chart above, adults of ages 50 and above (highest count- age 60 to 64) are more conscious of their health as they have a higher count compared to those below 50 in ensuring that they sleep 7 to 9hours per day and meet the aerobic exercise recommendations and eat at least one or more fruit and vegetable each per day. It could also be that there are "more" older adults in the population hence the higher count of them fulfilling case 1; we can only confirm this if we consider the number of those who fulfilled case 1 to those who did not within each group.

```{r}
age_case1<-scbrfss%>%filter(!is.na(tsleepexfrvg),!is.na(X_ageg5yr))%>%group_by(X_ageg5yr)%>%count(tsleepexfrvg)%>%mutate(percentage=n/sum(n))
age_case1%>%filter(tsleepexfrvg=="True")
```

From the above result, we can confirm that older adults fulfill case 1 more; with age 75 to 79 years actually having the highest percentage (25.06% of adults age 75 to 79 fulfill case 1 while 74.94% of adults do not) and age 18 to 24, the lowest (15.71% of adults age 18 to 24 fulfill case 1 while 84.29% do not). This can be seen in the light that older adults are retired and they have more time to rest and exercise compared to younger adults.

Percentage of case 1 that have good or better health/fair or poor health

```{r}
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(X_rfhlth))%>%summarise(perc_hg_b=sum(X_rfhlth=="Good or Better Health")/n(),perc_hf_p=sum(X_rfhlth=="Fair or Poor Health")/n())
```


*92.22% of adults who fulfill case 1 have good or better health*, which is a pretty good percentage. We can say that if at least 50% (as against 20.57%) of adults fulfill case 1, the general population will have a better health status than 80.67%. 

In order to know the distribution of health status of adults across age groups, we plot a chart Showing Health Status of Case 1 for different Age Groups.

```{r}
percent_rfhlth_case1<-scbrfss%>%filter(tsleepexfrvg=="True",!is.na(X_ageg5yr),!is.na(X_rfhlth))%>%group_by(X_ageg5yr)%>%count(X_rfhlth)%>%mutate(percentage=n/sum(n))
ggplot(percent_rfhlth_case1,aes(x=X_ageg5yr,y=percentage,fill=X_rfhlth))+geom_bar(stat= "identity",position = position_dodge(width = 0.9),width =1)+coord_flip()+geom_text(aes(label=round(percentage,2)),vjust=-0.25)+ggtitle("Chart Showing Health Status of Case 1 within Age Groups")+theme(plot.title = element_text(hjust = 0.5))
```

The result across age groups is quite similar. This explains the idea that adults who sleep 7-9hours per day, meet the aerobic exercise recommendations and eat at least one or more fruit and vegetable each per day are sure of good or better health irrespective of their age (84-96% of the time). The slight disparity between the age group could be attributed to the idea that aged adults are more prone to weakness/illness compared to younger adults, due to their age; so it is expected that younger adults are healthier than aged adults as seen in the plot of population health status across age groups.

**Question:** What is the probability that an adult age 65 and above reported having good or better health given that the adult fulfills case 1? Ans: 0.88 (88.81%)

```{r}
scbrfss%>%filter(tsleepexfrvg=="True",X_age65yr=="Age 65 or older",!is.na(X_rfhlth))%>%group_by(X_age65yr)%>%count(X_rfhlth)%>%mutate(probability=n/sum(n))
```


We can check if the health status of those that fulfill case 1 varies by month, by plotting a bar chart of case 1' health status across months (we use the file month).

```{r}
percent_mrfhlth_case1<-scbrfss%>%filter(tsleepexfrvg=="True",!is.na(fmonth),!is.na(X_rfhlth))%>%group_by(fmonth)%>%count(X_rfhlth)%>%mutate(percentage=n/sum(n))
ggplot(percent_mrfhlth_case1,aes(x=fmonth,y=percentage,fill=X_rfhlth))+geom_bar(stat= "identity",position = position_dodge(width = 0.9),width =1)+coord_flip()+geom_text(aes(label=round(percentage,2)),vjust=-0.25)+ggtitle("Chart Showing Health Status of Case 1 within Months")+theme(plot.title = element_text(hjust = 0.5))
```

We can see that health status of adults that fulfill case 1 is not dependent on the season of the year, same as that of the sample population because each month, the percentage of good or better health to fair or poor health is almost same. 

We want to find out what **number of healthy (physical, mental) and active days** a typical adult that fulfills case 1 has. We determine the shape of the distribution by plotting a histogram for each.

```{r}
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(gphyshlth))%>%ggplot(aes(gphyshlth))+geom_histogram()
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(gmenthlth))%>%ggplot(aes(gmenthlth))+geom_histogram()
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(activedays))%>%ggplot(aes(activedays))+geom_histogram() + geom_vline(aes(xintercept=mean(activedays)), color="blue", linetype="dashed", size=1)

```

Then we analyze the center of the distribution (For robust statistics for a left skewed distribution, we concentrate on the median and IQR of the data). We will find the mean and standard deviation of healthy days though. (N.B: the result of the first and second analysis for gphyshlth are same but with different codes)

```{r}
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(gphyshlth))%>%summarise(median(gphyshlth),mean(gphyshlth),IQR(gphyshlth),sd(gphyshlth))
scbrfss%>%filter(tsleepexfrvg=="True")%>%summarise(median(gphyshlth,na.rm = TRUE),mean(gphyshlth,na.rm = TRUE),IQR(gphyshlth,na.rm = TRUE),sd(gphyshlth,na.rm = TRUE))
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(gmenthlth))%>%summarise(median(gmenthlth),mean(gmenthlth),IQR(gmenthlth),sd(gmenthlth))
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(activedays))%>%summarise(median(activedays),mean(activedays),IQR(activedays),sd(activedays))
```

The distributions of gphyshlth,gmenthlth and activedays of Case 1 of the sampled population are left skewed, so a typical adult has 30 days each of good physical health, good mental health, active days (same as a typical adult of the sampled population)


### Case 2

**Those who sleep 7-9hrs per day and those who do any physical activity or exercise during the past 30 days other than their regular jobs and consume at least one or more fruits and vegetable each per day (tsleepanyexfrvg).**

We create a new data frame (sleepanyexfvg) and new variable (sleep_anyex_fr_vg) for Case 2
```{r}
sleepanyexfvg<-scbrfss%>%select(sleepbreaks,X_totinda,X_frtlt1,X_veglt1)%>%mutate(sleep_anyex_fr_vg=ifelse(sleepbreaks=="7-9"&X_totinda=="Had physical activity or exercise"&X_frtlt1=="Consumed fruit one or more times per day"&X_veglt1=="Consumed vegetables one or more times per day","True","False"))
table(sleepanyexfvg$sleep_anyex_fr_vg,useNA = "ifany")
```

Add the variable "sleep_anyex_fr_vg" to the dataframe scbrfss and save as "tsleepanyexfrvg"
```{r}
tsleepanyexfrvg<-sleepanyexfvg$sleep_anyex_fr_vg
scbrfss<-scbrfss%>%mutate(tsleepanyexfrvg)
```

Count and Percentage of the sampled population for Case 2
```{r}
scbrfss%>%filter(!is.na(tsleepanyexfrvg))%>%summarise(count_pop_2=sum(tsleepanyexfrvg=="True"),perc_pop_2=sum(tsleepanyexfrvg=="True")/n())
```
The adults that fulfill case 2 are 8.05% more than case 1. 

We want to find out the percentage of case 2 that have good or better health/fair or poor health
```{r}
scbrfss%>%filter(tsleepanyexfrvg=="True",!is.na(X_rfhlth))%>%summarise(perc_hg_b=sum(X_rfhlth=="Good or Better Health")/n(),perc_hf_p=sum(X_rfhlth=="Fair or Poor Health")/n())

```
The adults that fulfill case 1 have 0.99% more good or better health than case 2 adults. So we can infer that if one is able to sleep 7-9hrs per day and consume at least one or more fruits and vegetable each per day, there is no much difference in the outcome of health status if the aerobic exercise recommendation is not met provided he/she does any physical activity or exercise during the past 30 days other than their regular jobs.


### Case 3 

**Those who sleep 7-9hrs per day and those who do not do any physical activity or exercise but consume at least one or more fruits and vegetable each per day (tsleepnoextfrvg).**

We create a new data frame (sleepnoextfvg) and new variable (sleep_noex_tfr_vg) for Case 3

```{r}
sleepnoextfvg<-scbrfss%>%select(sleepbreaks,X_totinda,X_frtlt1,X_veglt1)%>%mutate(sleep_noex_tfr_vg=ifelse(sleepbreaks=="7-9"&X_totinda=="No physical activity or exercise in last 30 days"&X_frtlt1=="Consumed fruit one or more times per day"&X_veglt1=="Consumed vegetables one or more times per day","True","False"))
table(sleepnoextfvg$sleep_noex_tfr_vg,useNA = "ifany")
```

Add the variable "sleep_noex_tfr_vg" to the dataframe scbrfss and save as "tsleepnoextfrvg"
```{r}
tsleepnoextfrvg<-sleepnoextfvg$sleep_noex_tfr_vg
scbrfss<-scbrfss%>%mutate(tsleepnoextfrvg)
```

Count and Percentage of the sampled population for Case 3
```{r}
scbrfss%>%filter(!is.na(tsleepnoextfrvg))%>%summarise(count_pop_3=sum(tsleepnoextfrvg=="True"),perc_pop_3=sum(tsleepnoextfrvg=="True")/n())
```

Only 6.28% of adults in the sample population fulfill case 3.

Let us find out the percentage of case 3 that have good or better health/fair or poor health
```{r}
scbrfss%>%filter(tsleepnoextfrvg=="True",!is.na(X_rfhlth))%>%summarise(perc_hg_b=sum(X_rfhlth=="Good or Better Health")/n(),perc_hf_p=sum(X_rfhlth=="Fair or Poor Health")/n())

```
A very low percentage of adults fulfill case 3; but from the health status result, we can deduce the importance of participating in any exercise (either meet the aerobic exercise recommendation or take part in any physical activity or exercise other than work) as only 75.25% of case 3 adults have good or better health.


### Case 4

**Those who sleep 7-9hrs per day and meet the aerobic exercise recommendation but consume less than one fruits and vegetable each per day (tsleepexlfvg).**

We create a new data frame (sleepexlfvg) and new variable (sleep_ex_lfr_vg) for Case 4

```{r}
sleepexlfvg<-scbrfss%>%select(sleepbreaks,X_paindx1,X_frtlt1,X_veglt1)%>%mutate(sleep_ex_lfr_vg=ifelse(sleepbreaks=="7-9"&X_paindx1=="Met aerobic recommendations"&X_frtlt1=="Consumed fruit less than one time per day"&X_veglt1=="Consumed vegetables less than one time per day","True","False"))
table(sleepexlfvg$sleep_ex_lfr_vg,useNA = "ifany")
```

Add the variable "sleep_ex_lfr_vg" to the dataframe scbrfss and save as "tsleepexlfvg"
```{r}
tsleepexlfvg<-sleepexlfvg$sleep_ex_lfr_vg
scbrfss<-scbrfss%>%mutate(tsleepexlfvg)
```

Count and Percentage of the sample population for Case 4
```{r}
scbrfss%>%filter(!is.na(tsleepexlfvg))%>%summarise(count_pop_4=sum(tsleepexlfvg=="True"),perc_pop_4=sum(tsleepexlfvg=="True")/n())
```

Only 2.24% of adults in the sample population fulfill case 4.

Let us find out the percentage of case 4 that have good or better health/fair or poor health
```{r}
scbrfss%>%filter(tsleepexlfvg=="True",!is.na(X_rfhlth))%>%summarise(perc_hg_b=sum(X_rfhlth=="Good or Better Health")/n(),perc_hf_p=sum(X_rfhlth=="Fair or Poor Health")/n())

```
A very low percentage of adults fulfill case 4, but from the health status result, we can deduce the importance of participating in meeting the aerobic exercise recommendation. The percentage of good or better health is approximately 6% less than case 1 (difference in cases being fruits and vegetable consumption, each, at least one or more times per day) and about 11% more than those who did not do any physical activity or exercise and they consumed fruits and vegetable each at least one or more times per day. This enacts the importance of exercise, irrespective of having a healthy diet when it pertains to the health status of an adult.


### Case 5

**Those who sleep 7-9hrs per day and who do not do any physical activity or exercise and consume less than one fruits and vegetable each per day (tsleepexlfvg).**

We create a new data frame (a subset of scbrfss), "sleepnoexlfvg" and add new variable "sleep_noex_lfr_vg" for Case 5

```{r}
sleepnoexlfvg<-scbrfss%>%select(sleepbreaks,X_totinda,X_frtlt1,X_veglt1)%>%mutate(sleep_noex_lfr_vg=ifelse(sleepbreaks=="7-9"&X_totinda=="No physical activity or exercise in last 30 days"&X_frtlt1=="Consumed fruit less than one time per day"&X_veglt1=="Consumed vegetables less than one time per day","True","False"))
table(sleepnoexlfvg$sleep_noex_lfr_vg,useNA = "ifany")
```

Add the variable "sleep_noex_lfr_vg" to the dataframe scbrfss and save as "tsleepexlfvg"
```{r}
tsleepnoexlfvg<-sleepnoexlfvg$sleep_noex_lfr_vg
scbrfss<-scbrfss%>%mutate(tsleepnoexlfvg)
```

Count and Percentage of the sample population for Case 5
```{r}
scbrfss%>%filter(!is.na(tsleepnoexlfvg))%>%summarise(count_pop_5=sum(tsleepnoexlfvg=="True"),perc_pop_5=sum(tsleepnoexlfvg=="True")/n())
```

Only 2.73% of adults in the sample population fulfill case 5.

We want to find out the percentage of case 5 that have good or better health/fair or poor health
```{r}
scbrfss%>%filter(tsleepnoexlfvg=="True",!is.na(X_rfhlth))%>%summarise(perc_hg_b=sum(X_rfhlth=="Good or Better Health")/n(),perc_hf_p=sum(X_rfhlth=="Fair or Poor Health")/n())
```
A very low percentage of adults fulfill case 5, but from the health status result, we can see that sleeping 7-9hours a day without exercising and also consuming less than one fruit and vegetable each per day equates to fair or poor health 28.64% of the time. Those who consume at least one or more fruit each day without exercising (see case 3) have approximately 4% less chance of having fair and poor health.


### Case 6

**Those who sleep 7-9hrs per day and meet the aerobic exercise recommendation per week (tsleepex).**

We create a new data frame (sleepex), a subset of "scbrfss" and add new variable (sleep_ex) for Case 6

```{r}
sleepex<-scbrfss%>%select(sleepbreaks,X_paindx1)%>%mutate(sleep_ex=ifelse(sleepbreaks=="7-9"&X_paindx1=="Met aerobic recommendations","True","False"))
table(sleepex$sleep_ex,useNA = "ifany")
```

Add the variable "sleep_ex" to the dataframe scbrfss and rename as "tsleepex"
```{r}
tsleepex<-sleepex$sleep_ex
scbrfss<-scbrfss%>%mutate(tsleepex)
```

Count and Percentage of the sample population for Case 6
```{r}
scbrfss%>%filter(!is.na(tsleepex))%>%summarise(count_pop_6=sum(tsleepex=="True"),perc_pop_6=sum(tsleepex=="True")/n())
```

32.31% of adults in the sample population fulfill case 6.  Some of the 144,433 adults who fulfill case 6 fulfill cases 1 and 4.

Let us find out the percentage of case 6 that have good or better health/fair or poor health. 
```{r}
scbrfss%>%filter(tsleepex=="True",!is.na(X_rfhlth))%>%summarise(perc_hg_b=sum(X_rfhlth=="Good or Better Health")/n(),perc_hf_p=sum(X_rfhlth=="Fair or Poor Health")/n())
```
91% of adults who meet the aerobic exercise recommendation and sleep 7-9 hours per day have good or better health.


### Case 7

**Those who meet the aerobic exercise recommendation per week and consume at least one or more fruits and vegetable each per day (texfrvg)**

We create a new data frame (exfvg) and new variable (ex_fr_vg) for Case 7

```{r}
exfvg<-scbrfss%>%select(X_paindx1,X_frtlt1,X_veglt1)%>%mutate(ex_fr_vg=ifelse(X_paindx1=="Met aerobic recommendations"&X_veglt1=="Consumed vegetables one or more times per day"&X_frtlt1=="Consumed fruit one or more times per day","True","False"))
table(exfvg$ex_fr_vg,useNA = "ifany")
```

Add the variable "sleep_ex_fr_vg" to the dataframe scbrfss and rename as "texfrvg"
```{r}
texfrvg<-exfvg$ex_fr_vg
scbrfss<-scbrfss%>%mutate(texfrvg)
```

**Question:** Do those who sleep less than 7-9 hours or more report better health considering that they met the aerobic exercise recommendation and consumed at least one or more fruits and vegetable each per day? 

To answer this, we plot a bar chart to show the health status (X_rfhlth) for different sleep periods (sleepbreaks)

```{r}
percent_srfhlth_case7<-scbrfss%>%filter(texfrvg=="True",!is.na(sleepbreaks),!is.na(X_rfhlth))%>%group_by(sleepbreaks)%>%count(X_rfhlth)%>%mutate(percentage=n/sum(n))
ggplot(percent_srfhlth_case7,aes(x=sleepbreaks,y=percentage,fill=X_rfhlth))+geom_bar(stat= "identity",position = "dodge")+geom_text(aes(label=round(percentage,2),vjust=-0.5))+ggtitle("Chart Showing Health Status of Case 7 for different Sleep Period")+theme(plot.title = element_text(hjust = 0.5))
```

From the chart, we can see that those who sleep 7-9hours per day seems to have good or better health (92%) given case 7 is met compared to those who sleep less or more. However, those who sleep 5-6hours per day seconds that (86% of adults reported good or better health).


### Heart Attack and Stroke

#### Sample Population Heart Attack and Stroke Diagnosis 

*Research Question 2*

**Question:** What is the probability that an adult in the sample population  (who gave a response) have ever (been told they) had a heart attack? Remember we are only considering those who gave a yes or no response to the question.

```{r}
scbrfss%>%filter(!is.na(cvdinfr4))%>%count(cvdinfr4)%>%mutate(n/sum(n))
```
*5.99% of a total of 489,188 adults have ever (been told they) had a heart attack.* 

We can also go further to see the age group of those (5.99%) that were diagnosed with a heart attack.

```{r}
age_hattack<-scbrfss%>%filter(!is.na(X_ageg5yr),cvdinfr4=="Yes")%>%group_by(X_ageg5yr)%>%count(cvdinfr4)%>%ungroup %>%mutate(percentage=n/sum(n))
age_hattack
ggplot(age_hattack,aes(x=X_ageg5yr,y=percentage))+geom_bar(stat="identity")+ggtitle(label="Proportion of Heart Attack Diagnosis across Age Groups")+theme(plot.title = element_text(hjust = 0.5))+theme(axis.text.x = element_text(angle = 45,hjust = 1))
```

From the result above, we can see that the proportion of adults who had ever been *diagnosed with a heart attack is highest for age group 80 or older*; meaning 21% of the adults who ever (been told) had a heart attack are age 80 or older. We can infer that the chance of a heart attack increases as an adult’s age increases, though other factors like a general way of living (e.g. exercise, food consumption, amount of time one rests), genetics play a role.

We will look at some demographics (are they more of males or females, what race and are they older than 65 or younger) for those who had a heart attack.


```{r}
age65yr_hattack<-scbrfss%>%filter(!is.na(X_age65yr),cvdinfr4=="Yes")%>%group_by(X_age65yr)%>%count(cvdinfr4)%>%ungroup %>%mutate(percentage=n/sum(n))
ggplot(age65yr_hattack,aes(x=X_age65yr,y=percentage))+geom_bar(stat="identity")+geom_text(aes(label=round(percentage,2),vjust=-0.5))+ggtitle(label="Plot of Diagnosed Heart Attack for Ages below and above 65")+theme(plot.title = element_text(hjust=0.5))
```

*65% of the diagnosed adults that had a heart attack were 65 years and above*. We can generalize that older adults of age 65 and above have a higher chance of a heart attack compared to those below 65 years.

Sex of adults ever diagnosed with a heart attack in the sample population.

```{r}
sex_hattack<-scbrfss%>%filter(!is.na(sex),cvdinfr4=="Yes")%>%group_by(sex)%>%count(cvdinfr4)%>%ungroup %>%mutate(percentage=n/sum(n))
ggplot(sex_hattack,aes(x=sex,y=percentage))+geom_bar(stat="identity")+geom_text(aes(label=round(percentage,2),vjust=-0.5))+ggtitle(label="Proportion of Adults ever Diagnosed with a Heart Attack")+theme(plot.title = element_text(hjust=0.5))
```

Out of the 29,284 adults that were diagnosed with a heart attack, *55% was male and 45% female.* A question that may arise from this result which will require further observation, experiment and/or analysis are: are male adults more prone to a heart attack compared to females?

We also want to see if heart attack diagnosis is dependent on races.  

```{r}
race_hattack<-scbrfss%>%filter(!is.na(X_mrace1),cvdinfr4=="Yes")%>%group_by(X_mrace1)%>%count(cvdinfr4)%>%ungroup %>%mutate(percentage=n/sum(n))
ggplot(race_hattack,aes(x=X_mrace1,y=percentage))+geom_bar(stat="identity")+geom_text(aes(label=round(percentage,2),vjust=-0.3))+ggtitle(label="Distribution of the Sample Population' Heart Attack Diagnosis across Races")+theme(plot.title = element_text(hjust=0.5))+scale_x_discrete(label= function(x)lapply(strwrap(x,width = 15,simplify = FALSE),paste,collapse="\n"))#the last code (scale_x_discrete......) is for wrapping the text of the races
```

*84% of adults ever diagnosed with a heart attack are white. Black or African American ever diagnosed are 8%.* So we could generalize that whites are more susceptible to a heart attack but we might want to find out if the percentage of whites are extremely more than other races because that could be a reason for the above results (if the population is predominantly white, then definitely more whites will be subjected to a heart attack). 

```{r}
scbrfss%>%filter(!is.na(X_mrace1))%>%count(X_mrace1)%>%mutate(percentage=n/sum(n))
scbrfss%>%filter(is.na(X_mrace1))%>%count(X_mrace1)
```

82% of the sample population that gave a valid response is whites (N.B- only 8375 NAs), that is a pretty high percentage compared to other races. We can generalize that whites make up way more than half of the population, and thus, they are more likely to have a heart attack.

We can also visualize the likelihood of each race having a heart attack by plotting the percentage of those (each race) ever diagnosed with a heart attack.

```{r}
race_Hattack<-scbrfss%>%filter(!is.na(cvdinfr4),!is.na(X_mrace1))%>%group_by(X_mrace1)%>%count(cvdinfr4)%>%mutate(percentage=n/sum(n))
race_Hattack%>%filter(cvdinfr4=="No")
race_Hattack%>%filter(cvdinfr4=="Yes")
```

Visualizing the likelihood of each race having a heart attack, we have
```{r}
race_Hattack_plot<-race_Hattack%>%filter(cvdinfr4=="Yes")
ggplot(race_Hattack_plot,aes(x=X_mrace1,y=percentage))+geom_bar(stat="identity")+scale_x_discrete(label= function(x)lapply(strwrap(x,width = 15,simplify = FALSE),paste,collapse="\n"))
```

*American Indian or Alaskan Native diagnosed with a heart attack with respect to all American Indian or Alaskan Native  are highest* (7.99% i.e 719 out of 8997 American Indian or Alaskan) and Asians have the least (2.46% i.e 241 out of 9774 Asians) diagnosis within their race. We can generalise that 1 in every about 40 Asians are likely to be diagnosed with a heart attack in the States and about 1 in every 12 American Indian or Alaskan Native are likely to be diagnosed with a heart attack in the States. 

**Question:** What is the probability that an American Indian or Alaskan Native who was diagnosed with a heart attack is below the age of 65? 
```{r}
scbrfss%>%filter(X_mrace1=="American Indian or Alaskan Native",!is.na(X_age65yr),cvdinfr4=="Yes")%>%group_by(X_age65yr)%>%count(cvdinfr4)%>%ungroup()%>%mutate(percentage=n/sum(n))
```
In every 1 in 12 American Indian or Alaskan Native diagnosed with a heart attack, the likelihood of him/her being younger than 65 years is approximately 0.50.

**Question:**What is the probability that an Asian who was diagnosed with a heart attack is below the age of 65? 

```{r}
scbrfss%>%filter(X_mrace1=="Asian",!is.na(X_age65yr),cvdinfr4=="Yes")%>%group_by(X_age65yr)%>%count(cvdinfr4)%>%ungroup()%>%mutate(percentage=n/sum(n))
```
In every 1 in 40 Asians diagnosed with a heart attack, the likelihood of him/her being younger than 65 years is 0.55.


**Question:** What is the probability that an adult in the sample population  (who gave a response) have ever (been told they had/diagnosed with) a stroke? Remember we are only considering those who gave a yes or no response to the question.
We can decide to use the function summary() to know only the count.

```{r}
scbrfss%>%filter(!is.na(cvdstrk3))%>%count(cvdstrk3)%>%mutate(percentage=n/sum(n))
```


*4.16% of a total of 490,308 adults have ever (been told they) had a stroke.* 

We will look at some demographics (are they more of males or females, what race and are they older than 65 or younger) of those who had a heart attack.


```{r}
age65yr_stroke<-scbrfss%>%filter(!is.na(X_age65yr),cvdstrk3=="Yes")%>%group_by(X_age65yr)%>%count(cvdstrk3)%>%ungroup %>%mutate(percentage=n/sum(n))
ggplot(age65yr_stroke,aes(x=X_age65yr,y=percentage))+geom_bar(stat="identity")+geom_text(aes(label=round(percentage,2),vjust=-0.5))+ggtitle(label="Plot of Diagnosed Stroke for Ages below and above 65")+theme(plot.title = element_text(hjust=0.5))
```
 
*62% of the diagnosed adults that had stroke were 65 years and above (3% less than those diagnosed with a heart attack).* Adults of age 65 and above have a higher chance of a heart attack and also stroke . Further analysis in the future can be centered on if those who were diagnosed with a heart attack also had a stroke or vice versa.

Sex of adults in the sample population ever diagnosed with stroke
```{r}
sex_stroke<-scbrfss%>%filter(!is.na(sex),cvdstrk3=="Yes")%>%group_by(sex)%>%count(cvdstrk3)%>%ungroup %>%mutate(percentage=n/sum(n))
sex_stroke
ggplot(sex_stroke,aes(x=sex,y=percentage))+geom_bar(stat="identity")+geom_text(aes(label=round(percentage,2),vjust=-0.5))+ggtitle(label="Sex of Adults ever Diagnosed with a Stroke")+theme(plot.title = element_text(hjust=0.5))
```

Out of the 20,390 adults ever diagnosed with a stroke, 39% was male and 61% female, unlike heart attack that had 55% male diagnosis (Female had stroke more, compared to male). We can infer that females are more likely to have a stroke than a heart attack compared to male. A question which comes to mind is: why are female adults more prone to stroke diagnosis compared to male (this will require further observational/experimental study and analysis)

We also want to see if stroke attack diagnosis is dependent on races. 

First, we look at the diagnosed stroke cases across races.
```{r}
race_stroke<-scbrfss%>%filter(!is.na(X_mrace1),cvdstrk3=="Yes")%>%group_by(X_mrace1)%>%count(cvdstrk3)%>%ungroup %>%mutate(percentage=n/sum(n))
ggplot(race_stroke,aes(x=X_mrace1,y=percentage))+geom_bar(stat="identity")+geom_text(aes(label=round(percentage,2),vjust=-0.3))+ggtitle(label="Distribution of the Sample Population' Stroke Diagnosis across Races")+theme(plot.title = element_text(hjust=0.5))+scale_x_discrete(label= function(x)lapply(strwrap(x,width = 15,simplify = FALSE),paste,collapse="\n"))#the last code (scale_x_discrete......) is for wrapping the text of the races
```

Since the population is predominantly white, adults diagnosed with stroke are more of white. Though, comparing the results of heart attack and stroke, we can say that Whites are 5% more prone to a heart attack diagnosis than stroke diagnosis while Black or African Americans are 4% more prone to a stroke diagnosis compared to heart attack diagnosis.

We will visualize the likelihood of each race having a stroke by plotting the percentage of those (each race) ever diagnosed with a stroke.

```{r}
Race_Stroke<-scbrfss%>%filter(!is.na(cvdstrk3),!is.na(X_mrace1))%>%group_by(X_mrace1)%>%count(cvdstrk3)%>%mutate(percentage=n/sum(n))
Race_Stroke%>%filter(cvdstrk3=="No")
Race_Stroke%>%filter(cvdstrk3=="Yes")
```

Visualizing the likelihood of the above result for only those ever diagnosed with a stroke, we have
```{r}
Race_Stroke_plot<-Race_Stroke%>%filter(cvdstrk3=="Yes")
ggplot(Race_Stroke_plot,aes(x=X_mrace1,y=percentage))+geom_bar(stat="identity")+scale_x_discrete(label= function(x)lapply(strwrap(x,width = 15,simplify = FALSE),paste,collapse="\n"))
```

*American Indian or Alaskan Native and Black or African American (both) diagnosed with a stroke with respect to each of their race are equally highest* (about 6% each- 540 out of 9060 American Indian or Alaskan Native and 2455 out of 41,113 Black or African American) and *Asians have the least* (1.75% i.e 172 out of 9803 Asians) diagnosis within their race. We can generalize that 1 in about every 57 Asians is likely to be diagnosed with a stroke in the States, 1 in about every 17 American Indian or Alaskan is likely to be diagnosed with stroke and about 1 in about every 17 Black or African American is likely to be diagnosed with stroke in the States. 

#### Cases: 

*Research Question 3. N.B: Cases 1 to 5 for Health Status have been introduced earlier- see the "Research Question 1" section.*

*We will look at the count and percentage of adults that (was ever told they) had a heart attack, also stroke for each case to see if there is any considerable difference between cases.*

##### Case 1

**Those who sleep 7-9hrs per day and meet the aerobic exercise recommendation per week and consume at least one or more fruits and vegetable each per day (tsleepexfrvg)**

Before we delve into the analysis of case 1' heart attack and stroke diagnosis, let us get a further understanding of case 1 adults. We will look at their demographics: age again (this time below and above 65), sex and visualize only the race of adults who met case 1.

Age of those who fulfilled case 1
```{r}
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(X_age65yr))%>%group_by(X_age65yr)%>%count(tsleepexfrvg)%>%ungroup()%>%mutate(percentage=n/sum(n))
```
62.28% of adults who fulfil case 1 are age 65 and above.

Sex of those who fulfilled case 1
```{r}
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(sex))%>%group_by(sex)%>%count(tsleepexfrvg)%>%ungroup()%>%mutate(percentage=n/sum(n))
```

More females make up adults who fulfill case 1 (62% female).

Race of those who fulfilled case 1
```{r}
race_case1<-scbrfss%>%filter(tsleepexfrvg=="True",!is.na(X_mrace1))%>%group_by(X_mrace1)%>%count(tsleepexfrvg)%>%ungroup()%>%mutate(percentage=n/sum(n))
race_case1
ggplot(race_case1,aes(x=X_mrace1,y=percentage))+geom_bar(stat="identity")+scale_x_discrete(label= function(x)lapply(strwrap(x,width = 15,simplify = FALSE),paste,collapse="\n"))
```

89.31% of adults who fulfill case 1 are white as expected since the population of adults in the States is predominantly white.

*Since we now have a good understanding of our case 1 adults, we will go ahead with case 1' heart attack and stroke diagnosis analysis.*

We want to know the proportion of adults that fulfilled case 1 and was diagnosed with a heart attack.
```{r}
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(cvdinfr4))%>%count(cvdinfr4)%>%mutate(percentage=n/sum(n))
```

Also, let us get the proportion of Case 1 adults that had a stroke
```{r}
scbrfss%>%filter(tsleepexfrvg=="True",!is.na(cvdstrk3))%>%count(cvdstrk3)%>%mutate(percentage=n/sum(n))
```

The percentage of adults who fulfilled case 1, that had a heart attack is about 4.32% and more than those diagnosed with a stroke (2.63%).

**Question:** What percentage of the population who met case 1 and reported that (s)he had good or better health was also diagnosed with a heart attack?

```{r}
scbrfss%>%filter(tsleepexfrvg=="True",X_rfhlth=="Good or Better Health", !is.na(cvdinfr4))%>%summarise(prop_hattack=sum(cvdinfr4=="Yes")/n())
```

3.33% of adults who met case 1 and reported that (s)he had good or better health was also diagnosed with a heart attack.

**Question:** What is the chance that a Black or African American who met case 1 was ever diagnosed with a heart attack? Ans: 0.035

```{r}
scbrfss%>%filter(tsleepexfrvg=="True",X_mrace1=="Black or African American",!is.na(cvdinfr4))%>%count(cvdinfr4)%>%mutate(percentage=n/sum(n))
scbrfss%>%filter(tsleepexfrvg=="True",X_mrace1=="Black or African American",is.na(cvdinfr4))%>%count(cvdinfr4)
```
Note that the sum total of Black or African Americans who fulfil case 1 is 4006 but we excluded the NAs (15) of "cvdinfr4" in our analysis.
3.53% of Black or African Americans who met case 1 were once diagnosed with a heart attack


#### Case 2

**Those who sleep 7-9hrs per day and those who do any physical activity or exercise during the past 30 days other than their regular jobs and consume at least one or more fruits and vegetable each per day (tsleepanyexfrvg)**

We want to know the proportion of adults that fulfilled case 2 and were diagnosed with a heart attack.

```{r}
scbrfss%>%filter(tsleepanyexfrvg=="True",!is.na(cvdinfr4))%>%count(cvdinfr4)%>%mutate(percentage=n/sum(n))
```


Also, let us get the proportion of Case 2 adults that had a stroke
```{r}
scbrfss%>%filter(tsleepanyexfrvg=="True",!is.na(cvdstrk3))%>%count(cvdstrk3)%>%mutate(percentage=n/sum(n))
```

The percentage of adults who fulfilled case 2, that had a heart attack is about 4.23% and more than those diagnosed with a stroke (2.67%).


#### Case 3

**Those who sleep 7-9hrs per day and those who do not do any physical activity or exercise but consume at least one or more fruits and vegetable each per day (tsleepnoextfrvg)**

We want to know the proportion of adults that fulfilled case 3 and were ever diagnosed with a heart attack.

```{r}
scbrfss%>%filter(tsleepnoextfrvg=="True",!is.na(cvdinfr4))%>%count(cvdinfr4)%>%mutate(percentage=n/sum(n))
```

Also, let us get the proportion of Case 3 adults that ever had a stroke
```{r}
scbrfss%>%filter(tsleepnoextfrvg=="True",!is.na(cvdstrk3))%>%count(cvdstrk3)%>%mutate(percentage=n/sum(n))
```
The percentage of adults who fulfilled case 3, that ever had a heart attack is about 7.76% and more than those diagnosed with a stroke (5.49%). We can see the effect of doing exercise from the above result; though the adults slept 7-9 hours per day and consumed fruits and vegetable at least one or more times per day each, those who were diagnosed with a heart attack and also stroke are at least 1.8 times more than those diagnosed in cases 2 and 3.


#### Case 4

**Those who sleep 7-9hrs per day and meet the aerobic exercise recommendation but consume less than one fruit and vegetable each per day (tsleepexlfvg)**

We want to know the proportion of adults that fulfilled case 4 and were ever diagnosed with a heart attack.
```{r}
scbrfss%>%filter(tsleepexlfvg=="True",!is.na(cvdinfr4))%>%count(cvdinfr4)%>%mutate(percentage=n/sum(n))
```

Also, let us get the proportion of Case 4 adults that ever had a stroke
```{r}
scbrfss%>%filter(tsleepexlfvg=="True",!is.na(cvdstrk3))%>%count(cvdstrk3)%>%mutate(percentage=n/sum(n))
```
The percentage of adults who fulfilled case 4, that had a heart attack is about 5.36% and more than those diagnosed with a stroke (3.34%). 


#### Case 5

**Those who sleep 7-9hrs per day and who do not do any physical activity or exercise and consume less than one fruits and vegetable each per day (tsleepnoexlfvg).**

We want to know the proportion of adults that fulfilled case 5 and were ever diagnosed with a heart attack.
```{r}
scbrfss%>%filter(tsleepnoexlfvg=="True",!is.na(cvdinfr4))%>%count(cvdinfr4)%>%mutate(percentage=n/sum(n))
```

Also, let us get the proportion of Case 5 adults that ever had a stroke
```{r}
scbrfss%>%filter(tsleepnoexlfvg=="True",!is.na(cvdstrk3))%>%count(cvdstrk3)%>%mutate(percentage=n/sum(n))
```
The percentage of adults who fulfilled case 5, that ever had a heart attack is about 7.22% and more than those diagnosed with stroke (5.32%). 


### Summary of Cases 1 to 5: Heart Attack and Stroke

We will tabulate the results of cases 1 to 5 then visualize to know the case that has more diagnosed heart attack and also stroke. Due to the scope of my learning thus far, we will input the results above manually then create a table and then plot.

We will do that by creating a dataframe "Summary_Cases_HAttack_Stroke" that has 3 variables: *Cases*-Cases 1 to 5, *Percentage_HAttack*- percentage of adults in each case ever diagnosed with a heart attack and also the *Percentage_Stroke*- percentage of adults in each case ever diagnosed with a stroke.

```{r}
Cases<-c("Case 1","Case 2","Case 3","Case 4","Case 5")
Percentage_HAttack<-c(4.33,4.23,7.76,5.36,7.23)
Percentage_Stroke<-c(2.63,2.67,5.49,3.34,5.32)
Summary_Cases_HAttack_Stroke<-data.frame(Cases,Percentage_HAttack,Percentage_Stroke)
Summary_Cases_HAttack_Stroke
```

We will visualize the above results by plotting a bar chart for the cases
```{r}
plotH<-ggplot(Summary_Cases_HAttack_Stroke,aes(x=Cases,y=Percentage_HAttack))+geom_bar(stat = "identity")+ggtitle("% of Adults that had a Heart Attack")
plotS<-ggplot(Summary_Cases_HAttack_Stroke,aes(x=Cases,y=Percentage_Stroke))+geom_bar(stat = "identity")+ggtitle("Percentage of Adults that had Stroke")
ggarrange(plotH,plotS,ncol = 2,nrow = 1)
```

We can see that Cases 1 and 2 have a lower percentage of adults ever diagnosed with a heart attack and stroke.  Case 4 has a slightly higher percentage of adults diagnosed with a heart attack and also stroke (the difference with respect to cases 1 and 2 is the amount of fruits and vegetable consumed). Case 3 and Case 5 have more percentage of adults diagnosed with a heart attack and also a stroke.

**Conclusion:** Meeting the recommended aerobic exercise or doing any physical activity or exercise and consuming at least one or more fruits and vegetable each per day can be associated with reduced chances of a heart attack and also stroke, though other factors like genetics, race, age, sex, play a vital role.


### Summary of Cases 1 to 5: Health Status

We will tabulate the results of cases 1 to 5 then visualize to know the case that has good or better health compared to the others.

We will do that by creating a dataframe "Summary_Cases_Results" that has 5 variables: *Cases*-Cases 1 to 5, *Count*- number of adults in the sample population that fulfills each case, *Percentage_of Population*- percentage of adults in the sample population that fulfills each case, lastly percentage of adults in the sample population that have *good or better health* and *fair or poor health* for each case

```{r}
Cases<-c("Case 1","Case 2","Case 3","Case 4","Case 5")
Count<-c(94477,134971,29598,10547,12929)
Percentage_of_Population<-c(20.57,28.66,6.27,2.22,2.74)
Good_or_Better_Health<-c(92.22,91.23,75.25,86.44,71.36)
Fair_or_Poor_Health<-c(7.78,8.77,24.75,13.56,28.64)
Summary_Cases_Results<-data.frame(Cases,Count,Percentage_of_Population,Good_or_Better_Health,Fair_or_Poor_Health)
datatable(Summary_Cases_Results)
```

We will visualise the above results by plotting a bar chart for the cases
```{r}
plot1<-ggplot(Summary_Cases_Results,aes(x=Cases,y=Count))+geom_bar(stat = "identity")+ggtitle("Number of Adults for each Case")
plot2<-ggplot(Summary_Cases_Results,aes(x=Cases,y=Percentage_of_Population))+geom_bar(stat = "identity")+ggtitle("Percentage of Adults for each Case")
plot3<-ggplot(Summary_Cases_Results,aes(x=Cases,y=Good_or_Better_Health))+geom_bar(stat = "identity")+ggtitle("% of Adults with Good or Better Health")
plot4<-ggplot(Summary_Cases_Results,aes(x=Cases,y=Fair_or_Poor_Health))+geom_bar(stat = "identity")+ggtitle("% of Adults with Fair or Poor Health")
ggarrange(plot1,plot2,plot3,plot4,ncol = 2,nrow = 2)
```

Adults who met cases 1 and 2 (highest is case 2) are more than those who met cases 3, 4 and 5 each. A good number of the population (49.23%) have a healthy standard of living: sleep 7-9hours per day, meet the recommended aerobic exercise/do any physical activity or exercise and consume at least one or more fruits and vegetable each per day. We can see that more than 90% each of those who met case 1 and also case 2 have good or better health. For those (case 4) who consumed less fruit and vegetable compared to cases 1 and 2 but sleep and exercise like cases 1 and 2, 86.44% of them reported good or better health. Though exercising regularly and sleeping 7-9 hours per day is good, it is also important to consume at least one or more fruits and vegetable each day.

**Conclusion:** We can generalize that those who sleep 7-9hours per day, meet the recommended aerobic exercise/do any physical activity or exercise and consume at least one or more fruits and vegetable each per day have "good or better health", lower chances of a heart attack and also stroke than those who do not.

*N.B: The terms "proportion and percentage, in decimal", used in this analysis mean the same thing. Proportion sum equates to 1, and the percentage (%) sum equates to 100*. The results for the code used in calculating percentage are expressed in decimal.

* * *

### References

For this analysis, I used contents from the following websites as a guide: 

*1.*  https://www.cdc.gov

*2.*  https://www.heart.org

*3.*  https://health.gov

*4.*  https://www.sleepfoundation.org

*5.*  https://www.mayoclinic.org

*6.*  https://www.health.harvard.edu

*7.*  https://suzan.rbind.io

*8.*  https://www.sthda.com

*9.*  https://bradleyboehmke.github.io

*10.* https://stackoverflow.com

*11.* https://www.dummies.com

*12.* https://datacarpentry.org

*13.* https://stats.idre.ucla.edu/r

*14.* https://www.storybench.org

*15.* https://rstudio-pubs-static.s3.amazonaws.com/6975_c4943349b6174f448104a5513fed59a9.html

*16*  https://rstudio-pubs-static.s3.amazonaws.com/3364_d1a578f521174152b46b19d0c83cbe7e.html


I also used the book ["OpenIntro Statistics,"](https://www.openintro.org/) Third Edition, by David M Diez, Christopher D Barr, and Mine Cetinkaya-Rundel and definitely knowledge gained from the course "Introduction to Probability and Data," by Duke University on Coursera.

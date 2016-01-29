# Can survey data be used as an indicator of learning outcomes?
Karl Molden, Veronika Hulikova  
25 January 2016  



## Synopsis

The aims of this project are to show that the results of work done by [Sheffield Hallam University](https://www.heacademy.ac.uk/sites/default/files/resources/2.3%20Using%20UKES%20results%20and%20institutional%20award%20marks%20to%20explore%20the%20relationship%20between%20student%20engagement%20and%20academic%20achievement.pdf)  which identify a small but statistically significant relationship between responses to the HEA's UK Engagement Survey (UKES) and academic outcomes can be:

* Recreated with similar data from the University of Greenwich
* Extended from an annual survey to course level surveys conducted each term, and so potentially be useful as part of a learning analytics dataset

As such a dataset containing responses to the University Student Survey (USS), which from the 2014 session contains the UKES questions as a subset of the whole survey, was matched to a student dataset containing the Grade Point Average (GPA) and a second dataset containing responses to course evaluation surveys was matched to a dataset containing course grades.

Regression analysis was performed on the matched data to identify if correlations exist between responses to questions and GPA/course grades.

The headline results of this analysis are that:

* There are small but statistically significant correlations between UKES responses and academic outcomes
* We can find similar relationships between course evaluation data and academic outcome

A note about the UKES survey: *This material and its contents [UKES] is developed by The Higher Education Academy ("HEA"). Some of the questions in this survey are used with permission from The College Student Report, National Survey of Student Engagement, Copyright 2001-2016 The Trustees of Indiana University. With the exception of the aforementioned, the copyright in such material and content belongs to the HEA. No reproduction, modification, or adaptation is permitted without the prior written consent of the HEA © The Higher Education Academy 2012, Amended 2015, All Rights Reserved.*


## Data Processing

Whilst this is tailored to the Greenwich data sets, it should be straightforward to adapt to other, similar data.  For both the annual USS survey and the course evaluation data the processing is essentially the same:

* Match survey data with academic outcome data
* Filter data to the set needed to work with
* Perform any re-coding necessary to make the data ready for statistical analysis

Currently all of the data processing has been performed using 'R' and the code used for the whole analysis can be found here:

https://github.com/Karlos78/jisc_micro_project





The matched survey data is filtered so that it only includes the students which we are interested in, which in the case of the UKES are On-campus, undergraduate first years and the data is restricted to only the UKES questions. The question responses are re-coded as shown in the table below:

Response             | Re-coded Value
---------------------|-------------
Very much/Very often | 5
Quite a bit/Often    | 4
Sometimes/Some       | 2
Very little/Never    | 1






## Results
### UKES Analysis

Analysis of variance shows that seven of the UKES questions have a statistically significant (p < 0.05) correlation with GPA. Of these, four are the same as those found in the analysis performed by Sheffield Hallam.

- Q4a: During the current academic year, to what extent has your course challenged you to do your best work?
- Q5a: During the current academic year, about how often have you come to taught sessions prepared (completed assignments, readings, reports, etc.)?
- Q6a: Worked with other students on course projects or assignments.
- Q6b: Explained course material to one or more student.



```
## Analysis of Variance Table
## 
## Response: Stage.GPA
##             Df Sum Sq Mean Sq F value    Pr(>F)    
## Q2a.num      1   2254  2253.7  5.8921 0.0153583 *  
## Q2b.num      1     38    37.6  0.0983 0.7539910    
## Q2c.num      1    209   208.5  0.5451 0.4604632    
## Q2d.num      1    944   943.5  2.4668 0.1165463    
## Q2e.num      1    402   402.1  1.0513 0.3054117    
## Q3a.num      1      0     0.3  0.0008 0.9771699    
## Q4a.num      1   1712  1711.7  4.4751 0.0346023 *  
## Q5a.num      1   5138  5138.5 13.4342 0.0002581 ***
## Q6a.num      1   3737  3737.1  9.7703 0.0018170 ** 
## Q6b.num      1   2312  2311.9  6.0443 0.0140947 *  
## Q6c.num      1      1     1.2  0.0031 0.9553596    
## Q6d.num      1    286   286.5  0.7490 0.3869765    
## Q7a.num      1     85    84.8  0.2218 0.6377635    
## Q7b.num      1   4866  4865.9 12.7215 0.0003760 ***
## Q7c.num      1   4541  4541.1 11.8724 0.0005898 ***
## Q7d.num      1    439   439.1  1.1480 0.2841839    
## Q7e.num      1    166   165.8  0.4336 0.5103682    
## Residuals 1176 449811   382.5                      
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```





The table below shows the strength of the correlations found.

Question  | Correlation coefficient
----------|------------------------
Q4a       | 0.059
Q5a       | 0.091
Q6a       | 0.081
Q6b       | 0.117

Box-plots of GPA against response for these questions show that the main change in the distribution of GPA is between respondents who answer '1:Never/Very little' and those who give one of the other responses, '2:Sometimes/4:Often/5:Very often'.  The box-plots below show quite clearly how the lower end of the distributions become more tightly distributed around the median as the response changes from engaging less with a particular behaviour to engaging more.

<img src="micro_project_blog_files/figure-html/results_UKES_plots-1.png" title="" alt="" width="\maxwidth" />

The histograms below look more closely at the GPAs of respondents who answered 'Never' to question 6b compared to the other three responses. As can be seen, the GPA distribution for those who answered 'Never' has a lower mean as well as having a larger spread across the lower GPA values.

<img src="micro_project_blog_files/figure-html/results_dist-1.png" title="" alt="" width="\maxwidth" />

### Course Evaluations Analysis

Course evaluation surveys at Greenwich contain a standard set of 14 questions posed to every on-campus student on every course.


```
## Analysis of Variance Table
## 
## Response: m_grade
##             Df Sum Sq Mean Sq F value  Pr(>F)  
## Q1         360  33477   92.99  0.7034 0.99997  
## Q2           1      5    5.32  0.0402 0.84110  
## Q3           1     89   89.01  0.6733 0.41206  
## Q4           1    863  863.06  6.5288 0.01074 *
## Q5           1    464  464.10  3.5107 0.06122 .
## Q6           1    264  263.88  1.9962 0.15796  
## Q7           1    383  383.14  2.8983 0.08894 .
## Q8           1    603  603.13  4.5625 0.03289 *
## Q9           1     53   52.86  0.3998 0.52729  
## Q10          1    232  231.86  1.7540 0.18564  
## Q11          1      4    3.52  0.0267 0.87032  
## Q12          1    165  165.26  1.2502 0.26375  
## Q13          1     86   86.15  0.6517 0.41968  
## Q14          1    173  172.99  1.3086 0.25288  
## Residuals 1168 154403  132.19                  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```



Analysis of variance shows that two of these fourteen questions have a statistically significant (p < 0.5) correlation with academic outcome as measured by the grade achieved on that course, those questions being:

- Q4: I have received good support to manage my assessment workload.
- Q8: The learning environment for this course has been good.


## Conclusion & Recommendations

This project has shown that responses to some questions within student surveys are correlated with academic outcome. We have identified a relationship between questions in the UKES and GPA, as well as going on to show a similar relationship between course evaluation survey questions and course grades.

It should be possible to take this work further by identifying the academic behaviours which may be driving the survey responses, modifying the course structure so that this behaviour may be increased/decreased as required and then observing if this has an effect upon both survey response and academic outcome.

For instance, two of the UKES questions identified as having a statistically significant correlation with GPA are specifically about engagement with a student's peer group. A simple experiment might be to identify a programme or course which scores poorly on these questions and increase the amount of group work to see if this can be improved, and consequently, academic outcomes as measured by GPA.

Additionally, whilst further work needs to be done, the course evaluation survey results suggest that this relatively more "real-time" data might well be useful alongside other information in a learning-analytics application.



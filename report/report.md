# Stackoverflow Survey 2017

- the data contains a lot of information, only 4 questions are answered in this analysis.

**Questions which will be answered in the following parts:**

|#| Question | Additional Information | Helpful columns | Target column |
| ---| :--- | :---| :---| :---|
|1| Does the company influence the happiness/satisfaction of the users?  | only for employed users of a company (EmploymentStatus) | EmploymentStatus, CompanySize, CompanyType, InfluenceInternet, InfluenceWorkstation, InfluenceHardware, InfluenceServers, InfluenceTechStack, InfluenceDeptTech, InfluenceVizTools, InfluenceDatabase, InfluenceCloud, InfluenceConsultants, InfluenceRecruitment, InfluenceCommunication | CareerSatisfaction, JobSatisfaction  |
|2| Exists a correlation between "Overpaid" and "Salary", depending on the experience?  | - | YearsProgram, Overpaid, Salary | *TODO: Maybe use one to predict the other?*|
|3| Is there a programing language specific correlation between "OtherPeoplesCode - Maintaining other people's code is a form of torture" and "EnjoyDebugging -I enjoy debugging code"?| - | HaveWorkedLanguage, OtherPeoplesCode, EnjoyDebugging | *TODO: Maybe use one to predict the other?*|
|4|How many people, who program in Python, follow the PEP8 guidlines and use spaces instead of tabs?|-|HaveWorkedLanguage |TabsSpaces|

The questions have been found by looking at the df_schema in detail to find interesting questions.
 
## Question 1: Does the company influence the happiness/satisfaction of the users?
### Preprocessing
The first fact that must be considered to answer this question is EmploymentStatus. If someone is a student or freelancer, they cannot give any information about how a company affects their satisfaction. After this persons are extracted, all company related columns have to be taken into account: *EmploymentStatus*, *CompanySize*, *CompanyType*, *InfluenceInternet*, *InfluenceWorkstation*, *InfluenceHardware*, *InfluenceServers*, *InfluenceTechStack*, *InfluenceDeptTech*, *InfluenceVizTools*, *InfluenceDatabase*, *InfluenceCloud*, *InfluenceConsultants*, *InfluenceRecruitment*, *InfluenceCommunication*.
As all the company values have up to 5 different answer possibilities, they are all processed the same way:
``` Python
# remove entries which do not provide additional information
df_q1.CompanySize = df_q1.CompanySize.replace(["I don't know", "I prefer not to answer"], np.NaN)
df_q1 = df_q1.dropna(axis = 0, subset=['CompanySize'])
#print(df_q1.shape)
#df_q1 = pd.concat([df_q1, pd.get_dummies(df_q1.CompanySize, prefix='CompanySize')], ignore_index = True)
tmp = pd.get_dummies(df_q1.CompanySize, prefix='CompanySize')
#print(tmp.shape)
df_q1[tmp.columns] = tmp
#print(df_q1.shape)
df_q1 = df_q1.drop(labels=['CompanySize'], axis = 1)
```
### Modelling

## Question 2: Exists a correlation between "Overpaid" and "Salary", depending on the experience?
### Preprocessing
### Modelling

## Question 3: Is there a programing language specific correlation between "OtherPeoplesCode - Maintaining other people's code is a form of torture" and "EnjoyDebugging -I enjoy debugging code"?
### Preprocessing
### Modelling

## Question 4: How many people, who program in Python, follow the PEP8 guidlines and use spaces instead of tabs?
### Preprocessing
### Modelling

## Which questions have been answered with this analysis?
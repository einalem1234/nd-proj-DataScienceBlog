# Stackoverflow Survey 2017

Stackoverflow performs an anual survey. As stackoverflow is used by many developers, it is "the largest and most comprehensive survey of people who code around the world" [Ref 1](https://insights.stackoverflow.com/survey/). 
The survey covers a wide range of topics. From the technologies used to production blockers to working conditions, everything is covered.

As the data is so broad, in the following part, only the used data columns are mentioned and explained if needed.

**Questions which will be answered in the following parts:**

To get an idea of this huge data set, I had a look into the schema file which is provided additionally. In the following text I would like to answer some questions which came to me while looking at the data. These questions refer to the people behind the accounts, not to Stackoverflow relevant evaluation. Here are my questions:  

|#| Question | Helpful columns |
| ---| :--- | :---|
|1| Exists a correlation between *Overpaid* and the programming experience? | YearsProgram, Overpaid |
|2| Is there a programing language specific correlation between "OtherPeoplesCode - Maintaining other people's code is a form of torture" and "EnjoyDebugging -I enjoy debugging code"? | HaveWorkedLanguage, OtherPeoplesCode, EnjoyDebugging |
|3|How many people, who program in Python, follow the PEP8 guidlines and use spaces instead of tabs?|HaveWorkedLanguage, TabsSpaces |
|4| Does the company influence the happiness/satisfaction of the users?  | EmploymentStatus, CompanySize, CompanyType, InfluenceInternet, InfluenceWorkstation, InfluenceHardware, InfluenceServers, InfluenceTechStack, InfluenceDeptTech, InfluenceVizTools, InfluenceDatabase, InfluenceCloud, InfluenceConsultants, InfluenceRecruitment, InfluenceCommunication, CareerSatisfaction, JobSatisfaction  |
 

## Question 1: Exists a correlation between *Overpaid* and the programming experience?
### Preprocessing
To determine a correlation, you need values in the corresponding columns. Therefore, in the first step, all data records were removed where the entry in *Overpaid* was missing. By this step, the number of responses reduced from *19102* to *5184*.

*YearsProgram* is a categorical value, which define a time spans of one year each. These values are converted into a nested dictionary which match the years of experience with the Overpaid rate as it can be seen below. 
 ``` Python
## YEARS PROGRAM
# Create a nested dictionary which matches the years of experience with the overpaid rate
q1_dict_experience = defaultdict(dict)

for key, data in df_q1.groupby(by=['YearsProgram', 'Overpaid']):
    experience = key[0]
    overpaid_target = key[1]
    value = data.YearsProgram.count()
    q1_dict_experience[experience][overpaid_target] = value
 ```

### Analysis
To get comparable values for each time span, the values are calculated as percentage.
As it can be seen in the following figure, no correlation exists between the feeling of beeing Over- or Underpaid with the years of experience.
![Correlation of Overpaid and Years of experience](YearsProgram_vs_Overpaid.png)



## Question 2: Is there a programing language specific correlation between "OtherPeoplesCode - Maintaining other people's code is a form of torture" and "EnjoyDebugging -I enjoy debugging code"?
### Preprocessing
In the stackoverflow data set exists a column *HaveWorkedLanguage* which is a list of the different programming languages a respondent has been working with already. This list has been split into binary columns for each programming language. This preprocessing step can be found [here](../notebooks/Stackoverflow_Survey_2017.ipynb#Clean)
### Modelling

## Question 3: How many people, who program in Python, follow the PEP8 guidlines and use spaces instead of tabs?
### Preprocessing
### Modelling

## Question 4: Does the company influence the happiness/satisfaction of the users?
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


## Which questions have been answered with this analysis?
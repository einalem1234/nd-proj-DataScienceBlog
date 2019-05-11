**Questions which will be answered in the following parts:**

To get an idea of this huge data set, I had a look into the schema file which is provided additionally. In the following text I would like to answer some questions which came to me while looking at the data. These questions refer to the people behind the accounts, not to Stackoverflow relevant evaluation. Here are my questions:  

|#| Question | Helpful columns |
| ---| :--- | :---|
|4| Does the company influence the happiness/satisfaction of the users?  | EmploymentStatus, CompanySize, CompanyType, InfluenceInternet, InfluenceWorkstation, InfluenceHardware, InfluenceServers, InfluenceTechStack, InfluenceDeptTech, InfluenceVizTools, InfluenceDatabase, InfluenceCloud, InfluenceConsultants, InfluenceRecruitment, InfluenceCommunication, CareerSatisfaction, JobSatisfaction  | 

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

# EDA-Viewership-Analysis
📊**Exploratory Data Analysis (EDA) – Viewership Analysis**
1. Project Overview
This project focuses on performing Exploratory Data Analysis (EDA) on the BrightTV Viewership Dataset to uncover patterns in user engagement, content preferences, and platform usage. The dataset is sourced from internal streaming analytics systems and processed in Python within or Jupyter Notebook.
________________________________________
2. Objective
•	Analyze user demographics and engagement patterns.
•	Identify the most popular programs, genres, and devices.
•	Understand viewing trends across different regions and time periods.
•	Prepare clean, structured data for dashboard visualization and reporting.
________________________________________
3. Tools and Environment
•	Language: Python
•	Environment: Databricks / Jupyter Notebook
•	Libraries Used: 
•	import pandas as pd
•	import numpy as np
•	import matplotlib.pyplot as plt
•	import seaborn as sns
________________________________________
4. Dataset Metadata
•	Dataset Name: BrightTV Viewership Data
•	Source: BrightTV streaming analytics system (CSV format)
•	Records: 10,002
•	Columns: 9
•	Period Covered: January 2024 – June 2025
Field Name	Description	Data Type
User_ID	Unique viewer identifier	Integer
Age_Group	Age category of user	String
Gender	Gender of viewer	String
Region	Geographic region	String
Program_Name	Name of watched program	String
Genre	Type of content (Drama, News, Sports, etc.)	String
Watch_Time	Duration watched (minutes)	Integer
Device_Type	Device used (Mobile, Smart TV, Laptop, etc.)	String
View_Date	Viewing date and time	Date/Time
________________________________________
5. Data Joining (Merging user_profile and viewership)
The original dataset comes in two separate sheets:
•	user_profile.csv – Contains demographic details (User_ID, Age_Group, Gender, Region)
•	viewership.csv – Contains viewing activity (User_ID, Program_Name, Genre, Watch_Time, Device_Type, View_Date)
To create a single dataset for analysis, we perform an inner join on the User_ID column:
# Load datasets
user_profile = pd.read_csv('user_profile.csv')
viewership = pd.read_csv('viewership.csv')

# Join on User_ID
df = pd.merge(viewership, user_profile, on='User_ID', how='inner')

# Inspect joined data
df.info()
df.head()
✅ Result: A unified dataset combining demographic and viewership behavior, ready for cleaning and EDA.
________________________________________
6. EDA Steps
Step 1: Inspect the Data
df.info()
df.describe()
df.shape
df.isnull().sum()
Step 2: Data Cleaning
•	Remove duplicates and null values
•	Standardize text formats
•	Convert View_Date to datetime format
df.drop_duplicates(inplace=True)
df.dropna(inplace=True)
df['View_Date'] = pd.to_datetime(df['View_Date'])
df['Genre'] = df['Genre'].str.title()
________________________________________
7. Exploratory Visualizations
   
1. Viewer Distribution by Age Group
sns.countplot(x='Age_Group', data=df)
plt.title('Viewer Distribution by Age Group')
2. Gender vs Watch Time
sns.boxplot(x='Gender', y='Watch_Time', data=df)
plt.title('Gender vs Watch Time')
3. Top 10 Most Watched Programs
df['Program_Name'].value_counts().head(10).plot(kind='bar')
plt.title('Top 10 Most Watched Programs')
4. Popular Genres
sns.countplot(y='Genre', data=df, order=df['Genre'].value_counts().index)
plt.title('Most Watched Genres')
5. Regional Viewership
region_views = df.groupby('Region')['Watch_Time'].sum().sort_values(ascending=False)
region_views.plot(kind='bar')
plt.title('Total Watch Time by Region')
6. Device Type Usage
sns.countplot(x='Device_Type', data=df)
plt.title('Preferred Device Types')
7. Correlation Analysis
corr = df.corr(numeric_only=True)
sns.heatmap(corr, annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
________________________________________
8. Insights & Findings
•	Most viewers fall in the 25–34 age group.
•	Drama and Sports are the most popular genres.
•	Smart TVs and mobile devices dominate platform usage.
•	Regions with the highest engagement show stronger weekend activity.
•	Watch time is significantly higher in evening sessions.
________________________________________
9. Conclusion
The EDA successfully combined user profile and viewership data to uncover meaningful patterns in audience behavior. These insights can guide:
•	Content programming and scheduling
•	Targeted marketing campaigns
•	Product and platform development
This analysis also forms the foundation for advanced modeling (e.g., churn prediction, recommendation systems) and dashboard visualization within Databricks.



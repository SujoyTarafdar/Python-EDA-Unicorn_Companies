import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

uc_df=pd.read_csv('Unicorn_Companies.csv')

uc_df.head()

uc_df.tail()

## Checking for any Null values

uc_df.isnull().sum()

## Having a look at the Rows which have Null values

uc_df[uc_df['City'].isnull()]

## Checking for any Duplicat Values

uc_df[uc_df.duplicated()]

# Counting for Comapny names found Bolt company had invested in two different Sectors thats why have two records 

[uc_df['Company'].value_counts()]

## Checking for Any Duplicate values in Entire Data Set

uc_df[uc_df.duplicated()]

## Statistical details for numerical columns

uc_df.describe()


uc_df.head()

uc_df.info()

uc_df.columns

uc_df.head(20)

## Replacing Billions sign B & Dollar Sign $ in Valuation and Funding Column

uc_df['Valuation']=uc_df['Valuation'].replace('[\$,B]','',regex=True).astype(float)

uc_df['Funding']=uc_df['Funding'].replace('[M,\$,B]','',regex=True)



uc_df

## Plotting Number of Unicorn by Industry

industry_counts = uc_df['Industry'].value_counts()
plt.figure(figsize=(10, 6))
sns.barplot(y=industry_counts.index, x=industry_counts.values)
plt.title('Number of Unicorns by Industry')
plt.xlabel('Number of Unicorns')
plt.ylabel('Industry')
plt.show()

## Plotting Unicorn by Continents

continent_counts = uc_df['Continent'].value_counts()
plt.figure(figsize=(8, 5))
sns.barplot(y=continent_counts.index, x=continent_counts.values)
plt.title('Number of Unicorns by Continent')
plt.xlabel('Number of Unicorns')
plt.ylabel('Continent')
plt.show()

## Plotting Year of Foundation vs No of Companies

plt.figure(figsize=(10, 6))
sns.histplot(uc_df['Year Founded'], bins=30, kde=True)
plt.title('Distribution of Year Founded for Unicorn Companies')
plt.xlabel('Year Founded')
plt.ylabel('Number of Companies')
plt.show()

## Plotting Funding vs Valuation

plt.figure(figsize=(10, 7))
sns.scatterplot(x='Funding', y='Valuation', data=uc_df)
plt.title('Funding vs Valuation')
plt.xlabel('Funding')
plt.ylabel('Valuation')
plt.show()

## Plotting Company vs Valuation 

plt.figure(figsize=(10,6))
sns.barplot(y='Valuation',x='Company',data=uc_df)
plt.title('Company vs Valuation')
plt.xlabel('Company')
plt.ylabel('Valuation')
plt.show()


## Top 5 Companies by valuation

top_5_companies = uc_df.nlargest(5,'Valuation')[['Company','Valuation']]

plt.figure(figsize=(10, 6))
sns.barplot(x='Valuation', y='Company', data=top_5_companies, palette='viridis')
plt.title('Top 5 Companies by Highest Valuation')
plt.xlabel('Valuation')
plt.ylabel('Company')
plt.show()


## No of Unicorns by City

city_counts = uc_df['City'].value_counts().head(10)

plt.figure(figsize=(12, 8))
sns.barplot(x=city_counts.values, y=city_counts.index, palette='viridis')
plt.title('Number of Unicorns by City (Top 10)')
plt.xlabel('Number of Unicorns')
plt.ylabel('City')
plt.show()

## Bottom 5 companies in terms of Valuation

bottom_5_companies = uc_df.nsmallest(5,'Valuation')[['Company', 'Valuation']]
plt.figure(figsize=(10, 6))
sns.barplot(x='Valuation', y='Company', data=bottom_5_companies, palette='viridis')
plt.title('Bottom 5 Companies with least Valuation')
plt.xlabel('Valuation')
plt.ylabel('Company')
plt.show()



top_10_industries = uc_df.nlargest(10,'Valuation')[['Industry','Valuation']]

plt.figure(figsize=(10, 6))
sns.barplot(x='Valuation', y='Industry', data=top_10_industries, palette='viridis')
plt.title('Top 10 Industries by Highest Valuation')
plt.xlabel('Valuation')
plt.ylabel('Industry')
plt.show()


## Top 10 Countries having Highest Valued Unicorn Companies

country_valuations = uc_df.groupby('Country')['Valuation'].sum().sort_values(ascending=False)

top_10_countries = country_valuations.head(10)

plt.figure(figsize=(12, 8))
sns.barplot(x=top_10_countries.values, y=top_10_countries.index, palette='viridis')
plt.title('Top 10 Countries having Highest Valued Unicorn Companies')
plt.xlabel('Total Valuation')
plt.ylabel('Country')
plt.show()



















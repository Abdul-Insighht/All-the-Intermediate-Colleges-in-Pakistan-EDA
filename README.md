# All-the-Intermediate-Colleges-in-Pakistan-EDA
# Exploratory Data Analysis Project

# Cell 1
#Exploratory Data Analysis Project # 1
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Cell 2
# Load the dataset
df = pd.read_csv('All the Intermediate Colleges in Pakistan.csv')

# Cell 3
# Overview of the dataset
print("Dataset Overview:\n", df.info())

# Cell 4
df.columns

# Cell 5
df.dtypes

# Cell 6
df.shape

# Cell 7
# Checking for missing values
missing_values = df.isnull().sum()
print("\nMissing Values:\n", missing_values)

# Cell 8
# Basic statistics
print("\nBasic Statistics:\n", df.describe(include='all'))  # Use include='all' to get stats for all columns

# Cell 9
# Unique study programs
print("\nUnique Study Programs:\n", df['Study Program'].unique())

# Cell 10
# Handling missing values in 'Sector' for analysis
df['Sector'].fillna('Unknown', inplace=True)  # Replace missing values in 'Sector' with 'Unknown'


# Cell 11
# Analyzing the distribution of Sector (Private vs Public)
plt.figure(figsize=(8, 6))
sns.countplot(data=df, x='Sector')
plt.title('Distribution of Colleges by Sector (Private vs Public)')
plt.xticks(rotation=45)  # Rotate x-axis labels if necessary
plt.show()

# Cell 12
# Analyzing the distribution of Sector (Private vs Public and Unknown)
plt.figure(figsize=(8, 6))
ax = sns.countplot(data=df, x='Sector')
plt.title('Distribution of Colleges by Sector (Private vs Public and Unknown)')
plt.xticks(rotation=45)  # Rotate x-axis labels if necessary

# Adding the counts on top of the bars
for p in ax.patches:
    ax.annotate(f'{int(p.get_height())}', (p.get_x() + p.get_width() / 2., p.get_height()), 
                ha='center', va='baseline', fontsize=11, color='black', xytext=(0, 5), 
                textcoords='offset points')

plt.show()


# Cell 13
# Handling missing or improper values in 'Rating' column
# First, convert the 'Rating' column to a string type, extract numbers, and convert them back to float
df['Rating'] = df['Rating'].astype(str).str.extract('(\d+\.?\d*)').astype(float)

# Cell 14
# Analyzing the rating distribution
plt.figure(figsize=(8, 6))
sns.histplot(df['Rating'].dropna(), bins=5, kde=True)
plt.title('Distribution of College Ratings')
plt.xlabel('Rating')
plt.ylabel('Count')
plt.show()

# Cell 15
# Correlation between sectors and ratings (drop rows with missing 'Rating')
plt.figure(figsize=(8, 6))
sns.boxplot(data=df.dropna(subset=['Rating']), x='Sector', y='Rating')
plt.title('Rating Distribution by Sector')
plt.xticks(rotation=45)
plt.show()

# Cell 16
# Top locations with the most colleges
top_locations = df['Location'].value_counts().head(10)
plt.figure(figsize=(10, 6))
sns.barplot(x=top_locations.values, y=top_locations.index)
plt.title('Top 10 Locations with Most Colleges')
plt.xlabel('Number of Colleges')
plt.ylabel('Location')
plt.show()

# Cell 17

# Displaying the first few rows to understand the structure of the data
print(df.head())


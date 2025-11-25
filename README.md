# Agricultural-Commodity-Trends-Using-Python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# 1. Load the data (already done)
df=pd.read_csv("C:/Users/Ayush Gupta/OneDrive/Desktop/PYTHON PROJECT dataset.csv")
# 2. Information of data
info = df.info()

# 3. Summary statistics of the data
summary = df.describe(include='all')

# 4. Total rows and columns
shape = df.shape

# 5. Max values
max_values = df.max(numeric_only=True)

# 6. Min values
min_values = df.min(numeric_only=True)

# 7. Mode values
mode_values = df.mode().iloc[0]

# 8. Head function
head_data = df.head()

# 9. Tail function
tail_data = df.tail()

# 10. Sort data by 'Modal_x0020_Price'
sorted_data = df.sort_values(by='Modal_x0020_Price', ascending=False)

# 11. Use of loc - selecting specific rows and columns
loc_data = df.loc[0:4, ['State', 'District', 'Commodity', 'Modal_x0020_Price']]

# 12. Checking for missing values
missing_values = df.isnull().sum()

# 13. Filling missing values (if any)
df_cleaned = df.ffill()


# 14. Correlation matrix
correlation = df_cleaned.corr(numeric_only=True)

# 15. Value counts for a categorical column
value_counts = df['Commodity'].value_counts().head(10)

# 16. Unique commodities
unique_commodities = df['Commodity'].unique()

# 17. Number of unique commodities
num_unique_commodities = df['Commodity'].nunique()

# 18. Group by Commodity and calculate mean Modal Price
grouped_mean_price = df.groupby('Commodity')['Modal_x0020_Price'].mean().sort_values(ascending=False).head()

# 19. Histogram of Modal Price
plt.figure(figsize=(8, 5))
df['Modal_x0020_Price'].hist(bins=20)
plt.title('Histogram of Modal Price')
plt.xlabel('Modal Price')
plt.ylabel('Frequency')
plt.grid(False)
plt.tight_layout()
plt.show()

# 20. Boxplot using seaborn
plt.figure(figsize=(10, 6))
sns.boxplot(x='Commodity', y='Modal_x0020_Price', data=df[df['Commodity'].isin(value_counts.index)])
plt.xticks(rotation=90)
plt.title('Boxplot of Modal Price by Commodity')
plt.tight_layout()
plt.show()

# 21. Heatmap of correlation
plt.figure(figsize=(8, 6))
sns.heatmap(correlation, annot=True, cmap='coolwarm')
plt.title('Correlation Heatmap')
plt.tight_layout()
plt.show()

# 22. Bar plot for average modal price of top commodities
plt.figure(figsize=(10, 5))
grouped_mean_price.plot(kind='bar', color='skyblue')
plt.title('Average Modal Price of Top Commodities')
plt.ylabel('Average Modal Price')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 23. Count plot for top districts
plt.figure(figsize=(10, 5))
top_districts = df['District'].value_counts().head(10)
sns.barplot(x=top_districts.index, y=top_districts.values, palette='Set2',hue=top_districts.index,legend=False)
plt.title('Top 10 Districts by Market Entries')
plt.ylabel('Number of Entries')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 24. Scatter plot between Min and Max price
plt.figure(figsize=(8, 5))
sns.scatterplot(x='Min_x0020_Price', y='Max_x0020_Price', data=df)
plt.title('Min vs Max Price')
plt.tight_layout()
plt.show()

# 25. Line plot of Modal Price trend for a specific commodity
sample_commodity = 'Banana'
banana_df = df[df['Commodity'] == sample_commodity].sort_values(by='Arrival_Date')
plt.figure(figsize=(10, 5))
plt.plot(banana_df['Arrival_Date'], banana_df['Modal_x0020_Price'], marker='o')
plt.xticks(rotation=45)
plt.title(f'Modal Price Trend for {sample_commodity}')
plt.xlabel('Date')
plt.ylabel('Modal Price')
plt.tight_layout()
plt.show()

# Display textual outputs
{
    "Data Info": info,
    "Summary": summary,
    "Shape": shape,
    "Max Values": max_values,
    "Min Values": min_values,
    "Mode Values": mode_values,
    "Missing Values": missing_values,
    "Top Commodity Mean Modal Prices": grouped_mean_price
}

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('clothes_price_date.csv')

df.head()

df.info()

item_names = df['ItemName'].unique()
item_names

df['Category'].unique()

for item_name in item_names:
    row = df[df['ItemName'] == item_name].value_counts('Category')
    plt.title(f'{item_name} Breakdown by Category')
    sns.barplot(x=row.index, y=row)
    plt.show()

# For T-Shirt we will set to null any Category other than Topwear
df.loc[(df['ItemName'] == 'T-Shirt') & (df['Category'] != 'Topwear'), 'Category'] = np.nan
# For T-Shoes we will set to null any Category other than Footwear
df.loc[(df['ItemName'] == 'Shoes') & (df['Category'] != 'Footwear'), 'Category'] = np.nan
# For Jeans we will set to null Category with Footwear only
df.loc[(df['ItemName'] == 'Jeans') & (df['Category'] == 'Footwear'), 'Category'] = np.nan
# For Jacket we will set to null any Category other than Topwear and Outerwear
df.loc[(df['ItemName'] == 'Jacket') & (~df['Category'].isin(['Topwear', 'Outerwear'])), 'Category'] = np.nan
# For Dress we will set to null any Category other than Dresses and Topwear
df.loc[(df['ItemName'] == 'Dress') & (~df['Category'].isin(['Dresses', 'Topwear'])), 'Category'] = np.nan

df.info()

# Fill null values with the most frequent Category for each ItemName
for item_name in item_names:
    category = df[df['ItemName'] == item_name].value_counts('Category').index[0]
    myFilter = df['ItemName'] == item_name
    df.loc[myFilter, 'Category'] = df.loc[myFilter, 'Category'].fillna(category)
    
df.info()

for item_name in item_names:
    row = df[df['ItemName'] == item_name].value_counts('Category')
    plt.title(f'{item_name} Breakdown by Category')
    sns.barplot(x=row.index, y=row)
    plt.show()

df.to_csv('clothes_price_data_clean_category.csv', index=False)

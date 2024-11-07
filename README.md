# Exploratory Data Analysis

This repository will show you how to perform a exploratory data analysis on a dataset containing information about popular tracks on Most Streamed Spotify Songs 2023

***

### Preprocessing of Data Set

```python
#import necessary libraries needed
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import calendar
```
***

### Overview of dataset
1. How many rows and columns does the data set contain?
2. What are the data types of each column? Are there any missing values?

```python
df_spotify = pd.read_csv('spotify-2023 (2).csv', encoding='ISO-8859-1')
df_spotify
```

![image](https://github.com/user-attachments/assets/bf29649f-a53c-49ba-8f2f-f1a9ade7b231)

```python
#Display the number of rows and columns of dataset
df_spotify.info()
```
![image](https://github.com/user-attachments/assets/03587e13-214e-47d8-a9e3-99781d82d5de)

***

### Data Cleaning

```python
#To locate streams that are objects
df_spotify['streams'].iloc[574]
```

![image](https://github.com/user-attachments/assets/a7839bea-a0d7-42c7-b219-93a170583b44)

```python
#Convert streams to numeric values
df_spotify['streams'] = pd.to_numeric(df_spotify['streams'], errors = 'coerce')
df_spotify['streams']
```

![image](https://github.com/user-attachments/assets/fd65b566-d9a5-480b-a297-c6ca83982fc3)

```python
df_spotify['streams'].iloc[574]
```

![image](https://github.com/user-attachments/assets/98a4d711-8452-4987-afdf-86b16b6a3e42)

```python
df_spotify.at[574, 'streams'] = 227373748
df_spotify['streams'].iloc[574]
# fills missing value
```
![image](https://github.com/user-attachments/assets/cbd9cbc8-2e65-495f-9e69-fb2fd23e2fb1)

### For the in_deezer_playlist attribute
```python
#Replace comman with numeric values
df_spotify['in_deezer_playlists'] = df_spotify['in_deezer_playlists'].str.replace(",","").astype(float)
df_spotify['in_deezer_playlists']
```

![image](https://github.com/user-attachments/assets/20a48db5-dd38-43c0-9725-7d328794ee3d)

### For the in_shazam_charts attribute
```python
#Replace comman with numeric values
df_spotify['in_shazam_charts'] = df_spotify['in_shazam_charts'].str.replace(",","").astype(float)
df_spotify['in_shazam_charts']
```

![image](https://github.com/user-attachments/assets/4570fd43-9d5f-4abd-b132-7acf7d619047)

***

### Handling duplicate tracks and values
```python
duplicate_tracks = pd.DataFrame(df_spotify[df_spotify.duplicated(['track_name','artist(s)_name'])])
# checks duplicated tracks

print("The duplicate tracks that is in the dataset are ")
print()
print(duplicate_tracks[['track_name','artist(s)_name']])
```

![image](https://github.com/user-attachments/assets/7f954d33-c501-4551-91fc-bad331faa51b)

### For 'SPIT IN MY FACE'
```python
df_spotify.loc[(df_spotify['track_name']=='SPIT IN MY FACE!')]
```

![image](https://github.com/user-attachments/assets/76b311e8-44f4-4364-85f6-6c88d660cfca)

```python
df_spotify.drop(index=345, inplace=True)
df_spotify.loc[(df_spotify['track_name']=='SPIT IN MY FACE!')]
```

![image](https://github.com/user-attachments/assets/85846830-222b-4544-978b-663cb5f31591)

### For 'Take my breath'
```python
df_spotify.loc[(df_spotify['track_name']=='Take My Breath')]
```

![image](https://github.com/user-attachments/assets/00b0c7f0-68bc-4848-8ca3-8d79d80b9dfa)

```python
df_spotify.drop(index=512, inplace=True)
df_spotify.loc[(df_spotify['track_name']=='Take My Breath')]
```

![image](https://github.com/user-attachments/assets/7e13bff2-89ed-4c23-a541-85eaee39f1bc)

### For 'About Damn Time'
```python
df_spotify.loc[(df_spotify['track_name']=='About Damn Time')]
```

![image](https://github.com/user-attachments/assets/0ffe806b-0707-44fc-b37c-46db484dff83)

```python
df_spotify.drop(index=372, inplace=True)
df_spotify.loc[(df_spotify['track_name']=='About Damn Time')]
```

![image](https://github.com/user-attachments/assets/363f10ee-1cb6-4acf-8729-b27ca5704439)

### For 'SNAP'
```python
df_spotify.loc[(df_spotify['track_name']=='SNAP')]
```

![image](https://github.com/user-attachments/assets/002fbb46-4caa-48a7-8c84-6333f9abd4e3)

```python
df_spotify.drop(index=873, inplace=True)
df_spotify.loc[(df_spotify['track_name']=='SNAP')]
```

![image](https://github.com/user-attachments/assets/839eb434-16d3-4aca-ab73-eebea42271cb)

```python
df_spotify[df_spotify.duplicated(["track_name","artist(s)_name"])]
```

***

### Missing Value
```python
missing_values = df_spotify.isna().sum()

print("The attributes that have missing values in the dataset are ")
print()
print(missing_values[missing_values>0])
```
![image](https://github.com/user-attachments/assets/ce5c6f23-e518-4ebf-abcc-b8d93a127376)


```python
shazam_median = df_spotify['in_shazam_charts'].median()
f"The median value of the 'in_shazam_charts' is {shazam_median}"
```

![image](https://github.com/user-attachments/assets/e49c2864-09ed-462d-a36a-f1b84ff6dd26)

```python
missing_values = df_spotify.isna().sum()
print("The updated missing values are now ")
print()
print(missing_values[missing_values>0])
```

![image](https://github.com/user-attachments/assets/0b1dde73-69f2-4c5c-9219-7eda27c68597)

```python
shazam_median = df_spotify['in_shazam_charts'].median()
f"The median value of the 'in_shazam_charts' is {shazam_median}"
```

![image](https://github.com/user-attachments/assets/f10f82c1-eae8-49f5-aa38-f328b116f54c)

```python
df_spotify.isna().sum()
```

![image](https://github.com/user-attachments/assets/1ae8f11a-db01-49a9-a9bb-7fec2a2a8b4f)

***

### Basic Descriptive

1. What are the mean, median, and standard deviation of the streams column?

```python
f"The total streams of the most streamed spotify songs of 2023 is {df_spotify['streams'].sum()}"
```
![image](https://github.com/user-attachments/assets/799b88f3-7a47-4d1e-8a0a-9ede62412021)

```python
f"The mean of the total streams of the most streamed spotify songs of 2023 is {df_spotify['streams'].mean()}"
```
![image](https://github.com/user-attachments/assets/9d9fef89-352c-4ed1-b706-8ff3a71acdaa)

```python
f"The median of the total streams of the most streamed spotify songs of 2023 is {df_spotify['streams'].median()}"
```
![image](https://github.com/user-attachments/assets/73f922d3-af0e-43fa-b66b-95ac83ec1043)

```python
f"The standard deviation of the total streams of the most streamed spotify songs of 2023 is {df_spotify['streams'].std()}"
```
![image](https://github.com/user-attachments/assets/54c5702e-9255-4527-95e8-8bc7f76113eb)


```python
df_spotify[['track_name', 'streams']].sort_values(by='streams', ascending=False).head(10)
```
![image](https://github.com/user-attachments/assets/8a0350e3-d08b-468f-9130-a6dceace994f)

```python
sns.histplot(df_spotify, x= 'streams',color='blue', element="poly").set(title = 'Distribution of total streams')
sns.set_style("whitegrid", {'grid.linestyle': '--'})

plt.xlabel('Number of Streams by Billions')
plt.ylabel('Number of Tracks')
```
![image](https://github.com/user-attachments/assets/8c9b9db1-22c0-4585-bcc7-005a4496d3ea)

```python
# Create the displot for the 'released_year' column
ryd = sns.displot(df_spotify, x='released_year', color='blue', discrete=True, aspect=3)

# Set the title for the plot
ryd.fig.suptitle("Distribution of the Most Streamed Spotify Songs of 2023 by Released Year", fontsize=16)

# Get the underlying axis to customize further
ax = ryd.ax

# Add gridlines along the y-axis
ax.grid(True, axis="y", color="gray", alpha=0.5)

# Set the labels for x and y axes
ax.set_xlabel('Track Release Year', fontsize=12)
ax.set_ylabel('Number of Tracks', fontsize=12)

# Adjust layout to avoid overlap (especially with long titles)
plt.tight_layout()

# Show the plot
plt.show()
```
![image](https://github.com/user-attachments/assets/580b154c-f01b-4a15-aff9-1158036884a2)

```python
# Calculate first quartile (25th percentile)
Q1ry = df_spotify['released_year'].quantile(0.25)

# Calculate third quartile (75th percentile)
Q3ry = df_spotify['released_year'].quantile(0.75)

# Calculate Interquartile Range (IQR)
IQRry = Q3ry - Q1ry

# Identify outliers: values outside the range (Q1 - 1.5 * IQR) and (Q3 + 1.5 * IQR)
outliers_ry = df_spotify[(df_spotify['released_year'] < Q1ry - 1.5 * IQRry) | (df_spotify['released_year'] > Q3ry + 1.5 * IQRry)]

# Get the number of outliers
ry_outliers_num = outliers_ry.shape[0]

# Return the message about outliers
outlier_message = f"There are about {ry_outliers_num} outliers in the release year of tracks."

# Optionally, display the outliers for further inspection
outliers_ry.head()  # Show the first few rows of the outliers for inspection (optional)

# Display the outlier message
outlier_message
```
![image](https://github.com/user-attachments/assets/4c7073da-799e-457a-bf28-96b4134b2d61)

```python
plt.figure(figsize=(15, 5))
# To size the boxplots

sns.boxplot(x=df_spotify['released_year'], fliersize=3)
# Creates boxplot and resize the outlier data points

plt.title("Track Release Year Boxplot") 
# Sets title for the boxplot
plt.xlabel("Track Release Year")
# Labels x-axis
plt.show()
```
![image](https://github.com/user-attachments/assets/fe27f65f-982b-4e89-9b36-25049c986e21)

```python
ac = sns.displot(df_spotify, x='artist_count', color='Blue', discrete=True).set(title = "Distribution of the number of credited artists per track")
# To plot the distrbution of the released_year along with its distribution line, and each year being represented
# To plot the distrbution of the released_year along with its distribution line, and each artist count being represented
# also labels title

sns.set_style("white")

ax = ac.ax
ax.grid(True, axis="y", color="gray", alpha=0.5)
# to place grids along the x_axis

plt.xlabel('Number of Credited Artists')
plt.ylabel('Number of Tracks')
# labels x and y axes
```
![image](https://github.com/user-attachments/assets/c43ed6e2-ae7d-4018-ac7d-fd8275cb0ccb)

```python
Q1ac = df_spotify['artist_count'].quantile(0.25)
Q3ac = df_spotify['artist_count'].quantile(0.75)
IQRac = Q3ac - Q1ac

# Equation for finding outliers within a given data
outliers_ac = df_spotify[(df_spotify['artist_count'] < Q1ac - 1.5 * IQRac) | (df_spotify['artist_count'] > Q3ac + 1.5 * IQRac)]
ac_outliers_num = outliers_ac.shape[0]
f"There are about {ac_outliers_num} outliers within the release year attributes of the tracks."
```
![image](https://github.com/user-attachments/assets/1d3a1d99-4546-4523-b2a1-acff17ef751f)

```python
plt.figure(figsize=(15, 5))
# To size the boxplots

sns.boxplot(x=df_spotify['artist_count'], fliersize=3)
# Creates boxplot and resize the outlier data points

plt.title("Number of Credited Artist Per Track Boxplot") 
# Sets title for the boxplot
plt.xlabel("Track Release Year")
# Labels x-axis
plt.show()
```
![image](https://github.com/user-attachments/assets/15514dc9-4d3f-405e-af08-131dd2ee00ec)

***

### Top Performers

1. Which track has the highest number of streams? Display the top 5 most streamed tracks.

```python
df_spotify[['track_name', 'artist(s)_name','streams']].sort_values(by='streams', ascending=False).head()
# it sorts the data from greatest to least streams
# it locates and print the first 5 songs along with its track name and the number of streams
```
![image](https://github.com/user-attachments/assets/f385c347-ef44-435d-aff1-9d7bfe5eb280)

```python
df_spotify['artist(s)_name'] = df_spotify['artist(s)_name'].str.split(',')
df_spotify['artist(s)_name']
# turns all the artists into a list and splits all of them with a column
```
![image](https://github.com/user-attachments/assets/ea8d4350-4ee8-4bf5-ba5f-3648bbce200e)

```python
df_spotify = df_spotify.explode('artist(s)_name').reset_index(drop=True)
df_spotify['artist(s)_name'] = df_spotify['artist(s)_name'].str.strip()
df_spotify
# The .explode() makes it so that the list is counted as a row, we also reset index for cleaner analaysis
# The list of the seperated names in now stored in the column of the artist(s)_name
# The result can be seen below
```
![image](https://github.com/user-attachments/assets/0c2afc94-62d5-4718-a8aa-130b3006a59d)

### Top 5 most played artist based on number of songs/albums
```python
df_spotify['artist_name'].value_counts().head()
```
![image](https://github.com/user-attachments/assets/1970cc42-8909-40a0-8599-6096519eb6bd)

***

### Temporal trends

1. Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year

##### Number and month or releases

```python
sns.displot(data=df_spotify, x='released_year', element='poly', fill=False, discrete=True, aspect = 3)
# plots the tracks released vs the year it was released

plt.xlabel('Months')
plt.ylabel('Number of Tracks Released')
plt.title('Number of Tracks Released Per Month')
# labels the different parts of the plot such as the x-axis, y-axis, and the title
```
![image](https://github.com/user-attachments/assets/acaf5ccc-ebfe-4409-a6e5-03bbb89f3a45)

##### Releases over the month

```python
sns.displot(data=df_spotify, x='released_month', element='poly', fill=False, discrete=True, aspect = 3)
# plots the tracks released vs the months it was released on
sns.set_style("whitegrid", {'grid.linestyle': '--'})

plt.xlabel('Months')
plt.ylabel('Number of Tracks Released')
plt.title('Number of Tracks Released Per Month')
# labels the different parts of the plot such as the x-axis, y-axis, and the title


plt.xticks(ticks=range(1, 13), labels=[calendar.month_name[i] for i in range(1, 13)])
# uses calendar library to name the months for the x-axis

plt.xlim(1, 12)
# shows all the months
plt.show()
```
![image](https://github.com/user-attachments/assets/38051db5-04fc-46d4-b07a-fc56d8881e78)

***

### Genre and Music Characteristics





























































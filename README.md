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
#Load given dataset
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
# Locate row 574
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
# Locate track 'SPIT IN MY FACE'
df_spotify.loc[(df_spotify['track_name']=='SPIT IN MY FACE!')]
```

![image](https://github.com/user-attachments/assets/76b311e8-44f4-4364-85f6-6c88d660cfca)

```python
# Remove duplicate
df_spotify.drop(index=345, inplace=True)
df_spotify.loc[(df_spotify['track_name']=='SPIT IN MY FACE!')]
```

![image](https://github.com/user-attachments/assets/85846830-222b-4544-978b-663cb5f31591)

### For 'Take my breath'
```python
#Locate track 'TAKE MY BREATH'
df_spotify.loc[(df_spotify['track_name']=='Take My Breath')]
```

![image](https://github.com/user-attachments/assets/00b0c7f0-68bc-4848-8ca3-8d79d80b9dfa)

```python
#Remove duplicate
df_spotify.drop(index=512, inplace=True)
df_spotify.loc[(df_spotify['track_name']=='Take My Breath')]
```

![image](https://github.com/user-attachments/assets/7e13bff2-89ed-4c23-a541-85eaee39f1bc)

### For 'About Damn Time'
```python
#Locate track 'About Damn Time'
df_spotify.loc[(df_spotify['track_name']=='About Damn Time')]
```

![image](https://github.com/user-attachments/assets/0ffe806b-0707-44fc-b37c-46db484dff83)

```python
#Remove Duplicate
df_spotify.drop(index=372, inplace=True)
df_spotify.loc[(df_spotify['track_name']=='About Damn Time')]
```

![image](https://github.com/user-attachments/assets/363f10ee-1cb6-4acf-8729-b27ca5704439)

### For 'SNAP'
```python
#locate track 'SNAP'
df_spotify.loc[(df_spotify['track_name']=='SNAP')]
```

![image](https://github.com/user-attachments/assets/002fbb46-4caa-48a7-8c84-6333f9abd4e3)

```python
#Remove duplicate
df_spotify.drop(index=873, inplace=True)
df_spotify.loc[(df_spotify['track_name']=='SNAP')]
```

![image](https://github.com/user-attachments/assets/839eb434-16d3-4aca-ab73-eebea42271cb)

```python
#Locate tracks with duplicate
df_spotify[df_spotify.duplicated(["track_name","artist(s)_name"])]
```

***

### Missing Value
```python
#Locate tracks with missing values
missing_values = df_spotify.isna().sum()

print("The attributes that have missing values in the dataset are ")
print()
print(missing_values[missing_values>0])
```
![image](https://github.com/user-attachments/assets/ce5c6f23-e518-4ebf-abcc-b8d93a127376)


```python
#Calculate median of given track
shazam_median = df_spotify['in_shazam_charts'].median()
f"The median value of the 'in_shazam_charts' is {shazam_median}"
```

![image](https://github.com/user-attachments/assets/e49c2864-09ed-462d-a36a-f1b84ff6dd26)

```python
#Print output of missing values
missing_values = df_spotify.isna().sum()
print("The updated missing values are now ")
print()
print(missing_values[missing_values>0])
```

![image](https://github.com/user-attachments/assets/0b1dde73-69f2-4c5c-9219-7eda27c68597)

```python
#Fill missing values with the median
shazam_median = df_spotify['in_shazam_charts'].median()
f"The median value of the 'in_shazam_charts' is {shazam_median}"
```

![image](https://github.com/user-attachments/assets/f10f82c1-eae8-49f5-aa38-f328b116f54c)

```python
#Output
df_spotify.isna().sum()
```

![image](https://github.com/user-attachments/assets/1ae8f11a-db01-49a9-a9bb-7fec2a2a8b4f)

***

### Basic Descriptive

1. What are the mean, median, and standard deviation of the streams column?

```python
#Print total streams
f"The total streams of the most streamed spotify songs of 2023 is {df_spotify['streams'].sum()}"
```
![image](https://github.com/user-attachments/assets/799b88f3-7a47-4d1e-8a0a-9ede62412021)

```python
#Print mean of the total streams
f"The mean of the total streams of the most streamed spotify songs of 2023 is {df_spotify['streams'].mean()}"
```
![image](https://github.com/user-attachments/assets/9d9fef89-352c-4ed1-b706-8ff3a71acdaa)

```python
#Print total median of the streams
f"The median of the total streams of the most streamed spotify songs of 2023 is {df_spotify['streams'].median()}"
```
![image](https://github.com/user-attachments/assets/73f922d3-af0e-43fa-b66b-95ac83ec1043)

```python
f"The standard deviation of the total streams of the most streamed spotify songs of 2023 is {df_spotify['streams'].std()}"
```
![image](https://github.com/user-attachments/assets/54c5702e-9255-4527-95e8-8bc7f76113eb)


```python
#Print standard deviation of the total streams
df_spotify[['track_name', 'streams']].sort_values(by='streams', ascending=False).head(10)
```

2. What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?

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

2. Who are the top 5 most frequent artists based on the number of tracks in the dataset?

```python
df_spotify['artist(s)_name'].value_counts().head()
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

2. Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?

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

1. Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?

```python
#obtain correlations between streams and the given musical attributrs
correlationstreams = df_spotify[['streams', 'bpm', 'danceability_%', 'energy_%']].corr()['streams'].drop('streams')

print("Correlation of Streams with Musical Attributes: \n")
print(correlationstreams)
```
![image](https://github.com/user-attachments/assets/577f23bf-cda1-4e4a-98c2-2a9863952089)

2. Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?

```python
#get correlation between danceability_% and energy_%
danceability_energy_corr = df_spotify['danceability_%'].corr(df_spotify['energy_%'])
print(f"Correlation between Danceability % and Energy %: {danceability_energy_corr:.2f}")

#get correlation between valence_% and acousticness_%
valence_acousticness_corr = df_spotify['valence_%'].corr(df_spotify['acousticness_%'])
print(f"Correlation between Valence % and Acousticness %: {valence_acousticness_corr:.2f}")
```
![image](https://github.com/user-attachments/assets/8748572c-5567-4830-9d2c-69330d8db103)

```python
#graph the correlation for the attributes
attributes = df_spotify[['streams', 'bpm', 'danceability_%', 'energy_%', 'valence_%', 'acousticness_%']]
correlation_matrix = attributes.corr()

#create and plot using heatmap to observe the correlations 
plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, vmin = -1, vmax = 1, cmap='BuPu')
plt.title("Correlation Heatmap of Streams and the different Musical Atrributes")
plt.show()
```
![image](https://github.com/user-attachments/assets/9995c059-01eb-464f-aadb-4c6e7e601782)

***

### Platform Popularity

1. How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?

```python
track_platform_selected = ['in_spotify_playlists', 'in_spotify_charts', 'in_apple_playlists']

# Sum the occurrences of tracks across the selected platforms
platform_counts = df_spotify[track_platform_selected].sum()

# Create a bar plot for the summed occurrences of tracks
plt.figure(figsize=(10, 6))
sns.barplot(x=platform_counts.index, y=platform_counts.values, palette='viridis')

# Apply a logarithmic scale to the y-axis to deal with large range of occurrences
plt.yscale('log')

# Title and axis labels
plt.title("Selected Platform Statistics vs. Number of Occurring Tracks", fontsize=14)
plt.xlabel("Selected Platform", fontsize=12)
plt.ylabel("Total Number of Occurrences (Log Scale)", fontsize=12)

# Display the plot
plt.tight_layout()  # Adjust layout for better spacing
plt.show()
```
![image](https://github.com/user-attachments/assets/5f5a8373-e98f-4e21-9e66-aa597177c426)

```python
track_platform_selected = ['in_spotify_playlists', 'in_spotify_charts', 'in_apple_playlists']

# Calculate the mean of occurrences for each platform
platform_means = df_spotify[track_platform_selected].mean()

# Create a bar plot for the mean occurrences of tracks
plt.figure(figsize=(10, 6))
sns.barplot(x=platform_means.index, y=platform_means.values, palette='viridis')

# Apply a logarithmic scale to the y-axis to deal with large range of occurrences
plt.yscale('log')

# Title and axis labels
plt.title("Selected Platform Statistics vs. Mean of Number of Occurring Tracks", fontsize=14)
plt.xlabel("Selected Platform", fontsize=12)
plt.ylabel("Mean Number of Occurrences (Log Scale)", fontsize=12)

# Display the plot
plt.tight_layout()  # Adjust layout for better spacing
plt.show()
```
![image](https://github.com/user-attachments/assets/af22b8d1-7f85-4267-aa5e-3c87b9e3f1ea)

```python
# List of selected platform charts
track_platform_charts = ['in_spotify_charts', 'in_apple_charts', 'in_deezer_charts', 'in_shazam_charts']

# Calculate the mean of occurrences for each chart platform
chart_means = df_spotify[track_platform_charts].mean()

# Create a bar plot for the mean occurrences of tracks in platform charts
plt.figure(figsize=(10, 6))  # Set the figure size
sns.barplot(x=chart_means.index, y=chart_means.values, palette='viridis')

# Set title and axis labels
plt.title("Mean of Selected Platform Charts", fontsize=14)
plt.xlabel("Platform Charts", fontsize=12)
plt.ylabel("Mean Number of Occurrences", fontsize=12)

# Display the plot
plt.tight_layout()  # Adjust layout for better spacing
plt.show()
```
![image](https://github.com/user-attachments/assets/c3e8622c-f800-4ef8-b202-f26dd0f23187)

### Comparison of number of tracks/songs in playlist of platforms

```python
# List of selected platform playlists
track_platform_playlists = ['in_spotify_playlists', 'in_apple_playlists', 'in_deezer_playlists']

# Calculate the total occurrences of tracks for each platform
platform_playlist_totals = df_spotify[track_platform_playlists].sum()

# Create a bar plot for the total occurrences of tracks in platform playlists
plt.figure(figsize=(10, 6))  # Set the figure size
sns.barplot(x=platform_playlist_totals.index, y=platform_playlist_totals.values, palette='viridis')

# Set title and axis labels
plt.title("Playlists vs Total Number of Occurring Tracks", fontsize=14)
plt.xlabel("Platform Playlists", fontsize=12)
plt.ylabel("Number of Occurring Tracks (in Millions)", fontsize=12)

# Display the plot
plt.tight_layout()  # Adjust layout for better spacing
plt.show()
```
![image](https://github.com/user-attachments/assets/dd36c4d7-bb38-4ab2-b434-c25de979a8ec)

```python
# List of selected platform playlists
track_platform_playlists = ['in_spotify_playlists', 'in_apple_playlists', 'in_deezer_playlists']

# Calculate the mean occurrences for each platform
platform_playlist_means = df_spotify[track_platform_playlists].mean()

# If you want to display the values in millions (optional), divide by 1,000,000
platform_playlist_means /= 1_000_000  # Convert to millions

# Create a bar plot for the mean occurrences of tracks in platform playlists
plt.figure(figsize=(10, 6))  # Set the figure size
sns.barplot(x=platform_playlist_means.index, y=platform_playlist_means.values, palette='viridis')

# Set title and axis labels
plt.title("Playlists vs Number of Tracks (Mean)", fontsize=14)
plt.xlabel("Platform Playlists", fontsize=12)
plt.ylabel("Mean Number of Occurring Tracks (in Millions)", fontsize=12)

# Display the plot
plt.tight_layout()  # Adjust layout for better spacing
plt.show()
```
![image](https://github.com/user-attachments/assets/464e0dc7-77d0-45ff-88b4-70dc5edb91fd)

### Advanced Analysis

1. Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?
```python
# Grouping by 'key' and counting the number of tracks per key
df_key_counts = pd.DataFrame(df_spotify.groupby("key").size())

# Sort by the 'key' alphabetically (or by number of tracks if preferred)
df_key_counts = df_key_counts.sort_values(by=0, ascending=False).reset_index()

# Renaming the second column to 'number_of_tracks'
df_key_counts = df_key_counts.rename(columns={0: 'number_of_tracks'})

# Filter out 'Missing' and NaN keys
df_key_counts = df_key_counts[df_key_counts['key'] != 'Missing']
df_key_counts = df_key_counts[df_key_counts['key'].notna()]

# Display the cleaned and sorted DataFrame
df_key_counts
```
![image](https://github.com/user-attachments/assets/3f8b6e7a-390e-4743-87d0-b385fb2fd477)

```python
# Create the barplot
plt.figure(figsize=(12, 6))  # Set the figure size for better readability
sns.barplot(x='key', y='number_of_tracks', data=df_key_counts, palette='Set2')

# Add title and axis labels
plt.title("Key Count Barplot", fontsize=16)
plt.xlabel("Keys", fontsize=12)
plt.ylabel("Number of Tracks", fontsize=12)

# Display the plot
plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/46be028e-b9e5-42af-a31d-45e1038fc35e)

### Minor vs Major
```python
# Group by 'mode' and count the number of tracks per mode
df_mode_counts = pd.DataFrame(df_spotify.groupby("mode").size())

# Sort the DataFrame by the number of tracks in descending order
df_mode_counts = df_mode_counts.sort_values(by=0, ascending=False).reset_index()

# Rename the second column to 'number_of_tracks'
df_mode_counts = df_mode_counts.rename(columns={0: 'number_of_tracks'})

# Optionally, filter out missing values or any invalid modes if needed
df_mode_counts = df_mode_counts[df_mode_counts['mode'].notna()]

# Display the resulting DataFrame
df_mode_counts
```
![image](https://github.com/user-attachments/assets/cc3a94fb-43df-494e-b1e4-2295bc0f1ab8)

```python
sns.barplot(df_mode_counts, x = 'mode', y = 'number_of_tracks', palette='Set2')
# Creates mode vs. number of tracks barplot and colors it

plt.title("Mode vs. Total Tracks Barplot")
plt.xlabel("Mode")
plt.ylabel("Number of Tracks")
# Labels the plot's title, x-title, and y-title
```
![image](https://github.com/user-attachments/assets/a7980a83-36ae-4725-a21b-1e7e3bb9bcc7)

2. Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.
```python
# Define the platform columns that represent the presence of the artist in playlists
platform_playlists = ['in_spotify_playlists', 'in_apple_playlists', 'in_deezer_playlists']

# Group by artist name and sum the occurrences in playlists across platforms
df_artist_playlists = df_spotify.groupby('artist_name')[platform_playlists].sum()

# Create a total column by summing across the selected platforms for sorting purposes
df_artist_playlists['total_occurrences'] = df_artist_playlists[platform_playlists].sum(axis=1)

# Sort by the total occurrences in playlists across all platforms from greatest to least
df_artist_playlists = df_artist_playlists.sort_values(by='total_occurrences', ascending=False).reset_index()

# Select the relevant columns to display: artist name and occurrences across platforms
df_artist_playlists[['artist_name', 'in_spotify_playlists', 'in_apple_playlists', 'in_deezer_playlists', 'total_occurrences']].head()
```
![image](https://github.com/user-attachments/assets/d78d9f5f-6e9e-42fb-b5a6-8271d545560c)

```python
# Create subplots for 3 bar plots (Spotify, Apple Music, Deezer)
fig, axes = plt.subplots(ncols=3, figsize=(20, 6))

# Sort the DataFrame by 'in_spotify_playlists' and plot top 5 artists
sns.barplot(data=df_artist_playlists.sort_values('in_spotify_playlists', ascending=False).head(5), 
            x='artist_name', y='in_spotify_playlists', palette='Set2', ax=axes[0])
axes[0].set(title='Artist vs. Occurrence in Spotify Playlists',
            xlabel='Top Occurring Artists', ylabel='Number of Occurrences')

# Sort the DataFrame by 'in_apple_playlists' and plot top 5 artists
sns.barplot(data=df_artist_playlists.sort_values('in_apple_playlists', ascending=False).head(5),
            x='artist_name', y='in_apple_playlists', palette='Set2', ax=axes[1])
axes[1].set(title='Artist vs. Occurrence in Apple Music Playlists',
            xlabel='Top Occurring Artists', ylabel='Number of Occurrences')

# Sort the DataFrame by 'in_deezer_playlists' and plot top 5 artists
sns.barplot(data=df_artist_playlists.sort_values('in_deezer_playlists', ascending=False).head(5),
            x='artist_name', y='in_deezer_playlists', palette='Set2', ax=axes[2])
axes[2].set(title='Artist vs. Occurrence in Deezer Playlists',
            xlabel='Top Occurring Artists', ylabel='Number of Occurrences')

# Adjust the layout to prevent overlapping text
plt.tight_layout()

# Show the plots
plt.show()
```
![image](https://github.com/user-attachments/assets/50c620b4-7d12-4882-8e8b-c7df54e98a2a)

```python
df_total_playlists.head(10)
#get artsits with most plays
```
![image](https://github.com/user-attachments/assets/28218cd7-b62a-4556-a2eb-768499d65dc3)

```python
# Create a barplot for the top 10 artists based on total playlists
plt.figure(figsize=(12, 6))
sns.barplot(x='artist_name', y='total_playlists', data=df_total_playlists.head(10), palette='Set2')

# Add title and labels
plt.title("Top 10 Artists by Total Playlist Occurrences Across Platforms", fontsize=16)
plt.xlabel("Artist Name", fontsize=12)
plt.ylabel("Total Playlist Occurrences", fontsize=12)

# Rotate x-axis labels for better readability
plt.xticks(rotation=45)

# Adjust layout to prevent label overlap
plt.tight_layout()

# Show the plot
plt.show()
```
![image](https://github.com/user-attachments/assets/26aa48f6-c60e-4950-85da-36aec4912d11)
***

### Summary of statistics 
```python
### describe the given dataset
summary_statistics = df_spotify.describe()
summary_statistics
```
![image](https://github.com/user-attachments/assets/081788cb-a7b9-42ab-82c8-daccb6480a28)














































































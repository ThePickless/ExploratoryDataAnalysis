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























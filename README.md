# Olympic-Dashboard
This repository contains the Python scripts and Power BI files used to analyze and visualize the Paris 2024 Summer Olympics dataset. By combining the power of Python for data processing and Power BI for creating interactive dashboards, this project provides insights into various aspects of the upcoming Olympics, including athlete participation, medal trends, event schedules, and more.
## Project Overview

The Paris 2024 Olympic Dashboard is an interactive data analysis project that explores key insights from the Paris 2024 Summer Olympics dataset. Using Python for data preprocessing and Power BI for visualization, this project provides an in-depth view of athlete participation, medal counts, event schedules, and more.

By leveraging Python scripts to download and clean the dataset from Kaggle, and Power BI to visualize the data in an accessible and interactive way, this project aims to give users a comprehensive understanding of the games, helping them track performance trends, compare countries, and explore event schedules in an intuitive format.

This project serves as a valuable tool for both sports enthusiasts and data analysts who wish to gain insights into the 2024 Olympics and explore trends that can inform future Olympic events.
## Setup Instructions

### Step 1: Setting Up Kaggle API and Python Environment

Before you begin, you'll need to set up the **Kaggle API** and install the necessary Python libraries to download the Olympic dataset. Follow these steps:

#### 1.1 Kaggle Setup
1. **Sign up on Kaggle**: If you don't already have a Kaggle account, [sign up here](https://www.kaggle.com/).
2. **Create an API Token**:  
   - In your Kaggle account settings, go to the **"API"** section and click **"Create New API Token"**. This will download a `kaggle.json` file that contains your Kaggle API credentials.
3. **Save the API Token**:  
   - Place the `kaggle.json` file in a secure directory on your machine. This file will be used to authenticate the Kaggle API.

#### 1.2 Python Environment Setup
Make sure you have Python installed on your system. You will also need to install the following Python libraries:

```bash
pip install kaggle pandas

```
### Step 2: Python Script for Downloading the Dataset

The following Python script will automate the process of downloading the **Paris 2024 Olympic dataset** from Kaggle and loading it into Pandas DataFrames for analysis.

```python
import kaggle
import os
import pandas as pd

# Set Kaggle API credentials directory
os.environ['KAGGLE_CONFIG_DIR'] = 'C:/Users/your_user/.kaggle'  # Update this path to your Kaggle config directory

# Specify the dataset identifier
dataset = 'piterfm/paris-2024-olympic-summer-games'

# Set the download path
download_path = 'C:/Users/your_user/Downloads/Olympic/Source'  # Change this to your preferred download directory

# Remove existing files in the folder to prevent duplicates or outdated files
for file in os.listdir(download_path):
    file_path = os.path.join(download_path, file)
    try:
        if os.path.isfile(file_path):
            os.unlink(file_path)  # Delete the file
            print(f"Deleted {file_path}")
    except Exception as e:
        print(f"Error deleting {file_path}: {e}")

# Download the dataset using the Kaggle API and unzip the files
kaggle.api.dataset_download_files(dataset, path=download_path, unzip=True)

# List of CSV files to be imported
csv_files = [
    'athletes.csv',
    'events.csv',
    'medallists.csv',
    'medals.csv',
    'medals_total.csv',
    'schedules.csv',
    'schedules_preliminary.csv',
    'teams.csv',
    'torch_route.csv',
    'venues.csv'
]

# Initialize a dictionary to hold DataFrames
dataframes = {}

# Iterate through each CSV file and load it into a DataFrame
for file in csv_files:
    # Construct the full path to the CSV file
    file_path = os.path.join(download_path, file)
    
    # Load the CSV file into a Pandas DataFrame
    df = pd.read_csv(file_path)
    
    # Add the DataFrame to the dictionary using the file name as the key
    table_name = file.split('.')[0]  # Remove the .csv extension
    dataframes[table_name] = df
```
## Explanation of the Code

### Setting the Environment
We start by setting the `KAGGLE_CONFIG_DIR` to point to the directory containing the `kaggle.json` file. This enables the script to authenticate and access Kaggle’s API.

### Dataset Identifier
The dataset identifier `piterfm/paris-2024-olympic-summer-games` is used to specify which dataset to download.

### Clearing Existing Files
To prevent duplicates or outdated data, the script deletes any existing files in the download directory before proceeding with the new download.

### Downloading and Unzipping
The `kaggle.api.dataset_download_files` function downloads and unzips the dataset files to the specified path.

### Loading CSV Files into DataFrames
Finally, the script iterates through the list of CSV files, loading each into a Pandas DataFrame. These DataFrames are stored in a dictionary for easy access using the file name as the key.
## Step 3: Importing Data into Power BI

With the dataset downloaded and organized into DataFrames, we can now import this data into Power BI for visualization.

### Connecting Power BI to Python

1. **Open Power BI**: Start by opening Power BI Desktop.
2. **Get Data**: Click on “Get Data” in the Home tab and choose “Python script” as the data source.
3. **Load the Script**: Copy and paste the following Python script into the Power BI editor to load the DataFrames:

```python
# Import necessary libraries
import pandas as pd
import os

# Define the path to the downloaded CSV files
download_path = 'C:/Users/faisa/Downloads/Power BI_Imp Summary/Olympic/Source'

# Load the data into DataFrames
athletes = pd.read_csv(os.path.join(download_path, 'athletes.csv'))
events = pd.read_csv(os.path.join(download_path, 'events.csv'))
medallists = pd.read_csv(os.path.join(download_path, 'medallists.csv'))
medals = pd.read_csv(os.path.join(download_path, 'medals.csv'))
medals_total = pd.read_csv(os.path.join(download_path, 'medals_total.csv'))
schedules = pd.read_csv(os.path.join(download_path, 'schedules.csv'))
schedules_preliminary = pd.read_csv(os.path.join(download_path, 'schedules_preliminary.csv'))
teams = pd.read_csv(os.path.join(download_path, 'teams.csv'))
torch_route = pd.read_csv(os.path.join(download_path, 'torch_route.csv'))
venues = pd.read_csv(os.path.join(download_path, 'venues.csv'))
```
### Load the Data
Once the script is executed, Power BI will load the data from the CSV files into tables that can be used for building reports.

### Step 4: Creating Visualizations in Power BI
With the data loaded into Power BI, we can now create compelling visualizations to analyze the Olympic dataset. Here are a few examples:

#### Visual 1: Athlete Participation by Country
- **Type**: Bar Chart
- **Fields**: Use the `athletes` table to plot the number of athletes participating from each country. This provides a quick overview of which countries have the most representation in the Olympics.

#### Visual 2: Medal Count by Country
- **Type**: Pie Chart
- **Fields**: Utilize the `medals_total` table to display the total medal count for each country. This visualization helps identify the top-performing nations in terms of medals won.

#### Visual 3: Event Schedule
- **Type**: Table
- **Fields**: Use the `schedules` table to create a detailed schedule of events, including event names, dates, and venues. This allows viewers to plan their viewing schedule and follow specific events.

#### Visual 4: Torch Route Map
- **Type**: Map
- **Fields**: Employ the `torch_route` table to visualize the Olympic torch route on a map. This visualization adds geographical context to the relay and highlights the journey of the Olympic flame.

#### Visual 5: Medal Trends Over Time
- **Type**: Line Chart
- **Fields**: Use the `medals` table to display trends in medal wins over time, broken down by country or sport. This visualization offers insights into how countries’ performances have changed across different Olympics.

### Conclusion
By leveraging Python and Power BI, we’ve efficiently downloaded, organized, and visualized the Paris 2024 Olympic dataset. This project demonstrates the power of data analysis and visualization in understanding the dynamics of a global event like the Olympics.


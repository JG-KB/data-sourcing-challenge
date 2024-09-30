
# NASA CME and GST Data Analysis Project

This project retrieves and processes data from NASA's Coronal Mass Ejection (CME) and Geomagnetic Storm (GST) databases using their DONKI (Database Of Notifications, Knowledge, and Information) API. The project focuses on gathering CME and GST event data, cleaning and expanding the data, and merging the two datasets to analyze the time it takes for a CME to cause a GST.

## Table of Contents

- [Project Overview](#project-overview)
- [Installation](#installation)
- [Usage](#usage)
- [Functionality](#functionality)
  - [Part 1: Request CME Data](#part-1-request-cme-data)
  - [Part 2: Request GST Data](#part-2-request-gst-data)
  - [Part 3: Merging CME and GST Data](#part-3-merging-cme-and-gst-data)
  - [Additional Functionality](#additional-functionality)
- [Results](#results)
- [Files](#files)
- [Contributors](#contributors)

## Project Overview

This project uses the NASA DONKI API to extract and analyze data on CMEs and GSTs, which are significant space weather events. The primary goal is to calculate how long it takes for a CME to cause a corresponding GST and summarize this information statistically. The resulting data is then exported into a CSV file for further analysis.

### Key Features:

- Request data from NASA's DONKI API for both CME and GST events.
- Clean and process the data by expanding lists and handling missing values.
- Merge the two datasets based on common events.
- Calculate time differences between CME and GST events and analyze the results.

## Installation

1. Clone the repository to your local machine:
   ```bash
   git clone https://github.com/your-repo/nasa-cme-gst-analysis.git
   ```
   
2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Set up your NASA API key:
   - Create a `.env` file in the project directory.
   - Add the following line to the `.env` file, replacing `YOUR_NASA_API_KEY` with your actual API key:
     ```
     NASA_API_KEY=YOUR_NASA_API_KEY
     ```

4. Make sure you have the following libraries installed:
   - `requests`
   - `pandas`
   - `json`
   - `python-dotenv`

## Usage

Run the script to download CME and GST data from the NASA API, process the data, and generate the CSV output file:

```bash
python main.py
```

This script performs the following steps:
- Retrieves CME and GST data between specified dates.
- Processes the data to expand events, extract relevant details, and clean the datasets.
- Merges the two datasets based on event IDs.
- Calculates the time difference between CME and GST events.
- Exports the processed data to a CSV file for further analysis.

### Example:

```bash
$ python main.py
```

This will generate a CSV file named `merged_nasa_cme_gst_df.csv` in the current directory.

## Functionality

### Part 1: Request CME Data

- Constructs a query URL for the CME data using the NASA API and retrieves the results.
- Extracts relevant fields such as `activityID`, `startTime`, and `linkedEvents` from the data.
- Expands the `linkedEvents` list for each CME event into individual rows.
- Cleans the resulting DataFrame by converting columns to appropriate data types and filtering rows.

### Part 2: Request GST Data

- Constructs a query URL for the GST data using the NASA API and retrieves the results.
- Similar to CME data, extracts fields such as `gstID`, `startTime`, and `linkedEvents`.
- Explodes the `linkedEvents` list into individual rows and cleans the DataFrame.
- Filters the data to include only rows where the linked event is related to a CME.

### Part 3: Merging CME and GST Data

- Merges the CME and GST datasets on their event IDs.
- Creates a new column, `timeDiff`, which calculates the time difference between CME and GST events.
- Uses `describe()` to analyze the time differences between events.

### Additional Functionality

- The `extract_activityID_from_dict` function is used to extract event IDs from nested dictionaries.
- Exception handling is implemented to ensure the script runs smoothly even with missing or malformed data.

## Results

The analysis found the average time it takes for a CME to cause a GST:

- **Mean time difference**: Approximately 2 days and 21 hours.
- **Median time difference**: Approximately 2 days and 17 hours.
- **Minimum time difference**: 1 day and 8 hours.
- **Maximum time difference**: 6 days and 3 hours.

These results provide insights into the average delay between a CME event and its corresponding GST, which can help in space weather forecasting.

## Files

- `main.py`: The main script that runs the entire analysis.
- `nasa.env`: Stores the NASA API key (ensure this file is created with your API key).
- `requirements.txt`: Lists all the dependencies needed for the project.
- `merged_nasa_cme_gst_df.csv`: The output file containing the merged CME-GST data along with calculated time differences.



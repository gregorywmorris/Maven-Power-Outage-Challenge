# Maven-Power-Outage-Challenge
Maven Power Outage Challenge

├── LICENSE
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default Sphinx project; see sphinx-doc.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries.
│
├── notebooks          <- Jupyter notebooks.
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment,
│                         generated with `pip freeze > requirements.txt`
│
├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
├── src                <- Source code for use in this project.
│   ├── __init__.py    <- Makes src a Python module
│   │
│   ├── data           <- Scripts to download or generate data
│   │   └── make_dataset.py
│   │
│   ├── features       <- Scripts to turn raw data into features for modeling
│   │   └── build_features.py
│   │
│   ├── models         <- Scripts to train models and then use trained models to make
│   │   │                 predictions
│   │   ├── predict_model.py
│   │   └── train_model.py
│   │
│   └── visualization  <- Scripts to create exploratory and results-oriented visualizations

### Data Dictionary:
Field	Description
*  **Date & Time Event Began:**	The month day year and time (in 24-hour format) when the incident began.
*  **Date & Time of Restoration:** The month day year and time (in 24-hour format) when the event no longer met one of the 24 criteria for an emergency alert.
*  **Area Affected:** The name of the State(s) and political subdivision(s) (i.e. city town county etc.) affected by the incident. This represents the largest area affected by the incident and it's not a requirement to list all the cities and towns in a region or State.
*  **NERC Region:** The North American Electric Reliability Corporation (NERC) region responsible for the restoration
*  **Alert Criteria:**	Emergency criteria met that caused the form to be filled
*  **Event Type:** Cause of the incident
*  **Demand Loss (megawatts):** The amount of the peak demand involved over the entire incident. If the amount is unknown and you are unable to make an estimate then leave this blank.
*  **Number of Customers Affected:**	The total number of customers affected during the entire incident or disturbance which could be more than the peak number in the case of rolling blackouts. If this number cannot be estimated when the form is initially submitted check the unknown box.

**Additional Note:**

* The year range is from 2002 to 2023.

### Data Cleaning
Data Dictionary is used as a guide for expected values.

**Stage one:**
* Used the Data Dictionary as a guide for expected values.
* Formatted data tables:
    * Format to use 2022's column names as this format best fits the majority of the data.
    * For Alert criteria before 2015, list as 'unknown'.
    * Split combined date time columns for years before 2011.
    * Formatted the correct type for date, time, and integer columns.
* Dates transposed (showing as finishing before the start date), corrected the date and month then moved to the correct sheet when appropriate.
* Removed 'ongoing' from the date column.
* Remove gridlines and white background color.
* Sheet 2023: Removed Temp column.
* Sheet 2016: Only had data up to October 31st.
* Sheet 2011: the years 2077 (well into the future) and 2001 (before data collection) were corrected to 2011 to match the start date.
* Sheet 2004: Removed record with no start and end dates. Unable to confirm actuals.
* Sheet 2002 and 2003: Merge and center data cells by date across all columns where appropriate.

**Stage two:**
* Combined into a single sheet. Shape (3913,11).
* Format data to Calibri 10 middle center.
* Date Event Began: Ongoing /Unknown are all past dates that were not updated. These will be left blank to be able to properly format the data.
* Time Event Began: N/A and Ongoing made blank, words removed or transitioned to time ##:## AM/PM format.
* Date of Restoration: Ongoing made blank.
<br>
* Event Type: 
**Note:** Format so that similar items are grouped for analysis. Many nuanced details fail to provide additional insight and hinder analysis often due to the low present numbers. Grouping related instances will allow better general analysis.
    * Format as Text.
    * Converted all variants of physical attack or vandalism to Physical Attack/Vandalism.
    * Converted to Unkown: Unknown *, - Unknown, Distribution Interruption - Unknown Cause.
    * Convert to singular of for earthquake.
    * Removed descriptive text from a Thunderstorms data field.
    * All variants of winter, snow, ice or cold weather events converted to Winter/Snow/Ice.NOAA's National Severe Storms Laboratory [groups these as winter storms.](https://www.nssl.noaa.gov/education/svrwx101/winter/types/#:~:text=Winter%20Storms&text=While%20heavy%20snowfalls%20and%20severe,of%20ice%20on%20exposed%20surfaces.)
    * Converted all cyber attacks/events to Cyber Event.
    * Converted all variants of Brush Fire to Brush Fire.
    * Converted all variants of Breaker to Breaker Failure.
    *  All [CAISO (California Independent System Operator)](https://www.caiso.com/Documents/Rotating-Power-Outages-Fact-Sheet.pdf) variants converted to CAISO Initiated Interruption.
    * Converted all variants of Electrical System Separation/[Islanding](https://en.wikipedia.org/wiki/Islanding) to Electrical System Separation (Islanding).
    * All variants of Equipment Faulted/Failure/Malfunction converted to Equipment Malfunction.
    * Fuel Supply Deficiency
<br>
* Demand Loss(MW): 
    * The expected value is a number or left blank if unknown. All strings were removed.
    * Deleted: 'NA', 'unknown', '-', descriptive text.
    * For ranges, only accept the highest estimate.
    * Approx, greater/Less than converted to just the number given.
    * customers affected moved to the correct column, deleted peak and kept actual (and removed strings). 
    * Removed dates and times.
    * Error: Number stored as text, converted to a number.
    * Formated number with one decimal place to maintain the accuracy of estimates given.
<br>
* Number of Customers: 
    * The expected value is a number or left blank if unknown. 
    * Deleted descriptive text
    * Error: Number stored as text, converted to a number.
    * Deleted: 'NA' and 'unknown' strings, date, '-'.
    * Approx, greater/Less than converted to just the number given.
    * Converted utilities and industrial to just the number given.
    * Formatted to the whole number.


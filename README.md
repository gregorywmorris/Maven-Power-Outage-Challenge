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
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
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

Data Dictionary:
Field	Description
* Date & Time Event Began	The month day year and time (in 24-hour format) when the incident began.
* Date & Time of Restoration	The month day year and time (in 24-hour format) when the event no longer met one of the 24 criteria for an emergency alert.
* Area Affected	The name of the State(s) and political subdivision(s) (i.e. city town county etc.) affected by the incident. This represents the largest area affected by the incident and it's not a requirement to list all the cities and towns in a region or State.
* NERC Region North American Electric Reliability Corporation (NERC) region responsible for the restoration
* Alert Criteria	Emergency criteria met that caused the form to be filled
* Event Type	Cause of the incident
* Demand Loss (megawatts)	The amount of the peak demand involved over the entire incident. If amount is unknown and you are unable to make an estimate then leave this blank.
* Number of Customers Affected	The total number of customers affected during the entire incident or disturbance which could be more than the peak number in the case of rolling blackouts. If this number cannot be estimated when the form is initially submitted check the unknown box.

**Additional Note:**

* The year range is from 2002 to 2023.


Excell Data Cleaning:
* Used the Data Dictionary as a guide for expected values.
* Formatted data tables to match 2023's format. 
    * For Alert criteria before 2015, listed as 'unknown'.
    * Split combined date time columns for years before 2011.
    * Formatted the correct type for date, time, and integer columns.
* From multiple sheets: 
    * Dates transposed (showing as finishing before the start date), corrected the date and month then moved to the correct sheet when appropriate.
    * Removed 'ongoing' from the date column.
* Sheet 2011: the years 2077 (well into the future) and 2001 (before data collection) were corrected to 2011 to match the start date.
* Sheet 2004: Removed record with no start and end dates. Unable to confirm actuals.
* Sheet 2003: Merge and center data cells by date across all columns where appropriate.
* Combined into a single sheet. 
* Date columns: Ongoing /Unknown are all past dates that were not updated. These will be left blank to be able to properly format the data.
* Demand Loss(MW): Expected value is integer or left blank if unknown. Deleted: 'NA' and 'unknown' strings, '-'. Changed: 8-10k to 10k, customers affected moved to the correct column, deleted peak and kept actual (and removed strings). 
* Number of Customers: Expected value is integer or left blank if unknown. Deleted: 'NA' and 'unknown' strings, date, '-'. Changed: 37-40 to 40.


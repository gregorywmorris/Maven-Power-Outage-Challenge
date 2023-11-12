Maven Power Outage Challenge
==============================

Maven Analytics Challenge

Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
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
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io

Data Dictionary:
Field	Description
* Date & Time Event Began	The month day year and time (in 24-hour format) when the incident began.
* Date & Time of Restoration	The month day year and time (in 24-hour format) when the event no longer met one of the 24 criteria for an emergency alert.
* Area Affected	The name of the State(s) and political subdivision(s) (i.e. city town county etc.) affected by the incident. This represents the largest area affected by the incident and it's not a requirement to list all the cities and towns in a region or State.
* NERC Region	North American Electric Reliability Corporation (NERC) region responsible for the restoration
* Alert Criteria	Emergency criteria met that caused the form to be filled
* Event Type	Cause of the incident
* Demand Loss (megawatts)	The amount of the peak demand involved over the entire incident. If amount is unknown and you are unable to make an estimate then leave this blank.
* Number of Customers Affected	The total number of customers affected during the entire incident or disturbance which could be more than the peak number in the case of rolling blackouts. If this number cannot be estimated when the form is initially submitted check the unknown box.


Excell Data Cleaning:
* Formatted data tables to match 2023 format. 
    * For Alert criteria before 2015, listed as unknown.
    * Split combined date time columns for years before 2011.
    * Formatted date, time, and integer columns.
* Combined to single sheet. 
* Date columns: Ongoing /Unknown are all past dates that were not updated. These will be left blank inorder to be able to properly format the data.
* Demand Loss(MW): expected value is integer or left blank if unknown. Deleted: 'NA' and 'unknown' strings, '-'. Changed: 8-10k to 10k, customers affected moved to correct column, deleted peak and kept actual (and removed strings). 
* Number of Customers: Expected value is integer or left blank if unknown. Deleted: 'NA' and 'unknown' strings, date, '-'. Changed: 37-40 to 40.

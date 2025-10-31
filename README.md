## The dataset includes:
1.	City Data – There are multiple files for different cities and different cities, and each of these files contains:
•	From Date / To Date – The time range for data collection at each station.
•	PM2.5 (µg/m³) – The concentration of fine particulate matter.
•	Other parameters such as PM10, CO, CO₂, NO etc are also available but are not analyzed in this study.
2.	Stations_Info.csv – A reference file containing metadata for each monitoring station, including:
•	file_name: Associated data file for the station.
•	state and city: Geographical identifiers.
•	agency: Managing agency of the station.
•	station_location: Specific site of data collection.
•	start_month / start_month_num / start_year: Indicates when monitoring began at that station.
Usefulness for PM2.5 Analysis
This dataset is valuable for:
•	Trend Analysis – Identifying long-term changes in PM2.5 levels.
•	Spatial Analysis – Detecting pollution hotspots and comparing air quality between cities and states.
•	Correlation Studies – Assessing relationships between PM2.5 and meteorological variables (e.g., temperature, humidity, wind speed).
•	Forecasting Models – Developing predictive models to anticipate high pollution events and assist in proactive policymaking.

## Overview of the Approach
The system is built on a serverless architecture leveraging Amazon S3, AWS Glue, Amazon Athena, and Amazon QuickSight. The workflow comprises the following stages:
1.	Data Ingestion and Storage
o	Raw air quality CSV files for 453 Indian cities (2010–2023) are uploaded to Amazon S3.
o	Data is stored in its original format in a dedicated raw bucket for archival and reproducibility.
2.	Data Cataloging
o	AWS Glue Crawlers are configured to scan the S3 bucket and automatically detect schema details (column names, data types, formats).
o	The crawlers populate the AWS Glue Data Catalog, creating ready-to-use tables for querying in Athena.
3.	Data Processing and Querying
o	Amazon Athena is used to run SQL queries directly on the data stored in S3 without requiring any infrastructure setup.
o	Example queries include:
	Extracting PM2.5 annual averages for each city.
	Identifying top 10 polluted cities for each year.
	Filtering seasonal trends (winter vs. summer variations).
4.	Data Visualization
o	Amazon QuickSight is connected to Athena as a data source to create interactive dashboards.
o	Dashboards include:
	Line Charts showing yearly PM2.5 trends.
	Correlation Plots between PM2.5 and meteorological factors.
5.	Model Training
o	Training Model on SageMaker for prediction of PM 2.5 values. 

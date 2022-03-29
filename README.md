<h1>Data Talk Club</h1>
<h2>Data Engineering Zoom Camp</h2>
<p>
<h2>System Architecture Diagram<h2><br>
<img src="https://github.com/ptking777/dtc-de-project/blob/main/images/architecture.png" alt="Architecture Diagram">
<p>  
<br>
<h2>Final Project: NOAA Integrated Surface Database (ISD)</h2>
<h3>February, 2022</h3>
<br>
<h1>Abastract</h1>
The project will download and analyze data from the US National Oceanic and Atmospheric Administration (NOAA Integrated Surface Database (ISD)
made available on the Amazon Open Data Registry.
Data source: https://registry.opendata.aws/noaa-isd/
Data format: https://www.ncei.noaa.gov/data/global-hourly/doc/isd-format-document.pdf
<p>
The database includes over 35,000 stations worldwide, with some having data as far back as 1901. Currently, there are over 14,000 "active" stations updated
daily in the database. The total uncompressed data volume is around 600 gigabytes; however, it continues to grow as more data are added. ISD includes numerous parameters such as wind speed and direction, wind gust, temperature, dew point, cloud data, sea level pressure, altimeter setting, station pressure, present weather, visibility, precipitation amounts for various time periods, snow depth, and various other elements as observed by each station.
<p>
The data input will include a selection of weather stations (TBD) and span the years (2000, 2010 and 2020).
The data is publised in a fixed with format and spans several decades.
The project data will be downloaded and reformatted to CSV using Apache Nifi (https://nifi.apache.org/docs.html) running on a GCP VM instance.
The data will then be uploaded to Google Storage Cloud (https://cloud.google.com/storage/docs/) and analyzed using Google BigQuery (https://cloud.google.com/bigquery/docs/) and Google Data Studio (https://developers.google.com/datastudio/visualization/get-started).
<p>
<hr></hr>
<h1>Output Report Summary</h1>  
  <a href="https://github.com/ptking777/dtc-de-project/blob/main/REPORTS.md">View Report Summary</a>  
 <p> 
<hr></hr>  
<h1>Infrastructure Setup</h1>
<a href="https://github.com/ptking777/dtc-de-project/blob/main/gcp_env_setup.md">Setup GCP Infrastructure.</a>
<p>
<h1>Software Installation</h1>
<h2>Install Python and Docker on GCP VM instance</h2>
<a href="https://github.com/ptking777/dtc-de-project/blob/main/gcp_env_setup.md">Software Installations.</a>  
<p>
 <hr></hr> 
<h1>Project Setup</h1>  
 <h1>NiFi ETL Application</h1>
 <a href="https://github.com/ptking777/dtc_de_nifi_project/blob/main/README.md">Setup NiFi Project</a>
 <p>
 
 <h1>Databse Tool (DBT) Application</h1><br>
 <a href="https://github.com/ptking777/dbt_noaa_zoom/blob/main/README.md">Run DBT application from Docker</a>
 <p>
 
 
 

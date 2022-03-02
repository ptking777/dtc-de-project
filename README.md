Data Talk Club
Date Engineering Zoom Camp


Final Project:
NOAA Integrated Surface Database (ISD)
February, 2022


Abastract

The project will download and analyze data from NOAA Integrated Surface Database (ISD) made available on the Amazon Open Data Registry.
Data source: https://registry.opendata.aws/noaa-isd/
Data format: https://www.ncei.noaa.gov/data/global-hourly/doc/isd-format-document.pdf
The data input will include a selection of weather stations (TBD) and span the years (TBD: 2000 to 2020).
The data is publised in a fixed with format and spans several decades.
The project data will be downloaded and reformatted to CSV using Apache Nifi (https://nifi.apache.org/docs.html) running on a GCP VM instance.
The data will then be uploaded to Google Storage Cloud (https://cloud.google.com/storage/docs/) and analyzed using Google BigQuery (https://cloud.google.com/bigquery/docs/) and Google Data Studio (https://developers.google.com/datastudio/visualization/get-started).

# Splunk using Docker

Starter guide on how to use Splunk to analyze and create reports from server logs.

## Setup with Docker

1. Install Docker on your machine from https://www.docker.com/get-started 
2. Pull splunk container: ```docker pull splunk/splunk```

## Run Docker Container

1. Docker Command: ```docker run -e SPLUNK_START_ARGS=--accept-license -e SPLUNK_PASSWORD=password -p 8000:8000 splunk/splunk```
2. Ensure docker container is running: ```docker ps```
3. Login to the splunk portal with username 'admin' and the password you provided. The Splunk portal will be found at http://ip_of_your_system:8000

![Image of Dashboard] (https://github.com/Taha-Ansari/Splunk/imgs/0-dashboard.png)

## Upload Data

1. Go to the Home app by clicking the Splunk logo in the upper left hand of the interface. 
2. Click the Add Data icon. Then click the upload button.
3. You will be taken to the Select Source step. Click the Select Filebutton and choose the access_log.logfile supplied from the logs folder in this repo. 
4. Splunk should automatically set the source type correctly as 'access_combined_wcookie' for this file. Press next.
5. Enter web_application as the Host field value. Press next.
6. Press Review and then finish. Press add more data to add the rest of the logs, repeating this process.
7. Table below shows the values I used for each log when uploading the data: 

Filename | Source Type | Host Field Value
------------ | ------------- | -------------
access_log.log | access_combined_wcookie | web_application
linux_secure.log | linux_secure | web_server
db_audit.csv | csv | database

## Queries and Reports

Here is a sample of queries used on this dataset to generate reports of failed ssh logins on port 22 on the web server

### Grabbing failed password attempts from all logs
![Image search 1] (https://github.com/Taha-Ansari/Splunk/imgs/1-simple_search.png)

### Sorting failed password attempts on the webserver by number of login failures 
![Image search 2] (https://github.com/Taha-Ansari/Splunk/imgs/2-advanced_search.png)


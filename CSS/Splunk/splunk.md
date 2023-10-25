# Upload Access Log Data to Splunk: 

Open the browser 

Type the URL: http://127.0.0.1:8000/ 

Click (Add Data) 
A screenshot of a computer

Description automatically generated 

Click (Upload) 
A screen shot of a computer

Description automatically generated 

Click (Select File) 
A screenshot of a computer

Description automatically generated 

Navigate to Desktop then open (Practice-Data) then (www1) folder 

Select (access) file then hit Open 
 

Click (Next) at the top right 

On the left side Open the (Source Type) menu and select (Web è access_combined) 
A screenshot of a computer

Description automatically generated 

Click (Next) at the top right 

Type in the (Host field value) WebServer1 
A screenshot of a computer

Description automatically generated 

Click on (Create a new index) and type the (Index Name) access-log then hit (Save) 
A screenshot of a computer

Description automatically generated 

Click on (Review) at the top right then click (Submit) 

Click on (Add More Data) 
A screenshot of a computer

Description automatically generated 

Repeat the steps from 4 to 11 but select (www2) folder and type in the (Host field value) WebServer2 
A screenshot of a computer

Description automatically generated 
A screenshot of a computer

Description automatically generated 

After step 11 Select (access-log) from the index drop menu - DON’T click on (Create a new index) 
A screenshot of a computer

Description automatically generated 

Click on (Review) at the top right then click (Submit) 

Click on (Add More Data) 

Repeat the steps from 4 to 11 but select (www3) folder and type in the (Host field value) WebServer3 

After step 11 Select (access-log) from the index drop menu - DON’T click on (Create a new index) 

Click on (Review) at the top right then click (Submit) 
 

# Verify your work: 

Navigate to the Splunk Home Page: http://127.0.0.1:8000/ 

Click on Search & Reporting 
A screenshot of a computer

Description automatically generated 

On the right side of the search bar select (All time) 
A screenshot of a computer

Description automatically generated 

Type in the search the following: 
index="access-log" 
A screenshot of a computer

Description automatically generated 

Then hit the search icon on the right side 

You should get a result with 39,532 events 
A screenshot of a search engine

Description automatically generated 
 

 

Upload Security Log Data to Splunk: 

Open the browser 

Type the URL: http://127.0.0.1:8000/ 

Click (Add Data) 
A screenshot of a computer

Description automatically generated 

Click (Upload) 
A screen shot of a computer

Description automatically generated 

Click (Select File) 

Navigate to Desktop then open (Practice-Data) then (www1) folder 

Select (secure) file then hit Open 
A screenshot of a computer

Description automatically generated 

Click (Next) at the top right 

On the left side Open the (Source Type) menu and select (Operating System è linux_secure) 
A screenshot of a computer

Description automatically generated 

Click (Next) at the top right 

Type in the (Host field value) WebServer1 
A screenshot of a computer

Description automatically generated 

Click on (Create a new index) and type the (Index Name) security-log then hit (Save) 
A screenshot of a computer

Description automatically generated 

Click on (Review) at the top right then click (Submit) 

Click on (Add More Data) 
A screenshot of a computer

Description automatically generated 

Repeat the steps from 4 to 11 but select (www2) folder and type in the (Host field value) WebServer2 
A screenshot of a computer

Description automatically generated 
A screenshot of a computer

Description automatically generated 

After step 11 Select (security-log) from the index drop menu - DON’T click on (Create a new index) 
A screenshot of a computer

Description automatically generated 

Click on (Review) at the top right then click (Submit) 

Click on (Add More Data) 

Repeat the steps from 4 to 11 but select (www3) folder and type in the (Host field value) WebServer3 

After step 11 Select (security-log) from the index drop menu - DON’T click on (Create a new index) 

Click on (Review) at the top right then click (Submit) 

 

# Verify your work: 

Navigate to the Splunk Home Page: http://127.0.0.1:8000/ 

Click on Search & Reporting 
A screenshot of a computer

Description automatically generated 

On the right side of the search bar select (All time) 
A screenshot of a computer

Description automatically generated 

Type in the search the following: 
index="security-log" 
A screen shot of a computer

Description automatically generated 

Then hit the search icon on the right side 

You should get a result with 30,259 events 
A screenshot of a search

Description automatically generated 
 

 

# Exercises: 

Question: 
You have an (access) log, and you want to provide a report for the top (10) purchases in April for the TEE category. The report should contain the Shopper IP and how many times this shopper made a purchase. 
 
Answer: 
index=access action=purchase date_month=april categoryId=TEE 
| top limit=10 clientip 
| rename clientip as "Shopper IP", count as "Times" 
| fields - percent 
 
 

Question: 
You have a (security) log, and you want to provide a report of all IPs that tried to log in to the server with failed attempts and the reason is the wrong password. 
 
Answer: 
index="security" 
| table src, action, reason 
| where isnotnull(reason) 
| rename src as "Source IP", action as "Result", reason as "Reason" 
| where Reason = "Failed password" AND Result = "failure" 
 
 

Question: 
You have a (security) log, and your manager asked you to provide him with two reports. The first one shows a visual chart of the top 10 IPs that attempted to log in as Username “root”. The second report shows the total attempts of these IPs. 
 
Answer: 
Report1: 
index="security" user_name="root" 
| top limit=10 src 
| rename count as "Count of Events", src as "IP Address“ 

Report2: 
index="security" user_name="root" 
| top limit=10 src 
| stats sum(count) as "Total Attempts" 
 
 

Question: 
You have a (security) log, and your manager asked you to provide two reports. The first one shows the count of attempts (success or failure) for each IP address with the Login name that used on each attempt The second one shows the total of attempts of each IP address counted by the Login name. 
 
Answer: 
Report1: 
index=security 
| stats count by src, user, action 
| rename src as "Source IP", user as "Login Name", action as "Result", count as "Attempts" 

Report2: 
index=security 
| stats values(user), count(user) by src 
| fillnull value="NO DATA" 
| rename src as "Source IP", values(user) as "Login Name", count(user) as "Attempts" 

AndrewStone-Week-18-Homework-Lets-go-Splunking!

### Scenario

You have just been hired as an SOC Analyst by Vandalay Industries, an importing and exporting company.
 
- Vandalay Industries uses Splunk for their security monitoring and have been experiencing a variety of security issues against their online systems over the past few months. 
 
- You are tasked with developing searches, custom reports and alerts to monitor Vandalay's security environment in order to protect them from future attacks.


### System Requirements 

You will be using the Splunk app located in the Ubuntu VM.


### Your Objective 

Utilize your Splunk skills to design a powerful monitoring solution to protect Vandaly from security attacks.

After you complete the assignment you are asked to provide the following:

- Screen shots where indicated.
- Custom report results where indicated.

### Topics Covered in This Assignment

- Researching and adding new apps
- Installing new apps
- Uploading files
- Splunk searching
- Using fields
- Custom reports
- Custom alerts

Let's get started!

---

## Vandalay Industries Monitoring Activity Instructions


### Step 1: The Need for Speed 

**Background**: As the worldwide leader of importing and exporting, Vandalay Industries has been the target of many adversaries attempting to disrupt their online business. Recently, Vandaly has been experiencing DDOS attacks against their web servers.

Not only were web servers taken offline by a DDOS attack, but upload and download speed were also significantly impacted after the outage. Your networking team provided results of a network speed run around the time of the latest DDOS attack.

**Task:** Create a report to determine the impact that the DDOS attack had on download and upload speed. Additionally, create an additional field to calculate the ratio of the upload speed to the download speed.


1.  Upload the following file of the system speeds around the time of the attack.
    - [Speed Test File](resources/server_speedtest.csv)

    -- source="server_speedtest.csv" host="server_speedtest" sourcetype="Server  Speed Test"

2. Using the `eval` command, create a field called `ratio` that shows the ratio between the upload and download speeds.
   - Hint: The format for creating a ratio is: `| eval new_field_name = 'fieldA'  / 'fieldB'`

   -- source="server_speedtest.csv" host="server_speedtest" | eval ratio ='DOWNLOAD_MEGABITS' / 'UPLOAD_MEGABITS'

   ![evalration](https://github.com/iastoneCO/Images/blob/687dbf73573107c9a7d0cfb5e6cc74f01e22c95c/eval_ration_DL_UP_megabits.jpg)
      
3. Create a report using the Splunk's `table` command to display the following fields in a statistics report:
    - `_time`
    - `IP_ADDRESS`
    - `DOWNLOAD_MEGABITS`
    - `UPLOAD_MEGABITS`
    - `ratio`
  
  -- source="server_speedtest.csv"| eval ratio ='DOWNLOAD_MEGABITS' / 'UPLOAD_MEGABITS' | table _time IP_ADDRESS DOWNLOAD_MEGABITS PLOAD_MEGABITS Ratio


   Hint: Use the following format when for the `table` command: `| table fieldA  fieldB fieldC`

4. Answer the following questions:

    - Based on the report created, what is the approximate date and time of the attack?
        - Based on the bottom report, the attack began at Feb 23, 2020 14:30 (2:30PM)
    - How long did it take your systems to recover?
        - Systems recovered and were operation normal at 23:30 (11:30PM). It’s taking about 8 hours and 30 minutes. 

    ![reports](https://github.com/iastoneCO/Images/blob/687dbf73573107c9a7d0cfb5e6cc74f01e22c95c/server_spreadsheet_table_report.jpg)

Submit a screen shot of your report and the answer to the questions above.
 
### Step 2: Are We Vulnerable? 

**Background:**  Due to the frequency of attacks, your manager needs to be sure that sensitive customer data on their servers is not vulnerable. Since Vandalay uses Nessus vulnerability scanners, you have pulled the last 24 hours of scans to see if there are any critical vulnerabilities.

  - For more information on Nessus, read the following link: https://www.tenable.com/products/nessus

**Task:** Create a report determining how many critical vulnerabilities exist on the customer data server. Then, build an alert to notify your team if a critical vulnerability reappears on this server.

1. Upload the following file from the Nessus vulnerability scan.
   - [Nessus Scan Results](resources/nessus_logs.csv)

-- source="nessus_logs.csv" host="nessus_logs" sourcetype="nessus_logs"

                             - Counts 1,849

2. Create a report that shows the `count` of critical vulnerabilities from the customer database server.
   - The database server IP is `10.11.36.23`. 
   
                            - (dest_ip="10.11.36.23)

   - The field that identifies the level of vulnerabilities is `severity`.

                           - severity="critical"
      
3. Build an alert that monitors every day to see if this server has any critical vulnerabilities. If a vulnerability exists, have an alert emailed to `soc@vandalay.com`.

Screenshot: 
![severity](https://github.com/iastoneCO/Images/blob/687dbf73573107c9a7d0cfb5e6cc74f01e22c95c/critical_vulnerabilites.jpg)

-- source="nessus_logs.csv" host="nessus_logs" sourcetype="nessus_logs" dest_ip="10.11.36.23" severity="critical" | stats count

Submit a screenshot of your report and a screenshot of proof that the alert has been created.

                           - Resulted counts: 49
                           
![step2-ipaddress-49](https://github.com/iastoneCO/Images/blob/687dbf73573107c9a7d0cfb5e6cc74f01e22c95c/step2-ipaddress-vulnerabilites-49.jpg)

If a vulnerability exists, have an alert emailed to `soc@vandalay.com`.

Screenshot Alert Email:
![AlertEmail](https://github.com/iastoneCO/Images/blob/687dbf73573107c9a7d0cfb5e6cc74f01e22c95c/Step2-Alert-setup-email.jpg)



### Step 3: Drawing the (base)line

**Background:**  A Vandaly server is also experiencing brute force attacks into their administrator account. Management would like you to set up monitoring to notify the SOC team if a brute force attack occurs again.


**Task:** Analyze administrator logs that document a brute force attack. Then, create a baseline of the ordinary amount of administrator bad logins and determine a threshold to indicate if a brute force attack is occurring.

1. Upload the administrator login logs.
   - [Admin Logins](resources/Administrator_logs.csv)

                            - Counts: 3,742

2. When did the brute force attack occur?
   - Hints:
     - Look for the `name` field to find failed logins.
     - Note the attack lasted several hours.

      
3. Determine a baseline of normal activity and a threshold that would alert if a brute force attack is occurring.

-- source="Administrator_logs.csv" host="Administrator_logs" sourcetype="Administrator_logs" name="An account failed to log on"

4. Design an alert to check the threshold every hour and email the SOC team at SOC@vandalay.com if triggered. 

Submit the answers to the questions about the brute force timing, baseline and threshold. Additionally, provide a screenshot as proof that the alert has been created.
 
 
### Your Submission
  
In a word document, provide the following:
  - Answers to all questions where indicated. 
  - Screenshots where indicated.

-- I found the attack happened between 9 AM and 1 PM on February 21, 2020; during each of the four hours of the attack hit, the number of failed logins increased to an average of 124, 101, 121, 95, and 123. Therefore, I would make my opinion a baseline of standard failed login activity be less than 49 fail per hour, report with a threshold of the attack 50 pull hour triggered an alert. 

![AlertEmailtoBruteForce](https://github.com/iastoneCO/Images/blob/687dbf73573107c9a7d0cfb5e6cc74f01e22c95c/brute-froce-attack-timing.jpg)


----------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------------------------------------

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.

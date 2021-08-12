##AndrewStone-Week19-Homework-Protecting-VSI-from-Future-Attacks

### Scenario

In the previous class,  you set up your SOC and monitored attacks from JobeCorp. Now, you will need to design mitigation strategies to protect VSI from future attacks. 

You are tasked with using your findings from the Master of SOC activity to answer questions about mitigation strategies.

### System Requirements 

You will be using the Splunk app located in the Ubuntu VM.

### Logs

Use the same log files you used during the Master of SOC activity:

- [Windows Logs](resources/windows_server_logs.csv)
- [Windows Attack Logs](resources/windows_server_attack_logs.csv)
- [Apache Webserver Logs](resources/apache_logs.txt	)
- [Apache Webserver Attack Logs](resources/apache_attack_logs.txt	)

---

### Part 1: Windows Server Attack

Note: This is a public-facing windows server that VSI employees access.
 
#### Question 1
- Several users were impacted during the attack on March 25th.
- Based on the attack signatures, what mitigations would you recommend to protect each user account? Provide global mitigations that the whole company can use and individual mitigations that are specific to each user.

-- I would recommend mitigated protecting each user's accounts to put on a whitelist. Whitelisting an IP address compromises the security of the user and the reliability of the server for everyone else who uses it.

  
#### Question 2
- VSI has insider information that JobeCorp attempted to target users by sending "Bad Logins" to lock out every user.
- What sort of mitigation could you use to protect against this?

-- I found msad_action in the Splunk screen and run top limit=10 msad_action. The Locked out counted 309 and reset an account's password counted 295. I can see 14 user accounts and probably hacker(s) or user(s) tried to access and have third failed to be locked. I will write a baseline and send an email alert report to investigate locked mitigation, including monitoring access control of the users. If the users still repeat a few locked, we could create a new group and reduce typing the wrong user's login with a password. If that'll able to improve the solve problem.

![lockout](https://github.com/iastoneCO/Images/blob/1ab7b8cb242eb66b14379d806cdafea799bbf182/lockout-screehshot.jpg)

![lockout2](https://github.com/iastoneCO/Images/blob/1ab7b8cb242eb66b14379d806cdafea799bbf182/lockout-screehshot-2.jpg)


### Part 2: Apache Webserver Attack:

#### Question 1
- Based on the geographic map, recommend a firewall rule that the networking team should implement.
- Provide a "plain english" description of the rule.
  - For example: "Block all incoming HTTP traffic where the source IP comes from the city of Los Angeles."
- Provide a screen shot of the geographic map that justifies why you created this rule. 

- 

![TargetLA1](https://github.com/iastoneCO/Images/blob/1ab7b8cb242eb66b14379d806cdafea799bbf182/Target-at-LosAngeles-bars.jpg)

![TargetLA2](https://github.com/iastoneCO/Images/blob/1ab7b8cb242eb66b14379d806cdafea799bbf182/ZoomPlus-LA-1.jpg)

![TargetLA3](https://github.com/iastoneCO/Images/blob/1ab7b8cb242eb66b14379d806cdafea799bbf182/ZoomPlus-LA-2.jpg)
  
#### Question 2

- VSI has insider information that JobeCorp will launch the same webserver attack but use a different IP each time in order to avoid being stopped by the rule you just created.

- What other rules can you create to protect VSI from attacks against your webserver?
  - Conceive of two more rules in "plain english". 
  - Hint: Look for other fields that indicate the attacker.

  - I can create to protect VSI from Attacks against my webserver. That's way to add Whitelist all IP Addresses in our Network. 

  - I suggest to add the baseline an alert and investigate mitigation to attack against my webserver to check location, and blacklist IP Addresses coming where's from location.
  

### Guidelines for your Submission:
  
In a word document, provide the following:
- Answers for all questions.
- Screenshots where indicated

Submit your findings in BootCampSpot!

---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.

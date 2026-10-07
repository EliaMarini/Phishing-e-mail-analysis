<h1>Phishing e-mail analysis</h1>


<h2>Description</h2>
Phising e-mail analysis using "Let's Defend" platform
<br />


<h2>Scenario</h2>
<img width="1085" height="515" alt="scenario" src="https://github.com/user-attachments/assets/0341f306-2138-473d-86d1-f012b058f5ca" />
<br />

<h2>Objectives</h2>
<br />
<ul>
  <li>What is the sending email address?</li>
  <li>What is the email address of the recipient?</li>
  <li>What is the subject line of the email?</li>
  <li>What date was the Email sent?</li>
  <li>What is the originating IP?</li>
  <li>What country is the IP address from?</li>
  <li>What is the name of the attachment when you unzip it?</li>
  <li>What is the SHA-256 hash of the File?</li>
  <li>Is the email attachment malicious? </li>
</ul>


<h2>Walk-through:</h2>

<p align="center">
<img width="1025" height="782" alt="E-mail" src="https://github.com/user-attachments/assets/d120ecd5-ecbb-4d2a-b1d6-a11fe925df99" />
</p>
<br />

<p align="left">
  Already from the content of the e-mail we can observe suspicious activity: the sender states that he is using a different e-mail box from the main one and also he states that the
bank details are different from the old one... maybe he never had them in the first place.
</p>
<br />

<p align="center">
  <img width="1067" height="764" alt="E-mail header 1" src="https://github.com/user-attachments/assets/42a16ef0-76aa-485c-a818-7a527ed6e47b" />
</p>
<br />

<p align="left">
By analyzing the e-mail header i obtained the following data:
  <ul>
    <li>the e-mail was received from "united.com.sg (unknown [71.19.248.52])"</li>
    <li>the e-mail was delivered to "admin@malware-traffic-analysis.net"</li>
    <li>Time: 08 Feb 2021 23:15:11 -0800</li>
  </ul>
  <br />
I checked the IP with Virus Total
 <br />
  <br />
  <img width="1880" height="275" alt="IP sender check virus total" src="https://github.com/user-attachments/assets/e8902a15-8fb7-40aa-9ed6-b30c8f667620" />
 <br />
  <br />
The only information i got is the location: Canada
 <br />
I also checked the domain 
 <br />
 <br />
  <img width="1884" height="283" alt="Domain check virus total" src="https://github.com/user-attachments/assets/aa2700d2-67c9-41ab-a0ad-0429bde95243" />
 <br />
  <br />
The domain was registered 26 years ago in Singapore. Usually attackers use fresh domains created days or weeks before the attack so still nothing suspicious,
</p>
<br />
<br />

<p align="left">
  In the e-mail there is attached a .zip file named "united_scientifc_equipent.zip", inside there is an executable file
  <br />
  <br />
  <img width="841" height="616" alt="Attachment" src="https://github.com/user-attachments/assets/d5d98017-1579-404b-ba70-dadea4e7319c" />
  <br />
  <br />
  Using Powershell i got the hash in sha256
  <br />
  <br />
  <img width="921" height="700" alt="File_hash" src="https://github.com/user-attachments/assets/1eed046c-fd27-490f-8499-18f3cc2e5c3c" />
  <br />
  <br />
  I checked the file hash using Virus Total
  <br />
  <br />
  <img width="1884" height="274" alt="File_hash_check" src="https://github.com/user-attachments/assets/eb6add2d-bc2b-4f94-b897-fb041f42364d" />
  <br />
  <br />
</p>

<h1>Conclusions</h1>
<p align="left">
  The file is a malware. Virus total intel says that it is associated mainly to create windows scheduled tasks and possibly gain persistance in the affected systems. 
  The next step would be to analyze the malware behavior in a sandbox enviroment and look at network traffic and system events. Then i would search the sender ip (71.19.248.52)
  inside the SIEM and see if other hosts in the organization received network traffic from it and if the malware is present on them. 
</p>
<br />

<h1>Remediation</h1>
<p align="left">
  Once we stated that the attachment is a malware and we have identified all affected hosts, i would isolate them from the network, 
  block the sender ip with a firewall rule, invalidate active user sessions and change credentials (depending on organizations rules i might reimage the OS)
</p>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>

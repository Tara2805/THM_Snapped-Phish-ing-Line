# 
## THM_Snapped-Phish-ing-Line

### Description
As an IT department personnel of SwiftSpend Financial, one of your responsibilities is to support your fellow employees with their technical concerns. While everything seemed ordinary and mundane, this gradually changed when several employees from various departments started reporting an unusual email they had received. Unfortunately, some had already submitted their credentials and could no longer log in.

You now proceeded to investigate what is going on by:

Analysing the email samples provided by your colleagues.
Analysing the phishing URL(s) by browsing it using Firefox.
Retrieving the phishing kit used by the adversary.
Using CTI-related tooling to gather more information about the adversary.
Analysing the phishing kit to gather more information about the adversary.

## Q1
Who is the individual who received an email attachment containing a PDF?
### Answer
Open the directory named phish-emails. There is a total of 5 emails seen.
Investigate the contents of the files to get the flag

![alt text](/Images/q1.png)

### Flag
William McClean

## Q2
What email address was used by the adversary to send the phishing emails?
### Answer
Search the contents of the emails we found.
### Flag
Accounts.Payable@groupmarketingonline.icu

## Q3
What is the redirection URL to the phishing page for the individual Zoe Duncan? (defanged format)
### Answer
Find the email sent to Zoe by reading the emails again. Open the .html file attached in a text editor. 

![alt text](/Images/q3.png)

Then Use <a href="https://cyberchef.io/#recipe=Defang_URL(true,true,true,'Valid%20domains%20and%20full%20URLs')">Cyber Chef</a> to defang the URL and get the flag

### Flag
hxxp[://]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/?email=zoe[.]duncan@swiftspend[.]finance&error

## Q4 
What is the URL to the .zip archive of the phishing kit? (defanged format)
### Answer
Lets visit http://kennaroads.buzz/data/

![alt text](/Images/q4a.png)

We see a .zip file. Right-click the file and copy the URL. Defang it using CyberChef and submit the flag.
### Flag
hxxp[://]kennaroads[.]buzz/data/Update365[.]zip

## Q5
What is the SHA256 hash of the phishing kit archive?
### Answer
Download the zip archive on the THM VM and open the terminal and cd into the Downloads folder. Then get the hash using the following command:
    sha256sum file.zip

![alt text](/Images/Q5.png)

### Flag
ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686

# Q6
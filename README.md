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

## Q6
When was the phishing kit archive first submitted? (format: YYYY-MM-DD HH:MM:SS UTC)
### Answer
We need to use virusTotal for this one. Head on over to <a href="https://www.virustotal.com/gui/home/upload"> it </a>.

Paste in the hash value we found earlier into the search bar

![alt text](/Images/q6.png)

Select the details pane and read through the content to find the date/time stamp of the first submission
### Flag

2020-04-08 21:55:50 UTC

## Q7
When was the SSL certificate the phishing domain used to host the phishing kit archive first logged? (format: YYYY-MM-DD)
### Answer
Search the url of *kennaroads.buzz* on VirusTotal and find the date listed
### Flag 
2020-** **

## Q8
What was the email address of the user who submitted their password twice?
### Answer
If we go to the /Update 365 directory of the *kennaroads.buzz* url we are greeted by a log.txt file available for viewing. Click and open it. It is a file containing the logs of all those who have fallen for the phishing scam. It has stored all their actions/entries. Go through the list and see the log which has the same user. 

![alt text](/Images/q8.png)

### Flag
Found in the log.txt file

## Q9
What was the email address used by the adversary to collect compromised credentials?
### Answer
Download and unzip the Update.365.zip file. Then we need to use grep. 
    grep -E -r -o '[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}' /home/damianhall/Downloads/Update365

This will search for all emails in the unzipped folders files

So we got lots of instances but only 3 unqiue emails.

![alt text](/Images/q9.png)

The script that seems to collect the compromised data is /submit.php so the answer is the email which has access to this.

### Flag
Seen in image

## Q10
The adversary used other email addresses in the obtained phishing kit. What is the email address that ends in "@gmail.com"?
### Answer
We already have this from the previous grep search
### Flag
****@gmail.com

# Q11
What is the hidden flag?
### Answer
Go back to the /update365 url directory. If we try and open /open365 here we get a *Not Found*. 

Enumerating the sub-directories provides a flag.txt file which contains the flag encoded in base64. Lets use CyberChef to decode it!

![alt text](/Images/q11.png)

By using "from base64" on cyberchef we get a flag, but its reveresed! so add "reverse" to the cyberchef recipe to get the flag. 
### Flag
THM{****_****_***_***}
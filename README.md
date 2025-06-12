# New-Hire-Old-Artifacts-Splunk-
![image](https://github.com/user-attachments/assets/53117623-3d6e-4e37-b6e0-988a8075bba8)


Scenario: You are a SOC Analyst for an MSSP (managed Security Service Provider) company called TryNotHackMe.


A newly acquired customer (Widget LLC) was recently onboarded with the managed Splunk service. The sensor is live, and all the endpoint events are now visible on TryNotHackMe's end. Widget LLC has some concerns with the endpoints in the Finance Dept, especially an endpoint for a recently hired Financial Analyst. The concern is that there was a period (December 2021) when the endpoint security product was turned off, but an official investigation was never conducted. 

Your manager has tasked you to sift through the events of Widget LLC's Splunk instance to see if there is anything that the customer needs to be alerted on. 

Happy Hunting!


### A Web Browser Password Viewer executed on the infected machine. What is the name of the binary? Enter the full path.


I just search for Password viewer
## 🔍 Detected: Web Browser Password Viewer

### 🛠️ Splunk Search
```spl
Password Viewer
```
![image](https://github.com/user-attachments/assets/875d7818-cd29-40a9-a914-1db3cac772f8)


### What is listed as the company name?

We can see the name in the results

![image](https://github.com/user-attachments/assets/125e1649-7508-40cb-a912-4133d9b66711)

### Another suspicious binary running from the same folder was executed on the workstation. What was the name of the binary? What is listed as its original filename? (format: file.xyz,file.xyz)

We know `Sysmon Event ID=1` logs process creation.
To find the executed password viewer, we filtered for:

```
EventCode=1
```
then click on currentdirectory
![image](https://github.com/user-attachments/assets/c5f02988-797e-414c-9b6e-ed614a4f2f94)

then click on image to see suspicious file 
![image](https://github.com/user-attachments/assets/c6d6bb09-2248-4c06-beaf-bc267085366d)

since we know the suspicious file name is IonicLarge.exe we just search it in the query
![image](https://github.com/user-attachments/assets/04623f87-a6db-4d8c-8b44-c3c8036ec001)

### The binary from the previous question made two outbound connections to a malicious IP address. What was the IP address? Enter the answer in a defang format.

on the destinationip field we can see the ips and counts too
![image](https://github.com/user-attachments/assets/77fcec3a-7ff7-47f0-9720-ce755fc356e2)

### The same binary made some change to a registry key. What was the key path?

go to task category and click on the value set since we know the registry was changed
![image](https://github.com/user-attachments/assets/12e4c3db-4b82-4ce1-b215-dba92f278fd1)

![image](https://github.com/user-attachments/assets/e4cfcc70-4d7c-4704-89f8-bd700d7d4ddf)

### Some processes were killed and the associated binaries were deleted. What were the names of the two binaries? (format: file.xyz,file.xyz)
make a search with CommandLine=* then "taskkill /im"

do a table to see it clearly
![image](https://github.com/user-attachments/assets/4bab92ed-b47d-4cf2-bdf5-8df6635bfc0b)

### The attacker ran several commands within a PowerShell session to change the behaviour of Windows Defender. What was the last command executed in the series of similar commands?

![image](https://github.com/user-attachments/assets/87fe5967-2ff9-4442-9c41-c5662e7f698f)

![image](https://github.com/user-attachments/assets/d88b8f94-ca04-4f14-827e-a78e67c531e4)


### Based on the previous answer, what were the four IDs set by the attacker? Enter the answer in order of execution. (format: 1st,2nd,3rd,4th)

![image](https://github.com/user-attachments/assets/58a067a8-fee1-4a20-a9eb-c197fcfdf0b1)

### Another malicious binary was executed on the infected workstation from another AppData location. What was the full path to the binary?

![image](https://github.com/user-attachments/assets/e7d1b72a-55ae-4e99-832c-47ef15b8e5ce)

yeah this looks suspicious
![image](https://github.com/user-attachments/assets/c3e7dbdf-1da4-48b9-9daf-571d36e834b0)

### What were the DLLs that were loaded from the binary from the previous question? Enter the answers in alphabetical order. (format: file1.dll,file2.dll,file3.dll)


since we know the name of the executable we can search for the image loaded and see the dlls
![image](https://github.com/user-attachments/assets/97093b87-7e48-4611-8e0e-ed7315b3d026)














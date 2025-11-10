# web_vulnerablity_Scanning_using_nikto
Scan Both Public and local Server for misconfigurations, sensetive files, outdated softwares and other bugs.

## What is Nikto?
A powerful and fast web server Scanner use for Vulnerablity assessment.

## Why Nikto?
Nikto is widely used by ethical hackers, penetration testers, and cybersecurity professionals to identify potential security risks quickly and effectively. It helps ensure that web applications are safe, secure, and resistant to attacks.

## Requirements :-
1. Kali linux
2. Nikto - at least version 2.5
3. Python3 - used as a HTTP server for local testing
4. Public Target - (http://testphp.vulnweb.com)

### Check Kali linux
```cat /etc/os-release```

### Install Nikto
```sudo apt install nikto```

### Install Python
```sudo apt install python3```

## Execution of the Project
first command you will run is 
```nikto -h```
you can see there are a lot of help command in it. But the one that is going to be most usefull to you ammong these is 
```host+```
this command, what do you get in target in this host?
Either you will get the host or the URL.

## Scanning Public Server
We are going to run nikto on a public test target.
```nikto -h http://testphp.vulnweb.com```
press enter and we started scanning on it.

## Output Analysis
You need to pay attention in the four output points.
1. Missing anti-clickjacking Headers
2. Exposer of web server type and version
3. Availablity of default and potential dangerous files/folders
4. Basic information Disclosure headers like x-powered-By.

My Output - 
1. Server : nginx/1.19.0.
2. Retrieved x-powered-by header:php/5.6.40-38 + ubuntu 20.04.1 + ded.sury.org+1.
3. Anti-clickjacking x-Frame-options header is not present.

But now we have not recieved any such folder or file has been released.
so, In this we got three vulnerablity only.

## Scanning Local Server
In this we have use python3. So, we are going to do server local testing with python3.

### Check your IP address
```ifconfig```
On this i can run a web server through python

### Type command to host any folder
```python3 -m http.server<port_no>```
After type thi command whatever is in this directory will be hosted on port <port_no>.
meaning if i go to the browser and type <ip> and give the port <port_no>.
Then whatever data inside the folder will be hosted inside this kali linux machine.
That means you are seeing that it is running .

Now we do testing on this and that is called local testing.
```nikto -h <ip> -p <port_no>```
and start scanning

After scanning we will work on those four points. Which of these four pieces of information are we getting out of it.

## Output Analysis
1. server : simple HTTP/0.6 python/3.13.7
2. wp-cs-dump - this a folder that is visible that should not be visible.
   there are two cv values CVE-1999-0269. The vulnerability says is that if a folder is revealed , it could be dangerous. Which should not      be allowed. So this has been revealed here.
   Also, wp-config.php file found -> this file contains the credentials. Now we have seen this file also. so, this one information has been     revealed here
3. Anti-clickjacking x-Frame-option header is not present.
4. simple HTTP/0.6 appears to be outdated -> current is at least 1.2
so, there are the vulnerablities.

You want to make a report then it generate an output file and give it to us.
You need to type command 
```nikto -h <ip> -p <port_no> -output <fileName>```

You also make a tunning result means applied tuning for apecific scan.
You need to give command 
```nito -h <URL> -Tuning 1```
so, it will try to bring more optimized output by integrating and enhancing the performance with same tunning.

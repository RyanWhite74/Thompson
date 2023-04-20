# Thompson CTF

# Enumeration

### First things first let's run a port scan to see what opened ports we can find.

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled.png)

## We see 3 ports opened.

- **22/tcp running SSH, version OpenSSH 7.2p2**
- **8009/tcp running ajp13, version Apache Jserv (Protocol v1.3)**
- **8080/tcp running http, version Apache Tomcat 8.5.5**

## Let's check out Apache Tomcat running on port 8080 first.

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%201.png)

## We are brought to a quick start page where we see a manager app link. When you click the link, it asks you to login after trying a few default credentials for Apache Tomcat click cancel and you are given a 401 Unauthorized page that displays the correct login information.

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%202.png)

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%203.png)

# Initial foothold

### And just like that we are in as you can see, we have the ability to upload a WAR file which we will use msfvenom to create our payload.

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%204.png)

# msfvenom

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%205.png)

### We will then upload our payload using the manager and deploy it. (Remember the port you used in the payload as we will need it again soon)

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%206.png)

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%207.png)

### It is then added to our applications table where we can select it but first let's start up a netcat listener using your IP and the same port from above in my case I used 1234.

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%208.png)

### Once that is all setup click on the shell file we just uploaded and …. we get a shell.

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%209.png)

### We can upgrade our shell using **python -c 'import pty; pty.spawn ("/bin/bash")'**

# User.txt

### If we cd to the home directory, we see a user named jack and inside his directory we see 3 files one being user.txt.

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%2010.png)

# Privilege escalation and root.txt

### If we check out the crontab we can see a job running as root associated with the id.sh file, we found in the jack directory.

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%2011.png)

### There are a couple ways to go about this next step if you just want to go straight for the root.txt you can echo “cp /root/root.txt /home/jack/root.txt” > id.sh

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%2012.png)

### And finally, we have our root flag

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%2013.png)

### The next way we can get the flag is by becoming root to do that we will echo a tcp reverse shell into the id.sh file and a netcat listener.

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%2014.png)

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%2015.png)

### Now since we are root, we can just cat the root.txt file.

![Untitled](Thompson%20CTF%206c92a400c99d4f839592c3e82b7415b5/Untitled%2016.png)

### And with that we have completed the Thompson CTF on Try Hack Me

###

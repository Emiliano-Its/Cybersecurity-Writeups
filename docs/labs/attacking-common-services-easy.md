# Page 1

Information gathering;

We were commissioned bu the company Inlanefreight to conduct a penetration test to check three different servers. According to our information, the first is a server that manages emails, customers, and their files

We have to assess the inlanefreight.htb domain and obtain the flag.txt file.

We could start by the recognization in the server:

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Scann for ftp service:

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Scan for smtp service:

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Before we enumarate the first http scan, we can put the following in /etc/hosts file:

```
10.128.203.203.7		inlanefreight.htb
```

Scan for http service:

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Scan for https service:

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Scan for smtp (587) service:

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Scan for mysql service:

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

Scan for ms\_wbt-server service:

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

Now that we have a better overview of all the ports in the server, we can start to analyze each service:

First we try to login to the FTP server with anonymous credentials, it seems to be that the server is not supporting this configuration

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

We get the following by the http server:

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

In https, the site is asking credentials to log in:

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

XAMPP is a free, open-source, and cross-platform web server solution stack used to create a local host environment for testing and developing websites. It bundles Apache, MariaDB (database), PHP, and Perl into one package to simplify installing a local server on Windows, Linux, or macOS.

In the research we found some default credential for XAMPP package, but it seems not to work:

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

> Version: MariaDB 10.4.24

We tried anonymous authentication and it did not work:

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

Let's try to use some bruteforcing passwords in the services:

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

That does not work, let's try now use smtp-user-enum to enumerate users in the smtp server:

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

We have the that following user exists:

> fiona@inlanefreight.htb

Let's try to do a brute forcing password with the user that we just found:

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

With this credentils:

> fiona:987654321

We have access to the ftp server:

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Content of the expoused files:

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

And we have acces to the database

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

I did not find anything interesting in any table in any data base, so lets check if i can write a local file in the server with the following command:

```
mysql> show variables like "secure_file_priv";
```

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

It seems to be that we can write somenthing, let's try:

Based in the information we gather from the webserverinfo.txt, we know that the http server is running in the C:\xampp\htdocs\ directory, so lets try to write a file in that one, for then try to execute in the browser:

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

typing the [http://inlanefreight.htb/webshell.php?c=dir](http://inlanefreight.htb/webshell.php?c=dir), we could check that it worked

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

so lets find the flag.txt with [http://inlanefreight.htb/webshell.php?c=dir+/s+/b+C:](http://inlanefreight.htb/webshell.php?c=dir+/s+/b+C:)\flag.txt

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

And typing [http://inlanefreight.htb/webshell.php?c=type+C:\Users\Administrator\Desktop\flag.txt](http://inlanefreight.htb/webshell.php?c=type+C:\Users\Administrator\Desktop\flag.txt) to obtain the flag.txt content:

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

> Answer: HTB{t#3r3\_4r3\_tw0\_w4y$\_t0\_93t\_t#3\_fl49}

Yeii

---
description: >-
  This lab is targeting another internal server used to manage files and working
  material, such as forms. In addition, a database is used on the server, the
  purpose of which we do not know.
---

# Attacking Common Services - Hard

Start for scanning:

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

We try to access with smbclient to the share in the server

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

We have found some interesting files:

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

There are three files that seems to be credentials:

```
John:
Password Lists:

1234567
(DK02ka-dsaldS
Inlanefreight2022
Inlanefreight2022!
TestingDB123

Simon:
Credentials

(k20ASD10934kadA
KDIlalsa9020$
JT9ads02lasSA@
Kaksd032klasdA#
LKads9kasd0-@ 

Fiona:
Windows Creds

kAkd03SA@#!
48Ns72!bns74@S84NNNSl
SecurePassword!
Password123!
SecureLocationforPasswordsd123!!
```

And in one of the other two files have some interesting information:<br>

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

Trying with some combinations with the credentials the only that works was the following one:

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

In the remote desktop interface we found the sql server but we can not find any interesting:

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

Then we try to acces to the sql server with the cli tool sqsh, and try to fugure it out what user we can impersonate:

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

It seems to be a linked test server, the same that in the content of information.txt was talking about.

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

In that remote server where we have access, we have a testadmin privileges.

<figure><img src="../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

We found some credentials, but we still try to execute some commands.

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

We found flag.txt

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

Answer: HTB{46u$!n9\_l!nk3d\_$3rv3r$}

Yei!!

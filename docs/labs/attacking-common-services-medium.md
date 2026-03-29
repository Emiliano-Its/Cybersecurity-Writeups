---
description: >-
  This lab is described as an internal server (within the inlanefreight.htb
  domain) that manages and stores emails and files and serves as a backup of
  some of the company's processes.
---

# Attacking Common Services - Medium

From internal conversations, we heard that this is used relatively rarely and, in most cases, has only been used for testing purposes so far. It is required to asses de target server and find the falg.txt file.

Start scannig the target with nmap.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Below the dedicated scanning for each services recognize

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Try to see if there is a DNS zone transfer with dig tool

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Trying to get some more information in the target with the information gatered until now, i did not find something interesting. So i decided to make a another complete scan.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

We can see that there are two services that we did not  take account before. So, let's try to access in both server, in the 2121 i did not find anything with anonymous login, and in the 30021 the next results were found:<br>

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

So I could access to the share:

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Interesting, this probably are credentials for another service, that we could leverage, maybe the same ftp service:

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

And trying to access with these credetentials:

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Content of flag.txt:

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

> Answer: 1qay2wsx3EDC4rfv\_M3D1UM

Yeei!

---
description: >-
  Writeups about my approach in the skills assessment for Information Gathering
  - Web Edition module.
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Skills Assessment - Information Gathering (Web Edition)

Information gather in the context of the skills assessment:

&#x20; • Using `whois`

* Analysing `robots.txt`
* Performing subdomain bruteforcing
* Crawling and analysing results

Vhost needs for the questions:

<p align="center"><code>inlanefreight.htb</code></p>

Let's start.&#x20;

> &#x20;What is the IANA ID of the registrar of the inlanefreight.com domain?

We use whois tool for this one:

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

> _<mark style="color:$info;">**Answer: 468**</mark>_

Next question:

> What http server software is powering the inlanefreight.htb site on the target system?

First, we have to edit the /etc/hosts file adding the next line in the end with the ip address that hackthebox provided us:

```zsh
10.10.10.10    inlanefreight.htb
```

And then we can use the curl tool with the -I option to see the headers:

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

> _<mark style="color:$info;">**Answer: nginx**</mark>_

Next:

> What is the API key in the hidden admin directory that you have discovered on the target system?

For the this question, we start doing a vhost brute forcing, with gobuster, and we find the next vhost:

<p align="center"><kbd>web1137.inlanefreight.htb</kbd></p>

We poceed to add this vhost in the /etc/hosts file:

```zsh
10.10.10.10		web1337.nlanefreight.htb
```

Then with the help of ./finalrecon.py script we can find the robots.txt file, that contains the next lines:

```
User-agent: *
Allow: /index.html
Allow: /index-2.html
Allow: /index-3.html
Disallow: /admin_h1dd3n
```

We have the admin directory now. And when we acces to: <mark style="color:blue;">http://web1337.inlanefreight.htb\[PORT]/admin\_h1dd3n/index.html</mark>

We see the next results:

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

> _**Answer: e963d863ee0e82ba7080fbf558ca0d3f**_

For the next question:

> After crawling the inlanefreight.htb domain on the target system, what is the email address you have found?

First we brute force another one time the vhost in url <mark style="color:blue;">http://web1337.inlanefreight.htb:\[PORT]/</mark>

And we have the following results:

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Now, we can use the ReconSpider.py script for crawl the web page:

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

And then, see the results from the .json file generated:

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

> _**Answer: 1337testing@inlanefreight.htb**_

To finish, in the last question is requested an API key that the developers will be changing. The key is in the same .json fle:

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

> _**Answer: ba988b835be4aa97d068941dc852ff33**_

We dit it. Yei!

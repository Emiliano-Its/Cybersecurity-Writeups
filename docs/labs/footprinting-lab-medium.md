# Footprinting Lab - Medium

To begin we can gather the following information provided to us:

* User named HTB has been created.
* We need to obtain the credentials of this user as proof.
* We have to analyze a new service

Let's start for scan all the ports in the machine:

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

So, we can see that a well-known port promt to us when we make a scan, its the 2049: NFS - its purpose is to access file systems over a network as if they were local.

So in the gather of knowledge of this service we found the next one:

In the gather of knowledge of this service we found the next one: The NFS protocol has no mechanism for authentication or authorization. Instead, authentication is completely shifted to the RPC protocol's options. Rpc protocol fall on 111 tcp port, and actually we see it.&#x20;

Now, dive into the functionality of these services. Based in this [article](https://www.techtarget.com/searchapparchitecture/definition/Remote-Procedure-Call-RPC). It is a procedure that allow a program call a external funcition (function in another computer) like a internal funcition trough a framework. Based on the nfs functionality, we can see how they are related to.

when we try to interact with the rpc server we got this:

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

And when we mount with the following commands:

```zsh
Valemiliano@htb[/htb]$ mkdir target-NFS
Valemiliano@htb[/htb]$ sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock
Valemiliano@htb[/htb]$ cd target-NFS
Valemiliano@htb[/htb]$ tree .
```

we can see this:

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

And when we check the only file that seems to have information by its size, we can look at the following log:

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

we obtained a bunch of interesting information by this log:

Host: smtp.web.dev.inlanefreight.htb

port=25

USER: alex

password: lol123!mD

from="alex.g@web.dev.inlanefreight.htb"

And some extra information about smtp server config file. Just in case, i decide to scan the ports that in our initial scann appear like unknown:

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>



I don't see any interesting here. Let's try to use the credentials we found in the different kind of services. First we are going to try with smb service:

<figure><img src="../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

Mmm, maybe if we try by this way:

<div data-full-width="true"><figure><img src="../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure></div>



And we can also interact with spcclient:&#x20;

<figure><img src="../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

I got notice that we can list all the sharenames that are available executing the following command:

<figure><img src="../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

Then we can see what is within this share:

<figure><img src="../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

Content of important.txt:

> sa:87N1ns@slls83

It seems to be another credentials, trying with diferent services avalilable in the server that before we recognize i could obtain the following:

Fail attempts:

<figure><img src="../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

And in the last one:

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

We also have acces in via gui:<br>

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

i just decided use the gui and with the hint that htb provide to me, i know that we have to do something with the SQL Server Management Studio

So i open and start research and do some things. I found this table:

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>



And wiht the option select top 200 rows, i could have acces to the table:

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

And there is the password:

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

> Answer: lnch7ehrdn43i7AoqVPK4zWR
>
> yei!


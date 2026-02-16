# Footprinting Lab - Medium

So, the next information is gives to us:

* User named HTB has been created.
* We need to obtain the credentials of this user as proof.
* We have to analyze a new service

Let's start for scann all the ports in the machine:

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

So, we can see that a well-known port promt to us when we make a scan, its the 2049: NFS - its purpose is to access file systems over a network as if they were local.

so in the gather of knowledge of this service we found the next one:

In the gather of knowledge of this service we found the next one: The NFS protocol has no mechanism for authentication or authorization. Instead, authentication is completely shifted to the RPC protocol's options. Rpc protocol fall on 111 tcp port, and actually we see it.&#x20;

Now, dive into the functionality of these services. Based in this [article](https://www.techtarget.com/searchapparchitecture/definition/Remote-Procedure-Call-RPC). It is a procedure that allow a program call a external funcition (function in another computer) like a internal funcition trough a framework. Based on the nfs functionality, we can see how they are related to.

when we try to interact with the rpc server we got this:

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

# Phishing Analysis 1

## Scenario

A user has received a phishing email and forwared it to the SOC. Can you investigate the email and attachment to collect useful artifacts?

# Questions

## 1. Who is the primary recipient of this email?

Firstly, I open the provided file which contain the phishing email using TextEdit app on my Mac. (You should be able to use any TextEditor software.)

Here's the email header that I see when I opened it:

```
From: Mail Delivery System <Mailer-Daemon@se7-syd.hostedmail.net.au>
Sent: 18 March 2021 04:14
To: kinnar1975@yahoo.co.uk <kinnar1975@yahoo.co.uk>
Subject: Undeliverable: Website contact form submission
```

Now, we could easily see the primary recipient.

**Answer:** kinnar1975@yahoo.co.uk

## 2. What is the subject of this email?

We'll take a look at the header from the email above again specifically in the subject section.

**Answer:** Undeliverable: Website contact form submission

## 3. What is the date and time the email was sent?

Again, the answer is located in the header of the email.

**Answer:** 18 March 2021 04:14

## 4. What is the Originating IP?

To find the Originating IP, we'll have to dive through the texts and find the IP. **Make sure you find the origin, not the Kinnar's IP!**

Below is the Originate IP complete with it's host:

```
Received: from c5s2-1e-syd.hosting-services.net.au ([103.9.171.10])
	by se7-syd.hostedmail.net.au with esmtps (TLSv1.2:AES128-GCM-SHA256:128)
	(Exim 4.92)
	id 1lMk2r-0007vB-6O
	for kinnar1975@yahoo.co.uk; Thu, 18 Mar 2021 15:14:06 +1100
```

Now we can enter the IP for the answer.

**Answer:** 103.9.171.10

## 5. Perform reverse DNS on this IP address, what is the resolved host? (whois.domaintools.com)

I went to whois.domaintools.com and pasted the IP from the previous answer and we can see the resolved host from the details. *I found out later that I can just use my terminal to get the resolved host with this command:*

```
host 103.9.171.10

10.171.9.103.in-addr.arpa domain name pointer c5s2-1e-syd.hosting-services.net.au.
```

**Answer:** c5s2-1e-syd.hosting-services.net.au

## 6. What is the name of the attached file?

The name of the .eml file which we have downloaded and decompressed from .zip file.

**Answer:** Website contact form submission.eml

## 7. What is the URL found inside the attachment?

I opened the attachment from the .eml file from Mail app and we can see the malicious URL.

**Answer:** https://35000usdperwwekpodf.blogspot.sg?p=9swghttps://35000usdperwwekpodf.blogspot.co.il?o=0hnd

## 8. What service is this webpage hosted on?

By looking at the malicious URL above, I can easily tell that it is hosted on Blogspot as it is written clearly.

**Answer:** blogspot

## 9. Using URL2PNG, what is the heading text on this page?

I followed the guide by using URL2PNG and pasted the URL in the site and received a warning which initially I thought wasn't the answer but turns out it was.

**Answer:** Blog has been removed

# Conclusion
By finishing this practice, I learned the basics of analysing Phishing Email in which I am able to find who, when, why, what, and how the attack happened.
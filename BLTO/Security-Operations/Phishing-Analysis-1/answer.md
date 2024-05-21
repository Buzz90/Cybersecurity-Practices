# Phishing Analysis 1

## Scenario

A user has received a phishing email and forwared it to the SOC. Can you investigate the email and attachment to collect useful artifacts?

# Questions

## 1. Who is the primary recipient of this email?

Firstly, I open the provided file which contain the phishing email using online EML opener. (But I also learns that you could also open using TextEditor, which later I will use later.)

Here's the email header that I see when I opened it:

```
From: Mail Delivery System <Mailer-Daemon@se7-syd.hostedmail.net.au>
Sent: 18 March 2021 04:14
To: kinnar1975@yahoo.co.uk <kinnar1975@yahoo.co.uk>
Subject: Undeliverable: Website contact form submission
```

Now, we could easily see the primary recipient.

**Answer:** kinnar1975@yahoo.co.uk
# LAB: Exploiting an API endpoint using documentation

## Task(s):

To solve the lab, find the exposed API documentation and delete ```carlos```. You can log in to your own account using the following credentials: ```wiener:peter```.

## Instruction(s):

> To solve this lab, you'll need to know:
>
> - What API documentation is.
> - How API documentation may be useful to an attacker.
> - How to discover API documentation.
> 
> These points are covered in our API Testing Academy topic.

## Let's begin solving it!

First, I began by opening my Burp Suite and then navigate to ```Proxy``` tab, after that I open the browser through Burp Suite.

![Opening Burp Suite](/WSA(Burp)/LAB-1-API-Documentation/images/1.png)

Then I open the link from the button ```ACCESS THE LAB``` and paste it to Burp browser. I was greeted by a webpage and I follow the task to login first.

![Webpage to be exploited](/WSA(Burp)/LAB-1-API-Documentation/images/2.png)

I enter the given username: ```wiener``` and password: ```peter``` to the text box and pressed login.

![Logging in to account](/WSA(Burp)/LAB-1-API-Documentation/images/3.png)

It asks me to change the email for some reason and so I did.

![Changing email](/WSA(Burp)/LAB-1-API-Documentation/images/4.png)

I then go back to Burp Suite and navigate to ```HTTP history``` to review the all of the response from the site and I found the exposed API which is ```/api/user/wiener```, so that means that I will have to investigate each directory.

![Burp Suite HTTO Request](/WSA(Burp)/LAB-1-API-Documentation/images/5.png)

I started with ```/api``` first then I accessed the broken API and check whether carlos is a valid username from the ```GET``` function on the screen and it turns out it is a valid user because it returns with a valid username and email that is being used for Carlos's account.

![GET Carlos username](/WSA(Burp)/LAB-1-API-Documentation/images/6.png)


I can proceed by closing the tab and go to ```DELETE``` function and entered Carlos's username and press ```Send Request``` to proceed deleting his account.

![DELETE Carlos user](/WSA(Burp)/LAB-1-API-Documentation/images/7.png)


![FINISHED](/WSA(Burp)/LAB-1-API-Documentation/images/8.png)
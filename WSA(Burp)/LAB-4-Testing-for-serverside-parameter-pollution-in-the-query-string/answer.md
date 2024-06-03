# LAB: Exploiting server-side parameter pollution in a query string

### Link: [Click Me!](https://portswigger.net/web-security/learning-paths/api-testing/api-testing-testing-for-server-side-parameter-pollution-in-the-query-string/api-testing/server-side-parameter-pollution/lab-exploiting-server-side-parameter-pollution-in-query-string)

## Task(s):

To solve the lab, log in as the ```administrator``` and delete ```carlos```.

## Instruction(s):

> To solve this lab, you'll need to know:
>
> - How to use URL query syntax to attempt to change a server-side request.
> - How to use error messages to build an understanding of how a server-side API processes user input.
> 
> These points are covered in our API Testing Academy topic.

## Required Apps:
- Burp Suite
- Server-side variable names for Brute Attack. (You can get it from [/WSA(Burp)/Supporting-assets/](/WSA(Burp)/Supporting-assets/))


## Let's begin solving it!

On this lab, I wasn't given any credentials to login as ```administrator``` which means I need to get access one way or another. I started by opening the Lab link on my Burp Browser and I greeted with the same site as the [previous lab](/WSA(Burp)/LAB-3-Mass-assignment-vulnerabilities/answer.md).

!["Main Page"](/WSA(Burp)/LAB-4-Testing-for-serverside-parameter-pollution-in-the-query-string/images/1.png)

Next, I navigate to the login page then I tried to enter ```administrator``` as the username and randomly entering keywords as the password and tried to login which obviously gives me an ```Invalid username or password``` error. Then I checked on Burp Suite's HTTP history and it doesn't show anything useful.

!["Forgot Password Page"](/WSA(Burp)/LAB-4-Testing-for-serverside-parameter-pollution-in-the-query-string/images/2.png)

I clicked the **Forgot Password** button which leads me to this page that asks for a username:

!["Entered administrator username"](/WSA(Burp)/LAB-4-Testing-for-serverside-parameter-pollution-in-the-query-string/images/3.png)

Then I just enter ```administrator``` as username then I press **Submit** button. After that, it shows me a notification to check the email at ```*****@normal-user.net``` which still gave me nothing:

!["Entered administrator username"](/WSA(Burp)/LAB-4-Testing-for-serverside-parameter-pollution-in-the-query-string/images/4.png)

Since I just filled a textbox, then I checked the HTTP history again on Burp Suite and notice a few interesting details:

!["HTTP history detail"](/WSA(Burp)/LAB-4-Testing-for-serverside-parameter-pollution-in-the-query-string/images/5.png)

1. On ```/forgot-password``` request, we can see the token followed by the username that I inserted.
2. On ```/forgot-password``` response, we got 2 variable displayed, which is ```result``` and ```type```.
3. When I clicked the **Forgot Password** button, I received ```/static/js/forgotPassword.js``` URL.

!["HTTP history detail"](/WSA(Burp)/LAB-4-Testing-for-serverside-parameter-pollution-in-the-query-string/images/6.png)

4. On ```forgotPassword.js``` script, I got a ```reset_token``` parameter from ```/forgot-password?reset_token=${resetToken}```.

For now, I'll keep all the details above and proceed with trying to manipulate the **JSON** from ```/forgot-password``` and sending the ```POST /forgot-password``` to **Repeater**.

!["Repeater"](/WSA(Burp)/LAB-4-Testing-for-serverside-parameter-pollution-in-the-query-string/images/7.png)

Next, I will attempt to truncate the server-side request by adding URL-encoded ```#``` character (which is ```%23```) after ```administrator``` then I sent the request. Check the response i got below:

!["Response"](/WSA(Burp)/LAB-4-Testing-for-serverside-parameter-pollution-in-the-query-string/images/8.png)


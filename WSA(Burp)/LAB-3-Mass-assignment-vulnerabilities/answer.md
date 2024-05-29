# LAB: Exploiting a mass assignment vulnerability

### Link: [Click Me!](https://portswigger.net/web-security/learning-paths/api-testing/api-testing-mass-assignment-vulnerabilities/api-testing/lab-exploiting-mass-assignment-vulnerability#)

## Task(s):

To solve the lab, find and exploit a mass assignment vulnerability to buy a **Lightweight l33t Leather Jacket**. You can log in to your own account using the following credentials: ```wiener:peter```.

## Instruction(s):

> To solve this lab, you'll need to know:
> 
> - What mass assignment is.
> - Why mass assignment may result in hidden parameters.
> - How to identify hidden parameters.
> - How to exploit mass assignment vulnerabilities.
>
> These points are covered in our API Testing Academy topic.

## Required Apps:
- Burp Suite
- Content Type Converter (**Optional**)

## Let's begin solving it!

The task given on this Lab is not that different from the previous one, but this one requires me to identify hidden parameters and exploit mass assignment vulnerabilities.

I began by opening my **Burp Suite** and **Burp Browser** and quickly navigate to the link given by the Lab. Then I logged in using the credential given on the ```Task(s)``` which is:

> Username: ```wiener```
>
> Password: ```peter```

I then checked the ```HTTP history``` on Burp Suite to see if there are any vulnerabilities but turns out there are none. (shown in the image below)

!["HTTP History"](/WSA(Burp)/LAB-3-Mass-assignment-vulnerabilities/images/1.png)

Because I didn't find any ```/api``` that I can exploit, I will continue by going to ```Homepage``` on the website. In the [previous lab](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/answer.md), we can find ```/api``` just by browsing through the ```Homepage``` which is not the case on this one. So I had to browse the product named **Lightweight l33t Leather Jacket** because that's the targetted product.

!["HTTP History"](/WSA(Burp)/LAB-3-Mass-assignment-vulnerabilities/images/2.png)

Again, it doesn't give me any exposed ```/api```. Next, I tried to add the product to the cart and proceed to ```My Cart``` button which is located on the top right.

!["My Cart"](/WSA(Burp)/LAB-3-Mass-assignment-vulnerabilities/images/3.png)

After I clicked ```My Cart```, I checked my ```HTTP history``` on Burp Suite and finally got the vulnerable API: ```/api/checkout```.

!["API found"](/WSA(Burp)/LAB-3-Mass-assignment-vulnerabilities/images/4.png)

Now I can investigate ```Request``` and ```Response``` from ```/api/checkout``` which we can all see from the image below:

!["Request and Response"](/WSA(Burp)/LAB-3-Mass-assignment-vulnerabilities/images/5.png)

Few things to take note from the JSON here:
- On **Request**, we can see that it is using ```GET``` method to grab data. We will try to use other methods that are allowed.
- On **Response**, we can see that we have 2 parameters that we can try to manipulate which are ```chosen_discount``` and ```chosen_product```.

Since I already got ```api/checkout```, I will send it to ```Repeater``` to try to use other **HTTP Methods**.

!["OPTIONS Method"](/WSA(Burp)/LAB-3-Mass-assignment-vulnerabilities/images/6.png)

I used ```OPTION``` method and it gives me ```405 Method Not Allowed``` response followed by ```Allow: GET, POST``` which means that I can use ```POST``` to update data.

Since the **Response** I got earlier contains JSON, that means that I will have to generate a JSON Content-type on the request followed by the 2 parameters (```chosen_discount```, ```chosen_product```).

On the code below, I manipulate the ```chosen_discount``` and change the percentage to ```100``` so that there will be no cost for me to buy the product. Take a look the code below for the **Request** and **Response** after I sent it.

### Request:
```
POST /api/checkout HTTP/2
Host: 0a4b00f303c96b5285818aab00ae00a0.web-security-academy.net
Cookie: session=9fQ3cRoxuxtMnR7nr9gtVFumxEOhjzaB
Sec-Ch-Ua: "Chromium";v="125", "Not.A/Brand";v="24"
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36
Sec-Ch-Ua-Platform: "macOS"
Accept: */*
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://0a4b00f303c96b5285818aab00ae00a0.web-security-academy.net/cart
Accept-Encoding: gzip, deflate, br
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
Priority: u=1, i
Content-Type: application/json;charset=UTF-8
Content-Length: 7

{
    "chosen_discount":
    {"percentage":100 
    },
    "chosen_products":[
        {
            "product_id":"1",
            "name":"Lightweight \"l33t\" Leather Jacket",
            "quantity":1,
            "item_price":133700
        }
    ]
}
```

### Response:

```
HTTP/2 201 Created
Location: /cart/order-confirmation?order-confirmed=true
X-Frame-Options: SAMEORIGIN
Content-Length: 0
```

It seems that there are no errors and we can see that the order is confirmed from looking at line 2: ```Location: /cart/order-confirmation?order-confirmed=true```. Now I can refresh the page again and see that there are no more orders and I successfully finished the lab.

# Voila

!["FINISHED"](/WSA(Burp)/LAB-3-Mass-assignment-vulnerabilities/images/7.png)
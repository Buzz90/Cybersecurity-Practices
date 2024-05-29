# LAB: Finding and exploiting an unused API endpoint

## Task(s):

To solve the lab, exploit a hidden API endpoint to buy a **Lightweight l33t Leather Jacket**. You can log in to your own account using the following credentials: ```wiener:peter```.

## Instruction(s):

> To solve this lab, you'll need to know:
>
> - How to use error messages to construct a valid request.
> - How HTTP methods are used by RESTful APIs.
> - How changing the HTTP method can reveal additional functionality.
> 
> These points are covered in our API Testing Academy topic.

## Let's begin solving it!

As usual, I will use Burp Suite and paste the link used by the Lab there. I guess I don't need to screenshot it since I already explained in the [previous lab](/WSA(Burp)/LAB-1/answer.md).

Again, we'll login using the credentials that was given in the task:

> Username: ```wiener```

> Password: ```peter```

After succesfully logged in, I was greeted by the same window as in the [previous lab](/WSA(Burp)/LAB-1/answer.md) but this time, it has a few different things as mentioned in the picture below:

![My Account page](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/1.png)

But it is not that important so we can just ignore it. Next thing that I did was going back to the ```home``` page to get the lists of products and find the product that I need to buy, which is ```Lightweight l33t Leather Jacket```.

![Home Webpage](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/2.png)

As you can see from the screenshot above, the price of the product is ```$1336.70``` which I will have to change to ```$0``` later in order to get it for free.

Next, I press ```View details``` button to go to the product page. Before I change the product price, I will have to find the exposed API. Let's take a look at this Burp Suite ```HTTP History``` screenshot below:

![Burp Suite HTTP Request](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/3.png)

Once I identified API endpoints, I then interact with the API using Burp Repeater to investigate how the API will respond. To do that, will send the highlighted URL and ```Send to Repeater``` and then navigate to ```Repeater``` tab in Burp Suite.

![Burp Suite Repeater](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/4.png)

We can see the ```HTTP Methods``` on the first line of the Request. Now I will try other HTTP methods such as ```OPTIONS```, ```PATCH```, ```POST```, or ```DELETE```.

![OPTIONS Method used](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/5.png)

After I sent the request, it gives me error ```405 Method Not Allowed``` which means that ```OPTIONS``` method isn't available to be used. After the error, it gives me the allowed method to be used which are ```GET``` and ```PATCH```.

I will change the method in the Request from ```OPTIONS``` to ```PATCH``` and see what will happen.

![PATCH Method used](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/6.png)

Now it gives me another error ```400 Bad Request``` which is ```"Only 'aplication/json' Content-Type is supported"```. It means that the current Content-Type isn't **JSON**. I then convert the whole request to **JSON** by using **Content Type Converter** (You'll have to manually install it to your Burp).

After I converted it to **JSON**, It gives me few lines of code as you can see in the screenshot below:

![Converted to JSON](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/7.png)

I then sent the request again and now the error details changed to ```"'price' parameter missing in body."```. 

![Price parameter missing](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/8.png)

Since the response that I got is showing ```'price'```, that means I found the target. Now I will try to enter ```"price":0``` in the **JSON** body by replacing the ```"":""``` and then send the request. Take a look at the result:

![Price value changed](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/9.png)

Now that I have changed the price of the item, I will go back to the browser to check whether the pricetag has changed or not.

![Pricetag changed](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/10.png)

It seems that the pricetag has been succesfully changed, then I proceed to buy the product. Take a look at the image below:

![Cart preview](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/11.png)

It shows us that the **Total** is **$0**. That means that I should get this item for free when I place the order in which I did right after and I got this message:

![Order success](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/12.png)

# Voila

![FINISHED](/WSA(Burp)/LAB-2-Identifying-and-interacting-with-API-endpoints/images/13.png)
---
title: Petshop Pro
published: true
tags: Hacker101
---

# Flag 0

#### Hints:

* Something looks out of place with checkout
* It's always nice to get free stuff

I setup burp proxy to see communication between browser and server. After that I was observing exchanged data, and notice that information about items in cart was sending to server in post body.

![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag0/cart_post.png)

Then I modified price in burp and forward request to the server, after that flag was displayed in checkout page:

![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag0/flag.png)

* * *

# Flag 1

#### Hints:

* There must be a way to administer the app
* Tools may help you find the entrypoint
* Tools are also great for finding credentials

First hint gives me an idea to enumerate few popular page names as login, admin etc. And in that way I found login page:

![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag1/login_page.png)

First thing I was trying is few common usernames and logins, but they didn't work. I was trying to bypass login step, but I wasn't able to do that. So I decided to brute force credentials. To do that I was using  [Turbo Instuder](https://github.com/portswigger/turbo-intruder), it's an extension to burp.

Solution step by step:
1. Intercept login request in burp:
![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag1/login_request.png)

2. Send intercepted request to Turbo Intruder. (Right click on the request then choose "Send to turbo intruder):

3. Brute force username. I was using [rockyou.txt](https://www.kaggle.com/wjburns/common-password-list-rockyoutxt) list:
![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag1/username_attack.png)
after few minutes username has been located:
![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag1/username_found.png)

4. Prepare attack for password similarly to username attack.
![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag1/password_attack.png)
after few minutes all credentials were known to me:
![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag1/login_password.png)
I use those credentials to login and read flag:
![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag1/flag.png)

* * *

# Flag 2

#### Hints:

* Always test every input
* Bugs don't always appear in a place where the data is entered

Let's notice that now user can edit entry. 

![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag1/flag.png)

I was trying simple xss payload:

![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag2/xss.png)

after that go the cart, flag should be displayed:

![New post](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag2/flag.png)
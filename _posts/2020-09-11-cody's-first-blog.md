---
title: Cody's First Blog
published: true 
tags: Hacker101
---

# Flag 0

### Hints:
* What was the first input you saw?
* Figuring out what platform this is running on may give you some ideas
* Code injection usually doesn't work

First input: 

![First input](assets/firstBlog/flag0/input.png)

First I was trying with XSS. With second hints I use Wappalyzer to check what platform is running on. It uses php 5.5.8 so I decided to try to inject some php code.

![Payload](assets/firstBlog/flag0/pyaload.png)

After that flag is displayed:

![Flag](assets/firstBlog/flag0/flag.png)

* * *

# Flag 1
### Hints:
* Make sure you check everything you're provided
* Unused code can often lead to information you wouldn't otherwise get
* Simple guessing might help you out

I look into page source code and find this comment:

![Hidden pange](assets/firstBlog/flag1/page.png)

I go to this link, there is login form: 

![Hidden pange](assets/firstBlog/flag1/login.png)

Remove 'auth.' from url. login form will be bypassed, and flag displayed:

![Flag](assets/firstBlog/flag1/flag.png)
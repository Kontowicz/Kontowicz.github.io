---
title: TempImage
published: true 
tags: Hacker101
---

# Flag 0

#### Hints:
* File uploads can be hard to pin down
* What happens to your filename when you see an uploaded file?
* What if you make a small change to the path?

Intercept request with image, to filename add ../ and forward. 

![Orginal request](assets/TempImage/flag0/orginal_img.png) 

change to:

![Change to](assets/TempImage/flag0/mod_img.png) 

Alter all, flag will be displayed:

![Flag](assets/TempImage/flag0/flag.png) 

# Flag 1

### Hints:
* It clearly wants one specific format
* If you can't bypass that check, what can you do?
* Read up on PNG chunks

I spend a lot of time on this flag, step by step solution: 
1. List all files

![LS](assets/TempImage/flag1/modify.png) 
![Files](assets/TempImage/flag1/result.png) 

2. Then "print" all these files. Flag is in index.php so you can just run those payload:

![Cat](assets/TempImage/flag1/cat.png) 
![Flag](assets/TempImage/flag1/flag.png) 
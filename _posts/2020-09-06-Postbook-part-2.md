---
title: Postbook part 2
published: true
tags: Hacker101
---

# Flag 4

#### Hints:

* You can edit your own posts, what about someone else's?

Firstly create new post, then edit that post. After that change id value in URL to 2. Then modify that post (that post is owned by admin), and save it. Flag will should be displayed on the screen.

![Flag](/assets/postbook/flag4/flag.png)

* * *

# Flag 5

#### Hints:
* The cookie allows you to stay signed in. Can you figure out how they work so you can sign in to user with ID 1?

To check cookies do right click, select inspect element then go to Storage. Now you can view cookies.

![Cookie](/assets/postbook/flag5/cookie.png)

My cookie value is:
```
eccbc87e4b5ce2fe28308fd9f2a7baf3
```
I search that value in google, and get many results  connected to md5. So maybe cookie is just md5 hash of user id? Let's check that:
```
md5(1)=c4ca4238a0b923820dcc509a6f75849b
```
then just swap cookie value, and refresh page, next flag to the collection.

![Cookie](/assets/postbook/flag5/flag.png)

* * *

# Flag 6

#### Hints:
* Deleting a post seems to take an ID that is not a number. Can you figure out what it is?

![Cookie](/assets/postbook/flag6/post_id.png)

Just change it, it is an md5 hash. More about that case is write in flag 5. That task is very similar to previous.

![Flag](/assets/postbook/flag6/flag.png)
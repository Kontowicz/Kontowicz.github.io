---
title: Postbook part 1
published: true
tags: Hacker101
---

# Flag 0

#### Hits:
* The person with username "user" has a very easy password...

I just manually tried a few very common passwords. Do it on your own.
![Flag](/assets/postbook/flag0/flag.png)


# Flag 1

#### Hints:
* Try viewing your own post and then see if you can change the ID

Just have some fun with id param in URL.
![Flag](/assets/postbook/flag1/flag.png)

* * *

# Flag 2

#### Hints:
* You should definitely use "Inspect Element" on the form when creating a new post

I do that:
![Form inspection](/assets/postbook/flag2/form.png)

and very interesting is the highlighted hidden field. I change that value, and the next flag has been displayed.

![Form inspection](/assets/postbook/flag2/flag.png)

By this value, the post author is identified. So it is possible to easily submit a post as someone else, just by changing that value.

* * *

# Flag 3

#### Hints:
* 189 * 5

189 * 5 = 945 like in flag 2 go to post with that id.

![Form inspection](/assets/postbook/flag3/flag.png)
---
title: Encrypted Pastebin 1
published: true 
tags: Hacker101
---

# Flag 0

### Hints:
* What are these encrypted links?
* Encodings like base64 often need to be modified for URLs. Thanks, HTTP
* What is stopping you from modifying the data? Not having the key is no excuse

I created new post. After submitting post in address bar appears new url with param. I modified this value, and that caused an error:

![Flag](assets/encrypted_pastebin/flag0/flag.png)

flag is hidden in error message.

* * * 

# Flag 1

### Hints:
* We talk about this in detail in the Hacker101 Crypto Attacks video
* Don't think about this in terms of an attack against encryption; all you care about is XOR

Get closer look to error message:

![Error message](assets/encrypted_pastebin/flag0/flag.png)

and points of crypto attacks lesson:

![Lesson content](assets/encrypted_pastebin/flag1/lesson.png)

Based on error message and hints I found padding oracle error. This attack is time-consuming.

Result of padBuster attack:
![Flag](assets/encrypted_pastebin/flag1/flag.png)

Following script can be used to solve this task:

```python
import sys
import os
url = sys.argv[1]
host, post_id = url.split('post=')
host += 'post='
post_id = post_id.replace('~', '=').replace('!', '/').replace('-', '+')
os.system('padbuster {}{} {} 16'.format(host,post_id,post_id))
```

Copy, paste and save this code to file. For example name this file tmp.py, then run it in that way:

```
python3 tmp.py 'URL'
```
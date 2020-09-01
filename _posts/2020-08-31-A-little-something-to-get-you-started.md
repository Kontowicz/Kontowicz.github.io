---
title: A little something to get you started
published: true
tags: Hacker101
---

## Flag 0

### Hints:
* Take a look at the source for the page
* Does anything seem out of the ordinary?
* The page looks really plain
* What is that image?

### Initial page

![](/assets/{{ page.title | downcase | replace: ' ','-'}}/initial_page.png)

Right click, view page source, result: 
```html
<!doctype html>
<html>
	<head>
		<style>
			body {
				background-image: url("background.png");
			}
		</style>
	</head>
	<body>
		<p>Welcome to level 0.  Enjoy your stay.</p>
	</body>
</html>
```

Image background.png is not visible on base page. Any hidden resource on the page is interesting, let's check it out. Go to:

```
http://35.227.24.107/f642e8efd2/background.png
```

flag is displayed on this link. 

![](/assets/{{ page.title | downcase | replace: ' ','-'}}/flag.png)
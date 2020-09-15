---
title: Intentional Exercise
published: true 
tags: Hacker101
---

# Flag 0

### Hints:
* Check the manifest
* Is the link really broken?
* Launching from another app might help

After few minutes download apk file, and save it. Then convert it to .jar with following command:
```
d2j-dex2jar -f level13.apk
```
Also decompile sources:
```
apktool d level13.apk
```
Read manifest file, then open MainActivity file:

![MainActivity file](assets/intentional_exercise/source_code.png)

As you probably noticed app is communicating with URL, I check it out:

![Main page](assets/intentional_exercise/main_page.png)

Go to Flag:

![Invalid request](assets/intentional_exercise/page_invalid.png)

Nah, that would be too easy, there is nothing. I return to source code and read it carefully. After that I reconstruct final URL:

```
http://34.94.3.143/fa8af62290/appRoot/flagBearer?&hash=8743a18df6861ced0b7d472b34278dc29abba81b3fa4cf836013426d6256bd5e
```

![Flag](assets/intentional_exercise/flag.png)
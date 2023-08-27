+++
title = "Linux File Permissions"
date = "2023-04-27"
[taxonomies]
tags = ["linux", "permissions"]
+++

## Backstory

Each student in the Computer Science's department is assigned a user on the server. This allow us to have access to a variety of services inside the facilities, from printing quotas to Wi-Fi credentials. My favourite thing it's that they allow us to ssh remotely into our accounts with the [Apache's per-user web directories module](https://httpd.apache.org/docs/2.4/howto/public_html.html) enabled. That's right, this website is sponsored by Universidad de Chile and has been setup from the commodity of my home.

---

I have had experience setting up websites with `nginx`. I learnt the best practices from Debian and I keep everything tidy at all times. However, the department's server is configured using Apache and I am an unprivileged user. That was the first time I truly witnessed the power of Linux file permissions in action.

The instructions where pretty straightforward.

* Create a directory named `public_www`:
```bash
$ mkdir public_www
```

* Create the following file:
```html
public_www/index.html
--------------
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title> Hello world! </title>
</head>
<body>
Hello world!
</body>
</html> 
```

* Allow Apache to cross the home directory:
```bash
$ chmod o+x ~
```

* Allow Apache to read the directory's content:
```bash
$ chmod o+x public_www
$ chmod go+r public_www/index.html 
```

> Fun fact. The original instructions were incomplete and they didn't work when I followed them. I went to the help desk to inform the situation to the system administrator. It turns out Apache's changed its requirements and an aditional permission was required. That's how I got to be the first freshman of the year to claim their free web directory.

## Things go wrong

I setup a website on pure html. I started with something simple and useful: template configuration files for the university's Wi-Fi connections (as seen on my [previous post](https://users.dcc.uchile.cl/~tvillega/posts/beauchef-networks/)). Little did I know that code blocks render so awfully bad on mobile.

Learning CSS just to change the code blocks looked like a great idea at first, but since I have to actually keep the website updated I was adding an extra load on the long term. Therefore, I started searching for website templates. Nothing too fancy, just a static html made by someone else. That's when chaos began.

I downloaded the tar file and unpacked it on a path inside `public_www`. It didn't load. Instead of checking carefully the permissions, I just slammed `chmod 755` and saw my irresponsibility bear fruit. Then I remembered the system administrator and I told to myself: *"Hey! My sysadmin always uses the other thing, the one with the `+/-`. Let's revert the unnecesary permissions with that"*. That's when I got *the message*:
```bash
tvillega@servername ~/public_www $ ls -lha theslant
ls: cannot access 'theslant/.': Permission denied
ls: cannot access 'theslant/..': Permission denied
total 0
d????????? ? ? ? ?            ? .
d????????? ? ? ? ?            ? ..

```

The same error applied for `rm`. I always fix this with `sudo chmod 755`, but as an unprivileged user I found myself hopeless. The system administrator wasn't available on the help desk, so an unmovable `theslant` path lived on my web directory for a long time. It wasn't until the system administrator came back that I got to fix it. And I have to admit it, it was a really good life lesson.

## File Permissions (revisited)

The following permissions are available on Linux:

|   |4  |2  |1  |   |
|---|---|---|---|---|
|0  |-  |-  |-  |no permissions  |
|1  |-  |-  |x  |only execute   |
|2  |-  |w  |-  |only write   |
|3  |-  |w  |x  |write and execute   |
|4  |r  |-  |-  |only read   |
|5  |r  |-  |x  |read and execute   |
|6  |r  |w  |-  |read and write   |
|7  |r  |w  |x  |read, write and execute   |
---------------------

This are different for the `user`, `group` and `others`, in that order, as seen on the following snippet:

```bash
tvillega@servername /var/lib ls -lha
total 60K
drwxr-xr-x 1 root         root         316 Feb  9 21:46 .
drwxr-xr-x 1 root         root         116 Apr 26 23:29 ..
drwxr-xr-x 1 root         root          24 Apr 27 00:41 alsa
drwxr-xr-x 1 root         root           0 May 27  2022 arpd
drwxr-xr-x 1 root         root          26 Jun 18  2022 blueman
drwx------ 1 root         root          34 Jun 18  2022 bluetooth
drwxr-xr-x 1 colord       colord        58 Jun 18  2022 colord
drwxr-xr-x 1 root         root          20 Jun 17  2022 dbus
drwxr-x--- 1 root         root         566 Apr 21 13:23 dhcpcd
drwxrwxrwt 1 root         root           0 May 10  2021 ex
drwx------ 1 root         root         242 Apr 27 19:55 iwd
```

## My (very much needed) lesson

I explained my situation on the help desk. I couldn't `ls` nor `rm` a directory inside my home directory and I needed a privileged user to give me the read permissions back. Here comes the funny part, I diagnosed wrong my issue. The sysadmin told me *"You have read permissions, what you don't have it's **execute permissions**. That's why you can't run any command on that path"*.

I've been a faithful Linux user since Windows told me I need to buy a new computer to "fix the issues", however I was socked to realize I didn't fully understand it. The sysadmin told me that as long as I am the owner of the file/directory I can change all of its permissions. I never thought of that. I just *used* the permissions, I never saw the significance about their innerworks.

That day I learned two things:

1. Ownership it's more important than permissions, at least without messing with ACL.
2. `u|g|o` are symbolic notations for `user|group|others` and edited appending `[+|-][rwx]`
3. `4|2|1` are octals for `read|write|execute` and combinated as seen [here](https://users.dcc.uchile.cl/~tvillega/posts/linux-file-permissions/#file-permissions-revisited)

There's also `umask`, something that I always forget and it breaks my `texlive` from time to time.
But hey! That's for another story!

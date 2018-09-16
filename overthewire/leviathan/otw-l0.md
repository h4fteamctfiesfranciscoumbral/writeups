Let's start off by connecting!

```sh
$ ssh leviathan0@leviathan.labs.overthewire.org -p 2223
```

Alright. Let's see what we're dealing with here.

```sh
leviathan0@leviathan:~$ ls
leviathan0@leviathan:~$ ls -a
.  ..  .backup  .bash_logout  .bashrc  .profile
leviathan0@leviathan:~$ cd .backup/
leviathan0@leviathan:~/.backup$ ls
bookmarks.html
```

We have an interesting directory called ".backup" that seems to be storing an
html file full of bookmarks.

Upon reading it, we realize that it's chock full of data. Most of this we don't
need. Let's see if we can use "grep" to filter only data we want.

```sh
leviathan0@leviathan:~/.backup$ grep "password" bookmarks.html 
<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is rioGegei8m" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```

Got it! rioGegei8m

# cgi-programming

### This repository is to explain a quick and simple 'out-of-the-box' solution with examples for getting started in cgi programming.

# Prerequisite Information

## What is cgi programming?
Apache says "The CGI (Common Gateway Interface) defines a way for a web server to interact with external content-generating programs, which are often referred to as CGI programs or CGI scripts. It is a simple way to put dynamic content on your web site, using whatever programming language you're most familiar with."

In laymans, you can use a programming language of your choosing to create web pages, and write behind the scenes scripts that are built in to your page. So this way you're not limited to Javascript or PHP. I like python.

## Why use it?
Some people have languages that they are very comfortable with, and cgi programming allows you to use that language when building the web.

## How to use it
1. Pick your language (I'll be using Python in the examples, should be transferrable mainly)
2. Make sure you have Apache server downloaded (I'm currently using the latest 2.4.33) and you know which directory it is in.
3. Find your httpd.conf file. For me, it is here 'C:\Apache24\conf\httpd.conf'
4. Search your httpd.conf for these code blocks, and change them to the new code blocks I've offered. Your default blocks might be slightly different if you're using a different Apache version:

Change

    Define SRVROOT "/Apache24"
    ServerRoot "${SRVROOT}"
    
To

    Define SRVROOT "C:/Apache24"
    ServerRoot "${SRVROOT}"
----

Make sure ScriptAlias is as follows:

    ScriptAlias /cgi-bin/ "${SRVROOT}/cgi-bin/"
----
Change

    <Directory "${SRVROOT}/cgi-bin">
        AllowOverride None
        Options None
        Require all granted
    </Directory>
To

    <Directory "${SRVROOT}/cgi-bin">
        AllowOverride None
        Options ExecCGI
        AddHandler cgi-script .py
        Require all granted
    </Directory>
Or at least make sure

    Options ExecCGI
    AddHandler cgi-script .py
is in there.

----

Make sure

    LoadModule cgi_module modules/mod_cgi.so
is uncommented.

That should be all the changes for the httpd.conf file!

5. Now you can create a cgi script and place it in the 'Apache24\cgi-bin\' folder. View the examples folder for cgi examples that I've found or made and that work for me!
6. Now you can navigate to <urlname>/cgi-bin/hello.py (where urlname is the url apache listens to in httpd.conf and hello.py is the cgi script located in the \cgi-bin\ folder).
7.Ta-da! That's all folks.
  
## Notes

- Apache can be a pain to compile and install. I use [ApacheHaus](https://www.apachehaus.com). You can also find a list of places to download apache pre-compiled (not pre-configured) for Windows [here.](https://httpd.apache.org/docs/current/platform/windows.html)

## Other Sources (not necessarily updated and working)

https://httpd.apache.org/docs/2.4/howto/cgi.html

http://www.tutorialspoint.com/python/python_cgi_programming.htm


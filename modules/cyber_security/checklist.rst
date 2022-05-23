Lil Checklist
=============

A simple checklist of things to do in certain situations

PNG file?
---------

Try `gem install zsteg`

https://github.com/zed-0xff/zsteg

.. code-block:: shell
    :linenos:

    zsteg -a <filename>.png

Web Page XSS
------------

Simple automated XSS https://xsshunter.com/


MD5 based file validation?
--------------------------

Here's a site providing two files with a collision.

https://www.mscs.dal.ca/~selinger/md5collision/

Web Exploitation
----------------

1. Check the source
2. Check the Cookies
3. Make some requests in burp. Play around

Extras
******

If given the ability to reset passwords based on the
current session, check in burp for id's and exploit IDOR.


When viewing source code, look at dependency version and
then try to find a CVE for it.


Look for CVE's for data conversions, data types, anything
ran agaisnt end user data.


Run https://ngrok.com/ locally, allows for easy forwarding n such.

Tools
-----

Exploit Tar|Zip directory traversal
*******************************

https://github.com/ptoomey3/evilarc

EVTX parser
***********

https://github.com/williballenthin/python-evtx

Online PowerShell execution
***************************

https://tio.run/#powershell

Deobfuscate JS
**************

http://jsnice.org/


Inspiration | Writeups
----------------------

- https://systemweakness.com/cyber-apocalypse-ctf-2022-hackthebox-2697c9463a73
- https://mukarramkhalid.com/hack-the-box-cyber-apocalypse-2022-writeups/
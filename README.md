February 2015

I set up per-user traffic monitoring using
[DD-WRT](http://www.dd-wrt.com/) a Netgear WNDR4000 that I got on Ebay
for $35. 

The code here adapts and improves
[the wrtbwmon code](https://code.google.com/p/wrtbwmon/), which
maintains a database that is updated periodically and recycled every
month. This is a nice package with a set of scripts that does just
want you want, querying usage periodically, finding what's changed,
dumping it to a database, allowing a division between "peak" and
"non-peak" hours, and generating a nice web page that can be view

This release contains a few changes I had to make to get it to work on
build 21676 of DD-WRT.

### Instructions

1.  Install DD-WRT

    I installed from the instructions
    [on this page](http://www.dd-wrt.com/wiki/index.php/Netgear_WNDR4000).
    I first flashed with
    [the DD-WRT 21676 release](ftp://ftp.dd-wrt.com/betas/2013/05-27-2013-r21676/broadcom_K26/dd-wrt.v24-21676_NEWD-2_K2.6_mini-WNDR4000.chk),
    then upgraded to
    [the mini build](ftp://ftp.dd-wrt.com/betas/2013/05-27-2013-r21676/broadcom_K26/dd-wrt.v24-21676_NEWD-2_K2.6_mini-nv64k.bin). I
    do not know why this has to be done in two steps, but the
    instructions suggest that it should be.

2.  Enable JFFS

    Log into the web interface and enable JFFS2 support on the
    administrator page (Administration → Management). This a permanent
    flash-based filesystem that will survive power cycles, but that
    you also do not want to write to too often. 
    
3.  Deploy this code

    These instructions are modified from those found on the
    [wrtbwmon deployment page](https://code.google.com/p/wrtbwmon/wiki/Deploying)
    
    Login to your router and install:
    
        cd /jffs
        wget ...
        cd wrtbwmon
    
4.  Create the crontab entries

    From what I could tell, the best way to create crontab entries is
    through the web interface. The entries you want are in the file
    `crontab` and, assuming you followed all the suggested path names,
    can just be cut-and-pasted there.

5.  Viewing 

    You can view the results [on this page](http://192.168.1.1/user/usage.html).

### Other pages

I found
[this page](http://blog.billsdon.com/2014/02/usage-details-dd-wrt-router/)
to be helpful for setup issues, even though I didn't end up using that
code. [This site](http://clevarme.blogspot.com/2011/12/getting-dd-wrt-on-netgear-n750-wndr4000.html)
might also be
useful. [Here](http://www.dd-wrt.com/wiki/index.php/Netgear_WNDR4000)
is the main DD-WRT page.

### Description of changes

From the `wrtbwmon` code, I had to make a few changes to get it to
read in the hostnames from the DHCP leases file. This pertains to
DD-WRT build 21676; I don't know whether it applies elsewhere. The git
history contains the change.

---
layout: post
title:  "Install Ubuntu13.04 Mac OSX dual boot on Macbook pro"
date:   2013-03-09 15:47:34
categories: ubuntu
---

waiting for long time, buy the Macbook Pro 13-inch. Although without Retina Display. but it's so cool. Apple's hardware really unusual. I wanna install ubuntu on it, come on…

Install rEFIt
------------

Download rEFIt from http://refit.sourceforge.net. The current release rEFIt 0.14 (6.5M Mac disk image).
double-click on the “rEFIt.mpkg” package. It's will ok. If everything went well, you’ll see the rEFIt boot menu on the next restart.

Partition on OSX
---------------

Use Disk Utility partition the free space. Select the left side Macintosh HD root node, select the Partition on the top Tab. Click the plus(+) symbal on the bottom, make it the size you want for Ubuntu, disk format selected free space.

Create a bootable USB stick OSX
------------------------------

Download the 64-bit Mac (AMD64) desktop image(e.g. raring-desktop-amd64.iso) from ubuntu offical website. Convert the .iso file to .img using the convert option of hdiutil (e.g.,hdiutil convert -format UDRW -o ~/Download/raring-desktop-amd64.img ~/Download/raring-desktop-amd64.iso)

Insert flash media, run diskutil list on terminal (e.g. /dev/disk2).

Execute shell `sudo dd if=~/Download/raring-desktop-amd64.img.dmg of=/dev/rdiskN bs=1m` (replace ~/Download/raring-desktop-amd64.img.dmg with the path where the image file is located).

Run shell diskutil eject /dev/diskN and remove your flash media when the command completes.

Install Ubuntu
---------------

Restart your Mac and press alt/option key while the Mac is restarting to choose the USB stick.
It's will launch ubuntu on flash media. select install ubuntu, selected free space on Macintosh HD, partition /boot / swap /home Will soon installed successfull

Install Wifi driver
------------------

run lspci in your favorite terminal, look for the Network controller(e.g. BCM4331). Now install b43 wireless driver.2
Install b43 driver


{% highlight bash %}
      sudo add-apt-repository ppa:mpodroid/mactel
      sudo apt-get update
      sudo apt-get install b43-fwcutter firmware-b43-installer
{% endhighlight %}

Add line blacklist ndiswrapper to file /etc/modprobe.d/blacklist.conf
Create or edit the file /etc/pm/config.d/modules, content SUSPEND_MODULES="b43 bcma"
but failed. now install wl driver sudo apt-get install bcmwl-kernel-source

Config the keyboard
-----------------

Keyboard Layout -> Options… -> Alt/Win key behavior, selected Left Alt is swapped with Left Win

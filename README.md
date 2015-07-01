VPS2Void
========

The fastest way to convert a _VPS_ to [Void Linux](https://www.voidlinux.eu/)!

Author
------

[Kevin Berry](mailto:kevin@opensourcealchemist.com)
Based on the excellent vps2arch script by [Timothy Redaelli](mailto:tredaelli@archlinux.info)

Description
-----------

This script is used to convert a _VPS_, running another linux distro, to _Void Linux_.  
It should be **only** used if your _VPS_ provider doesn't provide you an _Void Linux_ image.

Disclaimer
----------

> I'm not responsible for any damage in your system and/or any violation of the agreement between you and your vps provider.  
> **Use at your own risk!**

How To
------

Download the script on your _VPS_ and execute it with root privileges

**WARNING** The script will **delete** any data in your _VPS_!

	wget http://git.io/vps2void
	chmod +x vps2void
	./vps2void

How does it work?
-----------------

It's Black Magic.
Just kiddin' 😏, the script itself is very simple.

In a nutshell, it will download the _base-voidstrap package_ and
extract the image to / and configure the _Bootstrap chroot_.

Now, about the **critical** part:

> How can you wipe the system without breaking everything?

It's simple: using `ld.so` from the _Bootstrap chroot_ to launch the `chroot` tool.

Since it will erase all the system directories except from the _Bootstrap chroot_, `/dev`, `/proc`, `/sys` and the like,
the only way to launch a command inside the _Bootstrap chroot_ is to using ld.so from the _Bootstrap chroot_ itself.

At this point _Void Linux_ has been installed, but not configured.
The script will provide a SSH-able system automagically configuring grub (or syslinux), network and restoring the root password from the original system (or by using `vps2void` as password if no root password was set).

Once done doing its job, the script will ask you to manually reboot your _VPS_ and voilà, PROFIT!

Does it really work?
--------------------

Almost.  I'm testing it on DigitalOcean presently, and will probably work it on Linode next.  I'm using Debian 7.0 as the base, so as to avoid all the systemd insanity.

On the [Tested VPS Providers](https://github.com/drizzt/vps2void/wiki/Tested-VPS-Providers) wiki page you can find a list of **Tested VPS Providers**.

Theoretically it should also work on **real** computers (running linux), but I think it's not worth it,
because you can install it in the canonical way.

Contributing
------------

If you have any useful modification, please use **Pull requests**.  
If you have successfully used this script on a different _distro_ - _VPS_ combination, please contact me so that I can update the above list.

If you are not a developer, but you still want to contribute, you can donate me an account on your _VPS_ provider and I'll do my best to support it.  
Or you can just donate me some bucks I'll spend to buy a _VPS_ on your provider in order to support it.

Caveats
-------

Networking is net configured, so please make sure to configure it before you reboot!

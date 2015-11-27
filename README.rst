lamby-ansible-router
====================

Failsafe mode
-------------

 * When "WPS/RESET" button lights, move the "3G/4G/WISP/AP" switch back and
   forth until the light flashes fast.

 * Connect ethernet with a static configuration:

     $ sudo ip addr add 192.168.1.2 dev eth0
     $ sudo ip route add 192.168.1.0/24 dev eth0

 * ``telnet 192.168.1.1``

 * ``mount_root``

 * ``mtd -r erase rootfs_data``

 * The device will reboot.

 * Reconnect ethernet via DHCP.

 * ``telnet 192.168.1.1``

 * ``passwd``

 * ``ssh-copy-id root@192.168.1.1``

More info here: https://wiki.openwrt.org/doc/howto/generic.failsafe


Raw commands
------------

Should work::

  ansible '*' -i hosts -u root -m raw -v -a 'ls /etc'

... but I think it's relying on SCP?

ANSIBLE_SCP_IF_SSH=1 needed.

No Python so no templating?


Links
-----

 * https://github.com/lefant/ansible-openwrt

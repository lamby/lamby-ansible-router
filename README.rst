lamby-ansible-router
====================

Notes
-----

Replace apostrophe's in SSID names with '\''

Failsafe mode
-------------

More info here: https://wiki.openwrt.org/doc/howto/generic.failsafe

 * When "WPS/RESET" button lights, move the "3G/4G/WISP/AP" switch back and
   forth until the light flashes fast.

 * Connect ethernet with a static configuration:

     * ``ip addr add 192.168.1.2 dev eth0``

     * ``ip route add 192.168.1.0/24 dev eth0``

 * ``telnet 192.168.1.1``

    * ``mount_root``

    * ``mtd -r erase rootfs_data``

 * The device will reboot.

 * Reconnect ethernet via DHCP::

   * ``dhclient eth0``

 * ``telnet 192.168.1.1``

    * ``passwd``

    * ``sed -i -e 's@192.168.1.1@192.168.2.1@g' /etc/config/network``

    * ``/etc/init.d/network restart``

 * Reconnect ethernet again via DHCP as we changed IP range::

   * ``dhclient eth0``

 * ``ssh-keygen -f "/home/lamby/.ssh/known_hosts" -R 192.168.2.1``

 * ``ssh root@192.168.2.1 'cat >> /etc/dropbear/authorized_keys && chmod 0600 /etc/dropbear/authorized_keys && chmod 0700 /etc/dropbear' < ~/.ssh/id_rsa.pub``

 * ``./apply``

 * ``ssh root@192.168.2.1``

 * ``opkg update``

 * ``opkg install kmod-rtl8192cu``

 * http://192.168.2.1/


Firmware images
---------------

 * http://downloads.openwrt.org/chaos_calmer/15.05/ar71xx/generic/openwrt-15.05-ar71xx-generic-tl-mr3020-v1-squashfs-factory.bin
 * http://downloads.openwrt.org/chaos_calmer/15.05/ar71xx/generic/openwrt-15.05-ar71xx-generic-tl-mr3020-v1-squashfs-sysupgrade.bin


Links
-----

 * https://github.com/lefant/ansible-openwrt
 * http://blog.philippklaus.de/2012/03/openwrt-on-a-tp-link-tl-mr3020-router/
 * https://dev.openwrt.org/ticket/12000

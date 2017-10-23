What we're doing here (see files in `setup`):

We're setting up Ubuntu 10.04 32bit and 64bit
LXC containers so that they:

1) are bridged directly to the host network which
in turn is bridged to the VBox interface and so they
get an IP via DHCP.

2) have host's luapower dir bind-mounted, which is
itself vboxfs-mounted from Windows.

HOWTO:

0. set the VM's network interface to Promiscuous
mode in VBox settings otherwise this will not work!

1. run ./lxc-create to create the two containers.

2. in /etc/network/interfaces we're adding a bridge
in which we add eth0. the bridge gets eth0's mac
so it gets the same ip as eth0 through dhcp.

3. in /var/lib/lxc/*/config we're setting the link
to br0 and eth0's ip to 0.0.0.0 which means dhcp.

4. in /etc/default/lxc we're disabling the LXC bridge.

5. you can now disable lxc-net with:

    sudo update-rc.d -f lxc-net remove

6. in /var/lib/lxc/*/fstab we're bind-mounting the
luapower dir from /home/cosmin.


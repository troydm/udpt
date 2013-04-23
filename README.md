UDPT - lightweight torrent tracker for linux.

This is a slightly modified experimental UDPT version
Original version is at [http://code.google.com/p/udpt/][1]

This modified version contains following changes:

    1. Running as linux/unix daemon
    2. Advertinsing local peers and remote peers seperately
    3. Some minor bug fixes

The main difference of this version of UDPT to an original is
the ability to run this torrent tracker inside a local network
and act as both local and remote network torrent tracker

## Use case:

For example your local subnet is 192.168.0.x and your remote ip 
for this network is 192.168.1.1. You run this torrent tracker on 192.168.0.1
and your torrent client that is seeding your torrent file is running on 192.168.0.2:12345 
Your router port forwards 192.168.1.1:12345 to your local network 192.168.0.2:12345 port (note: port should be the same)

Now let's consider two seperate leecher peer situations:
#### Local leecher 
Leecher running on 192.168.0.3 connects to your tracker from inside your network
Leecher gets one seeder peer on his announce containing local network address of 192.168.0.2:12345 and successfully downloads your torrent

#### Remote leecher 
Leecher is running on 192.168.1.2 on remote network and connects to your tracker through port forwarding on your router
Tracker sees that peer that is trying to get announce for local network peer is not running on local network so tracker subsitutes your local network
ip with an remote ip address specified in your configuration
Leecher gets one seeder peer on his announce containing remote networkd address of 192.168.1.1:12345 instead of 192.168.0.2:12345 
which is correct remote peer address and successfully downloads your torrent

Licensed under GNU GPLv3.
The license file is attached under the name gpl.txt.

Compiling under linux or linux environment (MinGW):

For Linux:
$ make linux

Running:
$ ./udpt [udpt.conf]

Running as daemon:
$ ./udpt -d [udpt.log] [udpt.conf]

Cleaning:
$ make clean

This software currently uses the Sqlite3 Library (public domain).

Developed by Naim A. <naim94a@gmail.com>.
Modified by Dmitry Geurkov <d.geurkov@gmail.com>.

[1]: http://code.google.com/p/udpt/

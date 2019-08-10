Sample init scripts and service configuration for magmelldollard
==========================================================

Sample scripts and configuration files for systemd, Upstart and OpenRC
can be found in the contrib/init folder.

    contrib/init/magmelldollard.service:    systemd service unit configuration
    contrib/init/magmelldollard.openrc:     OpenRC compatible SysV style init script
    contrib/init/magmelldollard.openrcconf: OpenRC conf.d file
    contrib/init/magmelldollard.conf:       Upstart service configuration file
    contrib/init/magmelldollard.init:       CentOS compatible SysV style init script

1. Service User
---------------------------------

All three Linux startup configurations assume the existence of a "magmelldollar" user
and group.  They must be created before attempting to use these scripts.
The OS X configuration assumes magmelldollard will be set up for the current user.

2. Configuration
---------------------------------

At a bare minimum, magmelldollard requires that the rpcpassword setting be set
when running as a daemon.  If the configuration file does not exist or this
setting is not set, magmelldollard will shutdown promptly after startup.

This password does not have to be remembered or typed as it is mostly used
as a fixed token that magmelldollard and client programs read from the configuration
file, however it is recommended that a strong and secure password be used
as this password is security critical to securing the wallet should the
wallet be enabled.

If magmelldollard is run with the "-server" flag (set by default), and no rpcpassword is set,
it will use a special cookie file for authentication. The cookie is generated with random
content when the daemon starts, and deleted when it exits. Read access to this file
controls who can access it through RPC.

By default the cookie is stored in the data directory, but it's location can be overridden
with the option '-rpccookiefile'.

This allows for running magmelldollard without having to do any manual configuration.

`conf`, `pid`, and `wallet` accept relative paths which are interpreted as
relative to the data directory. `wallet` *only* supports relative paths.

For an example configuration file that describes the configuration settings,
see `contrib/debian/examples/magmelldollar.conf`.

3. Paths
---------------------------------

3a) Linux

All three configurations assume several paths that might need to be adjusted.

Binary:              `/usr/bin/magmelldollard`  
Configuration file:  `/etc/magmelldollar/magmelldollar.conf`  
Data directory:      `/var/lib/magmelldollard`  
PID file:            `/var/run/magmelldollard/magmelldollard.pid` (OpenRC and Upstart) or `/var/lib/magmelldollard/magmelldollard.pid` (systemd)  
Lock file:           `/var/lock/subsys/magmelldollard` (CentOS)  

The configuration file, PID directory (if applicable) and data directory
should all be owned by the magmelldollar user and group.  It is advised for security
reasons to make the configuration file and data directory only readable by the
magmelldollar user and group.  Access to magmelldollar-cli and other magmelldollard rpc clients
can then be controlled by group membership.

3b) Mac OS X

Binary:              `/usr/local/bin/magmelldollard`  
Configuration file:  `~/Library/Application Support/Magmelldollar/magmelldollar.conf`  
Data directory:      `~/Library/Application Support/Magmelldollar`
Lock file:           `~/Library/Application Support/Magmelldollar/.lock`

4. Installing Service Configuration
-----------------------------------

4a) systemd

Installing this .service file consists of just copying it to
/usr/lib/systemd/system directory, followed by the command
`systemctl daemon-reload` in order to update running systemd configuration.

To test, run `systemctl start magmelldollard` and to enable for system startup run
`systemctl enable magmelldollard`

4b) OpenRC

Rename magmelldollard.openrc to magmelldollard and drop it in /etc/init.d.  Double
check ownership and permissions and make it executable.  Test it with
`/etc/init.d/magmelldollard start` and configure it to run on startup with
`rc-update add magmelldollard`

4c) Upstart (for Debian/Ubuntu based distributions)

Drop magmelldollard.conf in /etc/init.  Test by running `service magmelldollard start`
it will automatically start on reboot.

NOTE: This script is incompatible with CentOS 5 and Amazon Linux 2014 as they
use old versions of Upstart and do not supply the start-stop-daemon utility.

4d) CentOS

Copy magmelldollard.init to /etc/init.d/magmelldollard. Test by running `service magmelldollard start`.

Using this script, you can adjust the path and flags to the magmelldollard program by
setting the BITCOIND and FLAGS environment variables in the file
/etc/sysconfig/magmelldollard. You can also use the DAEMONOPTS environment variable here.

4e) Mac OS X

Copy org.magmelldollar.magmelldollard.plist into ~/Library/LaunchAgents. Load the launch agent by
running `launchctl load ~/Library/LaunchAgents/org.magmelldollar.magmelldollard.plist`.

This Launch Agent will cause magmelldollard to start whenever the user logs in.

NOTE: This approach is intended for those wanting to run magmelldollard as the current user.
You will need to modify org.magmelldollar.magmelldollard.plist if you intend to use it as a
Launch Daemon with a dedicated magmelldollar user.

5. Auto-respawn
-----------------------------------

Auto respawning is currently only configured for Upstart and systemd.
Reasonable defaults have been chosen but YMMV.

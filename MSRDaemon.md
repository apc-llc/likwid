# Introduction #

Because of the security problems with
read and writable msr device files likwid supports
now a daemon solution for use in security sensitive
areas as computing centers, companies or HPC clusters. This is required if you want to access the Uncore on recent Intel Server processors which is implemented by means of PCI devices.

# Basics #

The idea is that not all of likwid runs with privileges
but only the part which needs them, the msr read and write routines.

The likwid applications needing read/write access to msr registers
(likwid-perfctr and likwid-features) will start a daemon in their startup.
Only this daemon has access to the msr device files. Communication
between the likwid application and the daemon is implemented with
UNIX domain sockets. During exit of the application the daemon is terminated.
This enables a secure setup for the msr access without complicating things for the user.
Of course some  overhead is introduced against the direct version.

# Enable and Build #

To enable the communication with the daemon the variable 'ACCESSDAEMON' in config.mk
has to be set to a valid absolute path to the likwid-accessD executable.

To access daemon is no always build.
The executable will be in the likwid root directory. The standard `make install` target will
install the daemon with the other tools. If you specified a custom location you have to copy the daemon executable by hand. The daemon executable must have access to the msr device files.

Two scenarios are possible for configuration:

  * You set the daemon setuid root. This is the easiest way.
  * You set the daemon setgid to some perfctr group which has access rights on the msr device files.

For access to the PCI device files the daemon **must** be setuid root enabled.

# Protocol #

Every likwid instance will start its own daemon. This client-server pair will communicate
with a socket file in /tmp named likwid-PID . The daemon only accepts one connection. As soon as the connect is successful the socket file will be deleted.

From there the communication consists of write read pairs issued from the client.
The daemon will ensure allowed register ranges relevant for the likwid applications.
Other register access will be silently dropped and logged to /var/log/user.

On shutdown the client will terminate the daemon with a exit message.

The daemon has the following error handling:

  * To prevent daemons not stopped correctly the daemon has a timeout on startup.
  * If the client prematurely disconnects the daemon terminates.
  * If the client disconnects between a read and write the daemon catches SIGPIPE and disconnects.

# Known issues #


# Logging #

The msrD daemon will log its errors to syslog with USER events.
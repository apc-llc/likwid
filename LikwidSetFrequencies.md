

# Introduction #
Often systems are configured to use as little power as needed and therefore reduce the clock frequency of single cores. For benchmarking purpose, it is important to have a defined environment where all CPU cores work at the same speed. The operation is commonly only allowed to priviledged users since it may interfer with the needs of other users.

Starting with LIKWID version 3.1.2 we included a daemon and control script to change the frequency and scaling governor of affinity regions. All operations that require only readable access to the control files in sysfs are implemented in the script. Only the writable access is forbidden for normal users and requires a more priviledged daemon.


# Options #

```
-h          : this (help) message
-p          : print current frequencies
-l          : list available frequencies
-c domain   : likwid thread domain which to apply settings
              (set to N if omitted)
-g governor : set governor (ondemand, performance, turbo)
              (set to ondemand if omitted)
-f frequency: set fixed frequency, implicitly sets userspace
              governo
```

# Usage #

At first, you need to know the available frequencies for your CPU cores:
```
likwid-setFrequencies -l
```

In order to see which CPU core has which frequency:
```
likwid-setFrequencies -p
```

When you know a valid frequency for a range of CPU cores you can set them:
```
likwid-setFrequencies -c S0 -f 3.4
```
This sets all CPU cores of socket 0 to a frequency of 3.4 GHz. If the scaling governor of core 0 was something other than **userspace**, it is automatically set to **userspace**. If the -c is omitted, the whole Node (affinity domain N) is assumed, thus all cores are set to the frequency.

You can also change only the governor of an affinity domain. The common governors are **performance** (setting the core to the maximal frequency and eventually enable Turbo mode where SMT threads are deactivated) and **ondemand** (scales the frequency of the CPU core regarding the current workload of the CPU, commonly used to save energy).
```
likwid-setFrequencies -c C0 -g performance
```
Sets the scaling governor of all CPU cores in the cache group 0 to the performance governor. In order to get all affinity domains that are supported by the system, you can use the `likwid-pin` tool:
```
likwid-pin -p
```
Prints all available affinity domains, see LikwidPin Wiki page.

# Configuration of the setFreq daemon #

Since the daemon process `likwid-setFreq` requires higher priviledges than the control script `likwid-setFrequency`. There are two methods to grant this to the daemon:

## setuid root ##

The common way is to set suid permission bit for the daemon process. The daemon process is executed not with the uid of the caller anymore, but the uid ist changed to the root uid before execution. There exist some default GNU tools that are configured like this like `su` or `(un)mount`. You have to change to user/owner of the daemon process and set the suid bit:

```
sudo chown root:root likwid-setFreq
sudo chmod u+s likwid-setFreq
```

## capabilities ##

Since the Linux kernel 2.6.24 most file systems support the storing of capability flags besides executables. There exist a bunch of flags that give administrator a fine grained management option for risky executables. There are advantages and also disadvantages when using capabilites. The main advantages are that the process is still executed with the uid of the caller and only the rights that are needed by the processes can be granted. As a disadvantage, the Linux kernel needs to be compiled with special config options to enable the storing of capability flags in the file system. Additionally not all file system seem to support that feature. In order to make the daemon work with capability flags:

```
sudo chmod 0666 /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
sudo chmod 0666 /sys/devices/system/cpu/cpu*/cpufreq/scaling_setspeed
sudo setcap cap_sys_rawio+ep likwid-setFreq
```

This enables the daemon until the next reboot. In order to make the permissions persistent, you can use the udev system:

```
cat > /etc/udev/rules.d/99-persistent-setFreq.rules <<EOF
> KERNEL=="cpu*", RUN+="/bin/chmod 0666 /sys/devices/system/cpu/cpu%n/cpufreq/scaling_governor"
> KERNEL=="cpu*", RUN+="/bin/chmod 0666 /sys/devices/system/cpu/cpu%n/cpufreq/scaling_setspeed"
> EOF
```
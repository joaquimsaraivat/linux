# Kernel Compiling

### Obtain a kernel from source
wget https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.14.12.tar.xz
tar -xvpf linux-4.14.12.tar.xz
cd linux-4.14.12

### After download and extracting it
When compiling a kernel there are several configuration options to choose from. Sometimes, the best option is coping the config file existing in the target machine when compiling from it. There are, however several options to choose from:

- make config: Text based configuration. The options are prompted one after another. All options need to be answered, and out-of-order access to former options is not possible.
- make menuconfig: An ncurses-based pseudo-graphical menu (only text input). Navigate through the menu to modify the desired options.
- make defconfig: Generates a new config with default from the ARCH supplied defconfig file. Use this option to get back the default configuration file that came with the sources.
- make nconfig: Pseudo-graphical menu based on ncurses. Requires sys-libs/ncurses to be installed.
- make xconfig: Graphical menu using Qt5. Requires dev-qt/qtwidgets to be installed.
- make gconfig: Graphical menu using GTK. Requires x11-libs/gtk+, dev-libs/glib, and gnome-base/libglade to be installed.
- make oldconfig: Review changes between kernel versions and update to create a new .config for the kernel.
- make olddefconfig: Generates a new configuration with default values from the ARCH supplied defconfig file while, at the same time, maintaining all the previous options set in the .config file found at /usr/src/linux/.config. This is a fast and safe method for upgrading a config file that has all the configuration options it needs for hardware support while at the same time gaining bug fixes and security patches.
- make allyesconfig: Enables all configuration options in the kernel. It will set all kernel options to *. Make sure a backup of the current kernel configuration is acquired before using this option!
- make allmodconfig: Enables all modules in kernel

[source](https://wiki.gentoo.org/wiki/Kernel/Configuration)
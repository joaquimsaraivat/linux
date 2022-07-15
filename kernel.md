# Kernel Compiling

## Obtain a kernel from source

Go to [kernel.org](https://kernel.org)

Donwload the version you wish

wget [url]

tar -xvpf linux-version.tar.xz

cd linux-version

## After download and extracting it

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

## Compiling the kernel

After all the configurations are defined, we can start compiling the kernel.

First, get the number of cores your system has available

<code>cat /proc/cpuinfo | grep processor | wc -l</code>

When that has been defined, choose how many cores you want to use, in this example, four cores are being used.

make -j4 bzImage

When this is done, you need to compile the modules for this kernel

make -j4 modules

When they are done you can then installed them:

make modules_install

When all this is done, these commands should be executed.

cp arch/x86/boot/bzImage /boot/vmlinuz-generic-version

cp System.map /boot/System.map-generic-version

cp .config /boot/config-generic-version

cd /boot

rm -rf config System.map vmlinuz

ln -sf vmlinuz-fusion-4.19.232 vmlinuz

ln -s System.map-generic-version System.map

ln -s config-generic-version config

## Bootloader

### Lilo

If you are using lilo as bootloader, you should run, at the end of the process the following command

lilo

## Initrd.img

You can use an initrd.img in order to make the computer boot faster, in the case of slackware, there is a special tool that facilitates the operation

/usr/share/mkinitrd/mkinitrd_command_generator.sh -k 4.14.12

After running, copy and run the command that has been generated for you

## Some problems

### Compiler version

Sometimes the compiler is not up to date to the needs. In order to make this process easier you can use this:

https://gist.github.com/jeetsukumaran/5224956#file-build-gcc-sh-L11

The compiler is installed in the folder /platform/

### Compiling the kernel in one machine and installing in another

After the command:

make -j4 modules

Exit the folder

cd ..

Compress the folder

tar -zcvf archive_name.tar.gz folder_to_compress

and the send the compress archive to the destination, extract and proceded with the next steps.

## Sources

https://wiki.linuxquestions.org/wiki/How_to_build_and_install_your_own_Linux_kernel

http://web.mit.edu/linux/redhat/redhat-4.2/i386/doc/rhmanual/doc037.html

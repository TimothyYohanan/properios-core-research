## v0.0.1
### Features:
- A bare live-build project with a few additional items related to project set-up.

### Steps:
1. Ran '$ lb config' in the project root directory to create the live-build folder structure.
    - See Reference 1 - "4.3 First steps: building an ISO hybrid image".
2. Created the following additional files in the project root directory:
    - .gitignore
    - CHANGELOG.md
    - README.md
3. Configured the '$ lb config' command at /auto/config
    - See Reference 2
4. Configured the '$ lb clean' command at /auto/clean
    - See Reference 3
5. Created a 'scripts' directory for additional scripts
6. Created an 'install-dependencies' script in the 'scripts' directory.
    - This script will also perform various verifications to ensure that the system that it is run on can sucessfully build the project.

### Comments:
1. In /auto/config, '--firmware-chroot' is disabled. However, for various device drivers (i.e. wifi cards), this should be enabled.
2. In /auto/config, the 'non-free' and 'non-free-firmware' repositories are not included in '--archive-areas' and '--parent-archive-areas.' However, for various device drivers (i.e. graphics cards), these should be enabled.

### References:
1. https://live-team.pages.debian.net/live-manual/html/live-manual/index.en.html
2. https://manpages.debian.org/bookworm/live-build/lb_config.1.en.html
3. https://manpages.debian.org/bookworm/live-build/lb_clean.1.en.html

## v0.0.2
### Features:
1. The root user account is secured using a PIV Smart Card.
2. Creating new accounts requires authentication from the root user.
3. Changing the password on any account requires authentication from the root user.
4. Implements Properios Core Specification v1.0.0
    - The properios-core-specification git repository is included as a submodule in this project
        - Location on built system: /root/properios-core-specification 
        - Location within project directory: config/includes.chroot_after_packages/root/properios-core-specification
    - properios-core-specification contains a design specification file. That file *is* the authoritative design specification for properios-core.
    - properios-core-specification contains an example test script. When executed, that test script will determine whether the host system meets the design specification or not. 
        - For convenience, the root user can execute this script from any directory simply by executing the command '\$ test-system-against-design-spec'.

### Comments:
1. The PKCS-11 PAM module (a.k.a. the 'libpam-pkcs11' apt package) is well documented. 
    - See Reference 1.

### References:
1. https://opensc.github.io/pam_pkcs11/doc/pam_pkcs11.html 

## v0.0.3
### *Implements Properios Core Specification v2.0.0*
### Features:
1. The Debian kernel packages used in the project are now built from source with *minimal* modifications compared to the standard Debian Bookworm kernel.
    - Enabled 'CONFIG_IKCONFIG' to embed the .config file used to build the kernel within the bootable kernel image [a.k.a. /boot/vmlinuz-$(uname -r)]. This allows testing whether specific kernel settings mentioned in the Properios Specification(s) have been implemented according to the specification(s).
    - See Comment 4 and 5.

### Comments:
1. Shell scripts that are used by the '$ lb' command are located at /usr/lib/live/build on Debian systems which have the package installed.
2. When you examine the packages on the built system, you'll realize that the cleanup that I did in the '0002-remove-other-kernels.hook.chroot' hook was not complete. For research purposes, that is okay (I really could have left in the unused kernel package as well).
    $ dpkg -l | grep linux
3. The output of the '$ uname -r' command is now going to report the "prisine" Linux kernel version rather than the Debian kernel version since the kernel is being built from source. As of the time of writing, the "pristine" kernel version being used here is only a few days out of date compared to the one that is used in the Debian kernel, however, you wouldn't immediately realize this if you ran the aforementioned command on this version of properios-core-research and the previous version (or even the latest version of Debian Bookworm at the time of writing) and compared the outputs.
4. I've observed that the .config file provided on a Debian Live system built with the '$ lb' command builds the debug symbols package even if the host system (the Debian Live system which the .config file is gleaned from from) doesn't have the debug symbols package installed. I hope that there are no other differences between the provided .config and the kernel package, and indeed, it would make sense for only this difference to exist, but I am not certain of this. For my purposes this does not matter, but I considered it worth notating.
5. In the .config used in this project, building the debug symbols package (the 'linux-image' .deb package with the '-dbg' flag in its name) has been disabled to improve build speed, and also to decrease the final image size. To re-enable it, change the following settings using the GUI configurator during step 000005-configure-kernel:
   - Kernel hacking ---> Compile-time checks and compiler options ---> [*] Miscellaneous debug code
   - Kernel hacking ---> Compile-time checks and compiler options ---> Debug information (Rely on the toolchain's implicit default DWARF version) ---> (X) Rely on the toolchain's implicit default DWARF version
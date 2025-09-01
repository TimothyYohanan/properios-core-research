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
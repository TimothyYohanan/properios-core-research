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

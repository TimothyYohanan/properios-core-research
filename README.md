### Usage
    This repository has submodules. When you clone it, you need to use the '--recursive' flag so that they are also cloned:
    $ git clone --recursive <repo-url>

    Once you have the repository and its submodules, update the settings file if needed, then:
    $ su - root
    $ cd /path/to/project/directory
    $ ./scripts/install-dependencies
    $ lb config
    $ lb build
    $ exit

### Comments
The live-build tool offered by Debian, which I have utilized in this project, is a great one for consisely expressing a customized Debian-based system. In this project, I'm using it to sketch out the specification for a Linux system which ultimately may not be Debian-based.
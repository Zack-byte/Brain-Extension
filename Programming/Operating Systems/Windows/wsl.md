# Windows Subsystem For Linux (WSL)
Windows Subsystem for Linux lets developers run a GNU/Linux environment -- including most command-line tools, utilities, and application -- directly on Windows, unmodified, without the overhead of traditional virtual machine or dual boot setup. 

With WSL you can:
- Work with your favorite GNU/Linux distros
- Run cmd line tools such as `grep`, `sed`, `awk` or other ELF-64 binaries.
- Run Bash shell scripts and GNU/Linux command-line applications including:
  - Vim, emacs, tmux
  - Languages: NodeJS, Javascript, Python, Ruby, etc...
  - Services: SSHD, MySql, Apache, lightpd, MongoDB, PostgreSQL
- Install additional software using your own GNU/Linux distribution package manager.
- Invoke Windows applications using a Unix-like command-line shell
- Invoke GNU/Linux applications on Windows
- Run GNU/Linux graphical applications integrated directly to your Windows desktop
- Use GPU acceleration for machine learning, data science scenarios and more

## WSL 2
Windows Subsystem for Linux 2 is a new version of the WSL architecture that powers the WSL to run ELF64 binaries on Windows. Its primary goals are to increase file system performance, as well as adding full system call compatibility.

This new architecture changes how these Linux binaries interact with Windows on your computer's hardware, but still provides the same user experience as WSL 1.

Individual Linux distros can be run with either architecture. Each distro can be upgraded or downgraded at any time and you can run WSL 1 and 2 distros side by side. WSL 2 uses an entirely new architecture that benefits from running a real Linux kernel.

## Installing WSL
It's pretty easy to get started. First open a terminal (Powershell, cmd Prompt, etc...) and run this
```Powershell
wsl --install 
```

This enables the features necessary to run WSL and install the Ubuntu distribution of Linux. (The default can be configured).

The first time your launch a newly installed Linux distribution, a console window will open and you'll be asked to wait for files to de-compress and be stored on your machine. All future launches should take less than a second.

### Already Installed?
- If you run the above command and help text is written in the console then WSL is **ALREADY** installed and you can check which linux distros are installed by using
```powershell
# check for locally installed distros
wsl --list

# check for online distros
wsl --list online

# install distro by name
wsl install -d ubuntu
```

## Setup Linux User Info
Once WSL is installed you need to setup a user account and password follow <a src="https://docs.microsoft.com/en-us/windows/wsl/setup/environment">these best practices</a> in the microsoft documentation if desired.


```powershell
# check wsl version
wsl -l -v

# set default wsl verions
wsl --set-default-version <Version#>

# set default distribution
wsl --setdefault <DistributionName>
```
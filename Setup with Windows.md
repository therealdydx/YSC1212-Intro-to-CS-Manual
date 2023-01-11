# Setup with Windows

Because OCaml + Emacs does not work well on Windows, I will use WSL2 instead to run.

The instructions are as follows:

1. Setting up Ubuntu on Windows 10
2. Installing Graphical Shell on Windows 10
3. Installing Emacs on Ubuntu
4. Installing OCaml and Tuareg on Ubuntu
5. Setting up (If Emacs doesn't show on next boot)



### Setting Ubuntu on Windows

This is for Windows users that have not set up Ubuntu yet. If done so / other OS, ignore this.

To install Ubuntu on Windows, you would first need to setup WSL2. Refer to this [Windows Guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10) for a comprehensive guide on installing and setting up WSL2.

In short:

1. Enable WSL

Open PowerShell as Administrator and run:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

2. Enable Virtual Machine (VM) feature

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

3. Restart your computer to complete WSL install

4. Download Linux Kernel update

Please refer to this [download link](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi) or the link on the Windows Guide above for the download. 

Once done, it is time to setup WSL2 as your default version when installing new Linux distributions.

5. Set WSL2 as your default version

Now open PowerShell and run this command to set WSL2 as the default version.

```powershell
wsl --set-default-version 2
```

6. Install Ubuntu

Now open Microsoft Store and type in Ubuntu on the search bar. You can then download Ubuntu from there. After installing Ubuntu, a console window will open and you will need to create a user account and password for your new Linux distribution.

7. Install Windows Terminal

Download [Windows Terminal](https://docs.microsoft.com/en-us/windows/terminal/get-started).

Now open Windows Terminal, and create a new tab for Ubuntu. Now you are able to access WSL2 Ubuntu from your Windows Terminal, and we may move on to installing Emacs and OCaml on WSL2.



### Install Graphical Shell

Download VcxSrv from this [link](https://sourceforge.net/projects/vcxsrv/). Go to your Windows Defender Firewall, and enable VcxSrv to be enabled on private and public connections. Make sure it has been enabled to inbound and outbound connections.

Now install xfce-session back on your Ubuntu with the command:

```bash
sudo apt install xfce4-session
```

(2023-Jan-10 Update) If it doesn't work, run this command first before installing xfce-session

```sudo apt update
sudo apt upgrade
```

(2023-Jan-10 update) Also have heard that there's no option for gdm3 anymore - so can ignore below if it doesn't show!
(Thanks Si Min for the pointers!)

Select gdm3 when prompted during the download process for X Server.

Install gedit for testing:

```bash
sudo apt install gedit
```

Now change directory to etc, with the following line:

```bash
cat /etc/resolv.conf
```

Record the IP address at the bottom, the name server. 

Now add the following code to your bash file (I have used a random IP Address):

```bash
nano ~/.bashrc
export DISPLAY=172.26.192.1:0.0
export LIBGL_ALWAYS_INDIRECT=1
```

Whenever you need to launch Emacs, just type XLaunch in your search, and launch the application. When launching XLaunch, select:

1. Multiple Windows
2. Check all in the Extra Settings, including Disable Access Control
3. Run your apps



### Install Emacs on Ubuntu

Very simple, simply run the command:

```bash
sudo apt install emacs
```

Going back to Prof Danvy's notes, we need to configure our Emacs. Quoting Prof Danvy, after installing Emacs, one should configure it by adding the following to one’s .emacs file which is the user configuration file for Emacs. 

Firstly, run Emacs with the following command on your terminal:

```bash
emacs
```

Now, Emacs should be open on your computer. To this end,

1. press the control key and type `x` (i.e., `C-x`),
2. press the control key and type `f` (i.e., `C-f`),
3. type exactly `~/.emacs`, and
4. press the return key (the one written “enter” on the keyboard).

This maneuver will open up the .emacs file, which is most likely empty. Paste the following code into the buffer by pressing `C-y`:

```
(setq inhibit-startup-message t)  ; dont show the GNU splash screen
(transient-mark-mode t)           ; show selection from mark
(setq visible-bell 1)             ; turn off bip warnings
(show-paren-mode t)               ; turn on highlight paren mode
(fset 'yes-or-no-p 'y-or-n-p)     ; use y and n for questions
(global-font-lock-mode t)         ; enable syntax highlighting
(icomplete-mode 99)               ; better buffer switching
```

Now save the .emacs file by

1. pressing the control key and typing `x` (i.e., `C-x`), and
2. pressing the control key and typing `s` (i.e., `C-s`).

To quit Emacs after finishing, type C-z (control-Z).



### Install OCaml Dependencies + Tuareg on Ubuntu

Now you are back to the terminal from Emacs, after quitting. It is time to install the OCaml dependencies.

Install the relevant Linux packages that OCaml needs:

```bash
sudo apt install make m4 gcc pkg-config libx11-dev
```

Install the OPAM package manager for working with different OCaml libraries, line by line:

```shell
sudo add-apt-repository ppa:avsm/ppa
sudo apt install opam
opam init
eval $(opam env)
opam install -y dune core batteries utop graphics merlin ocp-indent tuareg
eval $(opam env)
```

Because there are some issues, we download the OCaml compiler:

```shell
sudo apt-get install ocaml-interp
sudo apt-get install tuareg-mode
```

Now check that the OCaml version is the correct version:

```bash
ocamlc --version
```

Now add the following line onto your Emacs, go to Emacs by typing `emacs` , and:

- press the control key and type `x` (i.e., `C-x`),
- press the control key and type `f` (i.e., `C-f`),
- type exactly `~/.emacs`, and
- press the return key (the one written “enter” on the keyboard)

Now paste this line right under the following code you have added previously, and save the file:

```
(load "/root/.opam/default/share/emacs/site-lisp/tuareg-site-file")
```



### Setting Up (if Emacs doesn't show on next use)

1. Run this code (change IP address with your own):

```shell
export DISPLAY=172.26.192.1:0.0
export LIBGL_ALWAYS_INDIRECT=1
```

2. Open XLaunch with multiple screens, and check all boxes when open
3. Now run emacs

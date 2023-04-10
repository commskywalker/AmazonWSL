# AmazonWSL
Amazon Linux on WSL (Windows 10 FCU or later) - Amazon Linux 2 and Amazon Linux 2023 updated from [AmazonWSL](https://github.com/yosukes-dev/AmazonWSL) (Thank you yosukes-dev!!!)
based on [wsldl](https://github.com/yuk7/wsldl)

### [Download AL2](https://github.com/commskywalker/AmazonWSL/blob/main/AL2.zip) or [Download AL2023](https://github.com/commskywalker/AmazonWSL/blob/main/AL2023.zip)

## An instruction on AWS Developer Tools Blog
The following link is to an article on the AWS Developer Tools Blog describing development with AmazonWSL.    
[Developing on Amazon Linux 2 using Windows - AWS Developer Tools Blog](https://aws.amazon.com/jp/blogs/developer/developing-on-amazon-linux-2-using-windows/)

## Requirements
* Windows 10 Fall Creators Update x64 or later. 
* Windows Subsystem for Linux feature is enabled.

## Install
#### 1. Download one of the installer zips linked above

#### 2. Extract all files in zip file to same directory

#### 3.Run corresponding executable (AL2.exe or AL2023.exe) to Extract rootfs and Register to WSL
Exe filename is using the instance name to register.
If you rename it you can register with a diffrent name and have multiple installs.

## Icon settings for Windows Terminal
![terminal-icon](https://raw.githubusercontent.com/commskywalker/AmazonWSL/master/img/terminal-icon.png)

The following is an example of `profiles.json` if you extracted to `C:\`
```
{
    "guid": "{dc13e3b1-2863-5b9b-9749-3a31bc67a12a}",
    "hidden": false,
    "name": "Amazon2",
    "source": "Windows.Terminal.Wsl",
    "icon": "C:\\AL2\\assets\\icon.png"
}
```

## How-to-Use(for Installed Instance)
#### exe Usage
```dos
Usage :
    <no args>
      - Open a new shell with your default settings.
    run <command line>
      - Run the given command line in that distro. Inherit current directory.
    runp <command line (includes windows path)>
      - Run the path translated command line in that distro.
    config [setting [value]]
      - `--default-user <user>`: Set the default user for this distro to <user>
      - `--default-uid <uid>`: Set the default user uid for this distro to <uid>
      - `--append-path <on|off>`: Switch of Append Windows PATH to $PATH
      - `--mount-drive <on|off>`: Switch of Mount drives
      - `--default-term <default|wt|flute>`: Set default terminal window
    get [setting]
      - `--default-uid`: Get the default user uid in this distro
      - `--append-path`: Get on/off status of Append Windows PATH to $PATH
      - `--mount-drive`: Get on/off status of Mount drives
      - `--wsl-version`: Get WSL Version 1/2 for this distro
      - `--default-term`: Get Default Terminal for this distro launcher
      - `--lxguid`: Get WSL GUID key for this distro
    backup [contents]
      - `--tgz`: Output backup.tar.gz to the current directory using tar command
      - `--reg`: Output settings registry file to the current directory
    clean
      - Uninstall the distro.
    help
      - Print this usage message.
```

#### Just Run exe
```cmd
>AL2.exe
[root@PC-NAME user]#
```

#### Run with command line
```cmd
>AL2.exe run uname -r
4.4.0-43-Microsoft
```

#### Run with command line with path translation
```cmd
>AL2.exe runp echo C:\Windows\System32\cmd.exe
/mnt/c/Windows/System32/cmd.exe
```

#### Change Default User(id command required)

The following is an example of adding a user to the "users" and "wheel" groups

_Note1: Replace `user` with your chosen user name._

```cmd
>AL2.exe run useradd -m -g users -G wheel -s /bin/bash user
```
_Note2: Before setting `user` as the default user, login with the user (`su - user`) and check if it is able to run commands as sudo (`sudo yum update`). If not, check further instructions below. Otherwise, skip for "Setting `user` as the default user"._

If `sudo` is not a recognized command, as root run `yum install -y sudo`.

After installation is complete, run the command `visudo` to edit the `/etc/sudoers` file, press the "i" key to enter edit mode.
Use the arrow keys to naviagte the file until you find the root user entry 'root ALL=(ALL:ALL) ALL', and add the user `user` right below, following the same format '`user` ALL=(ALL:ALL) ALL'.
Press ESC to leave edit mode, and type :wq to Save & Exit (or hold Shift key and press the "z" key 2x).

Setting `user` as the default user:
```cmd
>AL2.exe config --default-user user
>AL2.exe
[user@PC-NAME dir]$
```

#### Set "Windows Terminal" as default terminal
```cmd
>AL2.exe config --default-term wt
```

#### How to uninstall instance
```dos
>AL2.exe clean
```

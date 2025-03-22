# jails
A simple set of bash scripts for chroot management.

## Installation
Install `debootstrap` for your distro before using.
```
git clone https://github.com/toastmod/jails
cd jails
sudo ./install-jails
```

## Usage
### Creating a chroot

`jailmake [name] [arch] [release] [URL]`
#### Example:

In this example we create a chroot named `debian-chroot` running the `stable` release.
```
jailmake debian-chroot amd64 stable http://deb.debian.org/debian/
```

### Entering/Exiting/Unmounting
Enter your chroot like so:

```
sudo jails debian-chroot
```
(it will be automatically mounted if it isn't yet)

To run a command rather than enter the shell, simply pass the command in quotes like so:

```
sudo jails debian-chroot "su -- username"
```



After exiting, don't forget to unmount it:

```
sudo jails unmount debian-chroot
```

Note: **Forgetting to unmount can cause your PC to hang at shutdown.** This is caused by mount points such as `/dev/pts`  (the pseudo-terminal device), but shouldn't be detrimental, just annoying. 

### Manual mounting
If you want to mount your chroot without entering the shell, you can run:

```
sudo jails mount debian-chroot
```

## Shortcuts 
You can use `jaillink` to make shortcuts.

`jaillink login [jail name] [username] <shortcut name>"`

`jaillink shell [jail name] [command] <shortcut name>"`

#### Example:
```
sudo jaillink shell debian-chroot "echo Hello from debian!" debianhello
```
Then you can use yout shortcut like so:
```
$ sudo debainhello
Hello from debian!
```

### Creating a Login Shortcut
#### Example:
```
sudo jaillink login debian-chroot joe
```
Will allow you to use:
```
$ sudo debian-chroot
joe@hostname:~$
```
You can also use a custom shortcut name:
```
sudo jaillink login debian-chroot joe login-as-joe
```

```
$ sudo login-as-joe
joe@hostname:~$
```





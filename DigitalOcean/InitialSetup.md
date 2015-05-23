Initial Setup of Fedora 21
--------------------------

Step 1 — Create a Standard User Account
=======================================

Log in as root and then create a non-root account

```bash
useradd user_name
usermod -a -G wheel user_name
passwd user_name
```

Finally add your public key to `~/.ssh/authorized_keys`.  One reference used a utility called `ssh-copy-id`.  This may be worth looking into more.

Step 2 — Disallow Root Login and Password Authentication
========================================================

Open `/etc/ssh/sshd_config`.   Make the following changes/additions:

```
PermitRootLogin no
PasswordAuthentication no
GSSAPIAuthentication no
```

Save and exit the file, then restart `sshd`.

```
sudo systemctl reload sshd
```

If anyone tries to log in as root now, the response should be Permission denied (publickey).

Step 3 ­— Configuring the Time Zone
===================================

All the known timezones are under the `/usr/share/zoneinfo/` directory.  Create a symbolic soft link from your zone file to /etc/localtime (Using CST as an example):

```
sudo ln -sf /usr/share/zoneinfo/US/Central /etc/localtime
```

Step 4 — Enabling a Firewall
============================

```
sudo yum install -y firewalld
sudo systemctl enable firewalld
sudo systemctl start firewalld
```

To add services or ports use commands like the following:

```
sudo firewall-cmd --add-service=https
sudo firewall-cmd --add-port=443/tcp
```

These commands always need to be executed twice.  Once like displayed above then again with `--permanent` following `firewall-cmd`.  The first modified the current firewall rules and the second makes them persist on reboot.

Step 5 (Optional) - Installing Mlocate
======================================

The `locate` command is a very useful utility for looking up the location of files in the system. For example, to find a file called example, you would type:

```
locate example
```

That will scan the file system and print the location or locations of the file on your screen. There are more advanced ways of using locate, too.

To make the command available on your server, first you need to install the `mlocate` package.

```
sudo yum install -y mlocate
```

Then, run the updatedb command to update the search database.

```
sudo updatedb
```

After that, you should be able to use locate to find any file by name.

Credits
=======

These instructions were adapted from the original form found here: https://www.digitalocean.com/community/tutorials/initial-setup-of-a-fedora-21-server

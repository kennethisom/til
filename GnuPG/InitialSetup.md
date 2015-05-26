Initial Setup of GnuPG
======================

Installation
------------

```bash
sudo yum install -y gnupg
```

I installed `gpg4win` on my home computer to generate my keys because generating a key on a VM proved to be challenging at best.  I then imported these keys on my Linux VM.

```bash
gpg --import /path/to/file.gpg
```

I also used gpg4win to push my keys to the key server http://keys.gnupg.net/, though this could have been done manually.

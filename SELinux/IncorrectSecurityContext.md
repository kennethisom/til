Fixing Incorrect Security Context
---------------------------------

Moving a file instead of copying it with SELinux enabled will result in its security context being incorrect.  To view a file(s) security context execute:

```bash
ls -lrtZ [/path/to/directory/[or/file]]
```

If the security context is not correct the following command will correct it:

```bash
restorecon -v [-R] [/path/to/directory/[or/file]]
```

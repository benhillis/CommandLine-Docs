# Filesystem

> **Important note**:
> Bash on Windows and the Windows Subsystem for Linux are “beta” features. We know that there are issues and gaps in 
> compatibility. You should expect many things to work and for some things to fail. We appreciate 
> any and all constructive feedback you can share from your experiences in using Bash/WSL. 
> Your [bug reports](https://github.com/microsoft/bashonwindows) help us diagnose issues we 
> need to fix in order to deliver a great experience.

## Default Drive Mounting
By default, all fixed NTFS drives are mounted automatically in the `/mnt/` directory. It is reccommended that during your development you work as much as possible under these mount points as files created can be accessed both by Windows applications and your Linux enviroment. To learn more about these restrictions and guidance to prevent data loss take a look at our [blog](https://blogs.msdn.microsoft.com/wsl/2016/06/15/wsl-file-system-support/).

## Updates in the Fall Creators Update
Starting with this update it is possible to manually mount additional drives such as FAT and UNC network shares.
### Mounting DrvFS (USB drives, additional NTFS drives)
In order to mount a Windows drive using DrvFs, you can use the regular Linux mount command. For example, to mount a removable drive **D:** as `/mnt/d` directory, run the following commands:

```
$ sudo mkdir /mnt/d
$ sudo mount -t drvfs D: /mnt/d
```

Now, you will be able to access the files of your **D:** drive under `/mnt/d`. When you wish to unmount the drive, for example so you can safely remove it, run the following command:

```
$ sudo umount /mnt/d
```

### Mounting network locations
When you wish to mount a network location, you can of course create a mapped network drive in Windows and mount that as indicated above. However, it’s also possible to mount them directly using a UNC path:

```
$ sudo mount -t drvfs '\\server\share' /mnt/share
```

Note the single quotes around the UNC path; these are necessary to prevent the need to escape the backslashes. If you don’t surround the UNC path with single quotes, you need to escape the backslashes by doubling them (e.g. `\\\\server\\share`).

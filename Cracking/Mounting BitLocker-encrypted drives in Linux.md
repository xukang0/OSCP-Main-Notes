```
sudo apt-get install dislocker
```

create two folders which we will use to mount the VHD

```
sudo mkdir -p /media/bitlocker
```

```
sudo mkdir -p /media/bitlockermount
```

use `losetup` to configure the VHD as [loop device](https://en.wikipedia.org/wiki/Loop_device), decrypt the drive using `dislocker`, and finally mount the decrypted volume:

```
sudo losetup -f -P Backup.vhd
```

```
sudo dislocker -V /dev/loop0p1 -u[passwd] -- /media/bitlocker
```

```
sudo mount -o loop /media/bitlocker/dislocker-file /media/bitlockermount
```

If everything was done correctly, we can now browse the files:

```
cd /media/bitlockermount/
```

```
ls -la
```

Mounted.

```
cd /media/bitlockermount
```

```
ls -la
```

unmount it using the following commands:

```
sudo umount /media/bitlockermount
```

```
sudo umount /media/bitlocker
```


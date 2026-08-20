## Alternative Method to Download Files (Mount Shares locally)


Create a local mount folder 
```
mkdir -p /tmp/password_audit
```

 Mount the share using cifs 
```
sudo mount -t cifs "//192.168.242.175/Password Audit" /tmp/password_audit -o username='V.Ventz',password='HotelCalifornia194!`
```

 Copy everything to your local workspace 
 ```
 cp -r /tmp/password_audit/* ~/Desktop/PGPlay/Resourced/
 ```
 
Unmount when done 
```
sudo umount /tmp/password_audit
```
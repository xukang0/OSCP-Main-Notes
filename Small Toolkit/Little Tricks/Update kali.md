Full upgrade

```
sudo apt update && sudo apt full-upgrade -y
```

Remove unused files
```
sudo apt autoremove -y
```

```
sudo reboot
```

Install Deb files

```
sudo apt install ./[filename]
```

Check what it installed

```
dpkg -L [name] | grep bin
```
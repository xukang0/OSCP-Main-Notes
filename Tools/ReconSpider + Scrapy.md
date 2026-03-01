add to /etc/hosts/

```
sudo gedit /etc/hosts/
```

Get ReconSpider on Desktop

```
wget -O ReconSpider.zip https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip
```

```
unzip ReconSpider.zip 
```

Create virtual environment

```
python3 -m venv venv
source venv/bin/activate
```

Install scrapy in venv

```
pip3 install scrapy
```

Run script in venv

```
python3 ReconSpider.py http://inlanefreight.com
```
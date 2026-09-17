```
awk '{print $1}' users1 > users2
```

  ABarteski                           D        0  Wed Jun  3 12:47:11 2020

Chooses to extract only the 1st word.

```
cat accounts/xl/sharedStrings.xml | xmllint --xpath '//*[local-name()="t"]/text()' - | awk 'ORS=NR%5?",":"\n"'; echo First Name,Last Name,Email,Username,Password
```
#HackerLines

One liners for vulnerabilities

## Table of Contents
- [CLickjacking](https://github.com/grozdniyandy/hackerlines#clickjacking)

## Clickjacking
Code below will accept list of domains and find the ones vulneable to clickjacking.
Tik repo: https://github.com/grozdniyandy/tik
Vxod repo: https://github.com/grozdniyandy/vxod
```
./tik -f domains.txt -t 100
```
Code below will accept list of domains and find the ones vulneable to clickjacking and then it will check whether there is any input firleds in the MAIN page.
```
./tik -f domains.txt -t 100 > temp.txt && cat temp.txt | grep -oE '[a-zA-Z0-9.-]+\.com' > check.txt && cat check.txt | xargs -P20 -I {} ./vxod {} 2>/dev/null | grep contains > inputs
```

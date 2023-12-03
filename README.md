#HackerLines

One liners for vulnerabilities

## Table of Contents
- [Clickjacking](https://github.com/grozdniyandy/hackerlines#clickjacking)
- [Subdomain Takeover](https://github.com/grozdniyandy/hackerlines#subdomain-takeover)

## Clickjacking
Tik repo: https://github.com/grozdniyandy/tik
<br>
Vxod repo: https://github.com/grozdniyandy/vxod

Code below will accept list of domains and find the ones vulneable to clickjacking.
```
./tik -f domains.txt -t 100
```
Code below will accept list of domains and find the ones vulneable to clickjacking and then it will check whether there is any input firleds in the MAIN page.
```
./tik -f domains.txt -t 100 > temp.txt && cat temp.txt | grep -oE '[a-zA-Z0-9.-]+\.com' > check.txt && cat check.txt | xargs -P20 -I {} ./vxod {} 2>/dev/null | grep contains > inputs
```
## Subdomain Takeover
Zaxvat repo: https://github.com/grozdniyandy/zaxvat
<br>
Code below will accept list of domains and find the ones vulneable to subdomain takeover.
```
cat domains.txt | xargs -P100 -I {} ./zaxvat {} > takeover1
```
After checking all domaoins, you can grep vulnerable ones.
```
cat takeover1 | grep -A4 matches
```

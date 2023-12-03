# HackerLines

One liners for vulnerabilities

## Table of Contents
- [Clickjacking](https://github.com/grozdniyandy/hackerlines#clickjacking)
- [Subdomain Takeover](https://github.com/grozdniyandy/hackerlines#subdomain-takeover)
- [XSS](https://github.com/grozdniyandy/hackerlines#xss)

## Clickjacking
Tik repo: https://github.com/grozdniyandy/tik
<br>
Vxod repo: https://github.com/grozdniyandy/vxod

Code below will accept list of domains and find the ones vulneable to clickjacking.
```
tik -f domains.txt -t 100
```
Code below will accept list of domains and find the ones vulneable to clickjacking and then it will check whether there is any input firleds in the MAIN page.
```
tik -f domains.txt -t 100 > temp.txt && cat temp.txt | grep -oE '[a-zA-Z0-9.-]+\.com' > check.txt && cat check.txt | xargs -P20 -I {} vxod {} 2>/dev/null | grep contains > inputs
```
## Subdomain Takeover
Zaxvat repo: https://github.com/grozdniyandy/zaxvat
<br>
Code below will accept list of domains and find the ones vulneable to subdomain takeover.
```
cat domains.txt | xargs -P100 -I {} zaxvat {} > takeover1
```
After checking all domaoins, you can grep vulnerable ones.
```
cat takeover1 | grep -A4 matches
```
## XSS
Bablo repo: https://github.com/grozdniyandy/bablo
kXSS repo: https://github.com/grozdniyandy/kxss
<br>
If you have only 1 domain to check (You will have to stop crawler manually!)
```
bablo -t 10000 https://example.com >> bablo.txt
```
If you have to test tons of domains. It will scan each for 5 minutes (300 seconds)
```
cat domains.txt | xargs -P10 -I{} timeout 300s bablo -t 100 '{}' >> bablo.txt
```
After identifying the URLs, you can cheeck them for XSS
```
cat bablo.txt | grep '=' | grep -v 'instagram\|facebook\|twitter\|linkedin\|reddit' | xargs -P1000 -I {} kxss '{}' > xss1
```

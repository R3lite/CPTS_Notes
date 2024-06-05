We can look at SSL certificates
Source to find subdomains [crt.sh](https://crt.sh/)
We can access SSL certificate by:
````shell-session
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq .
````
### Filter domains:
````shell-session
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u
````
### Company hosted servers:
````shell-session
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done
````
*We may not be allowed to test third party services*

### Get a list of IP addresses
````shell-session
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f4 >> ip-addresses.txt;done
````
After that we can run a list of IP addresses through [Shodan](https://www.shodan.io/)

### DNS Records
```bash
dig any inlanefreight.com
```

### GrayHatWarefare
Tool for different searches, discovering AWS, Azure, and GCP. Allows for sorting and filtering by a file format
[GrayHatWarefare](https://buckets.grayhatwarfare.com/)

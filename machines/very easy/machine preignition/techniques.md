#Use gobuster to dir bust the wordpress site (and expose url for admin page)

``` bash
sudo gobuster dir -w /usr/share/wordlists/common.txt -u 10.129.187.44
```

_note: /usr/share/wordlists/common.txt is just a text file with all possible/common page names for a website_
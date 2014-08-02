---
layout: post
title:  "Custom Domain with GetHub Pages"
date:   2014-08-02 17:44:02
categories: jekyll
---
It's pretty simple to use a custom domain for your GitHub Page. Start by reading [GitHub Pages Basics](https://help.github.com/categories/20/articles) and then follow the directions.

Here's what I did:

## Update DNS in Route53

1. Login to your Amazon Web Services Console
2. Go to Route53
3. Go to Hosted Zones
4. Select the Domain Name and Go to Record Sets
5. Select "Create Record Set"
6. Add a CNAME Record from your desired custom name to your github page. In my case, I created a CNAME record named "github.ideoplex.com" and directed it to "ideoplex.github.io".

Verify your DNS setting from the command line with dig:

```
~ 17 $ dig github.ideoplex.com

; <<>> DiG 9.8.3-P1 <<>> github.ideoplex.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 38421
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;github.ideoplex.com.		IN	A

;; ANSWER SECTION:
github.ideoplex.com.	2558	IN	CNAME	ideoplex.github.io.
ideoplex.github.io.	2558	IN	CNAME	github.map.fastly.net.
github.map.fastly.net.	23	IN	A	23.235.46.133

;; Query time: 43 msec
;; SERVER: 10.0.1.1#53(10.0.1.1)
;; WHEN: Sat Aug  2 17:53:29 2014
;; MSG SIZE  rcvd: 120
```

You want to see your custom domain name (_github.ideoplex.com_) aliased to your github user page (_ideoplex.github.io_) aliased to something (_github.map.fastly.net_) that references an ip address (_23.235.46.133_).

## Add a CNAME record to your repository

The GitHub instructions to [add a CNAME record](https://help.github.com/articles/adding-a-cname-file-to-your-repository) are straight forward.

1. Identify the correct branch.
    * Use master for user and organization pages
    * Use gh-pages for project pages
2. Add a new file named __CNAME__ (all caps) to the branch root directory
3. Add a single line to the CNAME file that specifies the bare subdomain for your page (in my case, _github.ideoplex.com_)

Verify the CNAME behavior with curl:

```
~ 18 $ curl -I http://ideoplex.github.io/
HTTP/1.1 301 Moved Permanently
Server: GitHub.com
Content-Type: text/html
Location: http://github.ideoplex.com/
Expires: Sat, 02 Aug 2014 22:20:01 GMT
Cache-Control: max-age=600
Content-Length: 178
Accept-Ranges: bytes
Date: Sat, 02 Aug 2014 22:10:01 GMT
Via: 1.1 varnish
Age: 0
Connection: keep-alive
X-Served-By: cache-iad2120-IAD
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1407017401.351397276,VS0,VE1
Vary: Accept-Encoding
```

Here you want to see that your old github page url (_http://ideoplex.github.io/_) is redirected to your custom domain name (_http://github.ideoplex.com_).

## Wait

This was the hardest part. The first two steps took a couple of minutes, but it can take ten minutes for the changes to take effect at GitHub.

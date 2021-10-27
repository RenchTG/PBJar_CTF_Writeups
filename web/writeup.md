# Challenge Info:

#### Challenge Name: web

#### Challenge Author: eyangch

#### Challenge Description: I downloaded this program back when the version number was still v1. It's been a long time... I heard the most recent update has the flag in it. Download: http://147.182.172.217:42100/v1

#### Files Provided: none

# TLDR:

#### - Find the outer limits of the possible versions by just adding 0's.
#### - Use a binary search method to keep finding numbers between your limits until you get the newest version.

# In-Depth Solution: 

#### So to start off we go to the website on the link provided and a weird file is downloaded. It has a bunch of non-readable text on it, but some is readable. On it though we can find a link that takes us to download version 2. Once we download version 2 we get a link to version 3 and this will repeat. Our goal as the description states is to find the newest one. I start off by playing around with the url and I realize that I can change the url to get whatever version number I put in. I then proceed to find the limits of the version by just adding zeroes. Eventually I get the url:

#### `http://147.182.172.217:42100/v100000000`

#### to work while the url `http://147.182.172.217:42100/v1000000000` would give me the message:

#### `version not found`

#### After that I decided a write a script for me to perform a sort of binary search to find the number that is in between the two limits that I have set. I thought about automating this process so that I would send a web request with my script and based on the response I change my limits. The general idea is that if we do get a version back and it downloads a file, that is the new `min_limit` and if the website responds with 'version not found' we update the `max_limit`. 

```python
int(((max_limit - min_limit) / 2) + min_limit)
```

#### However of course I was too lazy so I kept inputting the version my program spit out by hand into the url and would change the variables myself accordingly. Anyways eventually the version number `v133791021` was able to give me the flag file. Then just run strings or cat:

#### `strings flag` or `cat flag`

#### And boom, there's our flag.

## Flag: flag{h0w_l0ng_wher3_y0u_g0ne_f0r_3910512832}

# Challenge Info:

#### Challenge Name: web

#### Challenge Author: eyangch

#### Challenge Description: I downloaded this program back when the version number was still v1. It's been a long time... I heard the most recent update has the flag in it. Download: http://147.182.172.217:42100/v1

#### Files Provided: none

# TLDR:

#### - Find the outer limits of the possible versions by just adding 0's.
#### - Use a binary search method to keep finding numbers between your limits until you get the newest version.

# In-Depth Solution: 

#### So to start off we go to the website on the link provided and a weird file is downloaded. It has a bunch of non-readable text on it, but some is readable. On it though we can find a link that takes us to download version 2. Once we download version 2 we get a link to version 3 and this will repeat. Our goal as the description states is to find the newest one. I start off 

## Flag: flag{h0w_l0ng_wher3_y0u_g0ne_f0r_3910512832}

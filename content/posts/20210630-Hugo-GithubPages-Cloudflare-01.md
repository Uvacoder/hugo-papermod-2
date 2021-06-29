---
draft: false

title: Github pages, Hugo and Cloudflare
description: Setting up a simple site with Hugo, Github Pages, and Cloudflare

date: 2021-06-29T21:00:00+01:00
tags: 
    - hugo
    - cloudflare
    - github pages
categories:
    - development
    - github pages
    - hugo
slug: 20210630-Hugo-GithubPages-Cloudflare-01
---
# Github pages, Hugo and Cloudflare
So I thought it was about time I started one of these things, collected some thoughts and put some ramblings out into the ether.

First things first - lets get started with how I setup this page!

## GitHub Pages
Basically we need to create a repo called: drtbz\drtbz.github.io
In there, we need a CNAME file with the sole line: `drtbz.com`
And chuck in a `README.md` with some text to check your site works.
That's it, for now!

## Cloudflare
I'm using cloudflare as both registrar and CDN/WAF for this project. You don't have to, but they have some cool stuff, and it's free.

As we're using an apex domain with Github Pages, we've gotta do the following:
 - 4 x A records to drtbz.com with IP's [185.199.108.153,185.199.109.153,185.199.110.153,185.199.111.153]
 - 1 x CNAME for `www` to `drtbz.github.io`
 - A whole bunch of SSL settings:
    - Set to `Full (Strict) mode` because we can.
    - Always use HTTPS
    - Enable HSTS with everything on and at least 6 months Max Age Header
    - Minimum TLS 1.2
    - Opportunistic Encryption ON
    - TLS 1.3 ON
    - Automatic HTTPS ReWrites ON
    - Certificate Transparency Monitoring - Optional, but kinda cool.

That's pretty much it from the cloudflare perspective. Very much set and forget, and just let it do it's thing!

Next up - we're going to setup HUGO, and then do some stuff with Github Actions to tie it all together.


+++
date = '2025-05-07T15:15:59+05:30'
draft = true
title = 'Setup'
+++

The website is being hosted on a local desktop without any static IP address, the way it is accessible to public ip addresses is due to Cloudflare, Cloudflare allows to setup a free tunnel - think of it as a VPN to cloudflare servers, if you are using cloudflare's DNS servers, you can route these DNS queries to a cloudflare's VPN to your personal computer.

Your personal computer needs to have the following things up and running

* `WARP` client to connect to CloudFlare's infra
* `cloudflared` running as a daemon to proxy requests
* your web server which will serve traffic



Once you are done with setting up your local machine, you need to route your DNS queries to cloudflared, this can be done on the cloudflare dashboard as shown below

![alt text](image.png)

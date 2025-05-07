+++
date = '2025-05-07T15:15:59+05:30'
draft = false
title = 'Setup'
+++

The website is being hosted on a local desktop without any static IP address, the way it is accessible to public ip addresses is due to Cloudflare, Cloudflare allows to setup a free tunnel - think of it as a VPN to cloudflare servers, if you are using cloudflare's DNS servers, you can route these DNS queries to a cloudflare's VPN to your personal computer.

Your personal computer needs to have the following things up and running

* `WARP` client to connect to CloudFlare's infra
* `cloudflared` running as a daemon to proxy requests
* your web server which will serve traffic



Once you are done with setting up your local machine, you need to route your DNS queries to cloudflared, this can be done on the cloudflare dashboard as shown below

![alt text](image.png)


The image above shows how public hostname is mapped to a service which is running locally at port 1313 (I'm running Hugo server) which is going to serve web requests from client.

It is amazing how much capability unlock this gives without getting tied to any cloud provider except for Cloudflare for sure ✨

PS: I forgot to mention that you do not need to buy an SSL certificate for your domain but these requests will still be served on HTTPS and browsers will not flag visits to your domain, again all thanks to Cloudflare's proxying. 


Here's how the final flow looks like

```

                                                                      │
                                                                      ▼

+--------+          +--------------------------+         +----------------+          +--------------------------+
| Client |          |                          |
|        |    ───▶  | Cloudflare DNS Resolver  |    ───▶  | DNS Resolution |   ───▶   | Cloudflare Proxy Server |
+--------+          +--------------------------+         +----------------+          +--------------------------+

```

                                                                      │
                                                                      ▼


                                        +-------------------------+ ───▶ +-----------------------------+
                                        | Cloudflare Tunneling    |      | Local Machine (cloudflared  |
                                        | (cloudflared daemon)    |      | + WARP connected)           |
                                        +-------------------------+      +-----------------------------+

---
layout: post
title:  "Migrating from Webfaction to Lightsail"
tags: hosting ubuntu linux
---

Going back to 2011, I've used Webfaction for hosting various personal and family
websites, email forwarding and file storage. For $9.50/mo, I get 100GB of
storage (which I'm not convinced is actually enforced) on a massive 24 core
Linux beast, a shell account with all the developer goodies you could ask for
and a full-featured and well-designed web control panel. Their support has
been good the few times I've needed it, and the company just has a cool
bootstrapped feel to it. Webfaction has a sensibly limited and well-executed
scope that is rarely found in a business that's been around as long as they
have.

Unfortunately, they've sold out to GoDaddy. Ugh. I've
spent the past few months migrating all my domains (both registrations and DNS)
from GoDaddy to AWS Route53. I finally don't have anything in that account any
more, and here my hosting company is about to force me back into the GoDaddy
sphere. 

GoDaddy is the hosting company developers love to hate. We use them at work for
domain registrations because they're cheap and they do that fairly well. We also
use them for certificates when Let's Encrypt doesn't fit the bill. But whenever
a customer actually hosts their website at GoDaddy, it doesn't go well at all.
My sense has been that if you just want to do a control panel install of
WordPress and use it from that interface, it probably works -- VERY slowly. But for a
developer trying to do anything else, it never seems to go well. And their support for doing anything outside of their web
control panel is useless. To be fair, GoDaddy does well with basic support - it's
responsive and effective, but their expertise is very limited. I've also had a
few interactions that make me want to push
them off a cliff. Recently, a GoDaddy support staffer tried to refuse refunding
an unused (never even issued) and fairly expensive certificate - something that
costs them nothing. They claimed I'd passed the 5 day limit for refunds. When I
asked where that policy was stated on their website, they pointed to something
clearly applying to domain names, not certificates. I had to threaten escalating
the issue to my credit card company before they finally caved and gave me the
refund. It's interactions like that - and the pain I've seen developers go
through trying to get custom-built sites working in their environment - that makes
Webfaction's migration to GoDaddy a non-starter for me. I won't even get into
the abrasively sexist marketing they're well known for.

Add to that the lack of information from Webfaction about the migration. It's
fairly non-existant. No useful detail. The Webfaction forums are filled with
angry customers asking what the hell is going on. Rather than get into that fray
only to get more frustrated, I'm taking this opportunity to move to my own
server, something I've considered doing for a while any way.

Lightsail is the slightly more consumer-friendly version of AWS's EC2 cloud
infrastructure service. While I use a personal AWS account for S3 and Route53 and know the
EC2 tools well - I use them extensively at work - Lightsail offers some niceties
that fit my personal use better. It offers a streamlined control panel for managing
instances, snapshots, IPs and the like. Most importantly, it has a simple monthly
fixed price for a server rather than the hard-to-predict per second pricing EC2
uses. And for developers, Lightsail can be managed via the aws-cli, which I
love.

So I've created an Ubuntu server with 2GB of RAM and a 60GB SSD for hosting a
handful of Wordpress and static sites (including this one) and forwarding email
for some of my domains. It's been a pleasure to set up and I now have root
access to my hosting environment, which is handy. At $10/mo, this has cost
parity with Webfaction, and I'm not losing any features. The whole setup took me
2 evenings - maybe a total of 5 hours, which includes 5 site migrations and a
postfix configuration I'd never done before. 

One lesson learned is to use the
plain Linux image and not one of the preconfigured application instances. I
started with a Wordpress instance, figuring it would save me time installing
stuff, only to find out it's a Bitnami install. Bitnami does not do things in a
standard way and is not appropriate, in my humble oppinion, for a production
server. Great for development - not so much for production. So I scrapped that
and took the time to build it out myself.

Farewell, Webfaction. It's been good. Do something fun with your GoDaddy payout!





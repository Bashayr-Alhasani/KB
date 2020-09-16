---
title: "Mostly Asked Questions"
description: "this is meta description"
draft: false
---

{{< faq "Can I download my external volumes?" >}}
No. you cannot download your external volume directly from the cloud. But you can contact your account manager to get your data.
{{</ faq >}}

{{< faq "I want to use your cloud as a DR for my local DC, is this possible?" >}}
Yes, it is possible. Cloud is a kind of Datacenter, that is why we are using the term Virtual Data Center. You can connect to our cloud Datacenter over internet or through a IP-VPN.
{{</ faq >}}

{{< faq "Can I use my own flavors?" >}}
No, You cannot use your own flavors at the moment. But if you need it really, and looking for a different flavor based on your application vendor requirement, you can contact your account manager to create custom flavors for your project.
{{</ faq >}}

{{< faq "Can I use Addrespair concept in for my HA applications?" >}}
Yes, this is possible. Allowed-address-pairs allow you to specify mac_address/ip_address (CIDR) pairs that pass through a port regardless of subnet. This enables the use of protocols such as VRRP, which floats an IP address between two instances to enable fast data plane failover.
{{</ faq >}}

{{< faq "What is this zone concept?" >}}
Our servers are physically deployed in the datacenter by rows. There is two rows at the moment. We consider two rows as two different zones. Customer will not feel any difference in zones. But customer can avail the advantage of zones while they are deploying HA applications. By choosing different zones, he can assure that his virtual servers will go to entire different computes and different storage pool.
{{</ faq >}}

{{< faq "What is the difference between SSD-GP and standard?" >}}
SSD-GP and Standards are Solid State Drive backed volumes. Advantage of SSD-GP is it assured a Guaranteed IOPs.
{{</ faq >}}

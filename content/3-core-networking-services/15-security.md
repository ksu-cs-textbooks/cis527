---
title: "Security"
weight: 75
pre: "15. "
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "/3-core-networking-services/15-security-slides.md" >}})**
* [Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security) on Wikipedia
* [Transport Layer Security (TLS)](https://hpbn.co/transport-layer-security-tls/) from High Performance Browser Networking on O'Reilly
* [Firewall](https://help.ubuntu.com/lts/serverguide/firewall.html.en) on Ubuntu Server Guide
* [Uncomplicated Firewall](https://wiki.ubuntu.com/UncomplicatedFirewall) on Ubuntu Wiki
* [Fine-tuning Firewall Rules: 10 Best Practices](https://www.esecurityplanet.com/network-security/finetune-and-optimize-firewall-rules.html) from eSecurity Planet

#### Video Transcript

Lastly, it is very important to take a few minutes to discuss some security concerns related to networking. While this isn't a security course, it is vital for system administrators to understand the security tradeoffs of any system they configure.

When dealing with networks, there are a few security concepts to keep in mind. First and foremost is your firewall. On any system you work with, you should ensure that the firewall is properly enabled. It should also be configured to only allow incoming connections on the smallest set of ports that will allow the server to function. In other words, you should only allow ports for software you are planning to use on the server, and all other ports should be blocked. This follows the security concept of "Principle of Least Privilege," where you only allow the smallest number of permissions required for the system to function.

Similarly, many larger networks should also employ some network monitoring software to scan for unwanted network traffic. While a firewall helps guard against incoming connections, it cannot detect a malicious outgoing connection from a compromised system. A proper network monitoring system could help you detect that breach and stop it before it becomes a larger issue.

For smaller networks and home users, simply installing and using a NAT router offers a significant layer of protection with minimal hassle. A NAT router will block all incoming traffic by default, unless you or one of your systems requests a port to be opened for a specific use. While it isn't a perfect system, in general this is much better than connecting a computer directly to the public internet itself.

Lastly, for any network connections, you should consider using some form of encryption and authentication on the connection. By doing so, you can be sure that you are connecting to the correct system on the other end, and that no one else can intercept your communication once it is established. Thankfully, there are many ways to accomplish this.

Many systems today use Transport Layer Security, or TLS, to help secure their network connections. TLS was formerly known as SSL, and while many users may use the terms interchangeably, technically SSL is an obsolete protocol that was replaced by TLS many years ago, so TLS is the proper way to refer to it today. The TLS name can also be a bit misleading, because it doesn't truly reside in the transport layer. Instead, it is typically above the transport layer, but below the top three application layers of the 7 layer OSI model. Many diagrams show it as part of the session layer, which is a pretty good way to think of it.

In essence, what TLS does is perform a handshake protocol after the TCP connection has been established between the two systems, but before any application data is sent or received. This diagram shows what a TLS handshake entails. The blue boxes at the top are the TCP connection being established, followed by the tan boxes giving the steps of the TLS handshake protocol. During that process, the two systems exchange security certificates, agree on an encryption algorithm, and generate a shared encryption key that is known only to those two systems. The sender and recipient can confirm each other's identity based on a "chain of trust" for the certificates presented; in essence, they look to see if the certificate is signed by someone they trust, in which case they can also trust the certificate itself. Once that is done, it then cedes control to the application, which can then start sending and receiving packets.

When a packet is transmitted, the TLS layer will encrypt the packet so that it cannot be read by others. It will also include a second part of the message, called a message authentication code or MAC, that will help detect if the encrypted packet is altered in any way.

Many protocols today use TLS by default, including HTTP. You've probably seen the `https` protocol in your web browser many times. That simply means that your browser is using TLS to communicate with the web server. In addition, many browsers will show information about the certificate presented by the web server, and will alert you if the certificate is untrusted.

This is a very brief overview of the security concerns involved in a networked world. I encourage you to consider taking additional courses in cyber security if you are interested in learning the details of how these systems are implemented. In any case, you should always be thinking about security as you configure your systems to connect to a network. 

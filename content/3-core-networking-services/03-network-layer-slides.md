---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 3 - Network Layer</p>
</section>
<section>
	<h3>Network Layer</h3>
	<ul>
		<li>Transmit Packets Between Connected Networks</li>
		<li>Typically uses the Internet Protocol (IP) for Addressing</li>
		<li>Most Routers Operate at this Layer</li>
	</ul>
</section>
<section>
	<h3>IPv4 Packet Structure</h3>
	<table style="width:100%" class="table">
		<tr><td align="center">Version Info</td><td align="center">Length</td></tr>
		<tr><td align="center">Packet ID</td><td align="center">Flags & Offset</td></tr>
		<tr><td align="center">Protocol & TTL</td><td align="center">Checksum</td></tr>
		<tr><td colspan="2" align="center">Source IP Address</td></tr>
		<tr><td colspan="2" align="center">Destination IP Address</td></tr>
		<tr><td colspan="2" align="center">Data...</td></tr>
	</table>
</section>
<section>
	<h3>IPv4 Addresses</h3>
	<ul>
		<li>32-bit Binary Numbers</li>
		<li>Unique Identifier on Network</li>
		<li>Usually Represented in Dot-Decimal Notation</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="/images/ipv4address_wiki.svg">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Dot-decimal_notation">Wikipedia</a></p>
</section>
<section>
	<h3>Old - Classful Networks</h3>
	<ul>
		<li>Network Determined by First 4 Bits</li>
			<ul>
				<li>Class A - 128 Networks, 16m Addresses Each</li>
				<li>Class B - 16k Networks, 1m Addresses Each</li>
				<li>Class C - 2m Networks, 256 Addresses Each</li>
				<li>Class D - Multicast</li>
			</ul>
		</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="/images/ipclasses_tcpip.png">
	<p class="imagecredit">Image Source: <a href="http://www.tcpipguide.com/free/t_IPClassfulAddressingNetworkandHostIdentificationan-3.htm">TCP/IP Guide</a></p>
</section>
<section>
	<img class="stretch plain" src="/images/map_of_the_internet_xkcd.jpg">
	<p class="imagecredit">Image Source: <a href="http://xkcd.com/195/">XKCD</a></p>
</section>
<section>
	<h3>New - Classless Inter-Domain Routing (CIDR)</h3>
	<ul>
		<li>Introduces Subnet Masking</li>
		<li>Subnet Mask Defines Network & Host Portion of Address</li>
		<li>Much More Flexible & Scalable</li>
	</ul>
</section>
<section>
	<h3>Subnet Mask Example</h3>
	<pre>
IP:   192.168.  2.130 11000000.00000000.00000010.10000010
Mask: 255.255.255.  0 11111111.11111111.11111111.00000000
Net:  192.168.  2.  0 11000000.00000000.00000010.--------
Host:   0.  0.  0.130 --------.--------.--------.10000010
</pre>
<br>
	<pre class="fragment">
IP:   192.168.  2.130 11000000.00000000.00000010.10000010
Mask: 255.255.255.192 11111111.11111111.11111111.11000000
Net:  192.168.  2.128 11000000.00000000.00000010.10------
Host:   0.  0.  0.  2 --------.--------.--------.--000010
</pre>
</section>
<section>
	<h3>CIDR Notation</h3>
	<ul>
		<li>IP Followed by Number of Leading 1s in Subnet Mask</li>
		<li>Example: 192.168.2.0/24
			<ul>
				<li>Network: 192.168.2.0</li>
				<li>Subnet Mask: 255.255.255.0</li>
			</ul>
		</li>
	</ul>
</section>
<section>
	<h3>CIDR Routing</h3>
	<img class="stretch plain" src="/images/cidrroute_wiki.svg">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing">Wikipedia</a></p>
</section>
<section>
	<h3>Reserved Spaces</h3>
	<ul>
		<li>10.0.0.0/8 - Class A</li>
		<li>172.16.0.0/12 - 16 &times; Class B</li>
		<li>192.168.0.0/16 - 256 &times; Class C</li>
		<li>127.0.0.0/8 - Loopback</li>
		<li>169.254.0.0/16 - Link-Local</li>
		<li>100.64.0.0/10 - Carrier-Grade NAT</li>
	</ul>
</section>
<section>
	<h3>Network Address Translation (NAT)</h3>
	<img class="stretch plain" src="/images/nat_tcpip.png">
	<p class="imagecredit">Image Source: <a href="http://www.tcpipguide.com/free/t_IPNATUnidirectionalTraditionalOutboundOperation.htm">TCP/IP Guide</a></p>
</section>
<section>
	<h3>IPv4 vs. IPv6</h3>
	<p>IPv4: 32-bit Addresses<br>2<sup>32</sup> = 4,294,967,296</p>
	<br>
	<p class="fragment">IPv6: 32-bit Addresses<br>2<sup>128</sup> = 340,282,366,920,938,463,463,<br>374,607,431,768,211,456<br>or 340 Undecillion addresses<p>
</section>
<section>
	<h3>IPv6 Packet Structure</h3>
	<img class="stretch plain" src="/images/ipv6_wiki.png">
	<p class="imagecredit">Image Source: <a href="http://en.wikipedia.org/wiki/Ipv6">Wikipedia</a></p>
</section>
<section>
	<h3>IPv6 Addresses</h3>
	<ul>
		<li>128-bit Binary Numbers</li>
		<li>8 Groups of 4 Hexadecimal Digits, Separated By Colons</li>
		<li>Representation May Be Simplified</li>
	</ul>
</section>
<section>
	<h3>IPv6 Address Reduction</h3>
	<ul>
		<li>Omit Leading 0s</li>
		<li>Combine Consecutive Empty Groups With :: Once Per Address</li>
	</ul>
<pre>
2001:0db8:85a3:0000:0000:8a2e:0370:7334
2001: db8:85a3:   0:   0:8a2e: 370:7334
2001: db8:85a3    ::     8a2e: 370:7334
2001:db8:85a3::8a2e:370:7334
</pre>
</section>
<section>
	<h3>IPv6 Addressing</h3>
	<ul>
		<li>Method Indicated by Prefix</li>
		<li>Each Method Uses a Different Format</li>
		<li>001 - Global Unicast</li>
		<li>FE80 - Link-Local</li>
		<li>FC & FD - Unique-Local</li>
		<li>Many Reserved Ranges</li>
	</ul>
</section>

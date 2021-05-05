---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 3 - DHCP</p>
</section>
<section>
	<h3>Special Thanks</h3>
	<br>
	<p>Much of this information adapted from <a href="https://russfeld.me/assets/oldimpress/images/cis527/dhcp.svg">slides</a> by <a href="http://people.cs.ksu.edu/~sgsax/">Seth Galitzer</a></p>
</section>
<section>
	<h3>History</h3>
	<ul>
		<li>1982 - TCP/IP Developed</li>
		<li>1985 - BOOTP Developed</li>
		<li>1987 - 20,000 Hosts on Internet</li>
		<li>1989 - DHC Working Group</li>
		<li>1993 - DHCP Defined (RFC 1531)</li>
		<li>1996 - ISC Server Released</li>
		<li>1997 - DHCP Finalized (RFC 2131)</li>
		<li>2003 - DHCP for IPv6 (RFC 3315)</li>
	</ul>
</section>
<section>
	<h3>Dynamic Host Configuration Protocol (DHCP)</h3>
	<ul>
		<li>Large Networks Difficult to Manage Manually</li>
		<li>Computers Are Now Mobile</li>
		<li>Need to Automatically Configure Network Settings</li>
	</ul>
</section>
<section>
	<h3>Why DHCP?</h3>
	<ul>
		<li>Leasing</li>
		<li>Renewal</li>
		<li>Configuration</li>
		<li>Portability</li>
		<li>Compatible with Static IP</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="../../images/dhcp_fossbytes.jpg">
	<p class="imagecredit">Image Source: <a href="https://fossbytes.com/dhcp-how-does-it-work/">Fossbytes</a></p>
</section>
<section>
	<img class="stretch plain" src="../../images/dhcp_multiple.png">
	<p class="imagecredit">Image Source: <a href="http://people.cs.ksu.edu/~russfeld/cis527spring2017/9dhcpdns/images/dhcp.svg">Seth Galitzer</a></p>
</section>
<section>
	<h3>Automatic Private IP Address (APIPA)</h3>
	<ul>
		<li>Used when DHCP Fails</li>
		<li>Assigns a Link-Local IP Address</li>
		<li>IPv4: 169.254.0.0/16</li>
		<li>IPv6: fe80::/10</li>
	</ul>
</section>
<section>
	<h3>Sample Configuration</h3>
	<pre style="font-size: .5em"><code>default-lease-time 600;  # in seconds
max-lease-time 7200;     # in seconds
authoritative;           # this server is authoritative
                         #   for this network segment

option domain-name "cis.ksu.edu";
option domain-name-servers 129.130.254.2, 129.130.254.3;
option subnet-mask 255.255.254.0;
option broadcast-address 129.130.11.255;
option routers 129.130.10.1;
option smtp-server smtp.cis.ksu.edu;
</code></pre>
</section>
<section>
	<h3>Sample Configuration</h3>
	<pre style="font-size: .5em"><code>#fixed-address
host eth0_bronco {
	option host-name "bronco";
	hardware ethernet ec:a8:6b:fe:2e:b5;
	fixed-address 129.130.10.190;
}

#dynamic pool
pool {
	range 129.130.10.209 129.130.10.229;
	range 129.130.10.245 129.130.10.255;
	range 129.130.11.201 129.130.11.254
}
</code></pre>
</section>

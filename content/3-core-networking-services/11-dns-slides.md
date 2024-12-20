---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 3 - DNS</p>
</section>
<section>
	<h3>Special Thanks</h3>
	<br>
	<p>Much of this information adapted from <a href="https://russfeld.me/assets/oldimpress/images/cis527/dns.svg">slides</a> by <a href="http://people.cs.ksu.edu/~sgsax/">Seth Galitzer</a></p>
</section>
<section>
	<h3>History</h3>
	<ul>
		<li>1965 - ARPANET</li>
		<li>1969 - 4 Nodes</li>
		<li>1971 - 15 Nodes</li>
		<li>1982 - TCP/IP Developed</li>
		<li>1984 - Over 1000 Hosts</li>
		<li>1987 - Over 20000 Hosts</li>
	</ul>
</section>
<section>
	<h3>hosts.txt</h3>
	<ul>
		<li>Hosted by SRI</li>
		<li>Maps System Names to IP Addresses</li>
		<li>Updated Manually</li>
		<li>Difficult to Avoid Collisions</li>
		<li>Maintain Consistency Across Systems</li>
	</ul>
</section>
<section>
	<h3>Domain Name Service (DNS)</h3>
	<ul>
		<li>Developed in 1983 (RFC 882-883)</li>
		<li>Finalized in 1987 (RFC 1035-1035)</li>
		<li>Distributed System of Name Servers</li>
		<li>Hierarchical, Consistent Name Space</li>
		<li>Multiple Protocols and Data Types</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="../../images/dns_wiki.png">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Domain_Name_System">Wikipedia</a></p>
</section>
<section>
	<img class="stretch plain" src="../../images/dns_lookup.png">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Domain_Name_System">Wikipedia</a></p>
</section>
<section>
	<h3>BIND</h3>
	<ul>
		<li>Widely Used DNS Server</li>
		<li>Latest: BIND 9</li>
		<li>Implements All IETF DNS Standards</li>
	</ul>
</section>
<section>
	<h3>DNS Record Types</h3>
	<ul>
		<li>SOA - Start of Authority</li>
		<li>A - IPv4 Address</li>
		<li>AAAA - IPv6 Address</li>
		<li>CNAME - Canonical Name (Alias)</li>
		<li>MX - Mail Exchange</li>
		<li>NS - Name Server</li>
		<li>PTR - Pointer (Reverse Lookup)</li>
		<li>TXT - Text</li>
	</ul>
</section>

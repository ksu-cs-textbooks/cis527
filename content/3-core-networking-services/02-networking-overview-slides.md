---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 3 - Networking Overview</p>
</section>
<section>
	<img class="stretch plain" src="../../images/circuit2.png">
</section>
<section>
	<img class="stretch plain" src="../../images/packet1.png">
</section>
<section>
	<img class="stretch plain" src="../../images/packet2.png">
</section>
<section>
	<img class="stretch plain" src="../../images/packet_switching_wiki.gif">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Packet_switching">Wikipedia</a></p>
</section>
<section>
	<img class="stretch plain" src="../../images/internet_wiki.jpg">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Computer_network">Wikipedia</a></p>
</section>
<section>
	<h3>7 Layer OSI Model</h3>
	<img class="stretch" src="../../images/7layer_github.gif">
	<p class="imagecredit">Image Source: <a href="https://github.com/zikrillah/F5-Blueprint-Material/wiki/OSI-Model">Jordan Head on StackExchange</a></p>
</section>
<section>
	<h3>Data Transmission</h3>
	<img class="stretch" src="../../images/layers_tcpip.png">
	<p class="imagecredit">Image Source: <a href="http://www.tcpipguide.com/free/t_IndirectDeviceConnectionandMessageRouting.htm">TCP/IP Guide</a></p>
</section>
<section>
	<h3>Encapsulation</h3>
	<img class="stretch" src="../../images/encapsulation_tcpip.png">
	<p class="imagecredit">Image Source: <a href="http://www.tcpipguide.com/free/t_DataEncapsulationProtocolDataUnitsPDUsandServiceDa.htm">Wikipedia</a></p>
</section>
<section>
	<h3>Physical - 1000BASE-T</h3>
	<img class="stretch" src="../../images/nic_wiki.jpg">
	<p class="imagecredit">Image Source: <a href="http://en.wikipedia.org/wiki/Ethernet_card">Wikipedia</a></p>
</section>
<section>
	<h3>Data Link - Ethernet</h3>
	<img class="stretch" src="../../images/ethernet_wiki.jpg">
	<p class="imagecredit">Image Source: <a href="http://en.wikipedia.org/wiki/Ethernet">Wikipedia</a></p>
</section>
<section>
	<h3>Media Access Control (MAC) Address</h3>
	<ul>
		<li>Physical Address of a Network Device</li>
		<li>Identifies Devices at Layer 2</li>
		<li>48-bit Address</li>
		<li>Example: 1a:2b:3c:d4:e5:f6</li>
		<li>Set by Manufacturer</li>
		<li>Can be Changed by User</li>
	</ul>
</section>
<section>
	<h3>Routing</h3>
	<ul>
		<li>Find Best Path from Point to Point on Network</li>
		<li>Prevent Loops</li>
		<li>Allow for Redundant Links</li>
		<li>Uses Variant of Spanning Tree Algorithm</li>
	</ul>
</section>
<section>
	<section>
		<img class="stretch plain" src="../../images/net1_wiki.svg">
		<p class="imagecredit">Image Source: <a href="http://en.wikipedia.org/wiki/Spanning_Tree_Protocol">Wikipedia</a></p>
	</section>
	<section>
		<img class="stretch plain" src="../../images/net2_wiki.svg">
		<p class="imagecredit">Image Source: <a href="http://en.wikipedia.org/wiki/Spanning_Tree_Protocol">Wikipedia</a></p>
	</section>
	<section>
		<img class="stretch plain" src="../../images/net3_wiki.svg">
		<p class="imagecredit">Image Source: <a href="http://en.wikipedia.org/wiki/Spanning_Tree_Protocol">Wikipedia</a></p>
	</section>
	<section>
		<img class="stretch plain" src="../../images/net4_wiki.svg">
		<p class="imagecredit">Image Source: <a href="http://en.wikipedia.org/wiki/Spanning_Tree_Protocol">Wikipedia</a></p>
	</section>
	<section>
		<img class="stretch plain" src="../../images/net5_wiki.svg">
		<p class="imagecredit">Image Source: <a href="http://en.wikipedia.org/wiki/Spanning_Tree_Protocol">Wikipedia</a></p>
	</section>
	<section>
		<img class="stretch plain" src="../../images/net6_wiki.svg">
		<p class="imagecredit">Image Source: <a href="http://en.wikipedia.org/wiki/Spanning_Tree_Protocol">Wikipedia</a></p>
	</section>
</section>
<section>
	<h3>Virtual LAN (VLAN)</h3>
	<ul>
		<li>Partition a Single Layer 2 Network</li>
		<li>Each Partition is Isolated</li>
		<li>Simplify Network Design</li>
		<li>Group Items by Function, Not Location</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="../../images/vlan_cisco.jpg">
	<p class="imagecredit">Image Source: <a href="https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst4500/12-2/25ew/configuration/guide/conf/vlans.html">Cisco</a></p>
</section>
<section>
	<h3>What's Next?</h3>
	<ul>
		<li>Layer 3: Network (IP)</li>
		<li>Layer 4: Transport (TCP/UDP)</li>
		<li>Layers 5-7: Application Protocols (HTTP, SNMP, etc.)</li>
	</ul>
</section>

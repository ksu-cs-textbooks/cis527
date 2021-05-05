---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 3 - Transport Layer</p>
</section>
<section>
	<h3>Transport Layer</h3>
	<ul>
		<li>Provides Host-to-Host Communication for Applications</li>
		<li>May Provide Reliability, Flow Control, Sustained Connections</li>
		<li>Typically TCP or UDP</li>
	</ul>
</section>
<section>
	<h3>Transmission Control Protocol (TCP)</h3>
	<ul>
		<li>Stateful</li>
		<li>Reliable
			<ul>
				<li>Acknowledge</li>
				<li>Retransmit</li>
				<li>Rearrange</li>
			</ul>
		</li>
		<li>Connection-Oriented</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="../../images/tcp_state_wiki.svg">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Transmission_Control_Protocol">Wikipedia</a></p>
</section>
<section>
	<h3>TCP Packet</h3>
	<table style="width:100%" class="table">
		<tr><td align="center">Source Port</td><td align="center">Dest. Port</td></tr>
		<tr><td colspan="2" align="center">Sequence Number</td></tr>
		<tr><td colspan="2" align="center">Acknowledgement Number</td></tr>
		<tr><td align="center">Options</td><td align="center">Length</td></tr>
		<tr><td align="center">Checksum</td><td align="center">Urgent</td></tr>
		<tr><td colspan="2" align="center">Data...</td></tr>
	</table>
</section>
<section>
	<h3>User Datagram Protocol (UDP)</h3>
	<ul>
		<li>Stateless</li>
		<li>Unreliable
			<ul>
				<li>No Guarantees!</li>
			</ul>
		</li>
		<li>Connectionless</li>
	</ul>
</section>
<section>
	<h3>UDP Packet</h3>
	<table style="width:100%" class="table">
		<tr><td colspan="2" align="center"><b>UDP Packet Structure</b></td></tr>
		<tr><td align="center">Source Port</td><td align="center">Dest. Port</td></tr>
		<tr><td align="center">Length</td><td align="center">Checksum</td></tr>
		<tr><td colspan="2" align="center">Data...</td></tr>
	</table>
</section>
<section>
	<h3>TCP</h3>
	<p>Great for long, reliable communication between two hosts</p>
	<h3>UDP</h3>
	<p>Great for short bursts of data which could be lost in transit</p>
</section>
<section>
	<h3>Ports</h3>
	<ul>
		<li>Virtual Connection Points on a Host</li>
		<li>Typically 1 Application per Port</li>
		<li>Numbered 0 - 65535 (2<sup>16</sup>)</li>
		<li>Several "Well Known" Ports Have Established Uses</li>
		<li>Outgoing Connections use High-Numbered "Ephemeral" Ports</li>
		<li>Example: 192.168.0.1:1234</li>
	</ul>
</section>
<section>
	<h3>Well Known Ports</h3>
	<ul>
		<li>21 - FTP</li>
		<li>22 - SSH</li>
		<li>23 - Telnet</li>
		<li>25 - SMTP</li>
		<li>53 - DNS</li>
		<li>80 - HTTP</li>
		<li>443 - HTTP over TLS/SSL</li>
	</ul>
</section>
<section>
	<h3>Summary</h3>
	<ul>
		<li>5 - 7: Application Writes a Letter</li>
		<li>4: Transport Adds To/From Name</li>
		<li>3: Network Adds To/From Address</li>
		<li>2: Data Link Puts Into Box(es)</li>
		<li>1: Physical Transports to Next PO</li>
	</ul>
</section>
<section>
	<h3>Summary</h3>
	<ul>
		<li>5 - 7: Application Creates a Packet</li>
		<li>4: Transport Adds To/From Port</li>
		<li>3: Network Adds To/From IP Address</li>
		<li>2: Data Link Puts Into Frame(s)</li>
		<li>1: Physical Transports to Next Node</li>
	</ul>
</section>

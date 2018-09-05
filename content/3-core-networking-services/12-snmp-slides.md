---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 3 - SNMP</p>
</section>
<section>
	<h3>Simple Network Management Protocol (SNMP)</h3>
	<ul>
		<li>Proposed in 1988</li>
		<li>Query Information from Network Devices</li>
		<li>Update Configuration Remotely</li>
		<li>Used in Network Monitoring</li>
		<li>Port 161</li>
	</ul>
</section>
<section>
	<h3>SNMP Versions</h3>
	<ul>
		<li>1.0 - Plain-text, No Security</li>
		<li>2.0 - Some Security, but Controversial</li>
		<li>2.0c "Community" - Without Controversial Security</li>
		<li>3.0 - Better Security & Authentication</li>
	</ul>
	<p>Most Devices Support Multiple Versions</p>
</section>
<section>
	<h3>SNMP Data</h3>
	<ul>
		<li>Data Presented as Variables</li>
		<li>Some Allow Write Access</li>
		<li>Hierarchical Structure</li>
		<li>Difficult to Read Directly</li>
	</ul>
</section>
<section>
	<h3>Management Information Base (MIB)</h3>
	<ul>
		<li>SNMP Does Not Define Variables</li>
		<li>MIB Defines Available Variables</li>
		<li>MIBs Vary by Device</li>
		<li>Standards Exist</li>
	</ul>
</section>
<section>
	<h3>Protocol Data Units (PDU)</h3>
	<ul>
		<li>GetRequest</li>
		<li>SetRequest</li>
		<li>GetNextRequest</li>
		<li>GetBulkRequest</li>
		<li>Response</li>
		<li>Trap</li>
		<li>InformRequest</li>
	</ul>
</section>
<section>
	<h3>Community String</h3>
	<ul>
		<li>Rudimentary Password</li>
		<li>Plaintext in SNMPv1</li>
		<li>Easily Sniffed via Wireshark</li>
		<li>Security was not a Concern Initially</li>
	</ul>
</section>

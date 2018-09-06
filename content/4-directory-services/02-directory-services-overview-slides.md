---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 4 - Directory Services Overview</p>
</section>
<section>
	<h3>Directory Service</h3>
	<ul>
		<li>Store and Retrieve Information</li>
		<li>Multiple Types
			<ul>
				<li>Users</li>
				<li>Groups</li>
				<li>Systems</li>
				<li>Resources</li>
			</ul>
		</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="/images/dns_wiki.png">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Domain_Name_System">Wikipedia</a></p>
</section>
<section>
	<h3>History</h3>
	<ul>
		<li>1988- X.500 Standard Published</li>
		<li>1992 - Samba Released</li>
		<li>1993 - Novell Directory Services</li>
		<li>1993 - Kerberos Protocol</li>
		<li>1999 - Microsoft Active Directory</li>
	</ul>
</section>
<section>
	<h3>X.500 Standard</h3>
	<ul>
		<li>Released in 1988</li>
		<li>Name Lookups for X.400 Email Standards</li>
		<li>Built for OSI Networking Protocols</li>
		<li>Defines Several Protocols
			<ul>
				<li>Directory Access Protocol (DAP)</li>
				<li>Directory System Protocol (DSP)</li>
				<li>Directory Information Shadowing Protocol (DISP)</li>
			</ul>
		</li>
	</ul>
</section>
<section>
	<h3>Lightweight Directory Access Protocol (LDAP)</h3>
	<ul>
		<li>Implementation of X.500 DAP Using TCP/IP</li>
		<li>Used by Many Systems
			<ul>
				<li>Microsoft Active Directory</li>
				<li>Novell Directory Services</li>
				<li>OpenLDAP</li>
			</ul>
		</li>
	</ul>
</section>
<section>
	<h3>LDAP vs. X.500</h3>
	<img class="stretch plain" src="/images/x500ldap_x500standard.png">
	<p class="imagecredit">Image Source: <a href="http://www.x500standard.com/index.php?n=X500.LDAPRelation">x500standard.com</a></p>
</section>
<section>
	<h3>LDAP Uses</h3>
	<img class="stretch plain" src="/images/ldap2_apache.png">
	<p class="imagecredit">Image Source: <a href="https://directory.apache.org/apacheds/basic-ug/1.2-some-background.html">Apache</a></p>
</section>
<section>
	<h3>LDAP Tree Structure</h3>
	<img class="stretch plain" src="/images/ldap_tree_openldap.gif">
	<p class="imagecredit">Image Source: <a href="http://www.openldap.org/doc/admin22/intro.html">Apache</a></p>
</section>
<section>
	<h3>LDAP Entry Items</h3>
	<ul>
		<li>dn - Distinguished Name</li>
		<li>cn - Common Name</li>
		<li>sn - Surname</li>
		<li>dc - Domain Component</li>
		<li>ou - Organizational Unit</li>
	</ul>
</section>
<section>
	<h3>Sample LDAP Entry</h3>
	<pre style="font-size: .75em"><code>dn: cn=John Doe,dc=example,dc=com
cn: John Doe
givenName: John
sn: Doe
telephoneNumber: +1 888 555 6789
telephoneNumber: +1 888 555 1232
mail: john@example.com
manager: cn=Barbara Doe,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top</code></pre>
</section>
<section>
	<h3>Novell Directory Services</h3>
	<ul>
		<li>Released in 1993 by Novell</li>
		<li>Now Called NetIQ eDirectory</li>
		<li>Originally Used IPX/SPX Protocols</li>
		<li>Most Common Directory Service Before Active Directory's Release</li>
	</ul>
</section>
<section>
	<h3>NDS Example</h3>
	<img class="stretch plain" src="/images/nds_novell.gif">
	<p class="imagecredit">Image Source: <a href="http://support.novell.com/techcenter/articles/dnd19970304.html">Novell</a></p>
</section>
<section>
	<h3>Workgroup/Homegroup</h3>
	<ul>
		<li>Windows File Sharing</li>
		<li>Each Computer Has Local Users</li>
		<li>Share Resources Without Server</li>
		<li>Designed for Home Users</li>
	</ul>
</section>
<section>
	<h3>Workgroup</h3>
	<img class="stretch plain" src="/images/workgroup_etutorials.jpg">
	<p class="imagecredit">Image Source: <a href="http://etutorials.org/Microsoft+Products/microsoft+windows+xp+professional+training+kit/Chapter+1+-+Introduction+to+Windows+XP+Professional/Lesson+3nbspUnderstanding+Workgroups+and+Domains/">eTutorials.org</a></p>
</section>
<section>
	<h3>Active Directory</h3>
	<ul>
		<li>Introduced in 1999 with Windows 2000</li>
		<li>Directory Service using LDAP and Kerberos</li>
		<li>Common in Windows-Based Enterprises</li>
		<li>Central Management of Security Policies and More</li>
	</ul>
</section>
<section>
	<h3>Domain</h3>
	<img class="stretch plain" src="/images/domain_etutorials.jpg">
	<p class="imagecredit">Image Source: <a href="http://etutorials.org/Microsoft+Products/microsoft+windows+xp+professional+training+kit/Chapter+1+-+Introduction+to+Windows+XP+Professional/Lesson+3nbspUnderstanding+Workgroups+and+Domains/">eTutorials.org</a></p>
</section>
<section>
	<h3>Kerberos</h3>
	<img class="stretch plain" src="/images/cerberus_wiki.jpg">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Cerberus">Wikipedia</a></p>
</section>
<section>
	<h3>Kerberos Protocol</h3>
	<ul>
		<li>Developed by MIT in 1980s</li>
		<li>Published in 1993 as RCF 1510</li>
		<li>Authentication via 3rd Party Server</li>
		<li>Used by Many LDAP Servers</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="/images/kerberos_wiki.svg">
	<p class="imagecredit">Image Source: <a href="http://en.wikipedia.org/wiki/Kerberos_%28protocol%29">Wikipedia</a></p>
</section>

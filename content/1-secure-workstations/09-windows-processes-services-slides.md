---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 1 - Windows 10 Processes & Services</p>
</section>
<section>
  <h3>Process</h3>
  <ul>
    <li>Any Program being Executed is a Process</li>
    <li>Processes Can Have Multiple <b>Threads</b> of Execution</li>
    <li>Consumes System Resources (RAM, CPU Time)</li>
  </ul>
</section>
<section>
  <h3>Process Information</h3>
  <ul>
    <li><b>PID</b> - Process Identifier</li>
    <li><b>Memory Usage</b></li>
    <li><b>Image Path</b> - Location of Executable File</li>
    <li><b>Command Line</b> - Options and Flags</li>
    <li><b>Ports</b> - Networking Information</li>
    <li><b>Description</b></li>
  </ul>
</section>
<section>
  <h3>Service</h3>
  <ul>
    <li>Program that Runs in the Background</li>
    <li>Managed by the Operating System, not the User</li>
    <li>Performs Important Functions Automatically</li>
    <li>Consumes System Resources</li>
  </ul>
</section>
<section>
  <h3>Pseudo Accounts</h3>
  <ul>
    <li><b>LocalSystem</b> - System-Level Tasks & Services</li>
    <li><b>LocalService</b> - Fewer Permissions than LocalSystem</li>
    <li><b>NetworkService</b> - Fewer Permissions than LocalService, but has Network Access</li>
  </ul>
</section>
<section>
  <h3>Service Host Process</h3>
  <h5>svchost.exe</h5>
  <ul>
    <li>Host Process for Many Services</li>
    <li>Conserve System Resources</li>
    <li>Targeted by Malware & Viruses</li>
  </ul>
</section>
<section>
  <h3>Next: Installing Software</h3>
</section>

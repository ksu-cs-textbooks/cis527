---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 1 - Users & Groups</p>
</section>
<section>
  <h3>User Accounts</h3>
  <ul>
    <li>Share Computer with Multiple People</li>
    <li>Different Permissions for Different Users</li>
    <li>Auditing: Who did What?</li>
    <li>Protect Against Unauthorized Use</li>
  </ul>
</section>
<section>
  <h3>Authentication vs. Authorization</h3>
  <ul>
    <li><b>Authentication</b> - Confirming a User's Identity (Logging In)</li>
    <li><b>Authorization</b> - Allow an Authenticated User Access to Resources</li>
    <li>Authentication <i>DOES NOT IMPLY</i> Authorization</li>
  </ul>
</section>
<section>
  <h3>Authentication Factors</h3>
  <p>One or More of the Following:</p>
  <ul>
    <li><b>Ownership</b> - Something User Has</li>
    <li><b>Knowledge</b> - Something User Knows</li>
    <li><b>Inherence</b> - Something User Is</li>
  </ul>
</section>
<section>
  <h3>Authorization Methods</h3>
  <ul>
    <li>Security Policies</li>
    <li>Access Control Lists (ACLs)</li>
    <li>File Security</li>
  </ul>
</section>
<section>
  <h3>User Identification</h3>
  <ul>
    <li>Unique Identifier for User Account</li>
    <li>Different Than Username</li>
    <li>User Can Change Username, Not Identifier</li>
    <li><b>Linux:</b> User Identifier (UID)</li>
    <li><b>Windows:</b> Security Identifier (SID)</li>
  </ul>
</section>
<section>
  <h3>User Account Information</h3>
  <ul>
    <li>UID / SID</li>
    <li>Username</li>
    <li>Password</li>
    <li>Home Directory</li>
    <li>Group Memberships</li>
  </ul>
</section>
<section>
  <h3>Groups</h3>
  <ul>
    <li>List of Accounts</li>
    <li>Can Assign Permissions to Groups of Users</li>
    <li>Users Can Have Multiple Groups</li>
    <li>Unique Identifier</li>
  </ul>
</section>
<section>
  <h3>Best Practices</h3>
  <ul>
    <li>Each Person has Unique Account</li>
    <li>Strong Passwords & Regular Changes</li>
    <li>Principle of Least Privilege (poLP)</li>
    <li>Create Audit Logs (Login/Logout/sudo)</li>
    <li>Disable Old Users ASAP</li>
    <li>Don't Use Admin Account for Daily Use</li>
  </ul>
</section>

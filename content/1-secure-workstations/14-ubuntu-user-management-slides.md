---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 1 - Ubuntu User Management</p>
</section>
<section>
  <h3>root</h3>
  <ul>
    <li>System Administrator Account</li>
    <li>UID = 0; GID = 0</li>
    <li>Complete Control - No Permissions Checks</li>
    <li>Disabled by Default - No Password</li>
    <li>Set a Password to Enable</li>
    <li>Use "sudo" Instead!</li>
  </ul>
</section>
<section>
  <h3>sudo</h3>
  <ul>
    <li>"Super User Do"</li>
    <li>Run Commands as "root" User</li>
    <li>Add Users to "sudo" Group</li>
    <li>Permissions in /etc/sudoers</li>
    <li>Use "visudo" to Edit File</li>
  </ul>
</section>
<section>
  <h3>Regular User Accounts</h3>
  <ul>
    <li>Can Log On Interactively</li>
    <li>Types: Standard & Administrator</li>
    <li>UID: Start at 1000 and Up</li>
    <li>Has Group of Same Name and GID</li>
    <li>Directory in /home</li>
    <li>Important for Module 4</li>
  </ul>
</section>
<section>
  <h3>System User Accounts</h3>
  <ul>
    <li>Cannot Log On Interactively</li>
    <li>Used by Programs & Services (Daemons)</li>
    <li>Help With File Permissions</li>
  </ul>
</section>
<section>
  <h3>Configuring User Accounts</h3>
  <ul>
    <li>Settings > Details > Users</li>
    <li>Users and Groups from gnome-system-tools</li>
    <li>Terminal</li>
  </ul>
</section>
<section>
  <h3>Terminal Commands</h3>
  <ul>
    <li><b>adduser - add a regular user</b></li>
    <li>useradd - add a system user</li>
    <li>userdel - remove a user</li>
    <li>usermod - modify a user
      <ul>
        <li>usermod -a -G &lt;group> &lt;user> - add user to a group</li>
    </li>
    <li>passwd - change a password</li>
  </ul>
</section>
<section>
  <h3>Terminal Commands</h3>
  <ul>
    <li><b>groupadd - add a group</b></li>
    <li>groupdel - remove a group</li>
    <li>groupmod - modify group</li>
    <li><i>gpasswd - change group restrictions & password</i></li>
    <li><i>newgrp - log in to a new group</i></li>
  </ul>
</section>
<section>
  <h3>Important Files</h3>
  <ul>
    <li>/etc/passwd</li>
    <li>/etc/shadow</li>
    <li>/etc/group</li>
    <li>/etc/gshadow</li>
  </ul>
</section>
<section>
  <h3>Next Step!</h3>
  <p>Start Lab 1, Task 5:</p>
  <p>Configure Ubuntu 18.04</p>
</section>

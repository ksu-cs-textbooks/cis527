---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 2 - Configuration Management Overview</p>
</section>
<section>
  <h3>Manual Configuration</h3>
  <p>Pros:</p>
  <ul>
    <li>Hands-on Management</li>
    <li>Customize Each Computer</li>
    <li>Low Barrier to Entry</li>
    <li>Good for Small Groups</li>
  </ul>
</section>
<section>
  <h3>Manual Configuration</h3>
  <p>Cons:</p>
  <ul>
    <li>Labor Intensive</li>
    <li>Inconsistent Configurations</li>
    <li>Updates on Per-Machine Basis</li>
    <li>Difficult for Large Groups</li>
  </ul>
</section>
<section>
  <h3>How Do We Make System Configuration Scalable?</h3>
</section>
<section>
  <h3>Automation Tools</h3>
  <ul>
    <li>GNU Make</li>
    <li>Scripts</li>
  </ul>
  <h3>Techniques</h3>
  <ul>
    <li>System Images</li>
    <li>Custom Installers</li>
  </ul>
</section>
<section>
  <h3>Defined Configuration</h3>
  <ul>
    <li>List of Configured Items</li>
    <li>High Level</li>
    <li>System Independent</li>
    <li>Any Admin Could Implement</li>
  </ul>
  <p class="fragment">Software Could Implement Too!</li>
</section>
<section>
  <h3>Configuration Management</h3>
  <ul>
    <li>Create Defined Configuration</li>
    <li>Use Tools To Apply Configuration</li>
    <li>Configuration as "Code"</li>
    <li>Reduce Errors & Downtime
      <ul>
        <li>70% of DC Outages Due to Human Error (Source: <a href="https://www.cw.com.hk/it-hk/uptime-institute-70-dc-outages-due-to-human-error">ComputerWorld HK)</a></li>
      </ul>
    </li>
  </ul>
</section>
<section>
  <h3>Tools</h3>
  <p><img class="plain imgcenter" style="height: 2em;" src="/images/puppet_logo.png"></p>
  <div class="container">
    <div class="col">
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/cfengine_wiki.svg"></p>
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/chef_logo.svg"></p>
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/bcfg2_logo.png"></p>
    </div>
    <div class="col">
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/ansible.png"></p>
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/salt_logo.png"></p>
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/vagrant_logo.svg"></p>
    </div>
  </div>
</section>
<section>
  <h3>DevOps</h3>
  <ul>
    <li>"Development Operations"</li>
    <li>Collaboration Between Development & Sysadmin Staff</li>
    <li>Agile Software Development &rarr; Agile Deployment & Testing</li>
    <li>Automation & Monitoring</li>
    <li>Short Development Cycles</li>
    <li>Increased Deployment Frequency</li>
  </ul>
</section>
<section>
  <h3>DevOps Tools</h3>
  <div class="container">
    <div class="col">
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/jenkins_logo.png"></p>
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/docker_logo.png"></p>
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/nagios_logo.png"></p>
    </div>
    <div class="col">
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/travis_logo.png"></p>
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/github_logo.png"></p>
      <p><img class="plain imgcenter" style="height: 2em;" src="/images/heroku_logo.svg"></p>
    </div>
  </div>
</section>

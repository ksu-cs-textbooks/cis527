---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 7 - Backups</p>
</section>
<section>
	<h3>Backup Strategy</h3>
	<ul>
		<li><b>Who</b> Has the Data</li>
		<li><b>What</b> Data to Store</li>
		<li><b>When</b> to Backup</li>
		<li><b>Where</b> to Store Backups</li>
		<li><b>Why</b> Data Loss Occurs</li>
		<li><b>How</b> to Create Backups</li>
	</ul>
</section>
<section>
	<h3>Who</h3>
	<ul>
		<li>Systems</li>
		<li>Servers</li>
		<li>Network Devices</li>
		<li>Credentials</li>
		<li>Security Keys</li>
		<li>Ownership</li>
		<li>Legal Issues</li>
	</ul>
</section>
<section>
	<h3>What</h3>
	<ul>
		<li>Accounting Data</li>
		<li>Human Resources</li>
		<li>Web Assets</li>
		<li>User Data & Files</li>
		<li>Network Configuration</li>
		<li>Filesystems</li>
		<li>Metadata</li>
	</ul>
</section>
<section>
	<h3>When</h3>
	<ul>
		<li>Yearly</li>
		<li>Monthly</li>
		<li>Weekly</li>
		<li>Daily</li>
		<li>Hourly</li>
		<li>Instantly</li>
	</ul>
</section>
<section>
	<h3>RPO vs. RTO</h3>
	<ul>
		<li><b>Recovery Point Objective</b>: How Much Data Might be Lost</li>
		<li><b>Recovery Point Actual</b>: How Much Data Was Lost</li>
		<li><b>Recovery Time Objective</b>: How Much Downtime Expected After Error</li>
		<li><b>Recovery Time Actual</b>: How Long it Actually Took</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="../../images/rpo_wiki.png">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Recovery_time_objective">Recovery Time Objective</a></p>
</section>
<section>
	<h3>Where</h3>
	<ul>
		<li>Hard Disk Drive (HDD)</li>
		<li>Solid State Drive (SSD)</li>
		<li>Optical (CD/DVD)</li>
		<li>Magnetic Tape</li>
		<li>Cloud Storage</li>
		<li>Physical Storage</li>
	</ul>
</section>
<section>
	<h3>Where</h3>
	<ul>
		<li>Online</li>
		<li>Near-Line</li>
		<li>Offline</li>
		<li>Offsite</li>
		<li>Backup Site</li>
	</ul>
</section>
<section>
	<h3>Optimization</h3>
	<ul>
		<li>Compression</li>
		<li>Deduplication</li>
		<li>Encryption</li>
		<li>Staging</li>
		<li>Refactoring</li>
	</ul>
</section>
<section>
	<h3>Why</h3>
	<ul>
		<li><b>Accidental Deletion</b></li>
		<li>Software Failures</li>
		<li>Hardware Failures</li>
		<li>Data Corruption</li>
		<li>Malicious Intent</li>
		<li>Natural Disasters</li>
	</ul>
</section>
<section>
	<h3>How</h3>
	<ul>
		<li>Unstructured</li>
		<li>Full</li>
		<li>Incremental</li>
		<li>Differential</li>
		<li>Reverse Delta</li>
		<li>Continuous</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="../../images/full_nakivo.png">
	<p class="imagecredit">Image Source: <a href="https://www.nakivo.com/blog/backup-types-explained-full-incremental-differential-synthetic-and-forever-incremental/">Nakivo</a></p>
</section>
<section>
	<img class="stretch plain" src="../../images/incremental_nakivo.png">
	<p class="imagecredit">Image Source: <a href="https://www.nakivo.com/blog/backup-types-explained-full-incremental-differential-synthetic-and-forever-incremental/">Nakivo</a></p>
</section>
<section>
	<img class="stretch plain" src="../../images/differential_nakivo.png">
	<p class="imagecredit">Image Source: <a href="https://www.nakivo.com/blog/backup-types-explained-full-incremental-differential-synthetic-and-forever-incremental/">Nakivo</a></p>
</section>
<section>
	<img class="stretch plain" src="../../images/reverse_nakivo.png">
	<p class="imagecredit">Image Source: <a href="https://www.nakivo.com/blog/backup-types-explained-full-incremental-differential-synthetic-and-forever-incremental/">Nakivo</a></p>
</section>
<section>
	<h3>Other Concerns</h3>
	<ul>
		<li>Data Security</li>
		<li>Validation</li>
		<li>Backup Window</li>
		<li>Performance Impact</li>
		<li>Costs & Resources</li>
		<li>Storage Capacity</li>
		<li>Distributed Availability</li>
	</ul>
</section>
<section>
	<h3>High Availability</h3>
	<img class="stretch plain" src="../../images/high_available_do.gif">
	<p class="imagecredit">Image Source: <a href="https://www.digitalocean.com/community/tutorials/what-is-high-availability">DigitalOcean</a></p>
</section>

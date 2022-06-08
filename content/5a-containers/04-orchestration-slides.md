---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 5.A - Orchestration</p>
</section>
<section>
	<h3>Container Orchestration</h3>
	<ul>
		<li>Deploy Containers at Scale</li>
		<li>Multiple Copies, Multiple Nodes</li>
		<li>Handle Routing, Restarting</li>
		<li>Lab 2 - Automate!</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="/images/5a/docker-swarm.png.webp">
	<p class="imagecredit">Image Source: <a href="https://devopscube.com/docker-container-clustering-tools/">DevopsCube</a></p>
</section>
<section>
	<h3>Docker Compose</h3>
	<ul>
		<li>Isolated Environments</li>
		<li>Preserve Data</li>
		<li>Infrastructure as Code</li>
		<li>Easily Apply Changes</li>
		<li>Portability</li>
	</ul>
</section>
<section>
	<h3>Docker Compose File</h3>
	<p>Filename: <code>docker-compose.yml</code></p>
	<pre><code class="yml">services:                   # top level item
  nginx:                    # name of service
    image: nginx:alpine     # image to use
    container_name: nginx1  # name of container</code></pre>
  mysql:
    image: mysql:latest
	container_name: mysql
</section>
<section>
	<h3>Docker Compose Commands</h3>
	<ul>
		<li><code>docker compose up [-d]</code></li>
		<li><code>docker compose down</code></li>
		<li><code>docker compose start</code></li>
		<li><code>docker compose run [service]</code></li>
	</ul>
</section>
<section>
	<h3>Composability</h3>
	<pre><code class="yml"># docker-compose.yml
services:
  webserver:
    container_name: webserver
    extends:
      file: nginx.yml
      service: nginx
    # custom configuration here</code></pre>
	<pre><code class="yml"># nginx.yml
services:
  nginx:
    image: nginx:alpine
    # default configuration here</code></pre>
</section>

---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 5.A - Docker</p>
</section>
<section>
	<img class="stretch plain" src="/images/5a/docker_logo.svg">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/File:Docker_logo.svg">Wikipedia</a></p>
</section>
<section>
	<h3>Terminology</h3>
	<ul>
		<li><b>Image:</b> read-only template to build a container. May be based on another image</li>
		<li><b>Container:</b> a runnable instance of an image</li>
		<li><b>Volume:</b> a persistent storage location outside a container</li>
	</ul>
</section>
<section>
	<h3>Docker Components</h3>
	<ul>
		<li>Docker Engine<ul>
			<li>Docker Daemon</li>
			<li>Docker Client</li>
		</ul></li>
		<li><i>Docker Desktop</i></li>
		<li>Docker Compose</li>
		<li><i>Registry</i></li>
	</ul>
</section>
<section>
	<h3>Docker Commands</h3>
	<ul>
		<li><code>pull</code> - Download an Image</li>
		<li><code>images</code> - List images</li>
		<li><code>run</code> - Create a Container</li>
		<li><code>start | stop</code> - Start/Stop Container</li>
		<li><code>ps</code> - List Running Containers</li>
		<li><code>exec</code> - Run Command in Container</li>
		<li><code>logs</code> - View Container Logs</li>
	</ul>
</section>
<section>
	<h3>Docker Images</h3>
	<ul>
		<li>Docker Hub</li>
		<li>Other Repositories</li>
		<li>Tags</li>
		<li>Alpine vs. Others</li>
		<li>Official vs. Community</li>
	</ul>
</section>
<section>
	<h3>Show Docker Hub</h3>
	<ul>
		<li>Official Images</li>
		<li>Hello World</li>
		<li>Nginx</li>
	</ul>
</section>
<section>
	<h3>Commands</h3>
	<ul>
		<li><code>docker pull hello-world</code></li>
		<li><code>docker run hello-world</code></li>
		<li><code>docker run -d nginx:alpine</code></li>
		<li><code>docker ps</code></li>
		<li><code>docker exec -it <nginx> /bin/sh</code></li>
		<li><code>curl localhost:80</code></li>
		<li><code>docker stop [container]</code></li>
		<li><code>docker container prune</code></li>
	</ul>
</section>
<section>
	<h3>Open Questions</h3>
	<ul>
		<li>How to access outside Docker?</li>
		<li>How to host own files in Nginx?</li>
		<li>How to persist data from Containers?</li>
		<li>How to simplify Docker commands?</li>
	</ul>
</section>
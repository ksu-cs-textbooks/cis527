---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 5.A - Building Images</p>
</section>
<section>
	<h3>Building Images</h3>
	<ul>
		<li>Create <code>Dockerfile</code></li>
		<li>Choose base image</li>
		<li>Configure image</li>
		<li>Copy application files</li>
		<li>Configure application</li>
		<li>Set command and ports</li>
	</ul>
</section>
<section>
	<h3>Follow Along!</h3>
	<p>https://docs.docker.com/get-started/</p>
</section>
<section>
	<h3>Step 1 - Get Code</h3>
	<pre><code class="bash">git clone https://github.com/docker/getting-started.git
cd getting-started/app
# open in text editor
</code></pre>
</section>
<section>
	<h3>Step 2 - Create Dockerfile</h3>
	<pre><code># syntax=docker/dockerfile:1
FROM node:12-alpine
RUN apk add --no-cache python2 g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000</code></pre>
</section>
<section>
	<h3>Step 3 - Build & Run</h3>
	<pre><code class="bash">docker build -t getting-started .
docker run -d -p 3000:3000 getting-started</code></pre>
</section>
<section>
	<h3>Step 4 - Updated & Rebuild</h3>
	<pre><code class="bash"># edit src/static/js/app.js line 56
docker build -t getting-started .
docker stop [container]
docker run -d -p 3000:3000 getting-started</code></pre>
</section>
<section>
	<h3>Step 5 - Share Container!</h3>
	<ul>
		<li>Docker Hub</li>
		<li>GitHub</li>
		<li>GitLab</li>
	</ul>
</section>
<section>
	<h3>Step 6 - Scan Image</h3>
	<pre><code class="bash">docker scan getting-started</code></pre>
    <img class="stretch plain" src="/images/5a/docker-vuln.png">
</section>
<section>
	<h3>Step 7 - Cached Layers</h3>
	<pre class="stretch"><code># syntax=docker/dockerfile:1
FROM node:12-alpine
RUN apk add --no-cache python2 g++ make
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install --production
COPY . .
CMD ["node", "src/index.js"]
EXPOSE 3000</code></pre>
	<pre><code># .dockerignore
node_modules</code></pre>
<br></br>
</section>

---
type: "reveal"
hidden: true
---
<section>
    <h2>CIS 527</h2><br><br><p>Lab 5.A - Reverse Proxy</p>
</section>
<section>
    <img class="stretch plain" src="/images/5a/reverse-proxy.webp">
    <p class="imagecredit">Image Source: <a href="https://linuxhandbook.com/nginx-reverse-proxy-docker/">Linux Handbook</a></p>
</section>
<section>
    <h3>Option 1 - Nginx</h3>
    <pre class="stretch"><code class="yml" style="font-size: 30px; line-height: 34px">services:
  nginx:
    image: nginx:alpine
    container_name: proxy
    ports:
      - "8080:80"
    volumes:
      - /home/cis527/docker/proxy:/etc/nginx/templates:ro
    networks:
      - default
      - internal
  whoami1:
    image: jwilder/whoami
    container_name: whoami1
    networks:
      - internal
  whoami2:
    image: jwilder/whoami
    container_name: whoami2
    networks:
      - internal
networks:
  internal:
    internal: true</code></pre>
</section>
<section>
    <h3>Option 1 - Nginx</h3>
    <pre class="stretch"><code class="nginx" style="font-size: 25px; line-height: 28px"># /home/cis527/docker/proxy/default.conf.template
server {
    listen 80;
    server_name one.local;
    location / {
        proxy_pass http://whoami1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_buffering off;
        proxy_request_buffering off;
        proxy_http_version 1.1;
        proxy_intercept_errors on;
    }
}
server {
    listen 80;
    server_name two.local;
    location / {
        proxy_pass http://whoami2:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_buffering off;
        proxy_request_buffering off;
        proxy_http_version 1.1;
        proxy_intercept_errors on;
    }
}</code></pre>
</section>
<section>
    <h3>Option 1 - Nginx</h3>
    <img class="stretch plain" src="/images/5a/proxy1.png">
</section>
<section>
    <h3>Option 2 - Nginx Proxy</h3>
    <pre class="stretch"><code class="yml" style="font-size: 25px; line-height: 27px">services:
  proxy:
    image: jwilder/nginx-proxy:latest
    container_name: proxy
    ports:
      - "8080:80"
    volumes:
      # Security Concern!
      - /var/run/docker.sock:/tmp/docker.sock:ro
    networks:
      - default
      - internal
  whoami1:
    image: jwilder/whoami
    container_name: whoami1
    networks:
      - internal
    environment:
      - VIRTUAL_HOST=one.local
      - VIRTUAL_PORT=8000
  whoami2:
    image: jwilder/whoami
    container_name: whoami2
    networks:
      - internal
    environment:
      - VIRTUAL_HOST=two.local
      - VIRTUAL_PORT=8000
networks:
  internal:
    internal: true</code></pre>
</section>
<section>
    <h3>Option 2 - Nginx Proxy</h3>
    <img class="stretch plain" src="/images/5a/proxy2.png">
</section>
<section>
    <h3>Security Concern</h3>
    <ul>
        <li>Uses Docker Socket</li>
        <li>Allows Detection of Containers</li>
        <li>root in container = root on host</li>
        <li>Secure using TLS</li>
        <li>Protect via proxy</li>
        <li><i>Don't expose to internet!</i></li>
    </ul>
</section>
<section>
    <h3>Option 3 - Traefik Proxy</h3>
    <img class="stretch plain" src="/images/5a/traefik-logo.svg">
    <p class="imagecredit">Image Source: <a href="https://doc.traefik.io/traefik/">Traefik</a></p>
</section>
<section>
    <h3>Option 3 - Traefik Proxy</h3>
    <pre class="stretch"><code class="yml" style="font-size: 24px; line-height: 26px">services:
  proxy:
    image: traefik:v2.7
    container_name: proxy
    command: --api.insecure=true --providers.docker
    ports:
      - "8080:80"       # proxy
      - "8081:8080"     # web dashboard
    volumes:
      # Security Concern!
      - /var/run/docker.sock:/var/run/docker.sock
    networks:
      - default
      - internal
  whoami1:
    image: jwilder/whoami
    container_name: whoami1
    networks:
      - internal
    labels:
      - "traefik.http.routers.whoami1.rule=Host(`one.local`)"
      - "traefik.http.services.whoami1.loadbalancer.server.port=8000"
  whoami2:
    image: jwilder/whoami
    container_name: whoami2
    networks:
      - internal
    labels:
      - "traefik.http.routers.whoami2.rule=Host(`two.local`)"
      - "traefik.http.services.whoami2.loadbalancer.server.port=8000"
networks:
  internal:
    internal: true</code></pre>
</section>
<section>
    <h3>Option 3 - Traefik Proxy</h3>
    <img class="stretch plain" src="/images/5a/proxy3.png"></img>
</section>
<section>
    <h3>Option 3 - Traefik Proxy</h3>
    <img class="stretch plain" src="/images/5a/traefik-dashboard.png"></img>
</section>
<section>
    <h3>Summary</h3>
    <ul>
        <li>Nginx</li>
        <li>Nginx Proxy</li>
        <li>Traefik</li>
        <li><i>Many Others</i></li>
    </ul>
    <p><i>Kubernetes handles this for you</i></p>
</section>
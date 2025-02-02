---
type: "reveal"
hidden: true
---
<section>
    <h2>CIS 527</h2><br><br><p>Lab 5.A - Resources</p>
</section>
<section>
    <h3>Container Resources</h3>
    <ul>
        <li>Mapped Network Ports</li>
        <li>Networks</li>
        <li>Environment Variables</li>
        <li>Storage Volumes</li>
    </ul>
</section>
<section>
    <h3>Mapped Ports</h3>
    <img class="stretch plain" src="/cis527/images/5a/docker-ports.png">
    <p class="imagecredit">Image Source: <a href="https://www.docker.com/blog/understanding-docker-networking-drivers-use-cases/">Docker</a></p>
</section>
<section>
    <h3>Mapped Ports</h3>
    <pre><code class="bash">docker run -d -p 8080:80 --name nginx1 nginx:alpine</code></pre>
    <pre><code class="yml">services:
  nginx:
    image: nginx:alpine
    container_name: nginx1
    ports:
      - "8080:80"</code></pre>
    <p><code>curl localhost:8080</code></p>
</section>
<section>
    <h3>Inspecting Ports</h3>
    <p><code>docker ps</code></p>
    <pre><code class="bash" style="font-size: 20px; line-height: 22px">CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                   NAMES
a1ef8911ce52   nginx:alpine   "/docker-entrypoint.…"   8 minutes ago   Up 8 minutes   0.0.0.0:8080->80/tcp    nginx1
</code></pre>
</section>
<section>
    <h3>Docker Networks</h3>
    <img class="stretch plain" src="/cis527/images/5a/docker-network.png">
    <p class="imagecredit">Image Source: <a href="https://docs.docker.com/engine/tutorials/networkingcontainers/">Docker</a></p>
</section>
<section>
    <h3>Docker Networks</h3>
    <pre><code style="font-size: 35px" class="bash">docker run -d -p 8080:80 --name nginx1 nginx:alpine
docker network create -d bridge --internal redis_network
docker network connect redis_network nginx1
docker run -d --name redis1 --network redis_network redis:latest</code></pre>
</section>
<section>
    <h3>Docker Networks</h3>
    <pre class="stretch"><code style="line-height: 48px" class="yml">services:
  nginx:
    image: nginx:alpine
    container_name: nginx1
    ports:
      - "8080:80"
    networks:
      - redis_network
      - default
  redis:
    image: redis:latest
    container_name: redis1
    networks:
      - redis_network
networks:
  redis_network:
    internal: true
    </code></pre>
</section>
<section>
    <h3>Inspecting Networks</h3>
    <p><code>docker network inspect [network]</code></p>
    <pre><code style="font-size: 20px; line-height: 22px" class="json">[ {
    "Name": "docker_default",
    ...
    "Containers": {
        "a1ef8911ce524b8345c0e047798072c4cba2c6bb1a2dafd4a37e9b577b2c34d0": {
            "Name": "nginx1",
            "EndpointID": "716dec048ad8b8ccdab793cceb93881c775af5335671555b3c437b395fde35dd",
            "MacAddress": "02:42:ac:15:00:02",
            "IPv4Address": "172.21.0.2/16",
            "IPv6Address": ""
} } } ]</code></pre>
<pre><code style="font-size: 20px; line-height: 22px" class="json">[ {
    "Name": "docker_redis_network",
    // ...
    "Containers": {
        "a1ef8911ce524b8345c0e047798072c4cba2c6bb1a2dafd4a37e9b577b2c34d0": {
            "Name": "nginx1",
            "EndpointID": "af8f3f616491df592fbc21d665e51e7a7f6989abc557e76ea56bf7c71158db00",
            "MacAddress": "02:42:ac:14:00:03",
            "IPv4Address": "172.20.0.3/16",
            "IPv6Address": ""
        },
        "bfa602ef48b0fe744d59d2c450f271ad108cae23c7cb5f2b4f021961db25a978": {
            "Name": "redis1",
            "EndpointID": "a0a761e9c91282bbb7715428385182f2dddcf0022c1f66731a91135a243bde19",
            "MacAddress": "02:42:ac:14:00:02",
            "IPv4Address": "172.20.0.2/16",
            "IPv6Address": ""
} } } ]</code></pre>
</section>
<section>
    <h3>Environment Variables</h3>
    <img class="stretch plain" src="/cis527/images/5a/docker-env.png">
    <p class="imagecredit">Image Source: <a href="https://vsupalov.com/docker-arg-env-variable-guide/">Vladislav Supalov</a></p>
</section>
<section>
    <h3>Environment Variables</h3>
    <pre><code style="font-size: 35px" class="bash">docker network create -d bridge --internal mysql_network
docker network create -d bridge mysql_default
docker run -d --name mysql1 --network mysql_network 
        -e MYSQL_ROOT_PASSWORD=password mysql:latest
docker run -d --name mysqladmin1 --network mysql_default 
        -e PMA_HOST=mysql1 -p 8080:80 phpmyadmin/phpmyadmin:latest
docker network connect mysql_network mysqladmin1
</code></pre>
</section>
<section>
    <h3>Environment Variables</h3>
    <pre class="stretch"><code style="font-size: 35px; line-height: 40px" class="yml">services:
  mysql:
    image: mysql:latest
    container_name: mysql1
    networks:
      - mysql_network
    environment:
      MYSQL_ROOT_PASSWORD: password
  mysqladmin:
    image: phpmyadmin/phpmyadmin:latest
    container_name: mysqladmin1
    ports:
      - "8080:80"
    networks:
      - default
      - mysql_network
    environment:
      PMA_HOST: mysql1
networks:
  mysql_network:
    internal: true</code></pre>
</section>
<section>
    <h3>Inspecting Environments</h3>
    <p><code>docker inspect [container]</code></p>
    <pre><code style="font-size: 20px; line-height: 22px" class="json">[ {
    // ... 
    "Name": "/mysql1",
    // ...
    "Config": {
        // ...
        "Env": [
            "MYSQL_ROOT_PASSWORD=password",
            "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
            "GOSU_VERSION=1.14",
            "MYSQL_MAJOR=8.0",
            "MYSQL_VERSION=8.0.29-1debian10"
        ],
        // ...
        "Image": "mysql:latest",
        // ...
    } 
} ]</code></pre>
</section>
<section>
    <h3>Storage Volumes</h3>
    <ul>
        <li>Add something to database</li>
        <li>Stop using <code>docker compose down</code></li>
        <li>Restart using <code>docker compose up -d</code></li>
        <li>Check database again - is it there?</li>
    </ul>
</section>
<section>
    <h3>Volumes & Mounts</h3>
    <img class="stretch plain" src="/cis527/images/5a/docker-volume.png">
    <p class="imagecredit">Image Source: <a href="https://docs.docker.com/storage/volumes/">Docker</a></p>
</section>
<section>
    <h3>Bind Mount</h3>
    <pre><code class="bash">mkdir /home/cis527/mysql
docker run -d --name mysql1 --network mysql_network 
        -e MYSQL_ROOT_PASSWORD=password 
        -v /home/cis527/mysql:/var/lib/mysql
        mysql:latest</code></pre>
    <pre class="stretch"><code style="font-size: 35px; line-height: 40px" class="yml">services:
  mysql:
    image: mysql:latest
    container_name: mysql1
    networks:
      - mysql_network
    environment:
      MYSQL_ROOT_PASSWORD: password
    volumes:
      - /home/cis527/mysql:/var/lib/mysql
  # ...</code></pre>
</section>
<section>
    <h3>Docker Volume</h3>
    <pre><code class="bash">docker volume create mysql_data
docker run -d --name mysql1 --network mysql_network 
        -e MYSQL_ROOT_PASSWORD=password 
        -v mysql_data:/var/lib/mysql
        mysql:latest</code></pre>
    <pre class="stretch"><code style="font-size: 35px; line-height: 40px" class="yml">services:
  mysql:
    image: mysql:latest
    container_name: mysql1
    networks:
      - mysql_network
    environment:
      MYSQL_ROOT_PASSWORD: password
    volumes:
      - mysql_data:/var/lib/mysql
  # ...
volumes:
  mysql_data:    
</code></pre>
</section>
<section>
    <h3>Inspecting Volumes</h3>
    <p><code>docker inspect [container]</code></p>
    <pre class="stretch"><code style="font-size: 35px; line-height: 42px" class="json">[ {
    // ...
    "Name": "/mysql1",
    // ...
    "Mounts": [
        {
            "Type": "volume",
            "Name": "docker_mysql_data",
            "Source": "/var/lib/docker/volumes/docker_mysql_data/_data",
            "Destination": "/var/lib/mysql",
            "Driver": "local",
            "Mode": "z",
            "RW": true,
            "Propagation": ""
        }
    ]
} ]</code></pre>
</section>
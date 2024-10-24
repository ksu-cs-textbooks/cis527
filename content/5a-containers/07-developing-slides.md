---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 5.A - Developing with Containers</p>
</section>
<section>
	<h3>Developing with Containers</h3>
	<ul>
		<li>Dockerfile</li>
		<li>Docker Compose</li>
		<li>Develop in Docker</li>
		<li>CI/CD Pipelines</li>
	</ul>
</section>
<section>
	<h3>Dockerfile</h3>
	<pre class="stretch"><code style="font-size: 28px; line-height: 40px"># For more information, please refer to https://aka.ms/vscode-docker-python
FROM python:3.8-slim
EXPOSE 5000
# Keeps Python from generating .pyc files in the container
ENV PYTHONDONTWRITEBYTECODE=1
# Turns off buffering for easier container logging
ENV PYTHONUNBUFFERED=1
# Install pip requirements
COPY requirements.txt .
RUN python -m pip install -r requirements.txt
WORKDIR /app
COPY . /app
# Creates a non-root user with an explicit UID and adds permission to access the /app folder
# For more info, please refer to https://aka.ms/vscode-docker-python-configure-containers
RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app
USER appuser
# During debugging, this entry point will be overridden. For more information, 
# please refer to https://aka.ms/vscode-docker-python-debug
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "wsgi:app"]</code></pre>
</section>
<section>
	<h3>Docker Compose</h3>
	<pre class="stretch"><code style="font-size: 28px; line-height: 40px">services:
  mysql:
    image: mysql:5.7
    container_name: mysql
    restart: unless-stopped
    ports:
      - '3306:3306'
    environment:
      MYSQL_DATABASE: officehours
      MYSQL_USER: officehours
      MYSQL_PASSWORD: password
      MYSQL_RANDOM_ROOT_PASSWORD: fact
  phpmyadmin:
    image: phpmyadmin:latest
    container_name: phpmyadmin
    restart: unless-stopped
    ports:
      - '8080:80'
    environment:
      PMA_ARBITRARY: 1
	</code></pre>
</section>
<section>
	<h3>Develop in Docker</h3>
    <img class="stretch plain" src="/cis527/images/5a/architecture-containers.png">
    <p class="imagecredit">Image Source: <a href="https://code.visualstudio.com/docs/remote/containers">Visual Studio Code</a></p>
</section>
<section>
	<h3>CI/CD Pipelines - GitHub</h3>
	<pre class="stretch"><code style="font-size: 35px; line-height: 39px" class="yml">name: Docker Image CI<br>
jobs:
  build:
    runs-on: ubuntu-latest<br>
    steps:
    - uses: actions/checkout@v3<br>
    - name: Login to GitHub Container Registry
      uses: docker/login-action@v1 
      with:
        registry: ghcr.io
        username: ${{ github.repository_owner }}
        password: ${{ secrets.GITHUB_TOKEN }}<br>
    - name: Build and push
      uses: docker/build-push-action@v2
      with:
        push: true
        tags: |
            ghcr.io/${{ github.repository_owner }}/ksucs-hugo:latest</code></pre>
</section>
<section>
	<h3>CI/CD Pipelines - GitLab</h3>
	<pre class="stretch"><code style="font-size: 30px; line-height: 32px" class="yml">image: docker:20.10.11<br>
variables:
  DOCKER_HOST: tcp://docker:2375
  DOCKER_TLS_CERTDIR: ""
  GIT_SUBMODULE_STRATEGY: recursive<br>
services:
  - docker:20.10.11-dind<br>
before_script:
  - docker info
  - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY<br>
build-latest:
  stage: build
  only:
    - master
    - main
  script:
    - docker pull $CI_REGISTRY_IMAGE:latest || true
    - >
      docker build --cache-from $CI_REGISTRY_IMAGE:latest 
      --tag $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA 
      --tag $CI_REGISTRY_IMAGE:latest .
    - docker push $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA
    - docker push $CI_REGISTRY_IMAGE:latest</code></pre>
</section>
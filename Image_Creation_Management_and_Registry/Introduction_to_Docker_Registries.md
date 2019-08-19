<h2>Introduction to Docker Registries</h2>
<div class="close-video-menu">&nbsp;</div>
<p>Docker registries provide a central location to store and distribute images. In this lesson, we will discuss what registries are and some of the available options for using them. We will demonstrate how to run a private registry, and discuss how to enable authentication and TLS to secure a private registry.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/registry/deploying/">https://docs.docker.com/registry/deploying/</a></li>
<li><a href="https://docs.docker.com/registry/configuration/">https://docs.docker.com/registry/configuration/</a></li>
<li><a href="https://docs.docker.com/registry/insecure/">https://docs.docker.com/registry/insecure/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<p>Run a simple registry:</p>
<pre><code>docker run -d -p 5000:5000 --restart=always --name registry registry:2
docker container stop registry &amp;&amp; docker container rm -v registry
</code></pre>
<p>Override the log level using an environment variable:</p>
<pre><code>docker logs registry
docker container stop registry &amp;&amp; docker container rm -v registry
docker run -d -p 5000:5000 --restart=always --name registry -e REGISTRY_LOG_LEVEL=debug registry:2
docker logs registry
docker container stop registry &amp;&amp; docker container rm -v registry
</code></pre>
<p>Secure the registry by generating an&nbsp;<code>htpasswd</code>&nbsp;file to be used for authentication:</p>
<pre><code>mkdir ~/registry
cd ~/registry
mkdir auth
docker run --entrypoint htpasswd registry:2 -Bbn testuser password &gt; auth/htpasswd
</code></pre>
<p>Generate a self-signed certificate. When generating the cert, leave the prompts blank&nbsp;<strong><em>except</em></strong>&nbsp;for&nbsp;<em>Common Name</em>. For&nbsp;<em>Common Name</em>, put the public hostname of the registry server. The public hostname is in the playground interface:</p>
<pre><code>mkdir certs
openssl req \
  -newkey rsa:4096 -nodes -sha256 -keyout certs/domain.key \
  -x509 -days 365 -out certs/domain.crt
</code></pre>
<p>Run the registry with authentication and TLS enabled:</p>
<pre><code>docker run -d -p 443:443 --restart=always --name registry \
  -v /home/cloud_user/registry/certs:/certs \
  -v /home/cloud_user/registry/auth:/auth \
  -e REGISTRY_HTTP_ADDR=0.0.0.0:443 \
  -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt \
  -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key \
  -e REGISTRY_AUTH=htpasswd \
  -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm" \
  -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd \
  registry:2</code></pre>

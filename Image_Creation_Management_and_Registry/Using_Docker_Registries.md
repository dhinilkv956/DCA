<h2>Using Docker Registries</h2>
<p>Once we have created a private registry, we need to be able to access and interact with it. In this lesson, we will discuss how to use registries from the command line then we will demonstrate how to authenticate against a private registry with a self-signed certificate, as well as how to push to and pull from a private registry.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/reference/commandline/push/">https://docs.docker.com/engine/reference/commandline/push/</a></li>
<li><a href="https://docs.docker.com/engine/reference/commandline/pull/">https://docs.docker.com/engine/reference/commandline/pull/</a></li>
<li><a href="https://docs.docker.com/engine/reference/commandline/login/">https://docs.docker.com/engine/reference/commandline/login/</a></li>
<li><a href="https://docs.docker.com/registry/insecure/">https://docs.docker.com/registry/insecure/</a></li>
<li><a href="https://docs.docker.com/engine/reference/commandline/search/">https://docs.docker.com/engine/reference/commandline/search/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<p>Pull and search images on Docker hub:</p>
<pre><code>docker pull ubuntu
docker search ubuntu
</code></pre>
<p>Attempt to authenticate against the private registry:</p>
<pre><code>docker login &lt;registry public hostname&gt;
</code></pre>
<p>Log in with the credentials we created earlier (<code>testuser</code>&nbsp;and&nbsp;<code>password</code>). A&nbsp;<code>certificate signed by unknown authority</code>&nbsp;message should pop up, because we are using a self-signed certificate.</p>
<p>Configure docker to ignore certificate verification when accessing the private registry:</p>
<pre><code>sudo vi /etc/docker/daemon.json
</code></pre>
<pre><code>{
  "insecure-registries" : ["&lt;registry public hostname&gt;"]
}
</code></pre>
<p>Restart docker:</p>
<pre><code>sudo systemctl restart docker
</code></pre>
<p>Try&nbsp;<code>docker login</code>&nbsp;again:</p>
<pre><code>docker login &lt;registry public hostname&gt;
</code></pre>
<p>This time it should work!</p>
<p>However, this method of accessing the registry is very insecure. It turns off certificate verification entirely, exposing us to man-in-the-middle attacks. So, let's do this the right way.</p>
<p>First, log out of the private registry:</p>
<pre><code>docker logout &lt;registry public hostname&gt;
</code></pre>
<p>Next, remove the&nbsp;<code>insecure-registries</code>&nbsp;key and value from&nbsp;<code>/etc/docker/daemon.json</code>.</p>
<p>Restart Docker:</p>
<pre><code>sudo systemctl restart docker
</code></pre>
<p>Download the cert public key from the registry and configure the local docker engine to use it:</p>
<pre><code>sudo mkdir -p /etc/docker/certs.d/&lt;registry public hostname&gt;
sudo scp cloud_user@&lt;registry public hostname&gt;:/home/cloud_user/registry/certs/domain.crt /etc/docker/certs.d/&lt;registry public hostname&gt;
</code></pre>
<p>Try&nbsp;<code>docker login</code>:</p>
<pre><code>docker login &lt;registry public hostname&gt;
</code></pre>
<p>Push to and pull from your private registry:</p>
<pre><code>docker pull ubuntu
docker tag ubuntu &lt;registry public hostname&gt;/ubuntu
docker push &lt;registry public hostname&gt;/ubuntu
docker image rm &lt;registry public hostname&gt;/ubuntu
docker image rm ubuntu
docker pull &lt;registry public hostname&gt;/ubuntu
</code></pre>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16415" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>

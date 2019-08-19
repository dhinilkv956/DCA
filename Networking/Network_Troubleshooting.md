<h2>Network Troubleshooting</h2>
<p>Docker has many powerful features that you can use to implement a container networking setup that meets your needs, but sometimes you will need to be able to locate and diagnose issues. In this lesson, we will discuss some basic troubleshooting techniques. We will talk about some ways of accessing useful log data, and we will discuss using the&nbsp;<code>netshoot</code>&nbsp;image to test from within various parts of your Docker networks.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://success.docker.com/article/troubleshooting-container-networking">https://success.docker.com/article/troubleshooting-container-networking</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Run a container and access the container logs.</p>
<pre><code> docker run --name log-container busybox echo Here is my container log!
 docker logs log-container
</code></pre>
</li>
<li>
<p>Run a service and access the service logs.</p>
<pre><code> docker service create --name log-svc --replicas 3 -p 8080:80 nginx
 curl localhost:8080
 docker service logs log-svc
</code></pre>
</li>
<li>
<p>Check the Docker daemon logs.</p>
<pre><code> sudo journalctl -u docker
</code></pre>
</li>
<li>
<p>Create a custom network with a container, and attach a netshoot container to the network for troubleshooting.</p>
<pre><code> docker network create custom-net
 docker run -d --name custom-net-nginx --network custom-net nginx
</code></pre>
</li>
<li>
<p>Inject a netshoot container into another container's network sandbox.</p>
<pre><code> docker run --rm --network custom-net nicolaka/netshoot curl custom-net-nginx:80
 docker run --rm --network container:custom-net-nginx nicolaka/netshoot curl localhost:80
</code></pre>
</li>
<li>
<p>Inject a netshoot container into the sandbox of a container that uses the&nbsp;<code>none</code>&nbsp;network.</p>
<pre><code> docker run -d --name none-net-nginx --network none nginx
 docker run --rm --network container:none-net-nginx nicolaka/netshoot curl localhost:80
</code></pre>
</li>
</ol>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16433" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>

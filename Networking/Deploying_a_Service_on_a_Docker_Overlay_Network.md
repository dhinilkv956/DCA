<h2>Deploying a Service on a Docker Overlay Network</h2>
<div class="close-video-menu">
<p>Overlay networks provide transparent network connectivity to containers running in a Swarm, regardless of whether they are running on the same or different nodes. In this lesson, we will discuss overlay networks and demonstrate how to use them to connect containers in a Docker Swarm.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/network/overlay/">https://docs.docker.com/network/overlay/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>List the networks on the host. You should be able to see the default&nbsp;<code>ingress</code>&nbsp;overlay network.</p>
<pre><code> docker network ls
</code></pre>
</li>
<li>
<p>Create an attachable overlay network.</p>
<pre><code> docker network create --driver overlay --attachable my-overlay
</code></pre>
</li>
<li>
<p>Create a service that uses that network, then test the network by attaching a container to it and using the container to communicate with the service.</p>
<pre><code> docker service create --name overlay-service --network my-overlay --replicas 3 nginx
 docker run --rm --network my-overlay radial/busyboxplus:curl curl overlay-service:80
</code></pre>
</li>
</ol>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16437" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>

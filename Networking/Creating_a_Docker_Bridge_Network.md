<h2>Creating a Docker Bridge Network</h2>
<p>Bridge networks facilitate communication between Docker containers on the same host. In this lesson, we will explore bridge networks in a little more detail. We will discuss the commands needed to create and use bridge networks. We will also examine Docker's embedded DNS, and how to use it to communicate with containers using container names and network aliases. We will also talk about some commands that can be used to manage existing networks on a Docker host.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/network/bridge/">https://docs.docker.com/network/bridge/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Create a bridge network and demonstrate that two containers can communicate using the network.</p>
<pre><code class="lang-bash"> docker network create my-net
 docker run -d --name my-net-busybox --network my-net radial/busyboxplus:curl sleep 3600
 docker run -d --name my-net-nginx nginx
 docker network connect my-net my-net-nginx
 docker exec my-net-busybox curl my-net-nginx:80
</code></pre>
</li>
<li>
<p>Create a container with a network alias and communicate with it from another container using both the name and the alias.</p>
<pre><code class="lang-bash"> docker run -d --name my-net-nginx2 --network my-net --network-alias my-nginx-alias nginx
 docker exec my-net-busybox curl my-net-nginx2:80
 docker exec my-net-busybox curl my-nginx-alias:80
</code></pre>
</li>
<li>
<p>Create a container and provide a network alias with the&nbsp;<code>docker network connect</code>&nbsp;command.</p>
<pre><code class="lang-bash"> docker run -d --name my-net-nginx3 nginx
 docker network connect --alias another-alias my-net my-net-nginx3
 docker exec my-net-busybox curl another-alias:80
</code></pre>
</li>
<li>
<p>Manage existing networks on a Docker host.</p>
<pre><code class="lang-bash"> docker network ls
 docker network inspect my-net
 docker network disconnect my-net my-net-nginx
 docker network rm my-net</code></pre>
</li>
</ol>

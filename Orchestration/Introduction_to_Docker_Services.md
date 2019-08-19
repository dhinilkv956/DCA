<h2>Introduction to Docker Services</h2>
<p>Services are the simplest way to make use of a Docker Swarm cluster. In this lesson, we will be discussing Docker services. We will demonstrate how to create and manage services and talk about several important concepts related to services.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/swarm/services/">https://docs.docker.com/engine/swarm/services/</a></li>
<li><a href="https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/">https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/</a></li>
<li><a href="https://docs.docker.com/engine/reference/commandline/service_create/">https://docs.docker.com/engine/reference/commandline/service_create/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Create a simple service running the&nbsp;<code>nginx</code>&nbsp;image.</p>
<pre><code> docker service create nginx
</code></pre>
</li>
<li>
<p>Create an&nbsp;<code>nginx</code>&nbsp;service with a specified name, multiple replicas, and a published port.</p>
<pre><code> docker service create --name nginx --replicas 3 -p 8080:80 nginx
</code></pre>
</li>
<li>
<p>Use a template to pass the node hostname to each container as an environment variable.</p>
<pre><code> docker service create --name node-hostname --replicas 3 --env NODE_HOSTNAME="{{.Node.Hostname}}" nginx
</code></pre>
</li>
<li>
<p>Get the container running on the current machine, and print its environment variables to verify that the&nbsp;<code>NODE_HOSTNAME</code>variable is set properly.</p>
<pre><code class="lang-bash"> docker ps
 docker exec &lt;CONTAINER_ID&gt; printenv
</code></pre>
</li>
<li>
<p>List the services in the cluster.</p>
<pre><code> docker service ls
</code></pre>
</li>
<li>
<p>List the tasks for a service.</p>
<pre><code> docker service ps nginx
</code></pre>
</li>
<li>
<p>Inspect a service.</p>
<pre><code> docker service inspect nginx
 docker service inspect --pretty nginx
</code></pre>
</li>
<li>
<p>Change a service.</p>
<pre><code> docker service update --replicas 2 nginx
</code></pre>
</li>
<li>
<p>Delete a service.</p>
<pre><code> docker service rm nginx
</code></pre>
</li>
<li>
<p>Create a global service.</p>
<pre><code>docker service create --name nginx --mode global nginx
</code></pre>
</li>
<li>
<p>Two different ways to scale a service:</p>
<pre><code>docker service update --replicas 3 nginx
docker service scale nginx=4</code></pre>
</li>
</ol>

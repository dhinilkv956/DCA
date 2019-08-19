<h2>Exposing Containers Externally</h2>
<p>Port publishing gives you the ability to expose your containers so that outside entities can communicate with them. In this lesson, we will discuss port publishing in the context of both individual containers and services. We will demonstrate some commands that you can use to examine published ports on existing containers, and we will also discuss the ingress and host publishing modes that you can use when publishing ports for services in Docker Swarm.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/reference/commandline/run/">https://docs.docker.com/engine/reference/commandline/run/</a></li>
<li><a href="https://docs.docker.com/engine/reference/commandline/service_create/">https://docs.docker.com/engine/reference/commandline/service_create/</a></li>
<li><a href="https://docs.docker.com/engine/reference/commandline/port/">https://docs.docker.com/engine/reference/commandline/port/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Run a container with a published port, then test and examine the published ports for the container.</p>
<pre><code> docker run -d -p 8080:80 --name nginx_pub nginx
 curl localhost:8080
 docker port nginx_pub
 docker ps
</code></pre>
</li>
<li>
<p>Create a service with a published port using the ingress publishing mode. Test the service and check which Swarm node the service's task is running on.</p>
<pre><code> docker service create -p 8081:80 --name nginx_ingress_pub nginx
 curl localhost:8081
 docker service ps nginx_ingress_pub
</code></pre>
</li>
<li>
<p>Create a service published using host mode. Check which node the task is running on and attempt to access it from the node where the task is running, as well as a node where it is not running.</p>
<pre><code> docker service create -p mode=host,published=8082,target=80 --name nginx_host_pub nginx
 docker service ps nginx_host_pub
</code></pre>
</li>
<li>
<p>Check which node the task is running on, and access the service from that node.</p>
<pre><code> curl localhost:8082
</code></pre>
</li>
<li>
<p>Try accessing the service from another node. It should fail.</p>
<pre><code> curl localhost:8082</code></pre>
</li>
</ol>

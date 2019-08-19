<h2>Using docker inspect</h2>
<p><code>docker inspect</code>&nbsp;is a great tool for managing and troubleshooting your Docker objects.&nbsp;<code>docker inspect</code>&nbsp;is the simplest way to find additional information about existing objects, such as containers, images, and services. In this lesson, we will talk about some of the different forms of&nbsp;<code>docker inspect</code>&nbsp;commands and some of the options associated with those commands.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/swarm/services/">https://docs.docker.com/engine/swarm/services/</a></li>
<li><a href="https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/">https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/</a></li>
<li><a href="https://docs.docker.com/engine/reference/commandline/service_create/">https://docs.docker.com/engine/reference/commandline/service_create/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Run a container and inspect it.</p>
<pre><code class="lang-bash"> docker run -d --name nginx nginx
 docker inspect &lt;CONTAINER_ID&gt;
</code></pre>
</li>
<li>
<p>List the containers and images to get their IDs, then inspect an image.</p>
<pre><code class="lang-bash"> docker container ls
 docker image ls
 docker inspect &lt;IMAGE_ID&gt;
</code></pre>
</li>
<li>
<p>Create and inspect a service.</p>
<pre><code class="lang-bash"> docker service create --name nginx-svc nginx
 docker service ls
 docker inspect &lt;SERVICE_ID&gt;
 docker inspect nginx-svc
</code></pre>
</li>
<li>
<p>Use the type-specific commands to inspect objects.</p>
<pre><code> docker container inspect nginx
 docker service inspect nginx-svc
</code></pre>
</li>
<li>
<p>Use the&nbsp;<code>--format</code>&nbsp;flag to retrieve a subset of the data in a specific format.</p>
<pre><code> docker service inspect --format='{{.ID}}' nginx-svc</code></pre>
</li>
</ol>

<h2>Building Efficient Images</h2>
<div class="close-video-menu">
<p>Executing containers is the core feature of Docker. In this lesson we will dive into the process of executing containers using&nbsp;<code>docker run</code>. We will demonstrate how to use this command, and learn some of the important options and flags that can be used with it. We will also discuss some additional commands that can allow us to manage containers on a host. After completing this lesson, we'll know how to run and manage containers with Docker.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/reference/run/">https://docs.docker.com/engine/reference/run/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<p>Run a simple container using the&nbsp;<code>hello-world</code>&nbsp;image:</p>
<pre><code>docker run hello-world
</code></pre>
<p>Run a container using a specific image tag:</p>
<pre><code>docker run nginx:1.15.11
</code></pre>
<p>Run a container with a command and arguments:</p>
<pre><code>docker run busybox echo hello world!
</code></pre>
<p>Run an Nginx container customized with a variety of flags:</p>
<pre><code>docker run -d --name nginx --restart unless-stopped -p 8080:80 --memory 500M --memory-reservation 256M nginx
</code></pre>
<p>List any currently running containers:</p>
<pre><code>docker ps
</code></pre>
<p>List all containers, both running and stopped:</p>
<pre><code>docker ps -a
</code></pre>
<p>Stop the Nginx container:</p>
<pre><code>docker container stop nginx
</code></pre>
<p>Start a stopped container:</p>
<pre><code>docker container start nginx
</code></pre>
<p>Delete a container (but it must be stopped first):</p>
<pre><code>docker container rm nginx</code></pre>
</div>

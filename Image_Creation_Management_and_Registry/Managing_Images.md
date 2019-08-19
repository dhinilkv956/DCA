<h2>Managing Images</h2>
<p>We have already learned how to create Docker images. In this lesson, however, we will learn how to manage the images located on a machine. We will demonstrate a few commands that are useful for downloading, inspecting, and removing images from the system.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/reference/commandline/image/">https://docs.docker.com/engine/reference/commandline/image/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<p>Download an image:</p>
<pre><code>docker image pull nginx:1.14.0
</code></pre>
<p>List images on the system:</p>
<pre><code>docker image ls
docker image ls -a
</code></pre>
<p>Inspect image metadata:</p>
<pre><code>docker image inspect nginx:1.14.0
docker image inspect nginx:1.14.0 --format "{{.Architecture}}"
docker image inspect nginx:1.14.0 --format "{{.Architecture}} {{.Os}}"
</code></pre>
<p>Delete an image:</p>
<pre><code>docker image rm nginx:1.14.0
</code></pre>
<p>Force deletion of an image that is in use by a container:</p>
<pre><code>docker run -d --name nginx nginx:1.14.0
docker image rm -f nginx:1.14.0
</code></pre>
<p>Locate a dangling image and clean it up:</p>
<pre><code>docker image ls -a
docker container ls
docker container rm -f nginx
docker image ls -a
docker image prune</code></pre>

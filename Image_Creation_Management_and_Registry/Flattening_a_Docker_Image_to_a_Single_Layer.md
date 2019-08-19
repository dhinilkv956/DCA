<h2>&nbsp;Flattening a Docker Image to a Single Layer</h2>
<p>In some rare cases, we may want to flatten the file system of a multi-layer image into a single layer. While Docker does not have a simple command to do this, we can accomplish it by exporting a container's filesystem and importing it as an image. In this lesson, we will see how to flatten an image filesystem into a single layer.</p>
<h3 id="lesson-reference">Lesson Reference</h3>
<p>Set up a new project directory to create a basic image:</p>
<pre><code>cd ~/
mkdir alpine-hello
cd alpine-hello
vi Dockerfile
</code></pre>
<p>Create a Dockerfile that will result in a multi-layered image:</p>
<pre><code>FROM alpine:3.9.3
RUN echo "Hello, World!" &gt; message.txt
CMD cat message.txt
</code></pre>
<p>Build the image and check how many layers it has:</p>
<pre><code>docker build -t nonflat .
docker image history nonflat
</code></pre>
<p>Run a container from the image and export its file system to an archive:</p>
<pre><code>docker run -d --name flat_container nonflat
docker export flat_container &gt; flat.tar
</code></pre>
<p>Import the archive to a new image and check how many layers the new image has:</p>
<pre><code>cat flat.tar | docker import - flat:latest
docker image history flat</code></pre>

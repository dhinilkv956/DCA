<h2>Introduction to Docker Images</h2>

<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/v17.09/engine/userguide/storagedriver/imagesandcontainers/">https://docs.docker.com/v17.09/engine/userguide/storagedriver/imagesandcontainers/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<p>Run a container. The image will be automatically downloaded if it does not exist on the system:</p>
<pre><code>docker run nginx:1.15.8
</code></pre>
<p>Download an image:</p>
<pre><code>docker image pull nginx
</code></pre>
<p>View file system layers in an image:</p>
<pre><code>docker image history nginx</code></pre>

<h2 id="images-and-layers">Images and layers</h2>
<p>A Docker image is built up from a series of layers. Each layer represents an instruction in the image&rsquo;s Dockerfile. Each layer except the very last one is read-only. Consider the following Dockerfile:</p>
<div class="language-conf highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code><span class="n">FROM</span> <span class="n">ubuntu</span>:<span class="m">15</span>.<span class="m">04</span>
<span class="n">COPY</span> . /<span class="n">app</span>
<span class="n">RUN</span> <span class="n">make</span> /<span class="n">app</span>
<span class="n">CMD</span> <span class="n">python</span> /<span class="n">app</span>/<span class="n">app</span>.<span class="n">py</span>
</code></pre>
</div>
</div>
<p>This Dockerfile contains four commands, each of which creates a layer. The&nbsp;<code class="highlighter-rouge">FROM</code>&nbsp;statement starts out by creating a layer from the&nbsp;<code class="highlighter-rouge">ubuntu:15.04</code>&nbsp;image. The&nbsp;<code class="highlighter-rouge">COPY</code>&nbsp;command adds some files from your Docker client&rsquo;s current directory. The&nbsp;<code class="highlighter-rouge">RUN</code>&nbsp;command builds your application using the&nbsp;<code class="highlighter-rouge">make</code>&nbsp;command. Finally, the last layer specifies what command to run within the container.</p>
<p>Each layer is only a set of differences from the layer before it. The layers are stacked on top of each other. When you create a new container, you add a new writable layer on top of the underlying layers. This layer is often called the &ldquo;container layer&rdquo;. All changes made to the running container, such as writing new files, modifying existing files, and deleting files, are written to this thin writable container layer. The diagram below shows a container based on the Ubuntu 15.04 image.</p>
<p><img src="https://docs.docker.com/v17.09/engine/userguide/storagedriver/images/container-layers.jpg" alt="Layers of a container based on the Ubuntu image" /></p>
<p>A&nbsp;<em>storage driver</em>&nbsp;handles the details about the way these layers interact with each other. Different storage drivers are available, which have advantages and disadvantages in different situations.</p>

<h2 id="container-and-layers">Container and layers</h2>
<p>The major difference between a container and an image is the top writable layer. All writes to the container that add new or modify existing data are stored in this writable layer. When the container is deleted, the writable layer is also deleted. The underlying image remains unchanged.</p>
<p>Because each container has its own writable container layer, and all changes are stored in this container layer, multiple containers can share access to the same underlying image and yet have their own data state. The diagram below shows multiple containers sharing the same Ubuntu 15.04 image.</p>
<p><img src="https://docs.docker.com/v17.09/engine/userguide/storagedriver/images/sharing-layers.jpg" alt="Containers sharing same image" /></p>
<blockquote>
<p><strong>Note</strong>: If you need multiple images to have shared access to the exact same data, store this data in a Docker volume and mount it into your containers.</p>
</blockquote>
<p>Docker uses storage drivers to manage the contents of the image layers and the writable container layer. Each storage driver handles the implementation differently, but all drivers use stackable image layers and the copy-on-write (CoW) strategy.</p>
<h2 id="container-size-on-disk">Container size on disk</h2>
<p>To view the approximate size of a running container, you can use the&nbsp;<code class="highlighter-rouge">docker ps -s</code>&nbsp;command. Two different columns relate to size.</p>
<ul>
<li>
<p><code class="highlighter-rouge">size</code>: the amount of data (on disk) that is used for the writable layer of each container</p>
</li>
<li>
<p><code class="highlighter-rouge">virtual size</code>: the amount of data used for the read-only image data used by the container plus the container&rsquo;s writable layer&nbsp;<code class="highlighter-rouge">size</code>. Multiple containers may share some or all read-only image data. Two containers started from the same image share 100% of the read-only data, while two containers with different images which have layers in common share those common layers. Therefore, you can&rsquo;t just total the virtual sizes. This will over-estimate the total disk usage by a potentially non-trivial amount.</p>
</li>
</ul>
<p>The total disk space used by all of the running containers on disk is some combination of each container&rsquo;s&nbsp;<code class="highlighter-rouge">size</code>&nbsp;and the&nbsp;<code class="highlighter-rouge">virtual size</code>&nbsp;values. If multiple containers started from the same exact image, the total size on disk for these containers would be SUM (<code class="highlighter-rouge">size</code>&nbsp;of containers) plus one container&rsquo;s (<code class="highlighter-rouge">virtual size</code>-&nbsp;<code class="highlighter-rouge">size</code>).</p>
<p>This also does not count the following additional ways a container can take up disk space:</p>
<ul>
<li>Disk space used for log files if you use the&nbsp;<code class="highlighter-rouge">json-file</code>&nbsp;logging driver. This can be non-trivial if your container generates a large amount of logging data and log rotation is not configured.</li>
<li>Volumes and bind mounts used by the container.</li>
<li>Disk space used for the container&rsquo;s configuration files, which are typically small.</li>
<li>Memory written to disk (if swapping is enabled).</li>
<li>Checkpoints, if you&rsquo;re using the experimental checkpoint/restore feature.</li>
</ul>

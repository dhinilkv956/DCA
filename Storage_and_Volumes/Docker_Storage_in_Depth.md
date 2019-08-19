<h2>Docker Storage in Depth</h2>
<div class="close-video-menu">&nbsp;</div>
<p>Storage is essential to almost any system, and containers are no exception. In this lesson, we will go into a little more detail about some of the storage driver concepts that we discussed earlier. We will go over the three most common storage drivers and discuss which operating systems they belong to. We will also discuss storage methods and how to locate the underlying data for containers and images on the host file system.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/storage/storagedriver/select-storage-driver/">https://docs.docker.com/storage/storagedriver/select-storage-driver/</a></li>
<li><a href="https://rancher.com/block-object-file-storage-containers/">https://rancher.com/block-object-file-storage-containers/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Run a basic container:</p>
<pre><code> docker run --name storage_nginx nginx
</code></pre>
</li>
<li>
<p>Use&nbsp;<code>docker inspect</code>&nbsp;to find the location of the container's data on the host:</p>
<pre><code class="lang-bash"> docker container inspect storage_nginx
 ls /var/lib/docker/overlay2/&lt;STORAGE_HASH&gt;/
</code></pre>
</li>
<li>
<p>Use&nbsp;<code>docker inspect</code>&nbsp;to find the location of an image's data:</p>
<pre><code> docker image inspect nginx</code></pre>
</li>
</ol>

<h2>Storage in a Cluster</h2>
<p>Docker volumes provide persistent storage to containers, and they can be shared between containers to allow them to interact with the same data. However, sharing volumes creates additional challenges in the context of a Swarm cluster, where containers may be running on different nodes. In this lesson, we will discuss how you can create shared volumes that work across multiple swarm nodes using the&nbsp;<code>vieux/sshfs</code>&nbsp;volume driver.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/storage/volumes/#share-data-among-machines">https://docs.docker.com/storage/volumes/#share-data-among-machines</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Install the&nbsp;<code>vieux/sshfs</code>&nbsp;plugin on all nodes in the swarm.</p>
<pre><code> docker plugin install --grant-all-permissions vieux/sshfs
</code></pre>
</li>
<li>
<p>Set up an additional server to use for storage. You can use the&nbsp;<code>Ubuntu 18.04 Bionic Beaver LTS</code>&nbsp;image with a size of&nbsp;<code>Small</code>. On this new storage server, create a directory with a file that can be used for testing.</p>
<pre><code> mkdir /home/cloud_user/external
 echo External storage! &gt; /home/cloud_user/external/message.txt
</code></pre>
</li>
<li>
<p>On the swarm manager, manually create a Docker volume that uses the external storage server for storage. Be sure to replace the text&nbsp;<code>&lt;STORAGE_SERVER_PRIVATE_IP&gt;</code>&nbsp;and&nbsp;<code>&lt;PASSWORD&gt;</code>&nbsp;with actual values.</p>
<pre><code class="lang-bash"> docker volume create --driver vieux/sshfs \
   -o sshcmd=cloud_user@&lt;STORAGE_SERVER_PRIVATE_IP&gt;:/home/cloud_user/external \
   -o password=&lt;PASSWORD&gt; \
   sshvolume

 docker volume ls
</code></pre>
</li>
<li>
<p>Create a service that automatically manages the shared volume, creating the volume on swarm nodes as needed. Be sure to replace the text&nbsp;<code>&lt;STORAGE_SERVER_PRIVATE_IP&gt;</code>&nbsp;and&nbsp;<code>&lt;PASSWORD&gt;</code>&nbsp;with actual values.</p>
<pre><code class="lang-bash"> docker service create \
   --replicas=3 \
   --name storage-service \
   --mount volume-driver=vieux/sshfs,source=cluster-volume,destination=/app,volume-opt=sshcmd=cloud_user@&lt;STORAGE_SERVER_PRIVATE_IP&gt;:/home/cloud_user/external,volume-opt=password=&lt;PASSWORD&gt; busybox cat /app/message.txt
</code></pre>
</li>
<li>
<p>Check the service logs to verify that the service is reading the test data from the external storage server.</p>
<pre><code class="lang-bash"> docker service logs storage-service
</code></pre>
</li>
</ol>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16430" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>

<h2>Docker Volumes</h2>

<p>Docker containers are designed so that their internal storage can be easily destroyed. However, sometimes you might need more permanent data. Docker volumes and bind mounts allow you to attach external storage to containers. In this lesson, we will discuss bind mounts and volumes. We will also demonstrate how to create them using both the&nbsp;<code>--mount</code>&nbsp;and&nbsp;<code>-v</code>&nbsp;flags. We will talk about sharing volumes between multiple containers and go over some commands you can use to manage volumes.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/storage/">https://docs.docker.com/storage/</a></li>
<li><a href="https://docs.docker.com/storage/bind-mounts/">https://docs.docker.com/storage/bind-mounts/</a></li>
<li><a href="https://docs.docker.com/storage/volumes/">https://docs.docker.com/storage/volumes/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Create a directory on the host with some test data.</p>
<pre><code> cd ~/
 mkdir message
 echo Hello, world! &gt; message/message.txt
</code></pre>
</li>
<li>
<p>Mount the directory to a container with a bind mount.</p>
<pre><code> docker run --mount type=bind,source=/home/cloud_user/message,destination=/root,readonly busybox cat /root/message.txt
</code></pre>
</li>
<li>
<p>Run a container with a mounted volume.</p>
<pre><code> docker run --mount type=volume,source=my-volume,destination=/root busybox sh -c 'echo hello &gt; /root/message.txt &amp;&amp; cat /root/message.txt'
</code></pre>
</li>
<li>
<p>Use the&nbsp;<code>-v</code>&nbsp;syntax to create a bind mount and a volume.</p>
<pre><code> docker run -v /home/cloud_user/message:/root:ro busybox cat /root/message.txt
 docker run -v my-volume:/root busybox sh -c 'cat /root/message.txt'
</code></pre>
</li>
<li>
<p>Use a volume to share data between containers.</p>
<pre><code> docker run --mount type=volume,source=shared-volume,destination=/root busybox sh -c 'echo I wrote this! &gt; /root/message.txt'
 docker run --mount type=volume,source=shared-volume,destination=/anotherplace busybox cat /anotherplace/message.txt
</code></pre>
</li>
<li>
<p>Create and manage volumes using&nbsp;<code>docker volume</code>&nbsp;commands.</p>
<pre><code> docker volume create test-volume
 docker volume ls
 docker volume inspect test-volume
 docker volume rm test-volume</code></pre>
</li>
</ol>

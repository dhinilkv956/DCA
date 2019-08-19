<p>Docker supports the ability to securely store certain encryption keys. These encryption keys are used to encrypt sensitive cluster data, but are stored unencrypted on the disks of swarm managers by default. Autolock allows for greater security for these keys, but requires each manager to be unlocked whenever Docker restarts. In this lesson, we will discuss autolock. We will demonstrate how to enable and disable autolock, as well as how to use it when it is enabled.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/swarm/swarm_manager_locking/">https://docs.docker.com/engine/swarm/swarm_manager_locking/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Enable autolock.</p>
<pre><code> docker swarm update --autolock=true
</code></pre>
</li>
<li>
<p>Make note of the unlock key!</p>
</li>
<li>
<p>Run a command to interact with the swarm, then restart docker and try the command again to verify that the swarm is locked.</p>
<pre><code> docker node ls
 sudo systemctl restart docker
 docker node ls
</code></pre>
</li>
<li>
<p>Unlock the swarm using the unlock key and verify that it is unlocked.</p>
<pre><code> docker swarm unlock
 docker node ls
</code></pre>
</li>
<li>
<p>Obtain the existing unlock key.</p>
<pre><code> docker swarm unlock-key
</code></pre>
</li>
<li>
<p>Rotate the unlock key.</p>
<pre><code> docker swarm unlock-key --rotate
</code></pre>
</li>
<li>
<p>Disable autolock.</p>
<pre><code> docker swarm update --autolock=false
 sudo systemctl restart docker
 docker node ls</code></pre>
</li>
</ol>

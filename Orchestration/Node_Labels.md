<h2>Node Labels</h2>
<p>Sometimes, you may wish to have more control over which nodes will be used to execute particular tasks in your swarm. In this lesson, we will talk about how you can use node labels to influence and even control which nodes will and will not be used to execute a given service's tasks.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/reference/commandline/node_update/#add-label-metadata-to-a-node">https://docs.docker.com/engine/reference/commandline/node_update/#add-label-metadata-to-a-node</a></li>
<li><a href="https://docs.docker.com/engine/swarm/services/#placement-constraints">https://docs.docker.com/engine/swarm/services/#placement-constraints</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>List your current nodes.</p>
<pre><code> docker node ls
</code></pre>
</li>
<li>
<p>Add a label to a node.</p>
<pre><code class="lang-bash"> docker node update --label-add availability_zone=east &lt;NODE_NAME&gt;
 docker node update --label-add availability_zone=west &lt;NODE_NAME&gt;
</code></pre>
</li>
<li>
<p>View existing labels with:</p>
<pre><code class="lang-bash"> docker node inspect --pretty &lt;NODE_NAME&gt;
</code></pre>
</li>
<li>
<p>You can use&nbsp;<code>--constraint</code>&nbsp;when creating a service to restrict which nodes will be used to execute a service's tasks.</p>
<pre><code> docker service create --name nginx-east --constraint node.labels.availability_zone==east --replicas 3 nginx
 docker service ps nginx-east
 docker service create --name nginx-west --constraint node.labels.availability_zone!=east --replicas 3 nginx
 docker service ps nginx-west
</code></pre>
</li>
<li>
<p>Use&nbsp;<code>--placement-pref</code>&nbsp;to spread tasks evenly based on the value of a specific label.</p>
<pre><code> docker service create --name nginx-spread --placement-pref spread=node.labels.availability_zone --replicas 3 nginx
 docker service ps nginx-spread</code></pre>
</li>
</ol>

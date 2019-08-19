<h2>Introduction to Docker Stacks</h2>
<p>Docker Swarm's orchestration functionality really shines when using stacks. Stacks allow you to easily manage complex, multi-container applications and orchestrate them within your swarm cluster. In this lesson, we will discuss Docker stacks. We will demonstrate how to create and manage Docker stacks, as well as a few of the available options for designing stacks.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/get-started/part5/">https://docs.docker.com/get-started/part5/</a></li>
<li><a href="https://docs.docker.com/engine/reference/commandline/stack/">https://docs.docker.com/engine/reference/commandline/stack/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Create a compose file for the stack.</p>
<pre><code> vi simple-stack.yml
</code></pre>
<pre><code> version: '3'
 services:
   web:
     image: nginx
   busybox:
     image: radial/busyboxplus:curl
     command: /bin/sh -c "while true; do echo Hello!; sleep 10; done"
</code></pre>
</li>
<li>
<p>Deploy the stack and examine it using various commands.</p>
<pre><code> docker stack deploy -c simple-stack.yml simple
 docker stack ls
 docker stack ps simple
 docker stack services simple
 docker service logs simple_busybox
</code></pre>
</li>
<li>
<p>Modify the stack to use an environment variable.</p>
<pre><code> vi simple-stack.yml
</code></pre>
<pre><code> version: '3'
 services:
   web:
     image: nginx
   busybox:
     image: radial/busyboxplus:curl
     command: /bin/sh -c "while true; do echo $MESSAGE; sleep 10; done"
     environment:
     - MESSAGE=Hello!
</code></pre>
<pre><code> docker stack deploy -c simple-stack.yml simple
 docker service logs simple_busybox
</code></pre>
</li>
<li>
<p>Modify the stack to expose a port.</p>
<pre><code> vi simple-stack.yml
</code></pre>
<pre><code> version: '3'
 services:
   web:
     image: nginx
     ports:
     - "8080:80"
   busybox:
     image: radial/busyboxplus:curl
     command: /bin/sh -c "while true; do echo $MESSAGE; sleep 10; done"
     environment:
     - MESSAGE=Hello!
</code></pre>
<pre><code> docker stack deploy -c simple-stack.yml simple
 curl localhost:8080
</code></pre>
</li>
<li>
<p>Modify the stack to use the BusyBox service to communicate with the web service.</p>
<pre><code> vi simple-stack.yml
</code></pre>
<pre><code> version: '3'
 services:
   web:
     image: nginx
     ports:
     - "8080:80"
   busybox:
     image: radial/busyboxplus:curl
     command: /bin/sh -c "while true; do echo $MESSAGE; curl web:80; sleep 10; done"
     environment:
     - MESSAGE=Hello!
</code></pre>
<pre><code> docker stack deploy -c simple-stack.yml simple
</code></pre>
</li>
<li>
<p>Delete the stack.</p>
<pre><code> docker stack rm simple</code></pre>
</li>
</ol>

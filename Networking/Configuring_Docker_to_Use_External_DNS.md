<h2>Configuring Docker to Use External DNS</h2>
<p>Docker containers use a DNS server to locate external servers when using hostnames. In some scenarios, you may wish to customize which external DNS server is used by your containers. In this lesson, we will discuss how to customize your external DNS, both for the Docker daemon as a whole and for individual containers.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/v17.09/engine/userguide/networking/default_network/configure-dns/">https://docs.docker.com/v17.09/engine/userguide/networking/default_network/configure-dns/</a></li>
<li><a href="https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-dns-options">https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-dns-options</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Edit the Docker daemon config file to set a custom DNS for the host.</p>
<pre><code> sudo vi /etc/docker/daemon.json
</code></pre>
<pre><code> {
   "dns": ["8.8.8.8"]
 }
</code></pre>
</li>
<li>
<p>Restart Docker.</p>
<pre><code> sudo systemctl restart docker
</code></pre>
</li>
<li>
<p>Test your DNS by looking up an external domain.</p>
<pre><code> docker run nicolaka/netshoot nslookup google.com
</code></pre>
</li>
<li>
<p>Run a container with a custom DNS and test it by doing an&nbsp;<code>nslookup</code>.</p>
<pre><code> docker run --dns 8.8.4.4 nicolaka/netshoot nslookup google.com</code></pre>
</li>
</ol>

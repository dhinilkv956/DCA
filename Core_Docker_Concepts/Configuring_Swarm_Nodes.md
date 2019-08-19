<h2>Configuring Swarm Nodes</h2>
<p>Docker swarm worker nodes handle the processing of workloads in the swarm cluster. We have already set up a swarm manager, so in this lesson we will discuss the process of adding worker nodes to the swarm. We will demonstrate this by adding our two worker nodes to the cluster that was initialized in the previous lesson.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/swarm/swarm-tutorial/add-nodes/">https://docs.docker.com/engine/swarm/swarm-tutorial/add-nodes/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<p>Install Docker Engine on both worker nodes:</p>
<pre><code>sudo apt-get update

sudo apt-get -y install \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg-agent \
  software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get update

sudo apt-get install -y docker-ce=5:18.09.5~3-0~ubuntu-bionic docker-ce-cli=5:18.09.5~3-0~ubuntu-bionic containerd.io

sudo usermod -a -G docker cloud_user
</code></pre>
<p>Get a join token from the manager. Run this command on the swarm manager:</p>
<pre><code>docker swarm join-token worker
</code></pre>
<p>Now copy the&nbsp;<code>docker swarm join</code>&nbsp;command provided in the output and run it on both workers:</p>
<pre><code>docker swarm join --token &lt;token&gt; &lt;swarm manager private IP&gt;:2377
</code></pre>
<p>On the swarm manager, verify that the two worker nodes have successfully joined:</p>
<pre><code>docker node ls</code></pre>

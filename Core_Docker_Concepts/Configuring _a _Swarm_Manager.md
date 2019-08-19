<p>The swarm manager is responsible for controlling and orchestrating the Docker swarm. It delegates workloads to the worker nodes in the cluster. In this lesson, we will discuss and demonstrate the process of initializing a new swarm and setting up the swarm manager.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/">https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<p>Install Docker Engine on the Swarm Manager:</p>
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
<p>Now initialize the swarm!</p>
<p><strong>Note:</strong>&nbsp;Be sure to use the private IP (NOT the public IP) for the&nbsp;<code>--advertise-addr</code>:</p>
<pre><code>docker swarm init --advertise-addr &lt;swarm manager private IP&gt;
</code></pre>
<p>This shows some basic information about the current status of the swarm:</p>
<pre><code>docker info
</code></pre>
<p>List the current nodes in the swarm and their status:</p>
<pre><code>docker node ls</code></pre>

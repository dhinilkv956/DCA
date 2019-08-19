<p>Install required packages:</p>
<pre><code>sudo apt-get update

sudo apt-get -y install \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg-agent \
  software-properties-common
</code></pre>
<p>Add the Docker GPG key and repo:</p>
<pre><code>curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
</code></pre>
<p>Install Docker CE packages:</p>
<pre><code>sudo apt-get update

sudo apt-get install -y docker-ce=5:18.09.5~3-0~ubuntu-bionic docker-ce-cli=5:18.09.5~3-0~ubuntu-bionic containerd.io
</code></pre>
<p>Give&nbsp;<code>cloud_user</code>&nbsp;permission to run docker commands:</p>
<pre><code>sudo usermod -a -G docker cloud_user
</code></pre>
<p>Log out and back in.</p>
<p>Test the installation by running a simple container:</p>
<pre><code>docker run hello-world</code></pre>

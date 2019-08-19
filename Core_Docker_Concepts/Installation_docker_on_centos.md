<p>Install required packages:</p>
<pre><code>sudo yum install -y device-mapper-persistent-data lvm2
</code></pre>
<p>Add the Docker CE repo:</p>
<pre><code>sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
</code></pre>
<p>Install the Docker CE packages and&nbsp;<code>containerd.io</code>:</p>
<pre><code>sudo yum install -y docker-ce-18.09.5 docker-ce-cli-18.09.5 containerd.io
</code></pre>
<p>Start and enable the Docker service:</p>
<pre><code>sudo systemctl start docker
sudo systemctl enable docker
</code></pre>
<p>Add&nbsp;<code>cloud_user</code>&nbsp;to the&nbsp;<code>docker</code>&nbsp;group, giving the user permission to run&nbsp;<code>docker</code>&nbsp;commands:</p>
<pre><code>sudo usermod -a -G docker cloud_user
</code></pre>
<p>Log out and back in.</p>
<p>Test the installation by running a simple container:</p>
<pre><code>docker run hello-world</code></pre>

<p>This lesson was performed on a CentOS 7 server running Docker CE</p>
<p>Get the current storage driver:</p>
<pre><strong><code>docker info
</code></strong></pre>
<p>Set the storage driver explicitly by providing a flag to the Docker daemon:</p>
<pre><strong><code>sudo vi /usr/lib/systemd/system/docker.service
</code></strong></pre>
<p>Edit the&nbsp;<strong><code>ExecStart</code></strong>&nbsp;line, adding the&nbsp;<code><strong>--storage-driver</strong> <strong>devicemapper</strong></code>&nbsp;flag:</p>
<pre><code>ExecStart=/usr/bin/dockerd --storage-driver devicemapper ...
</code></pre>
<p>sudo systemctl restart docker<br />sudo systemctl status dockerAfter any edits to the unit file, reload Systemd and restart Docker:</p>
<pre><strong><code>sudo systemctl daemon-reload
sudo systemctl restart docker
</code></strong></pre>
<p>We can also set the storage driver explicitly using the daemon configuration file. This is the method that Docker recommends. Note that we cannot do this and pass the<strong>&nbsp;<code>--storage-driver</code>&nbsp;</strong>flag to the daemon at the same time:</p>
<pre><strong><code>sudo vi /etc/docker/daemon.json
</code></strong></pre>
<p>Set the storage driver in the daemon configuration file:</p>
<pre><strong><code>{
  "storage-driver": "devicemapper"
}&nbsp;</code></strong></pre>
<p>Restart Docker after editing the file. It is also a good idea to make sure Docker is running properly after changing the configuration file:</p>
<pre><code><strong>sudo systemctl restart docker
sudo systemctl status docker</strong></code></pre>

<h2>Configuring DeviceMapper</h2>
<p>We have already discussed some of the storage drivers that are available with Docker, but in this lesson we will focus specifically on the DeviceMapper storage driver. We will configure DeviceMapper to use direct-lvm mode to manage storage on a block storage device, which is recommended when using DeviceMapper in production.</p>
<h3>Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/storage/storagedriver/device-mapper-driver/">https://docs.docker.com/storage/storagedriver/device-mapper-driver/</a></li>
</ul>
<h3>Lesson Reference</h3>
<ol>
<li>
<p>For this lesson, use a&nbsp;<code>CentOS 7</code>&nbsp;server with a size of&nbsp;<code>Small</code>. Before starting the lesson, you'll first need to install Docker.</p>
</li>
<li>
<p>Add a new storage device to your server. In Playground, select&nbsp;<code>Actions</code>, then select&nbsp;<code>Add /dev/xvdb</code>&nbsp;and wait for it to finish adding the device.</p>
</li>
<li>
<p>Stop and disable Docker.</p>
<pre><code> sudo systemctl disable docker
 sudo systemctl stop docker</code></pre>
</li>
<li>
<p>Delete any existing Docker data.</p>
<pre><code> sudo rm -rf /var/lib/docker</code></pre>
</li>
<li>
<p>Configure DeviceMapper in&nbsp;<code>daemon.json</code>.</p>
<pre><code> sudo vi /etc/docker/daemon.json</code></pre>
<pre><code> {
   "storage-driver": "devicemapper",
   "storage-opts": [
     "dm.directlvm_device=/dev/nvme1n1",
     "dm.thinp_percent=95",
     "dm.thinp_metapercent=1",
     "dm.thinp_autoextend_threshold=80",
     "dm.thinp_autoextend_percent=20",
     "dm.directlvm_device_force=true"
   ]
 }</code></pre>
</li>
<li>
<p>Start and enable Docker.</p>
<pre><code> sudo systemctl enable docker
 sudo systemctl start docker</code></pre>
</li>
<li>
<p>Check the storage driver information provided by&nbsp;<code>docker info</code>.</p>
<pre><code> docker info</code></pre>
</li>
<li>
<p>Run a container to verify that everything is working.</p>
<pre><code> docker run hello-world</code></pre>
</li>
</ol>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16425" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>

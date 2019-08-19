<p><strong>Storage drivers:</strong> Provide pluggable framework for managing the temporary, internal storage of a containers writable layer.<br />Docker support variety of storage drivers. The best storage driver to use depened on your enviornment and your storage needs.</p>
<p>Docker supports the following storage drivers:</p>
<p><strong>overlay2:</strong> is the preferred storage driver, for all currently supported Linux distributions, and requires no extra configuration.</p>
<p><strong>aufs:</strong> is the preferred storage driver for Docker 18.06 and older, when running on Ubuntu 14.04 on kernel 3.13 which has no support for overlay2.</p>
<p><strong>devicemapper:</strong> is supported, but requires direct-lvm for production environments, because loopback-lvm, while zero-configuration, has very poor performance. devicemapper was the recommended storage driver for CentOS and RHEL, as their kernel version did not support overlay2. However, current versions of CentOS and RHEL now have support for overlay2, which is now the recommended driver.</p>
<p>The <strong>btrfs</strong> and <strong>zfs</strong> storage drivers are used if they are the backing filesystem (the filesystem of the host on which Docker is installed). These filesystems allow for advanced options, such as creating &ldquo;snapshots&rdquo;, but require more maintenance and setup. Each of these relies on the backing filesystem being configured correctly.</p>
<p>The <strong>vfs</strong> storage driver is intended for testing purposes, and for situations where no copy-on-write filesystem can be used. Performance of this storage driver is poor, and is not generally recommended for production use.</p>

<b>Supported backing filesystems</b>   
With regard to Docker, the backing filesystem is the filesystem where /var/lib/docker/ is located. Some storage drivers only work with specific backing filesystems.
<table>
<thead>
<tr>
<th>Storage driver</th>
<th>Supported backing filesystems</th>
</tr>
</thead>
<tbody>
<tr>
<td><code class="highlighter-rouge">overlay2</code>,&nbsp;<code class="highlighter-rouge">overlay</code></td>
<td><code class="highlighter-rouge">xfs</code>&nbsp;with ftype=1,&nbsp;<code class="highlighter-rouge">ext4</code></td>
</tr>
<tr>
<td><code class="highlighter-rouge">aufs</code></td>
<td><code class="highlighter-rouge">xfs</code>,&nbsp;<code class="highlighter-rouge">ext4</code></td>
</tr>
<tr>
<td><code class="highlighter-rouge">devicemapper</code></td>
<td><code class="highlighter-rouge">direct-lvm</code></td>
</tr>
<tr>
<td><code class="highlighter-rouge">btrfs</code></td>
<td><code class="highlighter-rouge">btrfs</code></td>
</tr>
<tr>
<td><code class="highlighter-rouge">zfs</code></td>
<td><code class="highlighter-rouge">zfs</code></td>
</tr>
<tr>
<td><code class="highlighter-rouge">vfs</code></td>
<td>any filesystem</td>
</tr>
</tbody>
</table>

<b>LAB:</b>  

<p>This lesson was performed on a CentOS 7 server running Docker CE</p>
<p>Get the current storage driver:</p>
<pre><code>docker info
</code></pre>
<p>Set the storage driver explicitly by providing a flag to the Docker daemon:</p>
<pre><code>sudo vi /usr/lib/systemd/system/docker.service
</code></pre>
<p>Edit the&nbsp;<code>ExecStart</code>&nbsp;line, adding the&nbsp;<code>--storage-driver devicemapper</code>&nbsp;flag:</p>
<pre><code>ExecStart=/usr/bin/dockerd --storage-driver devicemapper ...
</code></pre>
<p>After any edits to the unit file, reload Systemd and restart Docker:</p>
<pre><code>sudo systemctl daemon-reload
sudo systemctl restart docker
</code></pre>
<p>We can also set the storage driver explicitly using the daemon configuration file. This is the method that Docker recommends. Note that we cannot do this and pass the&nbsp;<code>--storage-driver</code>&nbsp;flag to the daemon at the same time:</p>
<pre><code>sudo vi /etc/docker/daemon.json
</code></pre>
<p>Set the storage driver in the daemon configuration file:</p>
<pre><code>{
  "storage-driver": "devicemapper"
}
</code></pre>
<p>Restart Docker after editing the file. It is also a good idea to make sure Docker is running properly after changing the configuration file:</p>
<pre><code>sudo systemctl restart docker
sudo systemctl status docker
</code></pre>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16395" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>

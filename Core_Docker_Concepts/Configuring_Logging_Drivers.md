<h1 id="title">Configure logging drivers</h1>
<p><span class="reading-time" title="Estimated reading time"><span class="reading-time-label">Estimated reading time:&nbsp;</span>7 minutes</span></p>
<p>Docker includes multiple logging mechanisms to help you&nbsp;<a href="https://docs.docker.com/engine/admin/logging/view_container_logs/">get information from running containers and services</a>. These mechanisms are called logging drivers.</p>
<p>Each Docker daemon has a default logging driver, which each container uses unless you configure it to use a different logging driver.</p>
<p>In addition to using the logging drivers included with Docker, you can also implement and use&nbsp;<a href="https://docs.docker.com/engine/admin/logging/plugins/">logging driver plugins</a></p>


<b> LAB: </b>

<p>heck the current default logging driver:</p>
<pre><code>docker info | grep Logging
</code></pre>
<p>Edit&nbsp;<code>daemon.json</code>&nbsp;to set a new default logging driver configuration:</p>
<pre><code>sudo vi /etc/docker/daemon.json
</code></pre>
<p>Add the configuration to&nbsp;<code>daemon.json</code>:</p>
<pre><code>{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "15m"
  }
}
</code></pre>
<p>Restart docker after editing&nbsp;<code>daemon.json</code>:</p>
<pre><code>sudo systemctl restart docker
</code></pre>
<p>Run a docker container, overriding the system default logging driver settings:</p>
<pre><code>docker run --log-driver json-file --log-opt max-size=50m nginx
</code></pre>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16397" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>

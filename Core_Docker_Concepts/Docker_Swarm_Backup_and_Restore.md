<h2>Docker Swarm Backup and Restore</h2>

<p>f you are managing a swarm cluster, it is important to be able to backup current swarm data and restore a previous backup. In this lesson, we will demonstrate the process of performing a simple backup and restore in a swarm cluster.</p>
<h3>Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/swarm/admin_guide/#back-up-the-swarm">https://docs.docker.com/engine/swarm/admin_guide/#back-up-the-swarm</a></li>
</ul>
<h3>Lesson Reference</h3>
<h4>Create the Backup</h4>
<p>On the manager:</p>
<pre><code>sudo systemctl stop docker
sudo tar -zvcf backup.tar.gz -C /var/lib/docker swarm
sudo systemctl start docker</code></pre>
<h4>Restore from Backup</h4>
<p>On the manager:</p>
<pre><code>sudo systemctl stop docker
sudo rm -rf /var/lib/docker/swarm/*
sudo tar -zxvf backup.tar.gz -C /var/lib/docker/swarm/
sudo systemctl start docker
docker node ls</code></pre>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16401" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>

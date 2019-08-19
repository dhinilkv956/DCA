<p>Downgrade to a previous version:</p>
<pre><code>sudo systemctl stop docker
sudo apt-get remove -y docker-ce docker-ce-cli
sudo apt-get update
sudo apt-get install -y docker-ce=5:18.09.4~3-0~ubuntu-bionic docker-ce-cli=5:18.09.4~3-0~ubuntu-bionic
docker version
</code></pre>
<p>Upgrade to a new version:</p>
<pre><code>sudo apt-get install -y docker-ce=5:18.09.5~3-0~ubuntu-bionic docker-ce-cli=5:18.09.5~3-0~ubuntu-bionic
docker version
</code></pre>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16396" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>

<h2>Docker Compose</h2>
<p>Docker is a powerful tool for running containers, but many applications consist of a collection of multiple containers running different software and interacting with one another. These complex applications can become difficult to maintain when all of their components are managed separately. Docker Compose offers a solution to this problem by allowing you to declaratively describe a set of multiple resources and manage them as a unit. In this lesson, we will discuss Docker Compose and demonstrate creating and managing a simple, multi-container application.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/compose/">https://docs.docker.com/compose/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Install Docker Compose.</p>
<pre><code class="lang-bash"> sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 sudo chmod +x /usr/local/bin/docker-compose
 docker-compose version
</code></pre>
</li>
<li>
<p>Set up a Docker Compose project.</p>
<pre><code> mkdir nginx-compose
 cd nginx-compose
 vi docker-compose.yml
</code></pre>
</li>
<li>
<p>Create your&nbsp;<code>docker-compose.yml</code>.</p>
<pre><code> version: '3'
 services:
   web:
     image: nginx
     ports:
     - "8080:80"
   redis:
     image: redis:alpine
</code></pre>
</li>
<li>
<p>Start your Compose app.</p>
<pre><code> docker-compose up -d
</code></pre>
</li>
<li>
<p>List the Docker Compose containers, then stop the app.</p>
<pre><code> docker-compose ps
 docker-compose down
</code></pre>
</li>
</ol>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16423" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>

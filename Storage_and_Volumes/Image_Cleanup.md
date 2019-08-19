<h2>Image Cleanup</h2>
<p>Storage management is an important component of any system. In this lesson, we will talk about some of the tools you can use to manage Docker's disk usage, particularly when it comes to storing Docker images. We will discuss how to examine disk usage on a system, as well as how to easily clean up images that are no longer being used.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/reference/commandline/system_df/">https://docs.docker.com/engine/reference/commandline/system_df/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<ol>
<li>
<p>Display the storage space being used by Docker.</p>
<pre><code> docker system df
</code></pre>
</li>
<li>
<p>Display disk usage by individual objects.</p>
<pre><code> docker system df -v
</code></pre>
</li>
<li>
<p>Delete dangling images (images with no tags or containers).</p>
<pre><code> docker image prune
</code></pre>
</li>
<li>
<p>Pull an image not being used by any containers, and use&nbsp;<code>docker image prune -a</code>&nbsp;to clean up all images with no containers.</p>
<pre><code> docker image pull nginx 1.14.0
 docker image prune -a</code></pre>
</li>
</ol>

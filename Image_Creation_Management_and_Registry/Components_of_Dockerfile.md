<h2>The Components of a Dockerfile</h2>
<p>Docker can build images automatically by reading the instructions from a&nbsp;<code class="highlighter-rouge">Dockerfile</code>. A&nbsp;<code class="highlighter-rouge">Dockerfile</code>&nbsp;is a text document that contains all the commands a user could call on the command line to assemble an image. Using&nbsp;<code class="highlighter-rouge">docker build</code>&nbsp;users can create an automated build that executes several command-line instructions in succession.</p>
<p>This page describes the commands you can use in a&nbsp;<code class="highlighter-rouge">Dockerfile</code>. When you are done reading this page, refer to the&nbsp;<a href="https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/"><code class="highlighter-rouge">Dockerfile</code>&nbsp;Best Practices</a>&nbsp;for a tip-oriented guide.</p>
<p>&nbsp;</p>


<h2 id="usage">Usage</h2>
<p>The&nbsp;<a href="https://docs.docker.com/engine/reference/commandline/build/"><code class="highlighter-rouge">docker build</code></a>&nbsp;command builds an image from a&nbsp;<code class="highlighter-rouge">Dockerfile</code>&nbsp;and a&nbsp;<em>context</em>. The build&rsquo;s context is the set of files at a specified location&nbsp;<code class="highlighter-rouge">PATH</code>&nbsp;or&nbsp;<code class="highlighter-rouge">URL</code>. The&nbsp;<code class="highlighter-rouge">PATH</code>&nbsp;is a directory on your local filesystem. The&nbsp;<code class="highlighter-rouge">URL</code>&nbsp;is a Git repository location.</p>
<p>&nbsp;</p>


<h3>Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/reference/builder/">https://docs.docker.com/engine/reference/builder/</a></li>
</ul>
<h3>Lesson Reference</h3>
<p>Set up a project directory:</p>
<pre><code>mkdir ~/custom-nginx
cd ~/custom-nginx
vi index.html</code></pre>
<p>Add a simple message to&nbsp;<code>index.html</code>:</p>
<pre><code>Hello, World!</code></pre>
<p>Create a&nbsp;<code>Dockerfile</code>:</p>
<pre><code>vi Dockerfile</code></pre>
<p>Add some directives to the&nbsp;<code>Dockerfile</code>:</p>
<pre><code># Simple nginx image
FROM ubuntu:bionic

ENV NGINX_VERSION 1.14.0-0ubuntu1.3

RUN apt-get update &amp;&amp; apt-get install -y curl
RUN apt-get update &amp;&amp; apt-get install -y nginx=$NGINX_VERSION

CMD ["nginx", "-g", "daemon off;"]</code></pre>
<p>Build and test the image:</p>
<pre><code>docker build -t custom-nginx .
docker run --name custom-nginx -d -p 8080:80 custom-nginx
curl localhost:8080</code></pre>
<p>&nbsp;</p>
<div class="rating-content">
<div class="row">
<div id="la_video_16410" class="col-xs-12 rating-container">
<div class="row rating-content rating-dialog">
<div class="col-xs-12">&nbsp;</div>
</div>
</div>
</div>
</div>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code></code></pre>
</div>
</div>


Edit your Dockerfile:

cd ~/custom-nginx
vi Dockerfile
Add more customization to the Dockerfile:

# Simple nginx image
FROM ubuntu:bionic

ENV NGINX_VERSION 1.14.0-0ubuntu1.2

RUN apt-get update && apt-get install -y curl
RUN apt-get update && apt-get install -y nginx=$NGINX_VERSION

WORKDIR /var/www/html/
ADD index.html ./

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

STOPSIGNAL SIGTERM
HEALTHCHECK CMD curl localhost:80
Rebuild the image ad test it:

docker build -t custom-nginx .
docker run -d -p 8080:80 custom-nginx
curl localhost:8080
Locate our running container with docker ps, then remove it to clean up the environment:

docker ps
docker container rm -f <container id>



<h2 id="buildkit">BuildKit</h2>
<p>Starting with version 18.09, Docker supports a new backend for executing your builds that is provided by the&nbsp;<a href="https://github.com/moby/buildkit">moby/buildkit</a>project. The BuildKit backend provides many benefits compared to the old implementation.&nbsp;</p>
<ul>
<li>Detect and skip executing unused build stages</li>
<li>Parallelize building independent build stages</li>
<li>Incrementally transfer only the changed files in your build context between builds</li>
<li>Detect and skip transferring unused files in your build context</li>
<li>Use external Dockerfile implementations with many new features</li>
<li>Avoid side-effects with rest of the API (intermediate images and containers)</li>
<li>Prioritize your build cache for automatic pruning</li>
</ul>
<h2 id="from">FROM</h2>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>FROM &lt;image&gt; [AS &lt;name&gt;]
</code></pre>
</div>
</div>
<p>Or</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>FROM &lt;image&gt;[:&lt;tag&gt;] [AS &lt;name&gt;]
</code></pre>
</div>
</div>
<p>Or</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>FROM &lt;image&gt;[@&lt;digest&gt;] [AS &lt;name&gt;]
</code></pre>
</div>
</div>
<p>The&nbsp;<code class="highlighter-rouge">FROM</code>&nbsp;instruction initializes a new build stage and sets the&nbsp;<a href="https://docs.docker.com/engine/reference/glossary/#base-image"><em>Base Image</em></a>&nbsp;for subsequent instructions. As such, a valid&nbsp;<code class="highlighter-rouge">Dockerfile</code>&nbsp;must start with a&nbsp;<code class="highlighter-rouge">FROM</code>&nbsp;instruction. The image can be any valid image &ndash; it is especially easy to start by&nbsp;<strong>pulling an image</strong>&nbsp;from the&nbsp;<a href="https://docs.docker.com/engine/tutorials/dockerrepos/"><em>Public Repositories</em></a>.</p>
<ul>
<li>
<p><code class="highlighter-rouge">ARG</code>&nbsp;is the only instruction that may precede&nbsp;<code class="highlighter-rouge">FROM</code>&nbsp;in the&nbsp;<code class="highlighter-rouge">Dockerfile</code>. See&nbsp;<a href="https://docs.docker.com/engine/reference/builder/#understand-how-arg-and-from-interact">Understand how ARG and FROM interact</a>.</p>
</li>
<li>
<p><code class="highlighter-rouge">FROM</code>&nbsp;can appear multiple times within a single&nbsp;<code class="highlighter-rouge">Dockerfile</code>&nbsp;to create multiple images or use one build stage as a dependency for another. Simply make a note of the last image ID output by the commit before each new&nbsp;<code class="highlighter-rouge">FROM</code>instruction. Each&nbsp;<code class="highlighter-rouge">FROM</code>&nbsp;instruction clears any state created by previous instructions.</p>
</li>
<li>
<p>Optionally a name can be given to a new build stage by adding&nbsp;<code class="highlighter-rouge">AS name</code>&nbsp;to the&nbsp;<code class="highlighter-rouge">FROM</code>&nbsp;instruction. The name can be used in subsequent&nbsp;<code class="highlighter-rouge">FROM</code>&nbsp;and&nbsp;<code class="highlighter-rouge">COPY --from=&lt;name|index&gt;</code>&nbsp;instructions to refer to the image built in this stage.</p>
</li>
<li>
<p>The&nbsp;<code class="highlighter-rouge">tag</code>&nbsp;or&nbsp;<code class="highlighter-rouge">digest</code>&nbsp;values are optional. If you omit either of them, the builder assumes a&nbsp;<code class="highlighter-rouge">latest</code>&nbsp;tag by default. The builder returns an error if it cannot find the&nbsp;<code class="highlighter-rouge">tag</code> value</p>
</li>
</ul>
<h3 id="understand-how-arg-and-from-interact">Understand how ARG and FROM interact</h3>
<p><code class="highlighter-rouge">FROM</code>&nbsp;instructions support variables that are declared by any&nbsp;<code class="highlighter-rouge">ARG</code>&nbsp;instructions that occur before the first&nbsp;<code class="highlighter-rouge">FROM</code>.</p>
<pre><code class="language-Dockerfile">ARG  CODE_VERSION=latest
FROM base:${CODE_VERSION}
CMD  /code/run-app

FROM extras:${CODE_VERSION}
CMD  /code/run-extras
</code></pre>
<p>An&nbsp;<code class="highlighter-rouge">ARG</code>&nbsp;declared before a&nbsp;<code class="highlighter-rouge">FROM</code>&nbsp;is outside of a build stage, so it can&rsquo;t be used in any instruction after a&nbsp;<code class="highlighter-rouge">FROM</code>. To use the default value of an&nbsp;<code class="highlighter-rouge">ARG</code>&nbsp;declared before the first&nbsp;<code class="highlighter-rouge">FROM</code>&nbsp;use an&nbsp;<code class="highlighter-rouge">ARG</code>&nbsp;instruction without a value inside of a build stage:</p>
<pre><code class="language-Dockerfile">ARG VERSION=latest
FROM busybox:$VERSION
ARG VERSION
RUN echo $VERSION &gt; image_version</code><br /><br /><br /><br /></pre>
<h2 id="run">RUN</h2>
<p>RUN has 2 forms:</p>
<ul>
<li><code class="highlighter-rouge">RUN &lt;command&gt;</code>&nbsp;(<em>shell</em>&nbsp;form, the command is run in a shell, which by default is&nbsp;<code class="highlighter-rouge">/bin/sh -c</code>&nbsp;on Linux or&nbsp;<code class="highlighter-rouge">cmd /S /C</code>on Windows)</li>
<li><code class="highlighter-rouge">RUN ["executable", "param1", "param2"]</code>&nbsp;(<em>exec</em>&nbsp;form)</li>
</ul>
<p>The&nbsp;<code class="highlighter-rouge">RUN</code>&nbsp;instruction will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the&nbsp;<code class="highlighter-rouge">Dockerfile</code>.</p>
<p>&nbsp;</p>
<h2 id="cmd">CMD</h2>
<p>The&nbsp;<code class="highlighter-rouge">CMD</code>&nbsp;instruction has three forms:</p>
<ul>
<li><code class="highlighter-rouge">CMD ["executable","param1","param2"]</code>&nbsp;(<em>exec</em>&nbsp;form, this is the preferred form)</li>
<li><code class="highlighter-rouge">CMD ["param1","param2"]</code>&nbsp;(as&nbsp;<em>default parameters to ENTRYPOINT</em>)</li>
<li><code class="highlighter-rouge">CMD command param1 param2</code>&nbsp;(<em>shell</em>&nbsp;form)</li>
</ul>
<p>There can only be one&nbsp;<code class="highlighter-rouge">CMD</code>&nbsp;instruction in a&nbsp;<code class="highlighter-rouge">Dockerfile</code>. If you list more than one&nbsp;<code class="highlighter-rouge">CMD</code>&nbsp;then only the last&nbsp;<code class="highlighter-rouge">CMD</code>&nbsp;will take effect.</p>
<p><strong>The main purpose of a&nbsp;<code class="highlighter-rouge">CMD</code>&nbsp;is to provide defaults for an executing container.</strong>&nbsp;These defaults can include an executable, or they can omit the executable, in which case you must specify an&nbsp;<code class="highlighter-rouge">ENTRYPOINT</code>&nbsp;instruction as well.</p>
<p>&nbsp;</p>
<h2 id="environment-replacement">Environment replacement</h2>
<p>Environment variables (declared with&nbsp;<a href="https://docs.docker.com/engine/reference/builder/#env">the&nbsp;<code class="highlighter-rouge">ENV</code>&nbsp;statement</a>) can also be used in certain instructions as variables to be interpreted by the&nbsp;<code class="highlighter-rouge">Dockerfile</code>. Escapes are also handled for including variable-like syntax into a statement literally.</p>
<p>Environment variables are notated in the&nbsp;<code class="highlighter-rouge">Dockerfile</code>&nbsp;either with&nbsp;<code class="highlighter-rouge">$variable_name</code>&nbsp;or&nbsp;<code class="highlighter-rouge">${variable_name}</code>. They are treated equivalently and the brace syntax is typically used to address issues with variable names with no whitespace, like&nbsp;<code class="highlighter-rouge">${foo}_bar</code>.</p>
<p>The&nbsp;<code class="highlighter-rouge">${variable_name}</code>&nbsp;syntax also supports a few of the standard&nbsp;<code class="highlighter-rouge">bash</code>&nbsp;modifiers as specified below:</p>
<ul>
<li><code class="highlighter-rouge">${variable:-word}</code>&nbsp;indicates that if&nbsp;<code class="highlighter-rouge">variable</code>&nbsp;is set then the result will be that value. If&nbsp;<code class="highlighter-rouge">variable</code>&nbsp;is not set then&nbsp;<code class="highlighter-rouge">word</code>&nbsp;will be the result.</li>
<li><code class="highlighter-rouge">${variable:+word}</code>&nbsp;indicates that if&nbsp;<code class="highlighter-rouge">variable</code>&nbsp;is set then&nbsp;<code class="highlighter-rouge">word</code>&nbsp;will be the result, otherwise the result is the empty string.</li>
</ul>
<p>In all cases,&nbsp;<code class="highlighter-rouge">word</code>&nbsp;can be any string, including additional environment variables.</p>
<p>Escaping is possible by adding a&nbsp;<code class="highlighter-rouge">\</code>&nbsp;before the variable:&nbsp;<code class="highlighter-rouge">\$foo</code>&nbsp;or&nbsp;<code class="highlighter-rouge">\${foo}</code>, for example, will translate to&nbsp;<code class="highlighter-rouge">$foo</code>&nbsp;and&nbsp;<code class="highlighter-rouge">${foo}</code>&nbsp;literals respectively.</p>
<p>Example (parsed representation is displayed after the&nbsp;<code class="highlighter-rouge">#</code>):</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>FROM busybox
ENV foo /bar
WORKDIR ${foo}   # WORKDIR /bar
ADD . $foo       # ADD . /bar
COPY \$foo /quux # COPY $foo /quux
</code></pre>
</div>
</div>
<p>Environment variables are supported by the following list of instructions in the&nbsp;<code class="highlighter-rouge">Dockerfile</code>:</p>
<ul>
<li><code class="highlighter-rouge">ADD</code></li>
<li><code class="highlighter-rouge">COPY</code></li>
<li><code class="highlighter-rouge">ENV</code></li>
<li><code class="highlighter-rouge">EXPOSE</code></li>
<li><code class="highlighter-rouge">FROM</code></li>
<li><code class="highlighter-rouge">LABEL</code></li>
<li><code class="highlighter-rouge">STOPSIGNAL</code></li>
<li><code class="highlighter-rouge">USER</code></li>
<li><code class="highlighter-rouge">VOLUME</code></li>
<li><code class="highlighter-rouge">WORKDIR</code></li>
</ul>
<p>as well as:</p>
<ul>
<li><code class="highlighter-rouge">ONBUILD</code>&nbsp;(when combined with one of the supported instructions above)</li>
</ul>
<blockquote>
<p><strong>Note</strong>: prior to 1.4,&nbsp;<code class="highlighter-rouge">ONBUILD</code>&nbsp;instructions did&nbsp;<strong>NOT</strong>&nbsp;support environment variable, even when combined with any of the instructions listed above.</p>
</blockquote>
<p>Environment variable substitution will use the same value for each variable throughout the entire instruction. In other words, in this example:</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>ENV abc=hello
ENV abc=bye def=$abc
ENV ghi=$abc
</code></pre>
</div>
</div>
<p>will result in&nbsp;<code class="highlighter-rouge">def</code>&nbsp;having a value of&nbsp;<code class="highlighter-rouge">hello</code>, not&nbsp;<code class="highlighter-rouge">bye</code>. However,&nbsp;<code class="highlighter-rouge">ghi</code>&nbsp;will have a value of&nbsp;<code class="highlighter-rouge">bye</code>&nbsp;because it is not part of the same instruction that set&nbsp;<code class="highlighter-rouge">abc</code>&nbsp;to&nbsp;<code class="highlighter-rouge">bye</code>.</p>
<p>&nbsp;</p>
<h2 id="dockerignore-file">.dockerignore file</h2>
<p>Before the docker CLI sends the context to the docker daemon, it looks for a file named&nbsp;<code class="highlighter-rouge">.dockerignore</code>&nbsp;in the root directory of the context. If this file exists, the CLI modifies the context to exclude files and directories that match patterns in it. This helps to avoid unnecessarily sending large or sensitive files and directories to the daemon and potentially adding them to images using&nbsp;<code class="highlighter-rouge">ADD</code>&nbsp;or&nbsp;<code class="highlighter-rouge">COPY</code>.</p>
<p>&nbsp;</p>
<p>if a line in <code class="highlighter-rouge">.dockerignore</code>&nbsp;file starts with&nbsp;<code class="highlighter-rouge">#</code>&nbsp;in column 1, then this line is considered as a comment and is ignored before interpreted by the CLI.</p>
<p>Here is an example&nbsp;<code class="highlighter-rouge">.dockerignore</code>&nbsp;file:</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code># comment
*/temp*
*/*/temp*
temp?<br /><br /></code></pre>
<p>his file causes the following build behavior:</p>
<pre class="highlight"><code></code></pre>
<table>
<thead>
<tr>
<th>Rule</th>
<th>Behavior</th>
</tr>
</thead>
<tbody>
<tr>
<td><code class="highlighter-rouge"># comment</code></td>
<td>Ignored.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">*/temp*</code></td>
<td>Exclude files and directories whose names start with&nbsp;<code class="highlighter-rouge">temp</code>&nbsp;in any immediate subdirectory of the root. For example, the plain file&nbsp;<code class="highlighter-rouge">/somedir/temporary.txt</code>&nbsp;is excluded, as is the directory&nbsp;<code class="highlighter-rouge">/somedir/temp</code>.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">*/*/temp*</code></td>
<td>Exclude files and directories starting with&nbsp;<code class="highlighter-rouge">temp</code>&nbsp;from any subdirectory that is two levels below the root. For example,&nbsp;<code class="highlighter-rouge">/somedir/subdir/temporary.txt</code>&nbsp;is excluded.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">temp?</code></td>
<td>Exclude files and directories in the root directory whose names are a one-character extension of&nbsp;<code class="highlighter-rouge">temp</code>. For example,&nbsp;<code class="highlighter-rouge">/tempa</code>&nbsp;and&nbsp;<code class="highlighter-rouge">/tempb</code>&nbsp;are excluded.</td>
</tr>
</tbody>
</table>
<pre class="highlight"><code></code></pre>
<h2 id="env">ENV</h2>
<pre class="highlight"><code></code></pre>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>ENV &lt;key&gt; &lt;value&gt;
ENV &lt;key&gt;=&lt;value&gt; ...
</code></pre>
</div>
</div>
<pre class="highlight"><code></code></pre>
<p>The&nbsp;<code class="highlighter-rouge">ENV</code>&nbsp;instruction sets the environment variable&nbsp;<code class="highlighter-rouge">&lt;key&gt;</code>&nbsp;to the value&nbsp;<code class="highlighter-rouge">&lt;value&gt;</code>. This value will be in the environment for all subsequent instructions in the build stage and can be&nbsp;<a href="https://docs.docker.com/engine/reference/builder/#environment-replacement">replaced inline</a>&nbsp;in many as well.</p>
<p>For example:</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>ENV myName="John Doe" myDog=Rex\ The\ Dog \
    myCat=fluffy
</code></pre>
</div>
</div>
<p>and</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>ENV myName John Doe
ENV myDog Rex The Dog
ENV myCat fluffy
</code><br /><br /></pre>
<h2 id="add">ADD</h2>
<p>ADD has two forms:</p>
<ul>
<li><code class="highlighter-rouge">ADD [--chown=&lt;user&gt;:&lt;group&gt;] &lt;src&gt;... &lt;dest&gt;</code></li>
<li><code class="highlighter-rouge">ADD [--chown=&lt;user&gt;:&lt;group&gt;] ["&lt;src&gt;",... "&lt;dest&gt;"]</code>&nbsp;(this form is required for paths containing whitespace)</li>
</ul>
<blockquote>
<p><strong>Note</strong>: The&nbsp;<code class="highlighter-rouge">--chown</code>&nbsp;feature is only supported on Dockerfiles used to build Linux containers, and will not work on Windows containers. Since user and group ownership concepts do not translate between Linux and Windows, the use of&nbsp;<code class="highlighter-rouge">/etc/passwd</code>&nbsp;and&nbsp;<code class="highlighter-rouge">/etc/group</code>&nbsp;for translating user and group names to IDs restricts this feature to only be viable for Linux OS-based containers.</p>
</blockquote>
<p>The&nbsp;<code class="highlighter-rouge">ADD</code>&nbsp;instruction copies new files, directories or remote file URLs from&nbsp;<code class="highlighter-rouge">&lt;src&gt;</code>&nbsp;and adds them to the filesystem of the image at the path&nbsp;<code class="highlighter-rouge">&lt;dest&gt;</code>.</p>
<p>Each&nbsp;<code class="highlighter-rouge">&lt;src&gt;</code>&nbsp;may contain wildcards and matching will be done using Go&rsquo;s&nbsp;<a href="http://golang.org/pkg/path/filepath#Match">filepath.Match</a>&nbsp;rules. For example:</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>ADD hom* /mydir/        # adds all files starting with "hom"
ADD hom?.txt /mydir/    # ? is replaced with any single character, e.g., "home.txt"
</code></pre>
</div>
</div>
<p>The&nbsp;<code class="highlighter-rouge">&lt;dest&gt;</code>&nbsp;is an absolute path, or a path relative to&nbsp;<code class="highlighter-rouge">WORKDIR</code>, into which the source will be copied inside the destination container.</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>ADD test relativeDir/          # adds "test" to `WORKDIR`/relativeDir/
ADD test /absoluteDir/         # adds "test" to /absoluteDir/<br /><br /></code></pre>
<h2 id="copy">COPY</h2>
<pre class="highlight"><code></code></pre>
<p>COPY has two forms:</p>
<pre class="highlight"><code></code></pre>
<ul>
<li><code class="highlighter-rouge">COPY [--chown=&lt;user&gt;:&lt;group&gt;] &lt;src&gt;... &lt;dest&gt;</code></li>
<li><code class="highlighter-rouge">COPY [--chown=&lt;user&gt;:&lt;group&gt;] ["&lt;src&gt;",... "&lt;dest&gt;"]</code>&nbsp;(this form is required for paths containing whitespace)</li>
</ul>
<pre class="highlight"><code></code></pre>
<blockquote>
<p><strong>Note</strong>: The&nbsp;<code class="highlighter-rouge">--chown</code>&nbsp;feature is only supported on Dockerfiles used to build Linux containers, and will not work on Windows containers. Since user and group ownership concepts do not translate between Linux and Windows, the use of&nbsp;<code class="highlighter-rouge">/etc/passwd</code>&nbsp;and&nbsp;<code class="highlighter-rouge">/etc/group</code>&nbsp;for translating user and group names to IDs restricts this feature to only be viable for Linux OS-based containers.</p>
</blockquote>
<pre class="highlight"><code></code></pre>
<p>The&nbsp;<code class="highlighter-rouge">COPY</code>&nbsp;instruction copies new files or directories from&nbsp;<code class="highlighter-rouge">&lt;src&gt;</code>&nbsp;and adds them to the filesystem of the container at the path&nbsp;<code class="highlighter-rouge">&lt;dest&gt;</code>.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2 id="entrypoint">ENTRYPOINT</h2>
<p>ENTRYPOINT has two forms:</p>
<ul>
<li><code class="highlighter-rouge">ENTRYPOINT ["executable", "param1", "param2"]</code>&nbsp;(<em>exec</em>&nbsp;form, preferred)</li>
<li><code class="highlighter-rouge">ENTRYPOINT command param1 param2</code>&nbsp;(<em>shell</em>&nbsp;form)</li>
</ul>
<p>An&nbsp;<code class="highlighter-rouge">ENTRYPOINT</code>&nbsp;allows you to configure a container that will run as an executable.</p>
<p>For example, the following will start nginx with its default content, listening on port 80:</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>docker run -i -t --rm -p 80:80 nginx</code></pre>
<p>Command line arguments to&nbsp;<code class="highlighter-rouge">docker run &lt;image&gt;</code>&nbsp;will be appended after all elements in an&nbsp;<em>exec</em>&nbsp;form&nbsp;<code class="highlighter-rouge">ENTRYPOINT</code>, and will override all elements specified using&nbsp;<code class="highlighter-rouge">CMD</code>. This allows arguments to be passed to the entry point, i.e.,&nbsp;<code class="highlighter-rouge">docker run &lt;image&gt; -d</code>&nbsp;will pass the&nbsp;<code class="highlighter-rouge">-d</code>&nbsp;argument to the entry point. You can override the&nbsp;<code class="highlighter-rouge">ENTRYPOINT</code>&nbsp;instruction using the&nbsp;<code class="highlighter-rouge">docker run --entrypoint</code>&nbsp;flag.</p>
<p>The&nbsp;<em>shell</em>&nbsp;form prevents any&nbsp;<code class="highlighter-rouge">CMD</code>&nbsp;or&nbsp;<code class="highlighter-rouge">run</code>&nbsp;command line arguments from being used, but has the disadvantage that your&nbsp;<code class="highlighter-rouge">ENTRYPOINT</code>&nbsp;will be started as a subcommand of&nbsp;<code class="highlighter-rouge">/bin/sh -c</code>, which does not pass signals. This means that the executable will not be the container&rsquo;s&nbsp;<code class="highlighter-rouge">PID 1</code>&nbsp;- and will&nbsp;<em>not</em>&nbsp;receive Unix signals - so your executable will not receive a&nbsp;<code class="highlighter-rouge">SIGTERM</code>&nbsp;from&nbsp;<code class="highlighter-rouge">docker stop &lt;container&gt;</code>.</p>
<p>Only the last&nbsp;<code class="highlighter-rouge">ENTRYPOINT</code>&nbsp;instruction in the&nbsp;<code class="highlighter-rouge">Dockerfile</code>&nbsp;will have an effect.</p>
<p>&nbsp;</p>
<h2 id="volume">VOLUME</h2>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>VOLUME ["/data"]
</code></pre>
</div>
</div>
<p>The&nbsp;<code class="highlighter-rouge">VOLUME</code>&nbsp;instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers. The value can be a JSON array,&nbsp;<code class="highlighter-rouge">VOLUME ["/var/log/"]</code>, or a plain string with multiple arguments, such as&nbsp;<code class="highlighter-rouge">VOLUME /var/log</code>&nbsp;or&nbsp;<code class="highlighter-rouge">VOLUME /var/log /var/db</code>. For more information/examples and mounting instructions via the Docker client, refer to&nbsp;<a href="https://docs.docker.com/engine/tutorials/dockervolumes/#/mount-a-host-directory-as-a-data-volume"><em>Share Directories via Volumes</em></a>&nbsp;documentation.</p>
<p>The&nbsp;<code class="highlighter-rouge">docker run</code>&nbsp;command initializes the newly created volume with any data that exists at the specified location within the base image. For example, consider the following Dockerfile snippet:</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>FROM ubuntu
RUN mkdir /myvol
RUN echo "hello world" &gt; /myvol/greeting
VOLUME /myvol
</code></pre>
</div>
</div>
<p>This Dockerfile results in an image that causes&nbsp;<code class="highlighter-rouge">docker run</code>&nbsp;to create a new mount point at&nbsp;<code class="highlighter-rouge">/myvol</code>&nbsp;and copy the&nbsp;<code class="highlighter-rouge">greeting</code>file into the newly created volume.</p>
<p>&nbsp;</p>
<h2 id="user">USER</h2>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>USER &lt;user&gt;[:&lt;group&gt;] or
USER &lt;UID&gt;[:&lt;GID&gt;]
</code></pre>
</div>
</div>
<p>The&nbsp;<code class="highlighter-rouge">USER</code>&nbsp;instruction sets the user name (or UID) and optionally the user group (or GID) to use when running the image and for any&nbsp;<code class="highlighter-rouge">RUN</code>,&nbsp;<code class="highlighter-rouge">CMD</code>&nbsp;and&nbsp;<code class="highlighter-rouge">ENTRYPOINT</code>&nbsp;instructions that follow it in the&nbsp;<code class="highlighter-rouge">Dockerfile</code>.</p>
<blockquote>
<p><strong>Warning</strong>: When the user doesn&rsquo;t have a primary group then the image (or the next instructions) will be run with the&nbsp;<code class="highlighter-rouge">root</code>&nbsp;group.</p>
</blockquote>
</div>
</div>
<pre class="highlight"><code></code></pre>
<h2 id="stopsignal">STOPSIGNAL</h2>
<pre class="highlight"><code></code></pre>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>STOPSIGNAL signal
</code></pre>
</div>
</div>
<pre class="highlight"><code></code></pre>
<p>The&nbsp;<code class="highlighter-rouge">STOPSIGNAL</code>&nbsp;instruction sets the system call signal that will be sent to the container to exit. This signal can be a valid unsigned number that matches a position in the kernel&rsquo;s syscall table, for instance 9, or a signal name in the format SIGNAME, for instance SIGKILL.</p>
<h2 id="healthcheck">HEALTHCHECK</h2>
<p>The&nbsp;<code class="highlighter-rouge">HEALTHCHECK</code>&nbsp;instruction has two forms:</p>
<ul>
<li><code class="highlighter-rouge">HEALTHCHECK [OPTIONS] CMD command</code>&nbsp;(check container health by running a command inside the container)</li>
<li><code class="highlighter-rouge">HEALTHCHECK NONE</code>&nbsp;(disable any healthcheck inherited from the base image)</li>
</ul>
<p>The&nbsp;<code class="highlighter-rouge">HEALTHCHECK</code>&nbsp;instruction tells Docker how to test a container to check that it is still working. This can detect cases such as a web server that is stuck in an infinite loop and unable to handle new connections, even though the server process is still running.</p>
<pre class="highlight"><code></code><br /><br /><br /></pre>
</div>
</div>
</div>
</div>
<pre class="highlight"><code></code></pre>
</div>
</div>

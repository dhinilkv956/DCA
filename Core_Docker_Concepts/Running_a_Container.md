<p>Docker runs processes in isolated containers. A container is a process which runs on a host. The host may be local or remote. When an operator executes&nbsp;<code class="highlighter-rouge">docker run</code>, the container process that runs is isolated in that it has its own file system, its own networking, and its own isolated process tree separate from the host.</p>
<p>&nbsp;</p>
<p>The basic&nbsp;<code class="highlighter-rouge">docker run</code>&nbsp;command takes this form:</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>$ docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
</code></pre>
</div>
</div>
<p>The&nbsp;<code class="highlighter-rouge">docker run</code>&nbsp;command must specify an&nbsp;<a href="https://docs.docker.com/engine/reference/glossary/#image"><em>IMAGE</em></a>&nbsp;to derive the container from. An image developer can define image defaults related to:</p>
<ul>
<li>detached or foreground running</li>
<li>container identification</li>
<li>network settings</li>
<li>runtime constraints on CPU and memory</li>
</ul>


<h2 id="operator-exclusive-options">Operator exclusive options</h2>
<p>Only the operator (the person executing&nbsp;<code class="highlighter-rouge">docker run</code>) can set the following options.</p>
<ul>
<li><a href="https://docs.docker.com/engine/reference/run/#detached-vs-foreground">Detached vs foreground</a>
<ul>
<li><a href="https://docs.docker.com/engine/reference/run/#detached--d">Detached (-d)</a></li>
<li><a href="https://docs.docker.com/engine/reference/run/#foreground">Foreground</a></li>
</ul>
</li>
<li><a href="https://docs.docker.com/engine/reference/run/#container-identification">Container identification</a>
<ul>
<li><a href="https://docs.docker.com/engine/reference/run/#name---name">Name (--name)</a></li>
<li><a href="https://docs.docker.com/engine/reference/run/#pid-equivalent">PID equivalent</a></li>
</ul>
</li>
<li><a href="https://docs.docker.com/engine/reference/run/#ipc-settings---ipc">IPC settings (--ipc)</a></li>
<li><a href="https://docs.docker.com/engine/reference/run/#network-settings">Network settings</a></li>
<li><a href="https://docs.docker.com/engine/reference/run/#restart-policies---restart">Restart policies (--restart)</a></li>
<li><a href="https://docs.docker.com/engine/reference/run/#clean-up---rm">Clean up (--rm)</a></li>
<li><a href="https://docs.docker.com/engine/reference/run/#runtime-constraints-on-resources">Runtime constraints on resources</a></li>
<li><a href="https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities">Runtime privilege and Linux capabilities</a></li>
</ul>

<h3 id="detached--d">Detached (-d)</h3>
<p>To start a container in detached mode, you use&nbsp;<code class="highlighter-rouge">-d=true</code>&nbsp;or just&nbsp;<code class="highlighter-rouge">-d</code>&nbsp;option. By design, containers started in detached mode exit when the root process used to run the container exits, unless you also specify the&nbsp;<code class="highlighter-rouge">--rm</code>&nbsp;option. If you use&nbsp;<code class="highlighter-rouge">-d</code>&nbsp;with&nbsp;<code class="highlighter-rouge">--rm</code>, the container is removed when it exits&nbsp;<strong>or</strong>&nbsp;when the daemon exits, whichever happens first.</p>
<h3 id="foreground">Foreground</h3>
<p>In foreground mode (the default when&nbsp;<code class="highlighter-rouge">-d</code>&nbsp;is not specified),&nbsp;<code class="highlighter-rouge">docker run</code> can start the process in the container and attach the console to the process&rsquo;s standard input, output, and standard error. It can even pretend to be a TTY (this is what most command line executables expect) and pass along signals.&nbsp;</p>
<p>&nbsp;</p>
<h3 id="name---name">Name (--name)</h3>
<p>The operator can identify a container in three ways:</p>
<table>
<thead>
<tr>
<th>Identifier type</th>
<th>Example value</th>
</tr>
</thead>
<tbody>
<tr>
<td>UUID long identifier</td>
<td>&ldquo;f78375b1c487e03c9438c729345e54db9d20cfa2ac1fc3494b6eb60872e74778&rdquo;</td>
</tr>
<tr>
<td>UUID short identifier</td>
<td>&ldquo;f78375b1c487&rdquo;</td>
</tr>
<tr>
<td>Name</td>
<td>&ldquo;evil_ptolemy&rdquo;</td>
</tr>
</tbody>
</table>
<p>The UUID identifiers come from the Docker daemon. If you do not assign a container name with the&nbsp;<code class="highlighter-rouge">--name</code>&nbsp;option, then the daemon generates a random string name for you. Defining a&nbsp;<code class="highlighter-rouge">name</code>&nbsp;can be a handy way to add meaning to a container. If you specify a&nbsp;<code class="highlighter-rouge">name</code>, you can use it when referencing the container within a Docker network. This works for both background and foreground Docker containers.</p>
<p><strong>Note</strong>: Containers on the default bridge network must be linked to communicate by name.</p>
<p>&nbsp;</p>
<h3 id="imagetag">Image[:tag]</h3>
<p>While not strictly a means of identifying a container, you can specify a version of an image you&rsquo;d like to run the container with by adding&nbsp;<code class="highlighter-rouge">image[:tag]</code>&nbsp;to the command. For example,&nbsp;<code class="highlighter-rouge">docker run ubuntu:14.04</code>.</p>
<p>&nbsp;</p>
<h2 id="restart-policies---restart">Restart policies (--restart)</h2>
<p>Using the&nbsp;<code class="highlighter-rouge">--restart</code>&nbsp;flag on Docker run you can specify a restart policy for how a container should or should not be restarted on exit.</p>
<p>When a restart policy is active on a container, it will be shown as either&nbsp;<code class="highlighter-rouge">Up</code>&nbsp;or&nbsp;<code class="highlighter-rouge">Restarting</code>&nbsp;in&nbsp;<a href="https://docs.docker.com/engine/reference/commandline/ps/"><code class="highlighter-rouge">docker ps</code></a>. It can also be useful to use&nbsp;<a href="https://docs.docker.com/engine/reference/commandline/events/"><code class="highlighter-rouge">docker events</code></a>&nbsp;to see the restart policy in effect.</p>
<p>Docker supports the following restart policies:</p>
<table>
<thead>
<tr>
<th>Policy</th>
<th>Result</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>no</strong></td>
<td>Do not automatically restart the container when it exits. This is the default.</td>
</tr>
<tr>
<td><strong>on-failure</strong>[:max-retries]</td>
<td>Restart only if the container exits with a non-zero exit status. Optionally, limit the number of restart retries the Docker daemon attempts.</td>
</tr>
<tr>
<td><strong>always</strong></td>
<td>Always restart the container regardless of the exit status. When you specify always, the Docker daemon will try to restart the container indefinitely. The container will also always start on daemon startup, regardless of the current state of the container.</td>
</tr>
<tr>
<td><strong>unless-stopped</strong></td>
<td>Always restart the container regardless of the exit status, including on daemon startup, except if the container was put into a stopped state before the Docker daemon was stopped.</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>If a container is successfully restarted (the container is started and runs for at least 10 seconds), the delay is reset to its default value of 100 ms.</p>
<p>&nbsp;</p>
<p>The number of (attempted) restarts for a container can be obtained via&nbsp;<a href="https://docs.docker.com/engine/reference/commandline/inspect/"><code class="highlighter-rouge">docker inspect</code></a>. For example, to get the number of restarts for container &ldquo;my-container&rdquo;;</p>
<div class="highlighter-rouge">
<div class="highlight">


Overriding Dockerfile image defaults
When a developer builds an image from a Dockerfile or when she commits it, the developer can set a number of default parameters that take effect when the image starts up as a container.

Four of the Dockerfile commands cannot be overridden at runtime: FROM, MAINTAINER, RUN, and ADD. Everything else has a corresponding override in docker run. We’ll go through what the developer might have set in each Dockerfile instruction and how the operator can override that setting.

CMD (Default Command or Options)
ENTRYPOINT (Default Command to Execute at Runtime)
EXPOSE (Incoming Ports)
ENV (Environment Variables)
HEALTHCHECK
VOLUME (Shared Filesystems)
USER
WORKDIR

<pre class="highlight"><code>$ docker inspect -f "{{ .RestartCount }}" my-container
# 2
</code></pre>
</div>
</div>
<p>Or, to get the last time the container was (re)started;</p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>$ docker inspect -f "{{ .State.StartedAt }}" my-container
# 2015-03-04T23:47:07.691840179Z</code><br /><br /><br /></pre>
<h2 id="exit-status">Exit Status</h2>
<p>The exit code from&nbsp;<code class="highlighter-rouge">docker run</code>&nbsp;gives information about why the container failed to run or why it exited. When&nbsp;<code class="highlighter-rouge">docker run</code>exits with a non-zero code, the exit codes follow the&nbsp;<code class="highlighter-rouge">chroot</code>&nbsp;standard, see below:</p>
<p><strong><em>125</em></strong>&nbsp;if the error is with Docker daemon&nbsp;<strong><em>itself</em></strong></p>
<div class="highlighter-rouge">
<div class="highlight">
<pre class="highlight"><code>$ docker run --foo busybox; echo $?
# flag provided but not defined: --foo
  See 'docker run --help'.
  125</code></pre>
</div>
</div>
</div>
</div>




<h2 id="runtime-constraints-on-resources">Runtime constraints on resources</h2>
<p>The operator can also adjust the performance parameters of the container:</p>
<table>
<thead>
<tr>
<th>Option</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code class="highlighter-rouge">-m</code>,&nbsp;<code class="highlighter-rouge">--memory=""</code></td>
<td>Memory limit (format:&nbsp;<code class="highlighter-rouge">&lt;number&gt;[&lt;unit&gt;]</code>). Number is a positive integer. Unit can be one of&nbsp;<code class="highlighter-rouge">b</code>,&nbsp;<code class="highlighter-rouge">k</code>,&nbsp;<code class="highlighter-rouge">m</code>, or&nbsp;<code class="highlighter-rouge">g</code>. Minimum is 4M.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--memory-swap=""</code></td>
<td>Total memory limit (memory + swap, format:&nbsp;<code class="highlighter-rouge">&lt;number&gt;[&lt;unit&gt;]</code>). Number is a positive integer. Unit can be one of&nbsp;<code class="highlighter-rouge">b</code>,&nbsp;<code class="highlighter-rouge">k</code>,&nbsp;<code class="highlighter-rouge">m</code>, or&nbsp;<code class="highlighter-rouge">g</code>.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--memory-reservation=""</code></td>
<td>Memory soft limit (format:&nbsp;<code class="highlighter-rouge">&lt;number&gt;[&lt;unit&gt;]</code>). Number is a positive integer. Unit can be one of&nbsp;<code class="highlighter-rouge">b</code>,&nbsp;<code class="highlighter-rouge">k</code>,&nbsp;<code class="highlighter-rouge">m</code>, or&nbsp;<code class="highlighter-rouge">g</code>.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--kernel-memory=""</code></td>
<td>Kernel memory limit (format:&nbsp;<code class="highlighter-rouge">&lt;number&gt;[&lt;unit&gt;]</code>). Number is a positive integer. Unit can be one of&nbsp;<code class="highlighter-rouge">b</code>,&nbsp;<code class="highlighter-rouge">k</code>,&nbsp;<code class="highlighter-rouge">m</code>, or&nbsp;<code class="highlighter-rouge">g</code>. Minimum is 4M.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">-c</code>,&nbsp;<code class="highlighter-rouge">--cpu-shares=0</code></td>
<td>CPU shares (relative weight)</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--cpus=0.000</code></td>
<td>Number of CPUs. Number is a fractional number. 0.000 means no limit.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--cpu-period=0</code></td>
<td>Limit the CPU CFS (Completely Fair Scheduler) period</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--cpuset-cpus=""</code></td>
<td>CPUs in which to allow execution (0-3, 0,1)</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--cpuset-mems=""</code></td>
<td>Memory nodes (MEMs) in which to allow execution (0-3, 0,1). Only effective on NUMA systems.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--cpu-quota=0</code></td>
<td>Limit the CPU CFS (Completely Fair Scheduler) quota</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--cpu-rt-period=0</code></td>
<td>Limit the CPU real-time period. In microseconds. Requires parent cgroups be set and cannot be higher than parent. Also check rtprio ulimits.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--cpu-rt-runtime=0</code></td>
<td>Limit the CPU real-time runtime. In microseconds. Requires parent cgroups be set and cannot be higher than parent. Also check rtprio ulimits.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--blkio-weight=0</code></td>
<td>Block IO weight (relative weight) accepts a weight value between 10 and 1000.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--blkio-weight-device=""</code></td>
<td>Block IO weight (relative device weight, format:&nbsp;<code class="highlighter-rouge">DEVICE_NAME:WEIGHT</code>)</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--device-read-bps=""</code></td>
<td>Limit read rate from a device (format:&nbsp;<code class="highlighter-rouge">&lt;device-path&gt;:&lt;number&gt;[&lt;unit&gt;]</code>). Number is a positive integer. Unit can be one of&nbsp;<code class="highlighter-rouge">kb</code>,&nbsp;<code class="highlighter-rouge">mb</code>, or&nbsp;<code class="highlighter-rouge">gb</code>.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--device-write-bps=""</code></td>
<td>Limit write rate to a device (format:&nbsp;<code class="highlighter-rouge">&lt;device-path&gt;:&lt;number&gt;[&lt;unit&gt;]</code>). Number is a positive integer. Unit can be one of&nbsp;<code class="highlighter-rouge">kb</code>,&nbsp;<code class="highlighter-rouge">mb</code>, or&nbsp;<code class="highlighter-rouge">gb</code>.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--device-read-iops=""</code></td>
<td>Limit read rate (IO per second) from a device (format:&nbsp;<code class="highlighter-rouge">&lt;device-path&gt;:&lt;number&gt;</code>). Number is a positive integer.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--device-write-iops=""</code></td>
<td>Limit write rate (IO per second) to a device (format:&nbsp;<code class="highlighter-rouge">&lt;device-path&gt;:&lt;number&gt;</code>). Number is a positive integer.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--oom-kill-disable=false</code></td>
<td>Whether to disable OOM Killer for the container or not.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--oom-score-adj=0</code></td>
<td>Tune container&rsquo;s OOM preferences (-1000 to 1000)</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--memory-swappiness=""</code></td>
<td>Tune a container&rsquo;s memory swappiness behavior. Accepts an integer between 0 and 100.</td>
</tr>
<tr>
<td><code class="highlighter-rouge">--shm-size=""</code></td>
<td>Size of&nbsp;<code class="highlighter-rouge">/dev/shm</code>. The format is&nbsp;<code class="highlighter-rouge">&lt;number&gt;&lt;unit&gt;</code>.&nbsp;<code class="highlighter-rouge">number</code>&nbsp;must be greater than&nbsp;<code class="highlighter-rouge">0</code>. Unit is optional and can be&nbsp;<code class="highlighter-rouge">b</code>&nbsp;(bytes),&nbsp;<code class="highlighter-rouge">k</code>&nbsp;(kilobytes),&nbsp;<code class="highlighter-rouge">m</code>&nbsp;(megabytes), or&nbsp;<code class="highlighter-rouge">g</code>&nbsp;(gigabytes). If you omit the unit, the system uses bytes. If you omit the size entirely, the system uses&nbsp;<code class="highlighter-rouge">64m</code>.</td>
</tr>
</tbody>
</table>

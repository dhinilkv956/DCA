<h2>Namespaces and Cgroups</h2>


<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/engine/docker-overview/#the-underlying-technology">https://docs.docker.com/engine/docker-overview/#the-underlying-technology</a></li>
<li><a href="https://docs.docker.com/engine/security/userns-remap/">https://docs.docker.com/engine/security/userns-remap/</a></li>
</ul>

<h3 id="namespaces">Namespaces</h3>
<p>Docker uses a technology called&nbsp;<code class="highlighter-rouge">namespaces</code>&nbsp;to provide the isolated workspace called the&nbsp;<em>container</em>. When you run a container, Docker creates a set of&nbsp;<em>namespaces</em>&nbsp;for that container.</p>
<p>These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace.</p>
<p>Docker Engine uses namespaces such as the following on Linux:</p>
<ul>
<li><strong>The&nbsp;<code class="highlighter-rouge">pid</code>&nbsp;namespace:</strong>&nbsp;Process isolation (PID: Process ID).</li>
<li><strong>The&nbsp;<code class="highlighter-rouge">net</code>&nbsp;namespace:</strong>&nbsp;Managing network interfaces (NET: Networking).</li>
<li><strong>The&nbsp;<code class="highlighter-rouge">ipc</code>&nbsp;namespace:</strong>&nbsp;Managing access to IPC resources (IPC: InterProcess Communication).</li>
<li><strong>The&nbsp;<code class="highlighter-rouge">mnt</code>&nbsp;namespace:</strong>&nbsp;Managing filesystem mount points (MNT: Mount).</li>
<li><strong>The&nbsp;<code class="highlighter-rouge">uts</code>&nbsp;namespace:</strong>&nbsp;Isolating kernel and version identifiers. (UTS: Unix Timesharing System).</li>
</ul>
<h3 id="control-groups">Control groups</h3>
<p>Docker Engine on Linux also relies on another technology called&nbsp;<em>control groups</em>&nbsp;(<code class="highlighter-rouge">cgroups</code>). A cgroup limits an application to a specific set of resources. Control groups allow Docker Engine to share available hardware resources to containers and optionally enforce limits and constraints. For example, you can limit the memory available to a specific container.</p>

<h3 id="control-groups">Control groups</h3>
<p>Docker Engine on Linux also relies on another technology called&nbsp;<em>control groups</em>&nbsp;(<code class="highlighter-rouge">cgroups</code>). A cgroup limits an application to a specific set of resources. Control groups allow Docker Engine to share available hardware resources to containers and optionally enforce limits and constraints. For example, you can limit the memory available to a specific container.</p>
<h3 id="union-file-systems">Union file systems</h3>
<p>Union file systems, or UnionFS, are file systems that operate by creating layers, making them very lightweight and fast. Docker Engine uses UnionFS to provide the building blocks for containers. Docker Engine can use multiple UnionFS variants, including AUFS, btrfs, vfs, and DeviceMapper.</p>
<h3 id="container-format">Container format</h3>
<p>Docker Engine combines the namespaces, control groups, and UnionFS into a wrapper called a container format. The default container format is&nbsp;<code class="highlighter-rouge">libcontainer</code>. In the future, Docker may support other container formats by integrating with technologies such as BSD Jails or Solaris Zones.</p>

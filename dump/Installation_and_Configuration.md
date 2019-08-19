<div class="expectation ng-star-inserted">
<div>
<h4>Installation and Configuration</h4>
<div id="cdk-accordion-child-0" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-0">
<div class="mat-expansion-panel-body">
<div class="questions">
<div class="question-item ng-star-inserted">
<h3 class="question-title-number">1.</h3>
<p>Sara wants to run a container using the&nbsp;<code>busybox</code>&nbsp;image, and she wants to pass a custom command to the container:&nbsp;<code>echo Docker is great!</code>. Which of the following commands will accomplish this?</p>
<div id="cdk-accordion-child-6" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-6">
<div class="mat-expansion-panel-body">
<div>
<ul>
<li class="ng-star-inserted">
<div class="choice-item">
<p>A.&nbsp;<code>docker run busybox ["echo", "Docker is great!"]</code></p>
<span class="correction correct-false ng-star-inserted">close&nbsp;Your Answer</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this incorrect?</h5>
<p>The array syntax is appropriate for a Dockerfile, but not for specifying the command at the command line.</p>
</div>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>B.&nbsp;<code>docker run busybox echo Docker is great!</code></p>
<span class="correction correct-true ng-star-inserted">done&nbsp;Correct</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this correct?</h5>
<p>This command will successfully execute the&nbsp;<code>echo</code>&nbsp;command in the container and print the message to the screen.</p>
</div>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>C.&nbsp;<code>docker run busybox -c echo Docker is great!</code></p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>D.&nbsp;<code>docker run busybox -cmd echo Docker is great!</code></p>
</div>
</li>
</ul>
<div class="rating-content rating-dialog">
<div class="rating-buttons"><button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper"> </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
<button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper">  </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="question-item ng-star-inserted">
<h3 class="question-title-number">2.</h3>
<p>Which of the following commands will run a&nbsp;<code>busybox</code>&nbsp;container and automatically delete it once it exits?</p>
<div id="cdk-accordion-child-7" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-7">
<div class="mat-expansion-panel-body">
<div>
<ul>
<li class="ng-star-inserted">
<div class="choice-item">
<p>A.&nbsp;<code>docker run --restart no busybox</code></p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>B.&nbsp;<code>docker run --rm busybox</code></p>
<span class="correction correct-true ng-star-inserted">done&nbsp;Correct</span></div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>C.&nbsp;<code>docker run --rm --restart on-failure busybox</code></p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>D.&nbsp;<code>docker container rm busybox</code></p>
</div>
</li>
</ul>
<div class="rating-content rating-dialog">
<div class="rating-buttons"><button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper"> </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
<button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper">  </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="question-item ng-star-inserted">
<h3 class="question-title-number">3.</h3>
<p>Which of the following is not backed up when performing a Docker Trusted Registry (DTR) metadata backup?</p>
<div id="cdk-accordion-child-8" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-8">
<div class="mat-expansion-panel-body">
<div>
<ul>
<li class="ng-star-inserted">
<div class="choice-item">
<p>A. DTR Configurations</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>B. Role-based access control (RBAC) settings.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>C. Repository metadata.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>D. Docker images.</p>
<span class="correction correct-true ng-star-inserted">done&nbsp;Correct</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this correct?</h5>
<p>A DTR metadata backup does not include the images themselves.</p>
</div>
</div>
</li>
</ul>
<div class="rating-content rating-dialog">
<div class="rating-buttons"><button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper"> </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
<button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper">  </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="question-item ng-star-inserted">
<h3 class="question-title-number">4.</h3>
<p>Which of the following best describes the procedure for backing up the Universal Control Plane (UCP) metadata?</p>
<div id="cdk-accordion-child-9" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-9">
<div class="mat-expansion-panel-body">
<div>
<ul>
<li class="ng-star-inserted">
<div class="choice-item">
<p>A. Run a container from the&nbsp;<code>ucp</code>&nbsp;image with the&nbsp;<code>uninstall-ucp</code>&nbsp;command.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>B. Create an archive for all of the data under the&nbsp;<code>/var/data/ucp</code>&nbsp;directory.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>C. Create an archive for all of the data under the&nbsp;<code>/etc/docker/ucp</code>&nbsp;directory.</p>
<span class="correction correct-false ng-star-inserted">close&nbsp;Your Answer</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this incorrect?</h5>
<p>This is not part of the procedure for backing up the UCP metadata.</p>
</div>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>D. Run a container from the&nbsp;<code>ucp</code>&nbsp;image with the&nbsp;<code>backup</code>&nbsp;command.</p>
<span class="correction correct-true ng-star-inserted">done&nbsp;Correct</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this correct?</h5>
<p>This is the basic procedure for backing up the UCP metadata.</p>
</div>
</div>
</li>
</ul>
<div class="rating-content rating-dialog">
<div class="rating-buttons"><button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper"> </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
<button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper">  </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="question-item ng-star-inserted">
<h3 class="question-title-number">5.</h3>
<p>Which of the following commands will ensure that a container uses a maximum of 1 GB of active memory?</p>
<div id="cdk-accordion-child-10" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-10">
<div class="mat-expansion-panel-body">
<div>
<ul>
<li class="ng-star-inserted">
<div class="choice-item">
<p>A.&nbsp;<code>docker run --memory-swap 2G --memory-reservation 1G nginx</code></p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>B.&nbsp;<code>docker run --memory-swap 2G nginx</code></p>
<span class="correction correct-false ng-star-inserted">close&nbsp;Your Answer</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this incorrect?</h5>
<p>The&nbsp;<code>--memory-swap</code>&nbsp;flag manages total memory, including swap, not just active memory. With this command, it is possible for the container to use more than 1 GB active memory.</p>
</div>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>C.&nbsp;<code>docker run --memory 1G nginx</code></p>
<span class="correction correct-true ng-star-inserted">done&nbsp;Correct</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this correct?</h5>
<p>The&nbsp;<code>--memory</code>&nbsp;flag limits active memory.</p>
</div>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>D.&nbsp;<code>docker run --memory-reservation 1G nginx</code></p>
</div>
</li>
</ul>
<div class="rating-content rating-dialog">
<div class="rating-buttons"><button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper"> </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
<button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper">  </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="question-item ng-star-inserted">
<h3 class="question-title-number">6.</h3>
<p>What is the difference between a manager and a worker in Docker swarm?</p>
<div id="cdk-accordion-child-11" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-11">
<div class="mat-expansion-panel-body">
<div>
<ul>
<li class="ng-star-inserted">
<div class="choice-item">
<p>A. Managers create new workers.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>B. Managers handle networking, while workers handle containers.</p>
<span class="correction correct-false ng-star-inserted">close&nbsp;Your Answer</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this incorrect?</h5>
<p>Both managers and workers handle various aspects of networking and run containers.</p>
</div>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>C. Managers never execute containers, workers do.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>D. Managers control the cluster, while workers only execute workloads.</p>
<span class="correction correct-true ng-star-inserted">done&nbsp;Correct</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this correct?</h5>
<p>This describes the roles of managers and workers in a swarm.</p>
</div>
</div>
</li>
</ul>
<div class="rating-content rating-dialog">
<div class="rating-buttons"><button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper"> </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
<button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper">  </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="question-item ng-star-inserted">
<h3 class="question-title-number">7.</h3>
<p>How would we back up Docker Swarm?</p>
<div id="cdk-accordion-child-12" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-12">
<div class="mat-expansion-panel-body">
<div>
<ul>
<li class="ng-star-inserted">
<div class="choice-item">
<p>A. Back up the layered file systems of all containers running within the swarm.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>B. Back up the contents of&nbsp;<code>/etc/docker/swarm</code>&nbsp;on a Swarm manager.</p>
<span class="correction correct-false ng-star-inserted">close&nbsp;Your Answer</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this incorrect?</h5>
<p>This is not the correct directory to back up.</p>
</div>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>C. Back up the contents of&nbsp;<code>/etc/docker</code>&nbsp;on a Swarm manager.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>D. Back up the contents of&nbsp;<code>/var/lib/docker/swarm</code>&nbsp;on a Swarm manager.</p>
<span class="correction correct-true ng-star-inserted">done&nbsp;Correct</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this correct?</h5>
<p>We can back up Docker Swarm by backing up data in&nbsp;<code>/var/lib/docker/swarm</code>.</p>
</div>
</div>
</li>
</ul>
<div class="rating-content rating-dialog">
<div class="rating-buttons"><button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper"> </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
<button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper">  </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="question-item ng-star-inserted">
<h3 class="question-title-number">8.</h3>
<p>Amanda wants to execute a one-time job using a Docker container. However, occasionally, this job fails and needs to restart. Amanda doesn't want to restart it manually if it fails. Which command should she use to make sure that the container executes the one-time job successfully?</p>
<div id="cdk-accordion-child-13" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-13">
<div class="mat-expansion-panel-body">
<div>
<ul>
<li class="ng-star-inserted">
<div class="choice-item">
<p>A.&nbsp;<code>docker run --recover-failure cleanup-job</code></p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>B.&nbsp;<code>docker run --restart failure-only cleanup-job</code></p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>C.&nbsp;<code>docker run --restart unless-stopped cleanup-job</code></p>
<span class="correction correct-false ng-star-inserted">close&nbsp;Your Answer</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this incorrect?</h5>
<p>This restart policy will always restart the container even if it succeeds, running it multiple times when it should only run successfully once.</p>
</div>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>D.&nbsp;<code>docker run --restart on-failure cleanup-job</code></p>
<span class="correction correct-true ng-star-inserted">done&nbsp;Correct</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this correct?</h5>
<p>This restart policy will only restart the container if it exits with a non-zero exit code.</p>
</div>
</div>
</li>
</ul>
<div class="rating-content rating-dialog">
<div class="rating-buttons"><button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper"> </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
<button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper">  </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="question-item ng-star-inserted">
<h3 class="question-title-number">9.</h3>
<p>What procedure should we follow to upgrade the Docker engine on an Ubuntu server?</p>
<div id="cdk-accordion-child-14" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-14">
<div class="mat-expansion-panel-body">
<div>
<ul>
<li class="ng-star-inserted">
<div class="choice-item">
<p>A. Stop Docker, remove the packages, and then reinstall the packages with a newer version.</p>
<span class="correction correct-false ng-star-inserted">close&nbsp;Your Answer</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this incorrect?</h5>
<p>We don't need to stop Docker or remove the packages before upgrading.</p>
</div>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>B. Stop Docker, then install the packages with the newer version.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>C. Remove all containers, stop Docker, and then install the newer version.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>D. Install newer versions of the&nbsp;<code>docker-ce</code>&nbsp;and&nbsp;<code>docker-ce-cli</code>&nbsp;packages.</p>
<span class="correction correct-true ng-star-inserted">done&nbsp;Correct</span></div>
<div class="explanation ng-star-inserted">forum
<div>
<h5>Why is this correct?</h5>
<p>We must install newer versions of the packages in order to upgrade Docker.</p>
</div>
</div>
</li>
</ul>
<div class="rating-content rating-dialog">
<div class="rating-buttons"><button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper"> </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
<button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper">  </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="question-item ng-star-inserted">
<h3 class="question-title-number">10.</h3>
<p>Bob has set up a new Docker server. The&nbsp;<code>overlay2</code>&nbsp;driver is the default for the server, but he wants to use&nbsp;<code>devicemapper</code>&nbsp;instead. Which of the following are ways to implement this change?</p>
<div id="cdk-accordion-child-15" class="mat-expansion-panel-content ng-trigger ng-trigger-bodyExpansion mat-expanded" role="region" aria-labelledby="mat-expansion-panel-header-15">
<div class="mat-expansion-panel-body">
<div>
<ul>
<li class="ng-star-inserted">
<div class="choice-item">
<p>A. Set&nbsp;<code>storage-driver</code>&nbsp;to&nbsp;<code>devicemapper</code>&nbsp;in&nbsp;<code>/etc/docker/daemon.json</code>.</p>
<span class="correction correct-true ng-star-inserted">done&nbsp;Correct</span></div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>B. Add the&nbsp;<code>--storage-driver</code>&nbsp;flag to the&nbsp;<code>dockerd</code>&nbsp;call in Docker's unit file.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>C. Reformat the storage disk.</p>
</div>
</li>
<li class="ng-star-inserted">
<div class="choice-item">
<p>D. Use a different Docker version.</p>
</div>
</li>
</ul>
<div class="rating-content rating-dialog">
<div class="rating-buttons"><button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper"> </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
<button class="btn outline mat-button"></button><button class="btn outline mat-button"><span class="mat-button-wrapper">  </span></button>
<div class="mat-button-ripple mat-ripple">&nbsp;</div>
<div class="mat-button-focus-overlay">&nbsp;</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="expectation ng-star-inserted">
<div>&nbsp;</div>
</div>

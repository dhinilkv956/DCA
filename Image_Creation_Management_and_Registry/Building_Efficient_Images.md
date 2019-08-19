<h2>Building Efficient Images</h2>
<div class="close-video-menu">&nbsp;</div>
<p>Dockerfiles allow us to build our own images containing any software we need. However, it is important to ensure that our Dockerfiles are built to produce small, efficient images that do not contain unnecessary data. In this lesson, we will briefly discuss some general tips for creating efficient images. We will also demonstrate how to use multi-stage builds to significantly decrease image size in certain situations.</p>
<h3 id="relevant-documentation">Relevant Documentation</h3>
<ul>
<li><a href="https://docs.docker.com/develop/develop-images/dockerfile_best-practices/">https://docs.docker.com/develop/develop-images/dockerfile_best-practices/</a></li>
<li><a href="https://docs.docker.com/develop/develop-images/multistage-build/">https://docs.docker.com/develop/develop-images/multistage-build/</a></li>
</ul>
<h3 id="lesson-reference">Lesson Reference</h3>
<p>Create some project directories:</p>
<pre><code>cd ~/
mkdir efficient
mkdir inefficient
cd inefficient
</code></pre>
<p>Create the source code file:</p>
<pre><code>vi helloworld.go
</code></pre>
<pre><code>package main
import "fmt"
func main() {
    fmt.Println("hello world")
}
</code></pre>
<p>Create the Dockerfile:</p>
<pre><code>vi Dockerfile
</code></pre>
<pre><code>FROM golang:1.12.4
WORKDIR /helloworld
COPY helloworld.go .
RUN GOOS=linux go build -a -installsuffix cgo -o helloworld .
CMD ["./helloworld"]
</code></pre>
<p>Build and test the&nbsp;<code>inefficient</code>&nbsp;image:</p>
<pre><code>docker build -t inefficient .
docker run inefficient
docker image ls
</code></pre>
<p>Switch to the&nbsp;<code>efficient</code>&nbsp;project directory and copy the files from the&nbsp;<code>inefficient</code>&nbsp;project:</p>
<pre><code>cd ~/efficient
cp ../inefficient/helloworld.go ./
cp ../inefficient/Dockerfile ./
</code></pre>
<p>Change the Dockerfile to use a multi-stage build:</p>
<pre><code>vi Dockerfile
</code></pre>
<pre><code>FROM golang:1.12.4 AS compiler
WORKDIR /helloworld
COPY helloworld.go .
RUN GOOS=linux go build -a -installsuffix cgo -o helloworld .

FROM alpine:3.9.3
WORKDIR /root
COPY --from=compiler /helloworld/helloworld .
CMD ["./helloworld"]
</code></pre>
<p>Build and test the&nbsp;<code>efficient</code>&nbsp;image:</p>
<pre><code>docker build -t efficient .
docker run efficient
docker image ls</code></pre>

# pipeline-jenk
this is demo for crating and building application
Jenkins Pipeline is a combination of jobs to deliver software continuously using Jenkins.

I assume you know what Jenkins is. If not then check out this Udemy course to master Jenkins.

A Jenkins pipeline consists of several states or stages, and they get executed in a sequence one after the other. JenkinsFile is a simple text file that is used to create a pipeline as code in Jenkins. It contains code in Groovy Domain Specific Language (DSL), which is simple to write and human-readable.

Either you can run JenkinsFile separately, or you can run the pipeline code from Jenkins Web UI also. There are two ways you can create a pipeline using Jenkins.

Declarative – a new way of creating Jenkins Pipeline. Here you write groovy code containing “pipeline” blocks, which is checked into an SCM (Source Code Management)
Scripted – way of writing groovy code where the code is defined inside “node” blocks.
Before we get into the demo, if you have not installed Jenkins, please install it first. Make sure you have Jenkins up and running on your system.


Let me explain the above blocks.

The pipeline block consists of all the instructions to build, test, and deliver software. It is the key component of a Jenkins Pipeline.
An agent is assigned to execute the pipeline on a node and allocate a workspace for the pipeline.
A stage is a block that has steps to build, test, and deploy the application. Stages are used to visualize the Jenkins Pipeline processes.
A step is a single task to be performed, for example, create a directory, run a docker image, delete a file, etc.
The Groovy code above, I am using for the JenkinsFile. Any available agent is getting assigned to the pipeline. Then I am defining the Build stage and performing a simple echo step. Then I defined the Test stage where the step asks whether you want to proceed or not. After that, I have created a Deploy stage, which has two more stages in it running in parallel. Deploy start stage has a step with echo command, and Deploying now has a step that pulls a docker image of Nginx on the node. Finally, there is a Prod stage with a simple echo step.

The above-explained pipeline has stages that have simple steps for you to understand how it works. Once you learn how to create a Pipeline, you can add more complexity and create complex pipelines also.

Once you have the code in the Pipeline tab, click on Apply and Save. Finally, click on Build Now to start building the Jenkins Pipeline you just created.




Step 1 — Installing Docker
The Docker installation package available in the official Ubuntu repository may not be the latest version. To ensure we get the latest version, we’ll install Docker from the official Docker repository. To do that, we’ll add a new package source, add the GPG key from Docker to ensure the downloads are valid, and then install the package.

First, update your existing list of packages:

sudo apt update
Next, install a few prerequisite packages which let apt use packages over HTTPS:

sudo apt install apt-transport-https ca-certificates curl software-properties-common
Then add the GPG key for the official Docker repository to your system:

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
Add the Docker repository to APT sources:

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
This will also update our package database with the Docker packages from the newly added repo.

Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:

apt-cache policy docker-ce
You’ll see output like this, although the version number for Docker may be different:

Output of apt-cache policy docker-ce
docker-ce:
  Installed: (none)
  Candidate: 5:19.03.9~3-0~ubuntu-focal
  Version table:
     5:19.03.9~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
Notice that docker-ce is not installed, but the candidate for installation is from the Docker repository for Ubuntu 20.04 (focal).

Finally, install Docker:

sudo apt install docker-ce
Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:

sudo systemctl status docker
The output should be similar to the following, showing that the service is active and running:

Output
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2020-05-19 17:00:41 UTC; 17s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 24321 (dockerd)
      Tasks: 8
     Memory: 46.4M
     CGroup: /system.slice/docker.service
             └─24321 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
Installing Docker now gives you not just the Docker service (daemon) but also the docker command line utility, or the Docker client. We’ll explore how to use the docker command later in this tutorial.

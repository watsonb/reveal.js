# Containers 101



## Agenda

* Around the Room
* Preface
* What are Containers?
* Quick History
* What Problems do Containers Address?
* Practical Examples
* Demo
* Summary
* Q&A



## Around the Room

* Introduce yourself
  * A bit of work history and current work assignment



## Preface

* This is an introductory lesson in Containers
  * Will not get “too deep”, but provide concepts to help understand them
* Will make heavy use of analogy to further concepts
  * Analogies aren’t perfect



## What are Containers?

* Containers are an attempt to answer the following question:
  * Wouldn’t it be nice if there was a way to package applications and all of their dependencies into a single “thing” that would execute the same way everywhere?
* A common analogy is a cargo shipping container
  * Standard size (API)
  * Can put “stuff” into it
  * Can go just about anywhere due to standard form factor (cargo ships, trucks, rail, etc.)
  * Delivers capabilities to where it is shipped
  * Can be stored and delivered later
* Can separate concerns
  * Governing bodies can come up with container (and runtime) specifications
  * People that create applications and know their dependencies (developers) can “fill” (build) container images
  * People that deliver and ensure capabilities are available (operations) can instantiate containers based on built images


## What are Containers?

* What’s old is new (again)
  * Born out of the old mainframe days
  * Shared physical resource with multiple competing interests (users)
  * Provide mechanisms for process isolation and resource management
  * Maximize use of (expensive) physical resources
* Not the first attempt
  * FreeBSD → jails (2000)
  * VMWare workstation/ESX (2000ish)*
  * Solaris → domains (LDOMS) (2007)
    * More(ish) like VMs
  * Linux namespaces and control groups (cgroups) (2009)**

> * VMs != containers, but somewhat analogous (more later)
> ** Namespaces and cgroups are what really kicked things off (eventually Windows kernel, too)


## What are Containers?

Sometimes understanding what something “is” is accomplished by comparing it to what it is “not”

![VM vs Container](img/containers101/netapp_vm_vs_container.jpeg)

Note: 
* Common
  * Some physical machine(s)
  * CPU, Memory, Disk, Network

* VMs (hardware virtualization):
  * An OS with hypervisor software (scheduler, drivers for PHYS, etc.)
  * Guest OS (big) with its own scheduler and other overhead (but “standard PHYS” drivers)
  * Then you collect Guest OS dependencies to support the app
  * Then you install/run the app

* Containers (OS virtualization):
  * OS with scheduler, drivers, and other overhead
  * Container runtime (software like Docker, Podman, LXC, etc.)
  * App and deps packaged as container images and “pulled”/run on OS

* Draw examples of fully using PHYS resources (glass filled with ping-pong balls vs marbles/sand, etc.)
* Multiple OS(es) with overhead vs single OS context switching


## What are Containers?

* In the end, a container is:
  * Just a process launched by a container runtime on an OS
  * Process isolation via namespaces
    * Process running in container has limited visibility to other processes on host OS
  * Resource usage metered via cgroups
* A container image is (analogies in worse-to-better order) like:
  * An RPM/Deb (if only it has “all” dependencies)
  * A software package via a package manager
  * An OS iso image
  * An OS “live CD” iso image
* Using the above analogy, you instantiate a container by:
  * Booting that live CD
  * Making a container runtime extract a tarball and run a process



## Quick History

* What brought forth this “container revolution”?
* In short, Docker
  * namespaces and cgroups were “hard to use” natively
  * No standard way to build, store, retrieve, and instantiate (run) images
  * Docker made it easier to use and provided the runtime/tools to a variety of OSes
    * All manner of Linux distros
    * Mac
    * And, yes, even Windows
  * Docker defined the initial image specification and the build, pull, push, and run commands
* Analogous to Git
  * Initially very difficult for people who are not Linus Torvalds to use
  * Then came some command-line heroes and GitHub
  * Now it is fairly trivial



## What Problems do Containers Address?

Appropriate use of Containers can help alleviate the following:

* Dependency hell
* Develop against something that resembles production, but on your laptop/workstation
* Source control the container image build process (Dockerfile, Containerfile)
* Publish version(s) of image to registries for others to use
  * Only physically use storage for version “deltas”
* Quickly “install” and use containers (`docker pull` && `docker run`)
* Quickly roll forward/backward (`docker pull image:<version>` && `docker run image:<version>`)
* Place running containers across hosts and scale
  * Container orchestration (Docker Swarm, Kubernetes, OpenShift)



## Practical Examples (Development Aid 1)

* Front end developer needs “full stack” available
* Do you give developer access to test/qa/prod environments?
  * Dev environment is really for integrated tests, not day-to-day activities
* If environment is “containerized”:
  * Developer can pull various aspects of the stack
    * App container
    * DB container
    * LB container
    * Etc
* Developer can use container runtime (e.g. Docker) to pull down and run various containers locally and have something that resembles test/qa/prod
  * Of course, it won’t necessarily be data-complete or resource-complete
  * But is a suitable stand-in


## Practical Examples (Development Aid 2)

* Testing IaC
  * How do you test IaC?
  * Ideally, you’d need to be able to “spin up” fresh infrastructure, configure it, verify it, then destroy it
  * Rinse and repeat
* Enter, containers and Ansible/Molecule
  * Molecule is a tool that allows an Ansible developer to quickly create, converge, verify, and destroy infrastructure in order to test Ansible roles
  * Containers are a 1st class citizen and are “stand-ins” for testing against “real” hosts

Note: I will demonstrate this later.


## Practical Examples (Consistency)

* Ansible Execution Environments (EEs)
  * Are container images that contain an Ansible installation, OS filesystem, config files, OS packages, Python dependencies, etc.
  * A tool called ansible-builder invokes Docker or Podman to build the container image for you after templating an appropriate Dockerfile or Containerfile respectively
* Why have Ansible containerized?
  * Ansible is a relatively simple tool to install (yum install ansible, pip install ansible, etc.)
  * Pretty easy to learn and use
  * Want to manage VMWare, AWS, Azure?
    * Need Python libs (pyvmomi, boto3, msrestazure)
  * Want to make ISO images for cloud-init, interact with AD?
    * Need genisoimage, krb-utils, krb5.conf, etc.
  * If you put all of the above (and even more) into a container image:
    * Same environment is now usable everywhere you want to be: Jenkins CI, AWX/Tower, personal Linux environments, Windows WSL, etc.
  * No more “it works on my machine”
  * Getting the install/config to be identical everywhere is difficult, containers make it easier



## Demos

* Search & Pull
  * `podman search hello-world`
  * Search on DockerHub as well
* List images
* Run image
  * Hello World
  * Busybox and Nginx
    * https://docs.podman.io/en/latest/Introduction.html
* Ansible/Molecule
  * “Wrap” Docker to foster IaC development
* Ansible EEs
  * Show environment consistency



## Summary

* Appropriate use of Containers can:
  * Reduce dependency hell
  * Aid in development process
  * Separate concerns
  * Maximize resource utilization
  * Facilitate more graceful roll forward/back and scaling
  * Help ensure consistency “everywhere”



## Q&A

Are there any questions?

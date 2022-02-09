# Kubernetes 101



## Agenda

* Preface
* What is Kubernetes?
* Quick History
* Kubernetes Architecture and Deployment
* Hands-on Lab



## Preface

* This is an introductory lesson in Kubernetes
  * Will not get “too deep”, but provide concepts to help understand them
* Will make heavy use of analogy to further concepts
  * Analogies aren’t perfect



## What is Kubernetes?

* Kubernetes (often abbreviated as `k8s`) is a container management platform (CMP)
* OK, so what is a CMP?
* You know what containers are now, but how do you:
  * Deploy them across a distributed infrastructure?
  * Detect failure and restart them?
  * Automatically scale up/down (instantiate more instances) in response to
    changes in demand?
  * Manage inter-container ports/protocols/traffic/routing?
* A CMP provides answers to these questions, and `k8s` is a specific CMP implementation.


## What is Kubernetes?

* Kelsey Hightower (the defacto spokesperson for `k8s`) has a good analogy
* How do you make a Postal Service?
  * You come up with some standard form factors (envelopes, boxes)
  * You have customers that want to ship things from A to B
  * You have a pricing tier based on weight and time to deliver
  * You tell customers, you can ship anything you want, but it has to fit in
    the envelope/box (i.e. container)
  * Customer has to provide a return and delivery address
  * That's it


## What is Kubernetes?

* That's it?
* Yes, you (the customer) enter into a "contract" with the post office when you
  show up with a "container", with an address, and pay postage
* The post office **promises** you that the "container" will be delivered to said
  destination at the agreed upon date.
* You, the customer, have no knowledge of how the Post Office internals work
  * Weather delays halt flights
  * Postal carriers get sick
  * Trucks break down
  * You don't care so long as the "container" is delivered
* This is the **promise** `k8s` is offering for container-based application
  delivery
  * Servers break
  * DNS, DHCP, BGP
  * Don't care, just want the app running



## Quick(ish) History

* What sparked `k8s` development and how did it grow into this thing we have
  today?
* In short, **Google** wanted to compete with **Amazon** in PaaS.
* It all started back in 2010 with the advent of Docker.
  * You remember Docker, right?
* With containers being all the rage for application packaging Google was looking
  for a better method to manage the container lifecycle.
* They already had this thing internally called `Borg` to manage physical
  infrastructure by abstracting it away via infrastructure-as-code
  * Could they come up with something similar for containers?


## Quick(ish) History

* Google allocated a small set of internal resources (engineers) to start working
  on `k8s`
* The team wanted to open-source it, as they wanted contributions from the
  community (to solve problems they hadn't thought of)
* Google leadership struggled with this decision (but finally caved)
* Kubernetes was announed at DockerCon (2011)
  * Kind of overshadowed Docker itself
    * They didn't really have a CMP yet (`libswarm` was it)
  * Other start-ups at DockerCon started announcing their own CMP(ish) things


## Quick(ish) History

* Google wasn't the first or biggest/well-known company to undertake a CMP
* Others include:
  * Docker Swarm
  * Mesosphere
  * RedHat (Openshift/OKD)
  * Pivotal Cloud Foundry
  * IBM
* But Google kind of wanted to work _with_ (these **competitors**) to make something
  that would change the game


## Quick(ish) History

* Google realized it needed to hand off this work to a foundation to free it
  from being a "Google" thing and to allow the other "bigs" to contribute
* The Cloud Native Computing Foundation (CNCF) was formed and is the chief
  steward of `k8s` now.
  * Think of the Linux Foundation, the Apache Foundation, etc.
  * Works towards common standards that all are allowed to use and then tailor
    to make their own offerings
* Now, a lot of those other start-ups and "bigs" are using CNCF-backed "vanilla"
  Kubernetes as the foundation/base of their own products.


## Quick(ish) History

* There is a great 2-part documentary on the birth and rise of `k8s` put together
  by Honeypot and accessible on YouTube
  * [Part 1](https://www.youtube.com/watch?v=BE77h7dmoQU)
  * [Part 2](https://www.youtube.com/watch?v=318elIq37PE)



## Kubernetes Architecture and Deployment

* Some C-Level states:
  * > "We need this application to be highly available, highly scaleable,
    > be easy to deploy, update, rollback.  I know, let's use Kubernetes!"
* Now you have a Kubernetes problem!
* Kubernetes is complicated
  * Lots of pieces
  * Installed/configured across a distributed infrastructure
  * Constantly evolving and releasing new versions
* [CNCF Landscape](https://landscape.cncf.io/)


## Kubernetes Architecture and Deployment

* My first dive into Kubernetes:
  * Kelsey Hightower's [Kubernetes The Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way)
* Prompted me to make:
  * [Kubernetes The Easy Way](https://github.com/watsonb/k8s-playbooks)
  * A bunch of Ansible playbooks that would:
    * Spin up infrastructure on GCP
    * Perform the steps outlined in Kelsey's Gist
  * It worked (at the time)!


## Kubernetes Architecture and Deployment

* Nowdays there are `k8s` _distributions_:
  * Analogous to Linux distros
    * At the heart of Linux is the kernel, and distros leverage that
    * But there is more to a usable distro than the kernel
      * Package management, desktop, services, etc.
* So just as you have several Linux distros to choose from:
  * Debian/Ubuntu (and the 100's of variants thereof)
  * Enterprise Linux (RHEL, CentOS!, Rocky, Alma, etc.)
  * Slackware
  * Arch
* You have several Kubernetes distros to choose from:
  * Vanilla (CNCF) -> Ansible Kubespray
  * RedHat OpenShift/OKD
  * Konvoy
  * Rancher



## Hands-on Lab

* Kubernetes is hard, right?
* What if it didn't have to be?
* The CNCF sponsors a project called `minikube`
  * `minikube` provides super easy access to explore and play around with
    Kubernetes on your own workstation
  * Don't believe me?  We're going to do it.
  * What's the point?
    * Well, it can be used as a teaching tool
    * For both devs and ops

> Super **NOT** a production Kubernetes distro!


## Hands-on Lab

* Nearly all instructions will be taken (nearly verbaitm) from [k8s.io](https://minikube.sigs.k8s.io/docs/start/)

```bash
# download and run the all-in-wonder script
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# start the cluster
minikube start

# check it out
minikube kubectl -- get po -A
```


## Hands-on Lab

```bash
# let's save ourselves some keystrokes (we're lazy)
vim ~/.bashrc

# put this on the last line
alias kubectl="minikube kubectl --"

# pop open a new shell

# install and pull up the web-based dashboard (will be boring at first)
minikube dashboard

# leave dashboard running in browser, pop open a new shell

# deploy the nginx-based echoserver app
kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4
kubectl expose deployment hello-minikube --type=NodePort --port=8080

# inspect services
kubectl get services hello-minikube
```

Go back and check your dashboard now.


## Hands-on Lab

```bash
# let's have a look at what we actually deployed
minikube service hello-minikube

# view deployments
kubectl get deployments

# view pods
kubectl get pods

# view cluster events
kubectl get events

# view kubectl configuration
kubectl config view
```


## Hands-on Lab

```bash
# alright, enough fun, let's cleanup
docker ps  # what's running before cleanup?
minikube delete --all
docker ps  # what's running after cleanup?
```
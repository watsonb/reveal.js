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

* I tend to believe people appreciate things more when they know more about the
  origin story, so...
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
* But Google kind of wanted to work _with_ these **competitors** to make something
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


## Kubernetes Architecture and Deployment

In otherwords, your experience deploying, maintaining, upgrading, and
operating a Kubernetes cluster will largely depend on the distribution you
are using and the tooling they provide to fulfill these objectives.

There is tons of flexibility regarding all of the internals, for example:

* container runtime (runc, crun, docker, etc.)
* internal software defined networking implentation
* and more

A distribution will typically have an opinion on what works best and guide you
down the road of getting the cluster up and running with these opinions in mind.

> Opinionated can seem bad (especially if you don't agree with it) but it
> certainly wrangles in the seemingly infinite variability at play here



## Hands-on Lab (Minikube)

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


## Hands-on Lab (Minikube)

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


## Hands-on Lab (Minikube)

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


## Hands-on Lab (Minikube)

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


## Hands-on Lab (Minikube)

```bash
# alright, enough fun, let's cleanup
docker ps  # what's running before cleanup?
minikube delete --all
docker ps  # what's running after cleanup?
```



## Hands-on Lab (AWX)

* Some of you use Ansible, right? Right!?!?
* RedHat provides products named Tower, Automation Platform, and others that
  enable you to expose your playbooks in various ways
  * Web GUI to run playbooks
  * REST API to launch playbooks
  * And more...
* Like other RedHat models, AWX is the free upstream open source version of
  their commercial (supported) offering named Tower.
* How does this relate to Kubernetes?
  * Well there are Ansible modules for managing `k8s` clusters, but...
  * Recent versions of Tower are deployed via the `awx-operator` into a `k8s`
    cluster

> You can still deploy AWX via Docker on Linux, but `k8s` is "the way" now.


## Hands-on Lab (AWX)

* Fire up `minikube` again

```bash
minikube start --cpus=4 --memory=6g --addons=ingress

# verify some stuff
$ minikube kubectl -- get nodes
NAME       STATUS   ROLES                  AGE    VERSION
minikube   Ready    control-plane,master   113s   v1.22.2

$ minikube kubectl -- get pods -A
NAMESPACE       NAME                                        READY   STATUS      RESTARTS   AGE
ingress-nginx   ingress-nginx-admission-create--1-kk67h     0/1     Completed   0          2m1s
ingress-nginx   ingress-nginx-admission-patch--1-7mp2r      0/1     Completed   1          2m1s
ingress-nginx   ingress-nginx-controller-69bdbc4d57-bmwg8   1/1     Running     0          2m
kube-system     coredns-78fcd69978-q7nmx                    1/1     Running     0          2m
kube-system     etcd-minikube                               1/1     Running     0          2m12s
kube-system     kube-apiserver-minikube                     1/1     Running     0          2m16s
kube-system     kube-controller-manager-minikube            1/1     Running     0          2m12s
kube-system     kube-proxy-5mmnw                            1/1     Running     0          2m1s
kube-system     kube-scheduler-minikube                     1/1     Running     0          2m15s
kube-system     storage-provisioner
```


## Hands-on Lab (AWX)

We need to clone the Git project for `awx-operator`

```bash
mkdir -p ~/workspace/github/ansible
cd ~/workspace/github/ansible
git clone https://github.com/ansible/awx-operator.git
cd awx-operator
git checkout 0.16.1  # most recent release
```


## Hands-on Lab (AWX)

Kubernetes deployments are managed by `namespaces`, so we're going to set an
enviornment variable with our namespace that we can then refer to throughout.

```bash
export NAMESPACE=my-namespace
```

> I had to install the `kubectl` tool for the following `make` command to work

```bash
cd ~/Downloads
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
cd ~/workspace/github/ansible
```

Now we make the deployment via the included Makefile:

```bash
make deploy
```

After a little bit, you should see the operator running in minikube:

```bash
$ kubectl get pods -n $NAMESPACE
NAME                                               READY   STATUS    RESTARTS   AGE
awx-operator-controller-manager-66ccd8f997-rhd4z   2/2     Running   0          11s
```


## Hands-on Lab (AWX)

Let's set the default namespace for `kubectl` so we don't have to keep typing
it all the time:

```bash
$ kubectl config set-context --current --namespace=$NAMESPACE

Now make a text file:
vim demo.yml
```

And paste in the following:

```yaml
---
apiVersion: awx.ansible.com/v1beta1
kind: AWX
metadata:
  name: awx-demo
spec:
  service_type: nodeport
```


## Hands-on Lab (AWX)

Now we'll use `kubectl` to create an AWX instance in the `minikube` cluster

```bash
$ kubectl apply -f awx-demo.yml
awx.awx.ansible.com/awx-demo created
```

It may take a few minutes to fully deploy.  You can check operator logs to see
the progress:

```bash
$ kubectl logs -f deployments/awx-operator-controller-manager -c awx-manager
# keen eyes will notice this is actually an Ansible playbook running here
```

You should also see new resources and services:

```bash
$ kubectl get pods -l "app.kubernetes.io/managed-by=awx-operator"
NAME                        READY   STATUS    RESTARTS   AGE
awx-demo-77d96f88d5-pnhr8   4/4     Running   0          3m24s
awx-demo-postgres-0         1/1     Running   0          3m34s

$ kubectl get svc -l "app.kubernetes.io/managed-by=awx-operator"
NAME                TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
awx-demo-postgres   ClusterIP   None           <none>        5432/TCP       4m4s
awx-demo-service    NodePort    10.109.40.38   <none>        80:31006/TCP   3m56s
```


## Hands-on Lab (AWX)

* Let's kick the tires.
* First print out the admin password secret

```bash
$ kubectl get secret awx-demo-admin-password -o jsonpath="{.data.password}" | base64 --decode
yDL2Cx5Za94g9MvBP6B73nzVLlmfgPjR  # <--- your value will be different here
```

That secret is the password we'll use to login with the account: `admin`

Let's launch the service in a browser:

```bash
$ minikube service awx-demo-service --url -n $NAMESPACE
http://<ip address>:<port>
```

Open that address in browser and login with the admin account and the password
secret you retrieved.

When you're done poking around, cleanup:

```bash
minikube delete --all
```

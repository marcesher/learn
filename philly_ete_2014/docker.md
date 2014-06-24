April 22, 2014

Eric Windisch

Docker tries to solve the problem of "shipping code"

matrix hell: databases, apps, hosting environments

You're developing in your custom environment (laptop), but that's different from where it'll be hosted

So you make dev environments, but they look kinda like a dev laptop and kinda like prod, but not identical to either

Docker builds upon linux containers (LXC)... it's a bundling of services/processes. Think of it like sharing a WAR file.
That's what docker does for containers... creates standardized bundles

Bundle service config (think nginx) in the container

goal: deploy reliably and consistently

host and guest don't matter... you can run an ubuntu container inside a rhel host, and vice versa

they're just like the real thing. they're like VMs, but not quite because the process is running on the host directly

- build in seconds, run instantly

- can be higher-performing than native

- he says this is a good thing from a security perspective b/c you can control what the process is allowed to access

- the docker image can contain all the network resources (think: python packages, ruby gems, etc), so that you don't need to download these every times. Can set it up to also check for updates


How Docker Works

- it's a lightweight VM, but:

- own process space
- own network interface
- can run stuff as root
- can have its own /sbin/init, but that's not how most people use it


Another way to think about it:

- it's chroot on steroids
- container = isolated processes
- share kernel with host
- no device emulation

- sure, kernel vulnerabilities to have breakout potential, but you'd be keeping your kernel up to date anyway, so... no diff

- the processes can see a different subset of processes than normal, because the world is isolated

- this is all about namespaces

- his preso lists the different namespaces (I'm assuming it's also in the docs)


**User namespace**


- processes can run as root in the container, but it's not actually running as root on the host. It "thinks" it's root for its own purposes

- he describes this as like selinux

- it's locked down pretty tight by default, but you can pass --privilege (?) to give the privileges you need


## Using docker

- you have a docker file

"FROM ubuntu

RUN apt-get...
RUN apt-get...

"

each line in the docker file creates a new image (b/c of copy-on-write storage)

so if a line fails, you actually have the last successful image, and you can log into it and see what happened

If the build is successful, all intermediary images are deleted

## Migrating to docker

- try to have one service for container
- don't use containers as VMs, even if you can
- you don't need to move everything to docker
  - eg, keep syslog on the host if you must rather than creating a syslog container

- docker provides a security story by separating things into contexts

## How to use

- satisfied with your local build?
 - push it to registry (private or public)
 - run it in CI
 - run it in prod
 - if something goes wrong, roll back to previous image


## Heat

Heat is open source, like "cloud formation". openstack thingie

it's an orchestration service. you describe resources, etc

inside the heat config, describe which docker containers you need


## Demo

shows installing docker on ec2, using user-data (cloud init)

- he shows a short example with python, pulling things via pip. says in this way it's kind of like a way to ship python projects like a war file instead of pip installing requirements on the target server

## Downsides

 - he doesn't see many
 - compared with a VM, it's possible that a kernel exploit could lead to an easier breakout or more infection across containers, BUT b/c the container isn't a full VM, it has much less surface area and thus shouldn't be able to do as much as a full VM anyway


## How do you handle security updates (apt-get update && apt-get upgrade, etc)

 - you can do a new build of the container and tell it to update
 - OR you create an image, commit it, have that image based on the previous, and this new image is nothing but an apt-get update && apt-get upgrade


# Vagrant environment to test sameersbn/docker-gitlab Docker image

Vagrant environment to test [sameersbn/docker-gitlab](https://github.com/sameersbn/docker-gitlab) Docker image.

This installation mix the dockerized gitlab-ce ssh port with ssh on server host.

This configuration is based on [Exposing ssh port in dockerized gitlab-ce](https://blog.xiaket.org/2017/exposing.ssh.port.in.dockerized.gitlab-ce.html) post.

This repository is a [#1517](https://github.com/sameersbn/docker-gitlab/issues/1517) example, see [`expose-gitlab-ssh-port.sh`](expose-gitlab-ssh-port.sh) configuration script.

[GitLab Container Registry](https://github.com/sameersbn/docker-gitlab/blob/master/docs/container_registry.md) is enabled.

## Prerequisites

* Virtualbox
* Vagrant (tested with `2.1.1`)
* pwgen
* [vagrant-hostmanager](https://github.com/devopsgroup-io/vagrant-hostmanager) plugin

On OSX, execute this command with [brew](https://brew.sh/index_fr.html) to install this prerequisite:

```
$ brew cask install vagrant virtualbox
$ brew install pwgen
$ vagrant plugin install vagrant-hostmanager --plugin-version 1.8.9
```


## Start

```
$ ./container-registry.sh
$ cd nginx-proxy && ./generate-certificates.sh
$ vagrant up
```

Next instruction to test `git clone`:

1. Browse to http://gitlab.example.com and define your root user password.
2. Upload your ssh public key in http://gitlab.example.com/profile/keys
3. Create new project named `test1` http://gitlab.example.com/projects/new
4. Add `README.md` file to http://gitlab.example.com/root/test1 project
5. Clone the project:

```
$ git clone git@gitlab.example.com:root/test1.git
Cloning into 'test1'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
Receiving objects: 100% (3/3), 217 bytes | 217.00 KiB/s, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
```

Success 👍

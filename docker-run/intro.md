# The `docker run` command

Learn how to run a docker image in a container.

## Now docker hub has a pull rate limit

Recently I see this message quite often when I run a katacoda course:

`toomanyrequests: You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limit`

You can work around this by creating you own account on docker hub and authenticating inside the terminal session.

```text
$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: c6g4
Password: 
Login Succeeded
```

## Other katacoda resources

These are created by other authors. Summaries are my own.

* [What is a container image](https://www.katacoda.com/courses/container-runtimes/what-is-a-container-image) 
  * Anatomy of a docker image – technically this is just a `tar` archive.
    * A docker image consists of several layers. 
    * Each layer contains the modifications of the file system during one step when the docker image was created.
    * These layers are all stacked on each other at run time. Newer changes override older ones.
    * A few other files carry some fairly straightforward meta information.
  * It's possible to analyze and modify or even create a docker image from scratch by working on the `tar` archive directly.
  * Important `docker` subcommmands: `images`, `pull`, `save`, `import`
  * Take a deep dive: https://opencontainers.org/about/overview/
* [What is a container](https://www.katacoda.com/courses/container-runtimes/what-is-a-container)
  * A docker container is a process running on Linux.
  * Get a basic idea what a "process" is.
  * Docker uses [Linux namespaces](https://www.startpage.com/do/dsearch?query=linux+namespace) to limit what a container can see of the entire system where it is running.

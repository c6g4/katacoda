# Docker run

The `docker run` command is perhaps the most important. You need it run a docker image in a docker container.

A docker image encapsulates an entire environment.
It preserves a certain state of your work.
When you continue working with the image, you will add another layer of modifications to it.
When you run an image, docker will create a container for this run.
A container is an image where the latest layer is modifiable.

Later we will see how to create docker images. This is done by adding one layer after another.
For now, it should suffice to know that an image is like a container, but also the latest layer is immutable.


## Guess how to start …

`docker run`{{execute}}

`docker run --help`{{execute}}

Huh, that's a lot of options!

This is because docker run is the working horse that actually _does_ everything,
once the preparations have been set up.

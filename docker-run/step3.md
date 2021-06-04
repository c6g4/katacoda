# Cleaning up

By default docker does not delete a container when it is stopped.

So you can start it again later, the logs aren't lost, etc.

Run this a few times:

`docker start hello`{{execute interrupt}}

Now see how the logs append each time:

`docker logs hello`{{execute interrupt}}

## `docker ps`

However the default retention policy of docker also means that over time a lot of container will pile up somewhere.

You can see the running container like this:

`docker ps`{{execute interrupt}}

In order to see all containers, running or not, use:

`docker ps -a`{{execute interrupt}}

You can limit to only the latest 10 like this:

`docker ps -a -n 10`{{execute interrupt}}

## Deleting containers and images

We can ask docker to delete the `hello` container by its name:

`docker rm hello`{{execute interrupt}}

After this, it's gone. Caution: there is no _undo_.

`docker logs hello`{{execute interrupt}}

Instead of using the name, we can also specify the container by its id.

`docker rm a730fb7995c3`{{execute interrupt}}

(This container id won't exist on your machine, replace it with one from the `docker ps` output.)

If want to take a more radical approach, you can just delete all non-running containers like this:

`docker container prune``{{execute interrupt}}


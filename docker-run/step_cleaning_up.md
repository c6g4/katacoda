# Cleaning up

By default docker does not delete a container when it is stopped.

`docker run -d --name hello busybox echo 'Hello, world!'`{{execute interrupt}}

So you can start it again later, the logs aren't lost, etc.

Now run this a few times:

`docker start hello`{{execute interrupt}}

You can see how the logs append each time:

`docker logs hello`{{execute interrupt}}

## `docker ps`

The default retention policy of docker implies that over time a lot of container can pile up somewhere.

You can see the running containers like this:

`docker ps`{{execute interrupt}}

In order to see all containers, running or not, use:

`docker ps -a`{{execute interrupt}}

You can limit to only the latest 10 like this:

`docker ps -a -n 10`{{execute interrupt}}

## Deleting containers and images

We can ask docker to delete the `hello` container by its name:

`docker rm hello`{{execute interrupt}}

After this, it's gone. Caution: _there is no undo_.

`docker logs hello`{{execute interrupt}}

Instead of using the name, we can also specify the container by its id.

`docker rm a730fb7995c3`{{execute interrupt}}

(This container id won't exist on your machine, replace it with one from the `docker ps` output.)

If want to take a more radical approach, you can just delete all non-running containers like this:

`docker container prune`{{execute interrupt}}

But in general, the recommended practice is to not let containers pile up without giving any attention.
If you know you won't need the stopped container later, you can request `docker` to delete it immediately after the container stops, using the `--rm` option:

`docker rm hello`{{execute interrupt}}

`docker run -d --rm --name hello busybox echo 'Hello, world!'`{{execute interrupt}}

This time the container is not retained.

`docker rm hello`{{execute interrupt}}

Another advantage is that the name `hello` is also freed up.
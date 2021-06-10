# Using `docker attach` (and how to detach)

You can detach from a running container and `docker attach` to it later.

Let us walk through an example.

`docker run -it --name bb busybox`{{execute}}

Inside the busybox shell, we run a countdown:

`for n in $(seq 100 -1 1); do echo $n; sleep 1; done; echo boom!`{{execute}}

Intermittently, we can detach from the running container by typing Ctrl-p Ctrl-q (try it out!)

The count down is still progressing ... as we can see by taking a look at the last 10 lines of the logs:

`docker logs bb -n 10`{{execute}}

And we can attach to the `bb` container again:

`docker attach bb`{{execute}}

Attaching and detaching is different from starting and stopping.

For example, while attached to the `bb` container, type Ctrl-c to interrupt the countdown.

Then type Ctrl-d to quit the shell as well.

After this, also the container will stop, because the entrypoint has exited. We see this from the output of:

`docker ps -a`{{execute}}

The `bb` container does still exist (because we did not supply the `--rm` flag), but right now, it is in "exited" state.
Therefore,

`docker attach bb`{{execute}}

does not work right away. First we need to `start` the container again:

`docker start bb`

We are not attached to it yet, but we can see that is already running:

`docker ps -a`{{execute}}

Therefore, now it should work:

`docker attach bb`{{execute}}

The countdown is not running, but for example, the commmand history is still there - so changes in the file system are
persistent, whereas running processes are not. (Remember that a `docker run` is just a Linux process.)

`history`{{execute}}

Now start the countdown again and detach from it using the keystrokes.

We can stop a container we are not attached to, like this:

`docker stop bb`

This takes a little while, because docker will first attempt to stop the shell gracefully, but when a certain grace
period is over (default is 10 seconds), docker will kill it forcefully.

Or, as the [`docker stop` documentation](https://docs.docker.com/engine/reference/commandline/stop/) puts it:
"The main process inside the container will receive `SIGTERM`, and after a grace period, `SIGKILL`."

`docker stop --help`{{execute}}

Our little `for` loop did not listen to `SIGTERM`, but other applications running inside a container might use the grace
period to end themselves in a controlled way.

You can attach to the same contained process multiple times simultaneously, from different sessions on the Docker host.

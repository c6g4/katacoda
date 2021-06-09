# Interactive versus detached mode

This is a shell variant of the famous "Hello, world!" program:

`echo 'Hello, world!'`{{execute}}

The `busybox` docker image provides simple versions of many standard linux tools. So here is a variant using docker:

`docker run busybox echo 'Hello, world!'`{{execute interrupt}}

Note: this will `docker pull` the busybox from docker hub when you run it the first time. (...)

Remember that you can use `docker run`{{execute}} to get an idea what each part of the command means.

* busybox is the name of the docker image
* `echo 'Hello, world!'` is what is executed within the docker container

When the command has completed, the docker container stops as well.

## Interactive mode: `-it`

This is the usual combination when you want to interact through the terminal with a program running inside a docker
container.

```shell
  -i, --interactive                    Keep STDIN open even if not attached
  -t, --tty                            Allocate a pseudo-TTY
```

**Example**

Let us interact with a running `busybox` container:

`docker run -it busybox`{{execute interrupt}}

By default, the busybox image opens a `sh` shell:

`echo $0`{{execute}}

As usually, the zeroth position of the command line contains the name of the command that is run.

Let's see which files are there:

`ls`{{execute}}

This may no be not what you had expected. These files shown are not from the directory where you invoked the docker run
command. We are somewhere else:

`pwd`{{execute}}

So the working directory is `/`.

But who are we anyway?

`id`{{execute}}

By entering the docker container with the docker run command, we have adopted the identity of another user account. It
is not uncommon that you become `root` inside a docker container. This is another reason why `docker` requires
administrator permissions to run. (E.g. `sudo docker ...`)

The home directory is `/root`:

`cd`{{execute}}

`pwd`{{execute}}

Still we are just moving around inside the docker container.

You can quit the shell by typing `Ctrl-D` as usually. The docker container will then stop as well.

Docker is great for providing an encapsulated environment, and there is a smaller risk to do harm to damage to the
outside just by accident.

However docker does not provide security against hackers. In fact, it may open a lot of backdoors to the system where it
is running.

## Detached mode: `-d`

Use detached mode to run a container in the background. You can still interact with it by other means.
```shell
  -d, --detach                         Run container in background and print container ID
```
Let us try "Hello, world!" in detached mode:

`docker run -d busybox echo 'Hello, world!'`{{execute interrupt}}

We just get a container id in return, at least as seen from the command line.

When a container runs in detached mode, you need other means to interact with it.

## How to `--name` your container

There may be a lot of containers on a host when docker is used. Docker assigns a name automatically, but you can request a name using `--name`.

`docker run -d --name hello busybox echo 'Hello, world!'`{{execute interrupt}}

## `docker logs`

Now we can refer to the detached docker container by name and see its console output using the `docker logs` command

`docker logs hello`{{execute interrupt}}

There it is.
# Mounting directories

How can `docker` modify files outside the container?

Remember that when started this way, we did not see any directories from the host.

`docker run -it --rm busybox`{{execute interrupt}}

# `-v host_dir:cont_dir`

Our current working directory on the host is:

`echo $(pwd)`{{execute interrupt}}

(At this point, you may wish to create another directory on the host and `cd` to it.)

We can mount the working directory into the container using a _bind mount_.

`docker run -it --rm -v $(pwd):/hostpwd busybox`{{execute interrupt}}

`cd /`{{execute interrupt}}

`ls`{{execute interrupt}}

`ls hostpwd`{{execute interrupt}}

We can even modify the files on the host which are mounted in `/hostpwd` from the docker container.


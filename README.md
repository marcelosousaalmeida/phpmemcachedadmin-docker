Automated build of phpMemcachedAdmin with Docker
===========

### Use the pre built image
The pre built image can be downloaded using docker directly. After that you do not need to use this command again, you will have the image on your machine.

	$ sudo docker pull jacksoncage/phpmemcachedadmin


### Build the docker image by yourself
If you prefer you can easily build the docker image by yourself. After this the image is ready for use on your machine and can be used for multiple starts.

	$ cd phpmemcachedadmin-docker
	$ sudo docker build -t jacksoncage/phpmemcachedadmin .


### Start the container
The container has all pre requisites set up to run phpMemcachedAdmin application.

	$ sudo docker run -i -d -p 80 -v <local-path>:/phpmemcachedadmin jacksoncage/phpmemcachedadmin


#### Start the container and keep control
The command above starts the container in deamon mode (-d) and runs in the background. If you want to start it by yourself just to see what happens use this command:

	$ sudo docker run -i -t -p 80 -v <local-path>:/phpmemcachedadmin jacksoncage/phpmemcachedadmin bash

Notice the two changes made here, first we replaced the deamon switch (-d) with the tty switch (-t) which pipes the std in and std out to your terminal.

You now end up as a root user in the docker container and can do simple things like ls, cd and more. More complex things can be achieved after a `apt-get install` of one or more software(s) of choice.

### Get the container ip and port
The first command inspects your created container and get the IPv4 address. Second command docker exported port for 80.

    $ sudo docker inspect <container_id> | grep IPAddress | cut -d '"' -f 4
    $ sudo docker port <container_id> 80 | cut -d ":" -f2

Now go to `<your container's ip>:<container's port>` in your browser


### Stop the container
Stopping a running container is possible via the docker api. If only one instance of this container is running this command will stop it:

	$ sudo docker stop `sudo docker ps |grep jacksoncage/phpmemcachedadmin |cut -d\  -f1`

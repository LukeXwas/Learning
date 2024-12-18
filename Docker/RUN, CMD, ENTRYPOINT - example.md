Setup

mkdir -p /tmp/rekrutacja && cd /tmp/rekrutacja
clear
vim test.sh

#!/bin/bash

echo "$(date) $@" >> log.txt
cat log.txt

chmod +x test.sh 
./test.sh 1
history

Utworzmy sobie prostego Dockerfile

vim Dockerfile

FROM ubuntu
ADD test.sh .

**The _run_ Command
 
The _run_ instruction executes when we build the image. That means the command passed to _run_ executes on top of the current image in a new layer. Then the result is committed to the image.

Firstly, we’ll add a _run_ instruction to our Dockerfile:

FROM ubuntu:latest
ADD test.sh /
RUN ["/test.sh", "test 1"]

Secondly, let’s build our image with:

docker build -t myimage .

Now we expect to have a Docker image containing a _log.txt_ file with one _image created_ line inside. Let’s check this by running a container based on the image:

docker run myimage cat log.txt

When listing the contents of the file, we’ll see an output like this:

Fri Sep 18 20:31:12 UTC 2020 image created

If we run the container several times, we’ll see that the date in our log file doesn’t change. This makes sense because the **_run_ step executes at image build time**, not at the container runtime.

Polecenie run nie przyjmuje argumentow od uzytkownika, oraz nie moze zostac nadpisane poprzez docker run

**The _cmd_ Command

With the **_cmd_ instruction, we can specify a default command that executes when the container is starting.** Let’s add a _cmd_ entry to our Dockerfile and see how it works:

...
RUN  ["/test.sh", "test 1"]
CMD  ["/test.sh", "test 2"]

$ docker run myimage
Fri Sep 18 18:27:49 UTC 2020 image created
Fri Sep 18 18:34:06 UTC 2020 container started

If we run this multiple times, we’ll see that the _image created_ entry stays the same. But the _container started_ entry updates with every run. This shows how _cmd_ indeed executes every time the container starts.

**Notice we’ve used a slightly different _docker run_ command to start our container this time. Let’s see what happens if we run the same command as before:

$ docker run myimage cat log.txt
Fri Sep 18 18:27:49 UTC 2020 image created

**This time the _cmd_ specified in the Dockerfile is ignored. That’s because we have specified arguments to the _docker run_ command.

Let’s move on now and see what happens if we have more than one _cmd_ entry in the Dockerfile. Let’s add a new entry that will display another message:

...
RUN  ["/test.sh", "test 1"]
CMD  ["/test.sh", "test 2"]
CMD  ["/test.sh", "test 3"

After building the image and running the container again, we’ll find the following output:

$ docker run myimage
Fri Sep 18 18:49:44 UTC 2020 image created
Fri Sep 18 18:49:58 UTC 2020 container running

As we can see, the _container started_ entry is not present, only the _container running_ is. That’s because **only the last cmd is invoked if more than one is specified.**

**The _entrypoint_ Command

As we saw above, _cmd_ is ignored if passing any arguments when starting the container. What if we want more flexibility? Let’s say we want to customize the appended text and pass it as an argument to the _docker run_ command. 

For this purpose, let’s use _entrypoint._ We’ll specify the default command to run when the container starts. Moreover, we’re now able to provide extra arguments.

Let’s replace the _cmd_ entry in our Dockerfile with _entrypoint:_

...
RUN  ["/test.sh", "test 1"]
ENTRYPOINT ["/test.sh"]

Now let’s run the container by providing a custom text entry:

$ docker run myimage container running now
Fri Sep 18 20:57:20 UTC 2020 image created
Fri Sep 18 20:59:51 UTC 2020 container running now

We can see how **_entrypoint_ behaves similarly to** _**cmd**._ **And in addition, it allows us to customize the command executed at startup.**

Like with _cmd_, in case of multiple _entrypoint_ entries, only the last one is considered.

**Interactions Between _cmd_ and _entrypoint_

We have used both _cmd_ and _entrypoint_ to define the command executed when running the container. Let’s now move on and see how to use _cmd_ and _entrypoint_ in combination.

One such use-case is to define default arguments for _entrypoint._ Let’s add a _cmd_ entry after _entrypoint_ in our **Dockerfile**

...
RUN  ["/test.sh", "test 1"]
ENTRYPOINT ["/test.sh"]
CMD ["test 2"]

Now, let’s run our container without providing any arguments, and with the defaults specified in _cmd_:

$ docker run myimage
Fri Sep 18 21:26:12 UTC 2020 image created
Fri Sep 18 21:26:18 UTC 2020 container started

We can also override them if we choose so:

$ docker run myimage custom event
Fri Sep 18 21:26:12 UTC 2020 image created
Fri Sep 18 21:27:25 UTC 2020 custom event

**Something to note is the different behavior of _entrypoint_ when used in its shell form. Let’s update the _entrypoint_ in our Dockerfile:

...
RUN  ["/test.sh", "test 1"]
ENTRYPOINT /test.sh
CMD ["test 2"]

**In this situation, when running the container, we’ll see how Docker ignores any arguments passed to either _docker run_ or _cmd_.
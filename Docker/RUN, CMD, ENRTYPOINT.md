Shell and exec form

The RUN, CMD, and ENTRYPOINT instructions all have two possible forms:

**INSTRUCTION \["executable","param1","param2"] (exec form) -> RUN \["/log-event.sh", "image created"]
INSTRUCTION command param1 param2 (shell form) -> RUN apt-get update

The exec form makes it possible to avoid shell string munging, and to invoke commands using a specific command shell, or any other executable. It uses a JSON array syntax, where each element in the array is a command, flag, or argument.

The shell form is more relaxed, and emphasizes ease of use, flexibility, and readability. The shell form automatically uses a command shell, whereas the exec form does not.

**RUN

The **RUN** instruction will execute any commands to create a new layer on top of the current image. The added layer is used in the next step in the Dockerfile.

**The _run_ instruction executes when we build the image. That means the command passed to _run_ executes on top of the current image in a new layer. Then the result is committed to the image.

If we run the container several times, we’ll see that the date in our log file doesn’t change. **This makes sense because the run step executes at image build time, not at the container runtime.

Let’s now build our image again. We notice the creation time in our log didn’t change. This happens because Docker caches the result for the run instruction if the Dockerfile didn’t change. If we want to invalidate the cache, we need to pass the –no-cache option to the build command.

**CMD

The **CMD** instruction sets the command to be executed when running a container from an image.

You can specify CMD instructions using shell or exec forms:

    CMD ["executable","param1","param2"] (exec form)
    CMD ["param1","param2"] (exec form, as default parameters to ENTRYPOINT)
    CMD command param1 param2 (shell form)

There can only be one CMD instruction in a Dockerfile. If you list more than one CMD, only the last one takes effect.

**The purpose of a CMD is to provide defaults for an executing container.** These defaults can include an executable, or they can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.

 **If the user specifies arguments to docker run then they will override the default specified in CMD. If CMD is used to provide default arguments for the ENTRYPOINT instruction, both the CMD and ENTRYPOINT instructions should be specified in the exec form. 

Don't confuse RUN with CMD. RUN actually runs a command and commits the result; CMD doesn't execute anything at build time, but specifies the intended command for the image.

CMD is execute every time the container starts. This time the **_cmd_ specified in the Dockerfile is ignored. That’s because we have specified arguments to the _docker run_ command.

**ENTRYPOINT

An **ENTRYPOINT** allows you to configure a container that will run as an executable. 

ENTRYPOINT has two possible forms:

The exec form, which is the preferred form:

	ENTRYPOINT ["executable", "param1", "param2"]

The shell form:

	ENTRYPOINT command param1 param2

Command line arguments to **docker run \<image>** will be appended after all elements in an exec form **ENTRYPOINT**, and will override all elements specified using **CMD.

We can see how **_entrypoint_ behaves similarly to** _**cmd**._ **And in addition, it allows us to customize the command executed at startup.**

Like with _cmd_, in case of multiple _entrypoint_ entries, only the last one is considered.

If you would like your container to run the same executable every time, then you should consider using **ENTRYPOINT** in combination with **CMD**. See **ENTRYPOINT**. If the user specifies arguments to docker run then they will override the default specified in **CMD**, but still use the default **ENTRYPOINT**.

**ENTRYPOINT AND CMD

One such use-case **CMD is used to define default arguments for entrypoint**. 

**When we use docker run myimage with specific\<command> CMD will be override

If **CMD** is used to provide default arguments for the **ENTRYPOINT** instruction, both the **CMD** and **ENTRYPOINT** instructions should be specified in the [exec form](https://docs.docker.com/reference/dockerfile/#exec-form).

docker run myimage custom event
Fri Sep 18 21:26:12 UTC 2020 image created
Fri Sep 18 21:27:25 UTC 2020 custom event 

When we use shell form in ENTRYPOINT field, when we running the container, we’ll see how Docker ignores any arguments passed to either _docker run_ or _cmd_.

...
RUN ["/log-event.sh", "image created"]
ENTRYPOINT /log-event.sh
CMD ["container started"]

Fri Sep 18 21:26:12 UTC 2020 image created


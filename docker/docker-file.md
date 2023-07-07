### Basics of writing docker file.

#### What is difference between `COPY` and `ADD`
- `COPY` and `ADD` can be used for copy files from the host path to the docker. 
- `ADD` has a special ability where it not only copies files from the local path but also can add files from remote url and also extract them

#### When should we use `RUN` and `CMD`?
- `RUN` is used to run a command while the docker image is `building`, this is the key difference. RUN is while building but `not image running`. 
- ``` bash
    RUN cat ./filename # this will show the contents of filename in the docker image during the build.
   ```
- while `CMD` is used to run a starting command or script when the image is run.
- ``` bash
    CMD bash ./entry_script.sh 
  ```
- The above shown is  CMD shell. CMD can also used as exec mode. exec mode CMD donot invoke shell [ even though it does not invoke shell the image of docker should have a supporting OS underlying]
    ``` bash
     CMD ["/app", "--config", "config.yml"]
    ```

#### When to use CMD and ENTRYPOINT? 
- commands in `CMD`  which are mentioned in docker can be `overwritten` when running docker image.
- where as command using `ENTRYPOINT` cannot be overwritten when we run docker image.
- so `CMD` can be used to provide `starting arguments` for the docker run
- where as `ENTRYPOINT` we can give a `fixed script` we want to run for docker
- example
  ``` bash
   FROM ubuntu:latest
   ENTRYPOINT ["echo", "Hello,"]
   CMD ["Docker!"]
  ```
  the above example will print `Hello, Docker!` but running below will print `Hello, Goodbye`
  ```
  docker run <image> Goodbye
  ```


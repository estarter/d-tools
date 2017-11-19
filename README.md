# d-tools
The aim of this project is to tackle a problem of "too long commands" in docker.
It is a set of useful commands to deal with docker / docker-compose projects in a laconic way.

## How to use

Check out usage example based on [d-tools-example](https://github.com/estarter/d-tools-example) project ([screenplay](https://github.com/estarter/d-tools-example/blob/master/screenplay.txt)).

<a href="https://asciinema.org/a/148184?autoplay=1"><img src="https://asciinema.org/a/148184.png" /></a>

## Features

* Control sophisticated docker-compose project in a simple way
* Call it from any location
* Memorise your active docker-compose files and docker-compose project name
* Allows custom scripts before build process (TODO / WHY?)


Control commands (use `-h` option in cli):

* `dset` - specify project name and docker-compose files. `.d-tool.config.json` in local or home dir will be created.
* `dbuild` - build one, few or all images (wrapper for [docker-compose build](https://docs.docker.com/compose/reference/build/))
* `dup` - starts up the system (wrapper for [docker-compose up](https://docs.docker.com/compose/reference/up/))
* `dps` - shows running containers (wrapper for [docker ps](https://docs.docker.com/engine/reference/commandline/ps/))
* `ddown` - removes and clean up the system (wrapper for [docker-compose down](https://docs.docker.com/compose/reference/down/))
* `dcleanup` - remove all dangling images and volumes. It may save a lot of your HD.

Assistant commands:

* `dbash container` - get a bash session inside the container
* `dlog container` - prints out container's log using custom `/usr/bin/dlog` command. When you have a big zoo of
technologies and containers, with different path conventions, it's useful to have a same command that shows log files
([example](https://github.com/estarter/test-smtp-server/blob/master/Dockerfile#L21)).


Note that
* `dup` command would not recreate your containers on change. Use `docker rm` and `dcleanup` to recreate a container.
* `dbuild` command by default would pull the image. It's could be annoying, but allows to avoid some silly mistakes.

## How to install

Make it a git-submodule to your project.

```bash
git submodule add -b master https://github.com/estarter/d-tools.git
# add to the PATH variable to call the script from any location
echo "export PATH=$PATH:$(pwd)/d-tools" >> ~/.bashrc
```

Note that PATH variable would only work for one project.

## Related resources

1. [docker](https://docs.docker.com/) / [docker-compose](https://docs.docker.com/compose/)
2. [Docker for Java Developers](https://github.com/docker/labs/tree/master/developer-tools/java/)
3. [jq](https://stedolan.github.io/jq/) / [jid](https://github.com/simeji/jid)
4. [docker-tool](https://github.com/ohmystack/docker-tool)

## TODO

1. port d-scripts
   * dclient
   * ddeploy
   * dlog
2. add auto-complete
3. write unit test for them
4. automate build + PEP-check code

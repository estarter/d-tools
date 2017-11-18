# d-tools
The aim of this project is to tackle a problem of "too long commands" in docker.
It is a set of useful commands to deal with docker / docker-compose projects in a laconic way.

## How to use

**TODO** add asciicast

Screenplay: go to my project, add d-tools as a sub-module, add them to the path, dset, dbuild, dup, dlog, dbash, down.

## Features

* Control sophisticated docker-compose project in a simple way
* Call it from any location
* Memorise your active docker-compose files and docker-compose project name
* Allows custom scripts before build process (TODO / WHY?)


Commands (use `-h` option in cli):

* `dset` - specify project name and docker-compose files. `.d-tool.config.json` in local or home dir will be created.
* `dbuild` - build one, few or all images (wrapper for [docker-compose build](https://docs.docker.com/compose/reference/build/))
* `dup` - starts up the system (wrapper for [docker-compose up](https://docs.docker.com/compose/reference/up/))
* `dps` - shows running containers (wrapper for [docker ps](https://docs.docker.com/engine/reference/commandline/ps/))
* `dbash container` - get a bash session inside the container
* `ddown` - removes and clean up the system (wrapper for [docker-compose down](https://docs.docker.com/compose/reference/down/))
* `dcleanup` - remove all dangling images and volumes. It may save a lot of your HD.

## How to install

Make it a git-submodule to your project.

```
TODO how?
```

Add scripts to the PATH variable to call it from any location.

```bash
export PATH=$PATH:$(pwd)/d-tools
```

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

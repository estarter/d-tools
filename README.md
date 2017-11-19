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
* Allows [custom scripts](#prepare-docker-context) execution before docker build process


### Control commands

* `dset` - specify project name and docker-compose files. `.d-tool.config.json` in local or home dir will be created.
* `dbuild` - [prepare docker build context](#prepare-docker-context) and build one, few or all images (wrapper for [docker-compose build](https://docs.docker.com/compose/reference/build/)).
* `dup` - starts up the system (wrapper for [docker-compose up](https://docs.docker.com/compose/reference/up/))
* `dps` - shows running containers (wrapper for [docker ps](https://docs.docker.com/engine/reference/commandline/ps/))
* `ddown` - removes and clean up the system (wrapper for [docker-compose down](https://docs.docker.com/compose/reference/down/))
* `dcleanup` - remove all dangling images and volumes. It may save a lot of your HD.

### Assistant commands

* `dbash container` - get a bash session inside the container
* `dlog container` - prints out container's log using custom `/usr/bin/dlog` command. When you have a big zoo of
technologies and containers, with different path conventions, it's useful to have a same command that shows log files
([example](https://github.com/estarter/test-smtp-server/blob/master/Dockerfile#L21)).
* `dclient container` - run karaf's client command inside karaf container
* `ddeploy -c container file.jar` - deploy `file.jar` to `container` server, i.e. copy to the deploy folder `/d` that should be a symlink to actual deploy folder

Skip `container` parameter to use the same container:

```bash
dlog server
# server logs ...
dbash
# connects to server container
dlog
# server logs ...
```

### Prepare docker context

`dbuild` auto-discovers `prebuild.sh` scripts in any `build/context` folders defined in your docker-compose files
and execute it before running `docker-compose build` command.

That allows you to execute a custom actions just before docker-compose build command is called.
It's useful in non-trivial project to prepare docker build context automatically before building the image.
For example, you can run the build program in `prebuild.sh` (e.g. `maven`).

Try how it works in [test project](https://github.com/estarter/d-tools-example) (see [prebuild.sh example](https://github.com/estarter/d-tools-example/blob/master/images/client/prebuild.sh))

### Notes

* `-h` options in any script shows all available option
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

## Autocomplete

### BASH

```bash
sudo pip install argcomplete
activate-global-python-argcomplete

# add functions
echo 'eval "$(register-python-argcomplete dbash)"' >> ~/.bashrc
echo 'eval "$(register-python-argcomplete dbuild)"' >> ~/.bashrc
echo 'eval "$(register-python-argcomplete dclient)"' >> ~/.bashrc
echo 'eval "$(register-python-argcomplete ddeploy)"' >> ~/.bashrc
echo 'eval "$(register-python-argcomplete dlog)"' >> ~/.bashrc
echo 'eval "$(register-python-argcomplete dset)"' >> ~/.bashrc
```

### ZSH

```bash
sudo pip install argcomplete

# enable bash autocomplete supprot
echo 'autoload -Uz compinit bashcompinit' >> ~/.zshrc
echo 'compinit' >> ~/.zshrc
echo 'bashcompinit' >> ~/.zshrc
# add functions
echo 'eval "$(register-python-argcomplete dbash)"' >> ~/.zshrc
echo 'eval "$(register-python-argcomplete dbuild)"' >> ~/.zshrc
echo 'eval "$(register-python-argcomplete dclient)"' >> ~/.zshrc
echo 'eval "$(register-python-argcomplete ddeploy)"' >> ~/.zshrc
echo 'eval "$(register-python-argcomplete dlog)"' >> ~/.zshrc
echo 'eval "$(register-python-argcomplete dset)"' >> ~/.zshrc
```

## Related resources

1. [docker](https://docs.docker.com/) / [docker-compose](https://docs.docker.com/compose/)
2. [Docker for Java Developers](https://github.com/docker/labs/tree/master/developer-tools/java/)
3. [jq](https://stedolan.github.io/jq/) / [jid](https://github.com/simeji/jid)
4. [docker-tool](https://github.com/ohmystack/docker-tool)

## TODO

1. write unit test for them; current test solution: `cp ddeploy ddeploy.py && pytest ddeploy.py ; rm ddeploy.py` 
1. automate build + PEP-check code

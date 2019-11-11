# Docker - okta-awscli

Docker image for [okta-awscli](https://github.com/jmhale/okta-awscli) that
provides Okta authentication for [AWS CLI](https://aws.amazon.com/cli/).

## Getting Started

### Building with Docker

If you do not want to build this Docker image then feel free to skip to the
Installation section. Otherwise you can build this image with the following
commands:

```console
$ git clone https://github.com/nickjer/docker-okta-awscli.git
$ cd docker-okta-awscli
$ docker build --force-rm -t nickjer/docker-okta-awscli .
```

### Installing Docker Container

You can install it from [Docker Hub](https://hub.docker.com/) using:

```console
$ docker pull nickjer/docker-okta-awscli
```

## Usage

You can directly launch the `okta-awscli` command as:

```console
$ docker run --rm -it -v "$HOME:/data" nickjer/docker-okta-awscli <args>
```

Note that the `<args>` are any valid `okta-awscli` arguments.

### Helpful Shell Script

You can make a shell script that launches this as:

```bash
#!/usr/bin/env bash

AWS_PROFILE="${AWS_PROFILE:-default}"
OKTA_PROFILE="${OKTA_PROFILE:-${AWS_PROFILE}}"
#OKTA_PROFILE="${OKTA_PROFILE:-default}"

exec \
  docker run --rm -it -v "$HOME:/data" nickjer/docker-okta-awscli \
    --okta-profile "${OKTA_PROFILE}" \
    --profile "${AWS_PROFILE}" \
    "${@}"
```

Then you can run it as:

```console
$ ./my_script
...

$ AWS_PROFILE=my-aws-account ./my_script
...

$ OKTA_PROFILE=profile1 ./my_script --verbose
...
```

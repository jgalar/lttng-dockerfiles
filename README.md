# LTTng Dockerfiles

This repository contains various LTTng Dockerfiles.

Files under the `dev/` directory provide a base development environment
to work the LTTng project and run its test suite.

## Building an Ubuntu-based development image

A `Dockerfile` based upon the `ubuntu:latest` image is available
under `dev/ubuntu/latest`.

To build this image, run
```
cd dev/ubuntu/latest
docker build --build-arg lttng_branch=master       \
             --build-arg urcu_branch=stable-0.10   \
	     --build-arg bt_branch=master          \
	     --tag lttng-ubuntu-master .
```

This Dockerfile accepts `build-arg`s allowing you to
specify the upstream branches to use for the build:
  * `lttng_branch` (`lttng-tools` and `lttng-ust` branches to use, default to `master`)
  * `bt_branch` (`babeltrace` branch to use, defaults to `master`)
  * `urcu_branch` (`liburcu` branch to use, defaults to `stable-0.10`)

Source the `activate` script under `/home/dev/lttng/` to setup the virtual environment.

## Author

* **Jérémie Galarneau** - [jgalar](https://github.com/jgalar)

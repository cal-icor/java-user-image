# java-user-image

See this repository's
[CONTRIBUTING.md](https://github.com/cal-icor/java-user-image/blob/main/CONTRIBUTING.md)
for instructions.

## Java installation details

This image has Java installed via the 
[Jupyter Java project](https://github.com/jupyter-java) project. The Java 17
kernel is provided by [JJava](https://dflib.org/jjava/docs/1.x/) and the
runtime is [OpenJDK JRE 11.0.27](https://packages.ubuntu.com/jammy/openjdk-21-jre)
and [OpenJDK](https://packages.ubuntu.com/jammy/openjdk-21-jdk).

```
$ java -version
openjdk version "21.0.7" 2025-04-15
OpenJDK Runtime Environment (build 21.0.7+6-Ubuntu-0ubuntu122.04)
OpenJDK 64-Bit Server VM (build 21.0.7+6-Ubuntu-0ubuntu122.04, mixed mode, sharing)
$ javac -version
javac 21.0.7
```

## Building the image locally

You should use [repo2docker](https://repo2docker.readthedocs.io/en/latest/) to build and use/test the image on your own device before you push and create a PR.  It's better (and typically faster) to do this first before using CI/CD.  There's no need to waste Github Action minutes to test build images when you can do this on your own device!

Run `repo2docker` from inside the cloned image repo.  To run on a linux/WSL2 linux shell:
```
repo2docker . # <--- the path to the repo
```

If you are using an ARM CPU (Apple M* silicon), you will need to run `jupyter-repo2docker` with the following arguments:

```
jupyter-repo2docker --user-id=1000 --user-name=jovyan \
  --Repo2Docker.platform=linux/amd64 \
  --target-repo-dir=/home/jovyan/.cache \
  -e PLAYWRIGHT_BROWSERS_PATH=/srv/conda \
  . # <--- the path to the repo
```

If you just want to see if the image builds, but not automatically launch the server, add `--no-run` to the arguments (before the final `.`).

# haskell-ide-engine

Image intended to be used with the Remote feature of Visual Studio Code. It provides an environment with stack and hie already installed for ghc-8.6.5, and an unprivileged user with UID 1000.

**NOTE**: It is important that the user running in the container has the same UID as the one you are currently using in the host OS (for POSIX systems at least) otherwise newly create files from within the container will be created with a different UID (usually root if no configuration is provided).

# Instructions

In the root of the project create a directory `.devcontainer` with the following files:

```
$ cat devcontainer.json
---
{
  "name": "Haskell Docker Remote",
  "dockerFile": "Dockerfile",
  "remoteUser": "jack",
  "appPort": ["9000"],
  "extensions": ["alanz.vscode-hie-server"]
}
```

```
$ cat Dockerfile
---
FROM luvemil/haskell-ide-engine:<version>
```

If you need to add a user with a specific uid add a line

```
RUN useradd -u <UID> -g <GID> -ms /bin/bash <username>
```

to the Dockerfile. Remember to change the name of the user in `.devcontainer/devcontainer.json` too.

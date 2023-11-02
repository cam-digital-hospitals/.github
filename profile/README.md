# Digital Twins Dashboard

This organisation contains repositories for the Digital Twins Dashboard project from the Institute of Manufacturing,
University of Cambridge.

For development, it is reccomended to use VSCode.
See: https://code.visualstudio.com/docs/remote/wsl.
Install VSCode on the Windows side and Python on the WSL side (version 3.11 recommended).

## Developer Setup

Code style is checked using `pylint`.  Place [.pylintrc](https://github.com/cam-digital-hospitals/.github/blob/main/.pylintrc)
in the root folder of the project. This file primarily contains settings to disable
some `pylint` warnings.

To work on multiple repositories simultaneously:

1. `pip install virtualenvwrapper`
1. Create a root folder: `git clone https://github.com/cam-digital-hospitals/<myname>-dev.git digital-hospitals`.
    - *Create this repository first on GitHub.*
1. Add `"git.autoRepositoryDetection": "subFolders"` to `.vscode/settings.json`.
1. `git submodule add` each repository you want to run as a service and update `docker/docker-compose.yml` accordingly.
1. `git commit -am "add submodules"`
    - ***Important** to do this before any other changes so that Git sets up the links correctly.*
    - *Check for `create mode 160000` in the output.*
1. `mkvirtualenv digital-hospitals` or `workon digital-hospitals` if the virtual environment already exists.

Inside the virtual environment:

1. `pip install pip-tools`
1. Create the pip requirement files by running `pip-compile` in each submodule folder.
    - *Required to build the Docker containers.*
1. Create the *master* requirement file by running `pip-compile` in the project root.
1. `pip-sync` to install all Python requirements.
    - *Not strictly needed as we will use Docker to run services,
    but helpful for development in VSCode, e.g. syntax highlighting and linting.*

Repeat steps 2-4 each time new pip dependencies are added to any of the submodules.

## Docker setup

Note that Docker Desktop on Windows/Mac defines `host.docker.internal` to enable communication between
Docker containers and the host; however, this is not available on Linux.  Instead, define "extra-hosts"
in the Docker Compose file: see https://stackoverflow.com/a/67158212

To launch services:
```
cd docker
docker compose down
docker compose up
```

## Container registry

Prebuilt Docker containers, where availble, will be hosted at https://github.com/orgs/cam-digital-hospitals/packages.

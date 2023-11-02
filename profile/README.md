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

- `pip install virtualenvwrapper`
- Create a root folder (e.g. `digital-hospitals/`).
- Add `"git.autoRepositoryDetection": "subFolders"` to `.vscode/settings.json`.
- `git clone` each repository you want to run as a service and update `docker/docker-compose.yml` accordingly.
- `mkvirtualenv digital-hospitals` or `workon digital-hospitals` if the virtual environment already exists.

Inside the virtual environment:

- `pip install pip-tools`
- Create the pip requirement files by running `pip-compile` in each subfolder (required to build the
  Docker containers).
- Create the *master* requirement file by running `pip-compile` in the project root.
- `pip-sync` to install all Python requirements (not strictly needed as we will use Docker to run services,
  but helpful for development in VSCode, e.g. syntax highlighting and linting).

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

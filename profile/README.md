# Digital Twins Dashboard

This organisation contains repositories for the Digital Twins Dashboard project from the Institute of Manufacturing,
University of Cambridge.

For development, it is reccomended to use VSCode.
See: https://code.visualstudio.com/docs/remote/wsl.
Install VSCode on the Windows side and Python on the WSL side (version 3.11 recommended).

## Developer Setup

1. Fork the repo `cam-digital-hospitals/yinchi-dev`.
1. Run `git clone https://github.com/cam-digital-hospitals/<yourname-dev>.git digital-hospitals`, where
   `<yourname-dev>` is the name of your newly created repository.
1. `git submodule init hpath-sim` each repository you want to run as a service and update `docker/docker-compose.yml` accordingly.
1. `git submodule update`
    - To pull remote updates in the future, use `git pull --recurse-submodules` from the project root directory.
    - To push with submodule changes included, use `git push --recurse-submodules=on-demand` from the project root directory.

For more information on Git submodules, see: https://git-scm.com/book/en/v2/Git-Tools-Submodules

### VS Code set-up

The [WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) extension is required for
Python developement in WSL (Windows Subsystem for Linux).  Once installed, the simplest way to connect to WSL is
to click the green box in the lower-left corner of a VS Code window.  Note that it is **not** recommended to install VS Code
within WSL itself.

The included `settings.json` file includes definitions for the
[Todo Tree](https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree)
extension.  Other useful extensions include:

- [SQLite Viewer](https://marketplace.visualstudio.com/items?itemName=qwtel.sqlite-viewer)
- [Pylint](https://marketplace.visualstudio.com/items?itemName=ms-python.pylint),
  [autopep8](https://marketplace.visualstudio.com/items?itemName=ms-python.autopep8), and
  [isort](https://marketplace.visualstudio.com/items?itemName=ms-python.isort)
- [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)

### Python set-up 

1. `pip install virtualenvwrapper`
1. `mkvirtualenv digital-hospitals` or `workon digital-hospitals` if the virtual environment already exists.

Inside the virtual environment:

1. `pip install pip-tools`
1. Create the pip requirement files by running `upgrade-deps.sh`.
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

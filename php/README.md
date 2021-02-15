# Docker Apache and PHP 8 Server

This project can execute a PHP site in any folder from <https://localhost:8101/>.

Custom Apache and PHP configuration files can be found in the `config` directory.


## Image build

Build a Docker image from the `config` directory:

```sh
docker image build -t php8 .
```

> The image is named `php8` here, but any name can be used.


## Launch the container

Start a container in any directory with `docker run`:

```sh
docker run \
  -it --rm \
  -p 8101:80 \
  --name php8 \
  -v "$PWD":/var/www/html \
  php8
```

> **Windows Powershell note**: remove the line-breaks and `\` backslashes from this command.
>
> `$PWD` references the current directory on Linux and macOS. It cannot be used on Windows so the full path must be specified in Linux notation, e.g.
>
> ```sh
> -v /c/projects/mysite:/var/www/html
> ```

Open <http://localhost:8101/> in a browser and develop accordingly. This project directory provides some example PHP files.

Press `Ctrl | Cmd + C` in the terminal to stop the container.


## Launch the container with Docker Compose

Alternatively, copy `docker-compose.yml` to your PHP application directory and launch the site with:

```sh
docker-compose up
```

To stop, enter `docker-compose down` in another terminal.

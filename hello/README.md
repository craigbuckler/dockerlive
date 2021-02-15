# Node.js application development

Launch the application in debug mode:

1. Run `docker-compose up` to launch `index.js` using Nodemon.
1. Open <http://localhost:8103/> in a browser. Or add a name to the path, e.g. <http://localhost:8103/Craig>
1. Edit `index.js` and Nodemon will restart the application.

Debuggers can also be attached to the process at `localhost:9229`.

In Chrome: open <chrome://inspect> and click the target. Open **Sources**, press `Ctrl + P` and enter `index.js` to select `home/node/app/index.js`. Set breakpoints as appropriate.

In VS Code: add a breakpoint in `index.js`, click Debug, run `Attach` and debug.

Press `Ctrl|Cmd + C` to stop Docker Compose.


## Build in production mode

Debugging is not enabled:

```bash
docker image build -t hello .
docker run --rm --name hello -p 8103:8103 hello
```

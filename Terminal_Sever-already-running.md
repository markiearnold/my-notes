# Server is already running

## Default
In this example, the server is already running on port 3000

```
kill -9 $(lsof -i tcp:3000 -t)
```


## Docker
In this example, the server is already running for a docker app - which is running a rails app:

```bash
make shell
rm /home/app/tmp/pids/server.pid
exit
make start
```

In this example, the server is already running for a docker app - which is running a rails engine:

```bash
make shell
rm /home/app/src/spec/dummy/tmp/pids/server.pid
exit
make start
```

# Server is already running

In this example, the server is already running on port 3000

```
kill -9 $(lsof -i tcp:3000 -t)
```

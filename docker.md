
## Enable API server for Linux

1. Navigate to /lib/systemd/system in your terminal and open docker.service file

      ```bash vi /lib/systemd/system/docker.service```

2. Find the line which starts with ExecStart and adds -H=tcp://0.0.0.0:2375 to make it look like

      ```ExecStart=/usr/bin/dockerd -H=fd:// -H=tcp://0.0.0.0:2375```

3. Save the Modified File

4. Reload the docker daemon

      ```systemctl daemon-reload```
  
5. Restart the container

      ```sudo service docker restart```

6. Test if it is working by using this command, if everything is fine below command should return a JSON

      ```curl http://localhost:2375/images/json```

To test remotely, use the PC name or IP address of Docker Host

## Enable API server for MAC

For security reasons, we choose to not expose that port directly. However, as described in our FAQ you can run a socat container to redirect the Docker API exposed on the unix domain socket in Linux to the port of your choice on your OSX host:

```docker run -d -v /var/run/docker.sock:/var/run/docker.sock -p 127.0.0.1:1234:1234 bobrik/socat TCP-LISTEN:1234,fork UNIX-CONNECT:/var/run/docker.sock```


and then:


```export DOCKER_HOST=tcp://localhost:1234```



## Bookmarks

1. Container Health checkup - https://medium.com/better-programming/docker-healthchecks-eb744bfe3f3b

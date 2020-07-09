**Description**

My development environment using Docker. I generally run this on an unRAID server and have it set up so I can access it remotely.

**Applications Included**

[Rider](https://www.jetbrains.com/rider/)

[CLion](https://www.jetbrains.com/clion/)

[Ghidra](https://ghidra-sre.org/)

[Github Desktop](https://github.com/shiftkey/desktop/)

[Midnight Commander](https://www.jetbrains.com/clion/)

[Nano](https://www.nano-editor.org/)

[DBeaver](https://dbeaver.io/)

[Wine](https://www.winehq.org/)

[Chromium](https://www.chromium.org/)

[w3m](https://salsa.debian.org/debian/w3m/)

**Libraries Included**

[Google Fruit](https://github.com/google/fruit)

**Build notes**

Using ArchLinux. Forked (with thanks!) from Binhex.

**Usage**
```
docker run -d \
    -p 5900:5900 \
    -p 6080:6080 \
    --name=<container name> \
    -v <path for config files>:/config \
    -v <path for data files>:/data \
    -v /etc/localtime:/etc/localtime:ro \
    -e RIDER_PROPERTIES=<optional path to idea.properties file> \
    -e RIDER_VM_OPTIONS=<optional additional jvm options > \
    -e WEBPAGE_TITLE=<name shown in browser tab> \
    -e VNC_PASSWORD=<password for web ui> \
    -e UMASK=<umask for created files> \
    -e PUID=<uid for user> \
    -e PGID=<gid for user> \
    binhex/arch-rider
```

Please replace all user variables in the above command defined by <> with the correct values.

**Example**
```
docker run -d \
    -p 5900:5900 \
    -p 6080:6080 \
    --name=rider \
    -v /apps/docker/devenv:/config \
    -v /apps/docker/devenv/projects:/data \
    -v /etc/localtime:/etc/localtime:ro \
    -e WEBPAGE_TITLE=Devenv \
    -e VNC_PASSWORD=mypassword \
    -e UMASK=000 \
    -e PUID=0 \
    -e PGID=0 \
    rcannizzaro/devenv
```

**Access via web interface (noVNC)**

`http://<host ip>:<host port>/vnc.html?resize=remote&host=<host ip>&port=<host port>&&autoconnect=1`

e.g.:-

`http://192.168.1.10:6080/vnc.html?resize=remote&host=192.168.1.10&port=6080&&autoconnect=1`

**Access via VNC client**

`<host ip>::<host port>`

e.g.:-

`192.168.1.10::5900`

**Notes**

User ID (PUID) and Group ID (PGID) can be found by issuing the following command for the user you want to run the container as:-

```
id <username>
```
> [!NOTE]
> This was done on MX 25.1 KDE Edition

# Pre-requisites
- Install MX Linux (SysVinit)
- Update and install dependencies: ```sudo apt update && sudo apt-get upgrade -y && sudo apt-get install ffmpeg daemon -y```
- reboot, probably. Just for good measure

# Installing Navidrome
- Go to [the navidrome releases page](https://github.com/navidrome/navidrome/releases/latest)
- Get the navidrome_{version}\_linux\_{architecture}.tar.gz file
- Make a new directory: ```/opt/navidrome```
- Extract the contents of the downloaded release in ```/opt/navidrome```
- ```sudo chmod +x /opt/navidrome/navidrome```
- Configure a ```navidrome.toml``` file as per the [docs](https://navidrome.org/docs/usage/configuration)

## Creating a startup script
> [!IMPORTANT]
> You should read up on SysVinit startup scripts *yourself*.
> You probably shouldn't need a specific guide for this.
> I learned how to do that /today/, this is just what I came up with.

Make a file called ```/etc/init.d/navidrome```, with this as its contents:

```sh
#!/bin/sh
### BEGIN INIT INFO
# Provides:          navidrome
# Required-Start:
# Required-Stop:
# Default-Start:     2 3 4 5
# Default-Stop:
# Short-Description: A Music Server
# Description:
### END INIT INFO

ND_CONFIGFILE=/opt/navidrome/navidrome.toml

start() {
    daemon -D /opt/navidrome /opt/navidrome/navidrome
}

stop() {
    pkill navidrome
}

case "$1" in
    start)
        start
        ;;
    stop)
        stop
        ;;
    restart)
        start
        stop
        ;;
    *)
        echo "Not Implemented"
        ;;
esac
```

after you create this file, make sure to ```sudo chmod +x /etc/init.d/navidrome```.

### Enabling at boot
Open the MX Service Manager, browse to Navidrome and press "Enable at Boot"

# Installing Feishin

## Desktop version
- Just download the latest release from github (probably Feishin-linux-x64.tar.xz).

## Web version for self-hosting
Honestly you're probably better off using feishin.vercel.app
That said, here's how to do it:

### Docker
- Follow [the docker install guide](https://docs.docker.com/engine/install/debian/#install-using-the-repository)
- Verify docker is running by ```sudo service docker status```

- You can now install feishin using the normal docker installation method.


> [!NOTE]
> You can also install navidrome using docker, but if you're doing this on MX, it seems likely to me that you'd rather avoid docker altogether.

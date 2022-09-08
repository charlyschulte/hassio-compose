# Hass.io mit docker-compose
## One Click Installation
```shell
apt update && apt upgrade -y && apt install git -y && apt install docker.io -y && apt install docker-compose -y && git clone https://github.com/charlyschulte/hassio-compose.git && cd hassio-compose && echo "SUPERVISOR_SHARE=/home/$USER/hassio-config" > .env && docker-compose up -d
```
## Installation

```shell
$ git clone https://github.com/charlyschulte/hassio-compose.git
```

2. Create a `.env` file with `SUPERVISOR_SHARE` pointing to the directory where
you want to store all configuration data. __THIS MUST BE AN ABSOLUTE PATH!!!!__

```shell
$ cd hassio-compose
$ echo "SUPERVISOR_SHARE=/home/$USER/hassio-config" > .env
```

3. Start Hass.io using `docker-compose`:

```shell
$ docker-compose up
Recreating hassio_supervisor ... done
Attaching to hassio_supervisor
hassio_supervisor | Resetting last boot...
hassio_supervisor | Starting hassio...
hassio_supervisor | 19-05-02 14:29:00 INFO (MainThread) [__main__] Initialize Hass.io setup
hassio_supervisor | 19-05-02 14:29:00 INFO (MainThread) [__main__] Setup HassIO
hassio_supervisor | 19-05-02 14:29:00 INFO (SyncWorker_0) [hassio.docker.supervisor] Attach to Supervisor homeassistant/amd64-hassio-supervisor with version 162
hassio_supervisor | 19-05-02 14:29:00 INFO (SyncWorker_0) [hassio.docker.supervisor] Connect Supervisor to Hass.io Network
hassio_supervisor | 19-05-02 14:29:00 INFO (MainThread) [hassio.utils.gdbus] Introspect org.freedesktop.systemd1 on /org/freedesktop/systemd1
hassio_supervisor | 19-05-02 14:29:00 INFO (MainThread) [hassio.utils.gdbus] Connect to dbus: org.freedesktop.systemd1 - /org/freedesktop/systemd1
hassio_supervisor | 19-05-02 14:29:00 INFO (MainThread) [hassio.utils.gdbus] Introspect org.freedesktop.hostname1 on /org/freedesktop/hostname1
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.utils.gdbus] Connect to dbus: org.freedesktop.hostname1 - /org/freedesktop/hostname1
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.utils.gdbus] Introspect de.pengutronix.rauc on /
hassio_supervisor | 19-05-02 14:29:01 ERROR (MainThread) [hassio.utils.gdbus] DBus return error: b'Error: GDBus.Error:org.freedesktop.DBus.Error.ServiceUnknown: The name de.pengutronix.rauc was not provided by any .service files\n'
hassio_supervisor | 19-05-02 14:29:01 WARNING (MainThread) [hassio.dbus.rauc] Can't connect to rauc
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.host.info] Update local host information
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.utils.gdbus] Call org.freedesktop.DBus.Properties.GetAll on /org/freedesktop/hostname1
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.host.services] Update service information
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.utils.gdbus] Call org.freedesktop.systemd1.Manager.ListUnits on /org/freedesktop/systemd1
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.host.apparmor] Load AppArmor Profiles: set()
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.host.apparmor] AppArmor is not enabled on host
hassio_supervisor | 19-05-02 14:29:01 INFO (SyncWorker_2) [hassio.docker.interface] Attach to homeassistant/qemux86-64-homeassistant with version 0.92.1
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.addons.git] Load add-on /data/addons/core repository
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.addons.git] Load add-on /data/addons/git/a0d7b954 repository
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.addons] Load add-ons: 57 all - 57 new - 0 remove
hassio_supervisor | 19-05-02 14:29:01 INFO (MainThread) [hassio.updater] Fetch update data from https://s3.amazonaws.com/hassio-version/stable.json
hassio_supervisor | 19-05-02 14:29:02 INFO (MainThread) [hassio.snapshots] Found 0 snapshot files
hassio_supervisor | 19-05-02 14:29:02 INFO (MainThread) [hassio.discovery] Load 0 messages
hassio_supervisor | 19-05-02 14:29:02 INFO (MainThread) [hassio.ingress] Load 0 ingress session
hassio_supervisor | 19-05-02 14:29:02 INFO (MainThread) [__main__] Run Hass.io
hassio_supervisor | 19-05-02 14:29:02 INFO (MainThread) [hassio.misc.dns] Start DNS port forwarding for host add-ons
hassio_supervisor | 19-05-02 14:29:02 INFO (MainThread) [hassio.api] Start API on 172.30.32.2
hassio_supervisor | 19-05-02 14:29:02 INFO (MainThread) [hassio.addons] Startup initialize run 0 add-ons
hassio_supervisor | 19-05-02 14:29:02 INFO (MainThread) [hassio.addons] Startup system run 0 add-ons
hassio_supervisor | 19-05-02 14:29:02 INFO (MainThread) [hassio.addons] Startup services run 0 add-ons
hassio_supervisor | 19-05-02 14:29:02 INFO (SyncWorker_2) [hassio.docker.interface] Restart homeassistant/qemux86-64-homeassistant
hassio_supervisor | 19-05-02 14:29:17 INFO (MainThread) [hassio.homeassistant] Detect a running Home Assistant instance
hassio_supervisor | 19-05-02 14:29:17 INFO (MainThread) [hassio.addons] Startup application run 0 add-ons
hassio_supervisor | 19-05-02 14:29:17 INFO (MainThread) [hassio.tasks] All core tasks are scheduled
hassio_supervisor | 19-05-02 14:29:17 INFO (MainThread) [hassio.core] Hass.io is up and running
```

4. Integrate with however you run your docker instances (out of scope)

## Tips & tricks

### Stopping Containers

To stop the supervisor, just run:

```shell
$ docker-compose down
```

This will not stop Home Assistant or any addons. To do that, run:

```shell
$ docker stop homeassistant
$ docker ps | grep " addon_" | cut -f 1 -d ' ' | xargs docker stop
```

### Removing Containers

To remove the containers (stop them first), just do:

```shell
$ docker-compose rm
$ docker ps | grep " addon_" | cut -f 1 -d ' ' | xargs docker rm
```

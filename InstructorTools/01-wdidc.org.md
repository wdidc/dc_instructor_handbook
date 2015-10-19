# www.wdidc.org

see: https://github.com/wdidc/wdidc.org

## Provisioning an app

See: https://github.com/wdidc/wdidc.org/blob/gh-pages/deployment.md

## current: forever_service

TODO: move this to https://github.com/wdidc/wdidc.org

https://github.com/zapty/forever-service
- uses upstart instead of init.d
- uses updated scripts (updated with library), instead of obsolete/copied templates for init.d scripts.

### Usage

- install a new service
```
sudo forever-service install forever_attendance_api --script /var/www/api.wdidc.org/attendance/index.js
```

This creates `/etc/init/forever_attendance_api.conf` from a template in forever-service.

**Naming convention**: we recommend prefixing your service name with "forever_".  This makes it easier to find and control our services and indicates which tool we are using to monitor the app.

- actions for installed service
```
sudo status forever_attendance_api
sudo start forever_attendance_api
sudo stop forever_attendance_api
sudo restart forever_attendance_api
 ```

- list all "forever" services:

via forever:
```
sudo forever list
```

OR, via upstart
```
$ initctl list | sort | grep forever # depends on naming convention
```
see: http://upstart.ubuntu.com/cookbook/#initctl-commands-summary

OR (kind of), in `/etc/init`
```
ls /etc/init | grep forever # depends on naming convention
```

- enable/disable a service
see: http://askubuntu.com/questions/19320/how-to-enable-or-disable-services

### Setup

```
sudo npm install -g forever-service # needed once
```

### Why upstart instead of init.d?
- the "official" way for managing daemons in Ubuntu
- http://askubuntu.com/a/2078
- http://upstart.ubuntu.com


---


## Previous: init.d

Start/stop services:

```
sudo service <service_name> stop|start|restart
```

### Example: attendance api

```
sudo service forever_attendance_api restart
```

Where "forever_attendance_api" is the file name in `/etc/init.d`



## hooks/post_update

### TODO
- mirror, instead of `git pull` (to delete obsolete files)
  - git fetch all && git reset --hard origin/master

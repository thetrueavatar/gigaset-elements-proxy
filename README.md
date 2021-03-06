# gigaset-elements-proxy

Is a very simple gateway to gigaset-elements API:

- periodic re-authentication
- local proxy to the gigaset-elements APIs
- gigaset-elements events are periodically fetched and pushed to a MQTT broker

As gigaset-elements does not provide local network APIs, I use it to access my equipement from https://home-assistant.io

[![Dependency Status](https://gemnasium.com/badges/github.com/ycardon/gigaset-elements-proxy.svg)](https://gemnasium.com/github.com/ycardon/gigaset-elements-proxy)
[![Known Vulnerabilities](https://snyk.io/test/github/ycardon/gigaset-elements-proxy/badge.svg)](https://snyk.io/test/github/ycardon/gigaset-elements-proxy)

## Raw API

- [basestations](/api/v1/me/basestations)

- [events](/api/v2/me/events)
    - ?limit=
    - ?group=
    - ?from_ts= &to_ts=

- [cameras](/api/v1/me/cameras)
    - /[id]/liveview/start
    - /[id]/recording/[status|start|stop]

- [health](/api/v2/me/health)

- [notification settings](/api/v1/me/notifications/users/channels)

## Convenience APIs

- [live camera (redirect to a cloud-based RTSP stream)](/live): you have to set the camera id in the configuration file

- [live camera (local MJPEG stream)](/live-local): you have set your camera local infos in the configuration file

- [sensors status](/sensors)

## MQTT events

- pushes event to queue `/gigaset/<sensor_friendly_name>` with `true` or `fasle` payload
- motions events (movement detector and camera) automatically generate a delayed `false` event

## installation

from git

```
> git clone https://github.com/ycardon/gigaset-elements-proxy
> cd gigaset-elements-proxy
> npm install
> vim config/default.yaml    
> node app.js
```

from npm

```
install
> [sudo] npm install gigaset-elements-proxy -g

locate then edit config/default.yaml with
> npm list gigaset-elements-proxy

run
> ge-proxy
```

You can also check https://github.com/lorenwest/node-config/wiki/Configuration-Files

## credits

- Strongly inspired by the Python command line version that can be find under https://github.com/dynasticorpheus/gigaset-elements (thank you !!)
- Security audits
    - https://www.iot-tests.org/2017/01/testing-gigaset-elements-camera/
    - https://team-sik.org/sik-2016-044/
    - https://team-sik.org/sik-2016-045/
    - https://team-sik.org/sik-2016-046/
    - https://team-sik.org/sik-2016-047/
    - https://team-sik.org/sik-2016-048/

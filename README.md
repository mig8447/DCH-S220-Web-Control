# D-Link DCH-S220 REST API

This project aims to control via a custom REST API the D-Link's DCH-S220 Siren
to allow total customized control over this product for home automation
enthusiasts or hobbyists.

This project is only possible due to the great work of [@bikerp](https://github.com/bikerp)
and his [dsp-w215-hnap](https://github.com/bikerp/dsp-w215-hnap) repo.

The project must run on a device in the same network as your siren (on a
raspberry pi for example), you must open the configured ports on your router to
access it from the outside.

# Install

1. Clone this repo
2. Change into the project's root directory
3. Install the dependencies by executing
     ```sh
     npm i
     ```
4. Copy the `.env.example` into `.env` by executing
     ```sh
     cp .env.example .env
     ```
5. Edit the `.env` file to configure the authentication and siren parameters
6. Start the server by executing
     ```sh
     npm start
     ```

Additionally, you can add a watcher to the process with [pm2](http://pm2.keymetrics.io/)

# Consuming endpoints and controlling the siren

All endpoints must be consumed with HTTP GET under the root "/".

## Start sounding the siren

Parameters:
- `type`: 'start'
- `volume`: A value from 1 to 100
- `sound`: A value from 1 to 6
  - 1: emergency
  - 2: fire
  - 3: ambulance
  - 4: police
  - 5: door_chime
  - 6: beep
- `duration`: A value from 1 to 88888 (infinite)

cURL Example:
```sh
curl 'http://localhost:3000/?type=start&volume=20&sound=1&duration=30'
```

## Stop sounding the siren

Parameters: 
- `type`: 'stop'

cURL Example:
```sh
curl 'http://localhost:3000/?type=stop'
```

## Sound *n* beeps

Parameters: 
- `type`: 'beep'
- `times`: A number from 1 to n the siren must beep

cURL Example:
```sh
curl 'http://localhost:3000/?type=beep&times=1'
```

## Get the current status of the siren
Figure out if the siren is sounding or not.

Parameters: 
- `type`: 'status'

cURL Example:
```sh
curl 'http://localhost:3000/?type=status'
```

## Sample response
```http
HTTP/1.1 200 OK
Content-Type: application/json
Date: Sun, 06 Aug 2017 19:57:48 GMT
Connection: close
Transfer-Encoding: chunked

{"status":"OK","message":"Successfully processed","isPlaying":false}
```

# kunzite-softphone-iframe-demo


https://github.com/sostribe/kunzite-softphone-iframe-demo/assets/414967/af467c9c-9f6a-4020-ba8a-c1caf1970057


## Events Data payloads

Phone events (that are almost simetrical to the events offered by the socket api) can be used to open the widget 
on when ringing or calling.

 ```json
{
  "type": "phone:calling",
  "data": {
    "context": {
      "status": "online",
      "user": "johndoe@astroline.es",
      "extension": "200",
      "size": {
        "width": 320,
        "height": 460
      }
    },
    "id": "294e44c0-494d-487f-b286-2d22fb5b0c3a",
    "date": "2023-05-21T15:10:19.342Z",
    "from": "+34917370192",
    "to": "+34917370191",
    "direction": "outbound",
    "status": "ringing",
    "duration": 0,
    "wait": 0,
    "total": 0,
    "team": "Dev_Team"
  }
}
 ```

 ```json
{
  "type": "phone:ringing",
  "data": {
    "context": {
      "status": "online",
      "user": "johndoe@astroline.es",
      "extension": "200",
      "size": {
        "width": 320,
        "height": 460
      }
    },
    "id": "294e44c0-494d-487f-b286-2d22fb5b0c3a",
    "date": "2023-05-21T15:10:19.342Z",
    "from": "+34917370192",
    "to": "+34917370191",
    "direction": "inbound",
    "status": "ringing",
    "duration": 0,
    "wait": 0,
    "total": 0,
    "team": "Dev_Team"
  }
}
 ```

```json
{
  "type": "phone:accepted",
  "data": {
    "context": {
      "status": "online",
      "user": "johndoe@astroline.es",
      "extension": "200",
      "size": {
        "width": 320,
        "height": 460
      }
    },
    "id": "294e44c0-494d-487f-b286-2d22fb5b0c3a",
    "date": "2023-05-21T15:10:19.342Z",
    "from": "+34917370192",
    "to": "+34917370191",
    "direction": "inbound",
    "status": "answered",
    "duration": 0,
    "wait": 8,
    "total": 0,
    "team": "Dev_Team"
  }
}
```

```json
{
  "type": "phone:terminated",
  "data": {
    "context": {
      "status": "online",
      "user": "johndoe@astroline.es",
      "extension": "200",
      "size": {
        "width": 320,
        "height": 460
      }
    },
    "id": "294e44c0-494d-487f-b286-2d22fb5b0c3a",
    "date": "2023-05-21T15:10:19.342Z",
    "from": "+34917370192",
    "to": "+34917370191",
    "direction": "inbound",
    "status": "answered",
    "duration": 22,
    "wait": 8,
    "total": 30,
    "team": "Dev_Team"
  }
}
```
### calling vs ringing

`phone:ringing` is emitted when the softphone receives an incoming call, while `phone:calling` is emitted when the softphone is in the process of making an outgoing call.



## Performing Click2Call

```js
window.frames.sf.postMessage({ type: 'click2call', data: { number: '+34911085460' } }, '*');
```
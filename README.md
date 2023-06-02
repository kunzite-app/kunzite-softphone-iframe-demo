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

## Adding contacts 

The softphone can handle contacts in two different ways:

By dropping a VCF file anywhere within the softphone. In this case, the file will be handled and saved by the phone in the user's space.
By invoking contacts and passing the appropriate contacts format payload. This is the current method used by Kunzite to add integration contacts via a socket (currently managed exclusively by Kunzite), either from a parent iframe or from an addon. These contacts are volatile, and the user must ensure that the contacts are initialized at the appropriate time (preferably at the logged event).
Indexing contacts is a CPU/thread-friendly operation, and indexing only occurs during idle times to prevent freezing the UI.

We support up to 250k contacts (and even more) without interfering with the softphone interoperability. The only drawback is that it may take longer to find a user, depending on the amount of data to be ingested.

```js
const contacts = [
  { id: 'id1', name: 'John Doe', phones: ['+34666555444'] },
  { id: 'id2', name: 'Jennifer Doe', phones: ['+34666555444', '+34666777888'] },
];

window.frames.sf.postMessage({ type: 'contacts', data: { contacts } }, '*');
```
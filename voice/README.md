# Two services:
- Signaling
- Media-Server

## Signaling specifications:
- Handle rights
- Handle Media-Servers
- Is written in Elixir using Phoenix framework (Therefore the api is only a socket phoenix)

## Media-Server specifications:
- Handle media
- Is a SFU (Selective Forwarding Unit)
- Is written in Rust

### Connection flow:

![Connection flow](./connect.drawio.svg)

This diagrams illustrates the connection flow. And therefore will give us a starting point for the specifications.

### SDP and negotiation specification:

Perfect negotiation implementation:

![Negotiation](./negotiation.drawio.svg)

### Mute and unmute:

Mute implementation:

![Mute](./mute.drawio.svg)

```Typescript
/*
 * Principle: dont touch the tranceivers it is unnecessary negotiation
 * releasing the observed track and remove it from the stream sent to the server in order for the browser to know you are not listening anymore.
 */
cleanMediaStream(): void {
    audioTrack.stop();
    audioTrack = null;
    audioStream.getTracks().forEach((track) => {
        track.stop();
        audioStream.removeTrack(track);
    });
}
```

On the Media-Server side:

it is the same, remove the track from the stream.

### Media-Server handling:

- One Media-Server per server, handling all the voice channels in the server.
- The Signaling server keeps track of them (in a redis ? would be nice to enable better scalability in the future)

### Presence handling:

- The Signaling server keeps track of the presence of the users in the voice channels.
- Storage in a redis as well might be an option

### Why redis ? (To be challenged)

We need a fast cache storage to store short lived data.
But we also need something that is not heavy to call on every request.

### Security

Be authenticated to access the Signaling server and write checks on the Signaling server.
The Signaling server is responsible for the safekeeping of the credentials for the stunnerGateways.
TURN authenticated via Stunner (To be further searched on the possibilities).

### Deployment Diagram

![Deployment Diagram](./deployment.drawio.svg)
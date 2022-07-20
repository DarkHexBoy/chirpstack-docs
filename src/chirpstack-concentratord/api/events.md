# Events

Events are published by Concentratord and can be received by creating a
[ZeroMQ SUB](http://zguide.zeromq.org/page:all#toc49) socket. The first frame
holds the event type (string), the second frame holds the event payload encoded
using [Protobuf](https://developers.google.com/protocol-buffers)
(see `api/proto/gw/gw.proto` in [chirpstack](https://github.com/chirpstack/chirpstack)
for the Protobuf message definitions).

## `up`

Uplink received by the gateway (`UplinkFrame` Protobuf message).

## `stats`

Gateway statistics (`GatewayStats` Protobuf message).

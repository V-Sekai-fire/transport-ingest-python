# transport-ingest-python

A second, independent receiver for the fabric's unreliable input datagrams, checked against the golden vectors the first one uses.

## What it is for

The C transports run one QUIC stack on both ends, so nothing in them shows that the wire contract is implementable from its specification. This receiver uses a QUIC and TLS stack that shares no code with them, and where the two disagree, one of them is wrong about the contract. It holds no authority and keeps no state. The packet layout is emitted by `contract-entity-packet` and vendored here, never edited. RFD 2123 owns the topic.

## Build and run

```sh
pixi run check
pixi run selftest
pixi run serve
```

`check` runs the conformance gate and `selftest` shows it failing on planted input. `serve` runs the receiver and needs `cert.pem` and `key.pem` in the working directory.

## Licence

MIT; see `LICENSE`.

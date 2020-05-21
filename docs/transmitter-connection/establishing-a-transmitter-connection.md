---
tags: [transmitter-connection]
---

# Establishing a transmitter connection

Transmitter connections consist of two connections to a node:
1. A intermittent connection via HTTP to the REST API for initial announcement of a new connection, heartbeat messages and transmitter configurations.
2. A continuous RabbitMQ connection to receive the data to be transmitted and to publish telemetry data.

The procedure for a new transmitter connection is as follow:
1. Announce the transmitter via a call to `POST /transmitters/_bootstrap`.
2. The response is either the transmitter configuration or an error message.
3. On success, initiate the RabbitMQ connection to receive calls and send telemetry.
4. After the connection has been established, a periodical heartbeat must be sent to `POST /transmitters/_heartbeat`.
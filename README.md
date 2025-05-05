# spaceswarm-proxy-ws
Proxy spaceswarm connections over websockets with auto-reconnect logic

```
npm -s spaceswarm-proxy-ws
```

Uses the [spaceswarm-proxy](https://github.com/samooth/spaceswarm-proxy) module.

## Example

```js

const SpaceswarmServer = require('spaceswarm-proxy-ws/server')

// Initialize the proxy server
// Also specify any options for spaceswarm here
// https://github.com/spaceswarm/spaceswarm
const server = new SpaceswarmServer()

// Start listening on clients via websocket protocol
server.listen(3472)


const SpaceswarmClient = require('spaceswarm-proxy-ws/client')

// Initialize a proxied spaceswarm
// Also specify any options for spaceswarm-proxy client
// https://github.com/RangerMauve/spaceswarm-proxy#client
const swarm = new SpaceswarmClient({
  // Specify a list of proxy servers available to connect to
	proxy: ['ws://127.0.0.1:3472']
})

// Same as with spaceswarm
swarm.on('connection', (connection, info) => {
	const stream = getSomeStream(info.topic)

	// Pipe the data somewhere
	// E.G. spacedrive.replicate()
	connection.pipe(stream).pipe(connection)
})

swarm.join(topic)

swarm.leave(topic)
```

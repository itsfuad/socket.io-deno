# History

| Version                  | Release date   |
| ------------------------ | -------------- |
| [0.2.1](#021-2025-01-09) | January 2025   |
| [0.2.0](#020-2022-10-11) | October 2022   |
| [0.1.1](#011-2022-09-14) | September 2022 |
| [0.1.0](#010-2022-09-12) | September 2022 |

# Release notes

## [0.2.1](https://github.com/socketio/socket.io-deno/compare/0.2.0...0.2.1) (2025-01-09)

### Bug Fixes

- check if websocket is open before writing
  ([#22](https://github.com/socketio/socket.io-deno/issues/22))
  ([d08f8f2](https://github.com/socketio/socket.io-deno/commit/d08f8f2152e06f95dd026eccc610c4c644bbde36))
- make socket#nsp public
  ([84d97be](https://github.com/socketio/socket.io-deno/commit/84d97be72cfd661e0ea20578149f7d527de6b39d))
- use Deno.serve() instead of serve()
  ([5a27581](https://github.com/socketio/socket.io-deno/commit/5a27581b00a6491d15530a6333b863b85694a36c))

BREAKING CHANGE :warning:

Please use `Deno.serve()` instead of `serve()`, which was removed in Deno v1.

Before:

```ts
import { serve } from "https://deno.land/std@0.220.1/http/server.ts";
import { Server } from "https://deno.land/x/socket_io@0.2.0/mod.ts";

const io = new Server();

await serve(io.handler(), {
  port: 3000,
});
```

After:

```ts
import { Server } from "https://deno.land/x/socket_io@0.2.0/mod.ts";

const io = new Server();

Deno.serve({
  handler: io.handler(),
  port: 3000,
});
```

## [0.2.0](https://github.com/socketio/socket.io-deno/compare/0.1.1...0.2.0) (2022-10-11)

### Bug Fixes

- **engine:** properly pause the polling transport during upgrade
  ([c706741](https://github.com/socketio/socket.io-deno/commit/c706741544e33ca364ef88e3779aa8d4ee3739f0)),
  closes [#4](https://github.com/socketio/socket.io-deno/issues/4)
- restore socket.to() and socket.except() methods
  ([4ce5f64](https://github.com/socketio/socket.io-deno/commit/4ce5f646a95d9dd522fdf3c86951f82d641e3418)),
  closes [#3](https://github.com/socketio/socket.io-deno/issues/3)
- **server:** send events once the handshake is completed
  ([518f534](https://github.com/socketio/socket.io-deno/commit/518f534e1c205b746b1cb21fe76b187dabc96f34))

### Features

- implement catch-all listeners
  ([333dfdd](https://github.com/socketio/socket.io-deno/commit/333dfdd8d0f8a3409e2f22a765b775f77fb05d85))

Syntax:

```js
io.on("connection", (socket) => {
  socket.onAnyIncoming((event, ...args) => {
    // ...
  });

  socket.onAnyOutgoing((event, ...args) => {
    // ...
  });
});
```

- implement the Redis adapter
  ([39eaa0e](https://github.com/socketio/socket.io-deno/commit/39eaa0e755cf16d7b099711c5ff759290103bfd3))

```js
import { serve } from "https://deno.land/std@a.b.c/http/server.ts";
import {
  createRedisAdapter,
  createRedisClient,
  Server,
} from "https://deno.land/x/socket_io@x.y.z/mod.ts";

const [pubClient, subClient] = await Promise.all([
  createRedisClient({
    hostname: "localhost",
  }),
  createRedisClient({
    hostname: "localhost",
  }),
]);

const io = new Server({
  adapter: createRedisAdapter(pubClient, subClient),
});

await serve(io.handler(), {
  port: 3000,
});
```

## [0.1.1](https://github.com/socketio/socket.io-deno/compare/0.1.0...0.1.1) (2022-09-14)

### Bug Fixes

- disallow duplicate WebSocket connections with same sid
  ([193a9b5](https://github.com/socketio/socket.io-deno/commit/193a9b5db50e396025d32ac5166be7b5c39c6ddc))
- disallow mismatching transport
  ([6b2cc16](https://github.com/socketio/socket.io-deno/commit/6b2cc16a269405f8087b95ea563c0f9b746312bd))
- prevent crash when using custom headers
  ([dfe3122](https://github.com/socketio/socket.io-deno/commit/dfe3122865e768ae75e1d4d8c92a47961d708ee9))
- send a "noop" packet when transport is already closed
  ([3b1eb82](https://github.com/socketio/socket.io-deno/commit/3b1eb82d1e9e44660b43651dceb05b88bd1b5350))

## 0.1.0 (2022-09-12)

This is the first release of this library!

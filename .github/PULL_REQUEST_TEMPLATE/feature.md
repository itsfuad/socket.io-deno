---
name: Feature implementation
about: A new awesome feature
title: ''
labels: 'enhancement'
assignees: ''
---

Related issue or discussion:

**New behavior**

```ts
import { Server } from "https://deno.land/x/socket_io@x.y.z/mod.ts";

const io = new Server();

io.on("connection", (socket) => {
  console.log(`socket ${socket.id} connected`);

  socket.emit("hello", "world");

  socket.on("disconnect", (reason) => {
    console.log(`socket ${socket.id} disconnected due to ${reason}`);
  });
});

Deno.serve({
  handler: io.handler(),
  port: 3000,
});
```

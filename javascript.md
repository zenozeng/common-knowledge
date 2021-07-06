# JavaScript

## Event Loop

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop
- https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/#what-is-the-event-loop
- https://html.spec.whatwg.org/multipage/webappapis.html#event-loops

### Phases (Node.js)

1. **timers**: `setTimeout` & `setInterval`
2. **pending callbacks**: IO Callbacks deferred to the next loop iteration
3. **idle, prepare**: used internally
4. **poll**: retrieve new I/O events; execute I/O related callbacks
5. **check**: `setImmediate`
6. **closed callbacks**: `on('close')`

**nextTick**: fires immediately on the same phase

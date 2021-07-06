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

```javascript
console.log('start');
setTimeout(() => console.log('timeout 0'), 0);
setImmediate(() => console.log('immediate'));
Promise.resolve().then(() => console.log('promise'));
(function () { 
  (async function() { 
    console.log('async') 
  })() 
})();
process.nextTick(() => {
  console.log('nextTick 1')
  process.nextTick(() => {
    console.log('nextTick 2')
  })
});
console.log('end');
```

```
start
async
end
nextTick 1
nextTick 2
promise
timeout 0
immediate
```

#### Vue.nextTick

- Promise.resolve().then() (microtask)
- MutationObserver (microtask)
- setImmediate
- setTimeout(fn, 0)

https://github.com/vuejs/vue/blob/0603ff695d2f41286239298210113cbe2b209e28/src/core/util/next-tick.js

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
setTimeout(() => {
  console.log('timeout 0 - 1');
  setTimeout(() => {
    console.log('timeout 0 - 2');
  }, 0);
}, 0);
setImmediate(() => console.log('immediate'));
Promise.resolve().then(() => console.log('promise'));
(function () { 
  (async function() { 
    console.log('async');
  })() 
})();
process.nextTick(() => {
  console.log('nextTick 1');
  process.nextTick(() => {
    console.log('nextTick 2');
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
timeout 0 - 1
immediate
timeout 0 - 2
```

#### macrotasks & microtasks

macrotasks (tasks): 
- setTimeout
- setInterval
- setImmediate
- requestAnimationFrame
- I/O
- UI rendering

microtasks:
- process.nextTick
- Promises
- queueMicrotask
- MutationObserver

> First, each time a task exits, the event loop checks to see if the task is returning control to other JavaScript code. If not, it runs all of the microtasks in the microtask queue. The microtask queue is, then, processed multiple times per iteration of the event loop, including after handling events and other callbacks.
> 
> Second, if a microtask adds more microtasks to the queue by calling queueMicrotask(), those newly-added microtasks execute before the next task is run. That's because the event loop will keep calling microtasks until there are none left in the queue, even if more keep getting added.

References:
- https://stackoverflow.com/questions/25915634/difference-between-microtask-and-macrotask-within-an-event-loop-context
- https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide

#### Vue.nextTick

- Promise.resolve().then() (microtask)
- MutationObserver (microtask)
- setImmediate
- setTimeout(fn, 0)

https://github.com/vuejs/vue/blob/0603ff695d2f41286239298210113cbe2b209e28/src/core/util/next-tick.js

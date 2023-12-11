# TypeScript SimpleEvent

## Example of usage

```typescript
// SomeService.ts

import {SimpleEvent} from '@osx11/simple-event';

let i = 0;
const someEvent = new SimpleEvent<number>();

const callback = (v: number) => {
  console.log(v);
}

someEvent.addEventListener(callback);

setInterval(() => someEvent.emit(++i), 1000);
```

- If you need an event type with `addEventListener` and `removeEventListener` methods only (to prevent unintended emit),
you can use `someEvent.asSubscribeOnlyEvent()`

- To unsubscribe, use `someEvent.removeEventListener(callback)` modify the code as following:
```typescript
const subscription = someEvent.addEventListener(v => console.log(v));

// run where needed
subscription.unsubscribe()
```

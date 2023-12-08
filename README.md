# TypeScriptSimpleEvent

## Example of usage

```typescript
// SomeService.ts

import {SimpleEvent} from '@osx11/simple-event';

export class SomeService {
  constructor() {
    this.startLoop();
  }

  private readonly _onSomeEvent = new SimpleEvent<number>();

  get onSomeEvent() {
    return this._onSomeEvent.asSubscribeOnlyEvent();
  }

  private startLoop() {
    let i = 1;

    setInterval(() => {
      // emit value for event every second
      this._onSomeEvent.emit(i);
      i++;
    }, 1000)
  }
}

// ------------

// AnotherService.ts

import { SimpleEventSubscription } from '@osx11/simple-event';
import {SomeService} from './SomeService.ts';

export class AnotherService {
  constructor() {
    this._listener = this.someService.onSomeEvent.addEventListener(v => {
      // this will log N every second (when event is emitted)
      console.log('New value', v)
    });
  }
  
  private _listener: SimpleEventSubscription | undefined;
  
  private readonly someService = new SomeService();
  
  // dispose should be called where unsubscribe is needed.
  // e.g. in return callback of useEffect in React
  dispose() {
    this._listener?.unsubscribe();
  }
}
```

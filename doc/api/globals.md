# Global objects

<!--introduced_in=v0.10.0-->

<!-- type=misc -->

These objects are available in all modules.

The following variables may appear to be global but are not. They exist only in
the scope of [CommonJS modules][]:

* [`__dirname`][]
* [`__filename`][]
* [`exports`][]
* [`module`][]
* [`require()`][]

The objects listed here are specific to Node.js. There are [built-in objects][]
that are part of the JavaScript language itself, which are also globally
accessible.

## Class: `AbortController`

<!-- YAML
added:
  - v15.0.0
  - v14.17.0
changes:
  - version: v15.4.0
    pr-url: https://github.com/nodejs/node/pull/35949
    description: No longer experimental.
-->

<!-- type=global -->

A utility class used to signal cancelation in selected `Promise`-based APIs.
The API is based on the Web API [`AbortController`][].

```js
const ac = new AbortController();

ac.signal.addEventListener('abort', () => console.log('Aborted!'),
                           { once: true });

ac.abort();

console.log(ac.signal.aborted);  // Prints true
```

### `abortController.abort([reason])`

<!-- YAML
added:
  - v15.0.0
  - v14.17.0
changes:
  - version:
      - v17.2.0
      - v16.14.0
    pr-url: https://github.com/nodejs/node/pull/40807
    description: Added the new optional reason argument.
-->

* `reason` {any} An optional reason, retrievable on the `AbortSignal`'s
  `reason` property.

Triggers the abort signal, causing the `abortController.signal` to emit
the `'abort'` event.

### `abortController.signal`

<!-- YAML
added:
  - v15.0.0
  - v14.17.0
-->

* Type: {AbortSignal}

### Class: `AbortSignal`

<!-- YAML
added:
  - v15.0.0
  - v14.17.0
-->

* Extends: {EventTarget}

The `AbortSignal` is used to notify observers when the
`abortController.abort()` method is called.

#### Static method: `AbortSignal.abort([reason])`

<!-- YAML
added:
  - v15.12.0
  - v14.17.0
changes:
  - version:
      - v17.2.0
      - v16.14.0
    pr-url: https://github.com/nodejs/node/pull/40807
    description: Added the new optional reason argument.
-->

* `reason`: {any}
* Returns: {AbortSignal}

Returns a new already aborted `AbortSignal`.

#### Static method: `AbortSignal.timeout(delay)`

<!-- YAML
added:
  - v17.3.0
  - v16.14.0
-->

* `delay` {number} The number of milliseconds to wait before triggering
  the AbortSignal.

Returns a new `AbortSignal` which will be aborted in `delay` milliseconds.

#### Static method: `AbortSignal.any(signals)`

<!-- YAML
added:
  - v20.3.0
  - v18.17.0
-->

* `signals` {AbortSignal\[]} The `AbortSignal`s of which to compose a new `AbortSignal`.

Returns a new `AbortSignal` which will be aborted if any of the provided
signals are aborted. Its [`abortSignal.reason`][] will be set to whichever
one of the `signals` caused it to be aborted.

#### Event: `'abort'`

<!-- YAML
added:
  - v15.0.0
  - v14.17.0
-->

The `'abort'` event is emitted when the `abortController.abort()` method
is called. The callback is invoked with a single object argument with a
single `type` property set to `'abort'`:

```js
const ac = new AbortController();

// Use either the onabort property...
ac.signal.onabort = () => console.log('aborted!');

// Or the EventTarget API...
ac.signal.addEventListener('abort', (event) => {
  console.log(event.type);  // Prints 'abort'
}, { once: true });

ac.abort();
```

The `AbortController` with which the `AbortSignal` is associated will only
ever trigger the `'abort'` event once. We recommended that code check
that the `abortSignal.aborted` attribute is `false` before adding an `'abort'`
event listener.

Any event listeners attached to the `AbortSignal` should use the
`{ once: true }` option (or, if using the `EventEmitter` APIs to attach a
listener, use the `once()` method) to ensure that the event listener is
removed as soon as the `'abort'` event is handled. Failure to do so may
result in memory leaks.

#### `abortSignal.aborted`

<!-- YAML
added:
  - v15.0.0
  - v14.17.0
-->

* Type: {boolean} True after the `AbortController` has been aborted.

#### `abortSignal.onabort`

<!-- YAML
added:
  - v15.0.0
  - v14.17.0
-->

* Type: {Function}

An optional callback function that may be set by user code to be notified
when the `abortController.abort()` function has been called.

#### `abortSignal.reason`

<!-- YAML
added:
  - v17.2.0
  - v16.14.0
-->

* Type: {any}

An optional reason specified when the `AbortSignal` was triggered.

```js
const ac = new AbortController();
ac.abort(new Error('boom!'));
console.log(ac.signal.reason);  // Error: boom!
```

#### `abortSignal.throwIfAborted()`

<!-- YAML
added:
  - v17.3.0
  - v16.17.0
-->

If `abortSignal.aborted` is `true`, throws `abortSignal.reason`.

## Class: `Blob`

<!-- YAML
added: v18.0.0
-->

<!-- type=global -->

See {Blob}.

## Class: `Buffer`

<!-- YAML
added: v0.1.103
-->

<!-- type=global -->

* {Function}

Used to handle binary data. See the [buffer section][].

## Class: `ByteLengthQueuingStrategy`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`ByteLengthQueuingStrategy`][].

## `__dirname`

This variable may appear to be global but is not. See [`__dirname`][].

## `__filename`

This variable may appear to be global but is not. See [`__filename`][].

## `atob(data)`

<!-- YAML
added: v16.0.0
-->

> Stability: 3 - Legacy. Use `Buffer.from(data, 'base64')` instead.

Global alias for [`buffer.atob()`][].

## `BroadcastChannel`

<!-- YAML
added: v18.0.0
-->

See {BroadcastChannel}.

## `btoa(data)`

<!-- YAML
added: v16.0.0
-->

> Stability: 3 - Legacy. Use `buf.toString('base64')` instead.

Global alias for [`buffer.btoa()`][].

## `clearImmediate(immediateObject)`

<!-- YAML
added: v0.9.1
-->

<!--type=global-->

[`clearImmediate`][] is described in the [timers][] section.

## `clearInterval(intervalObject)`

<!-- YAML
added: v0.0.1
-->

<!--type=global-->

[`clearInterval`][] is described in the [timers][] section.

## `clearTimeout(timeoutObject)`

<!-- YAML
added: v0.0.1
-->

<!--type=global-->

[`clearTimeout`][] is described in the [timers][] section.

## `CloseEvent`

<!-- YAML
added: v23.0.0
-->

<!-- type=global -->

The `CloseEvent` class. See [`CloseEvent`][] for more details.

A browser-compatible implementation of [`CloseEvent`][]. Disable this API
with the [`--no-experimental-websocket`][] CLI flag.

## Class: `CompressionStream`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`CompressionStream`][].

## `console`

<!-- YAML
added: v0.1.100
-->

<!-- type=global -->

* {Object}

Used to print to stdout and stderr. See the [`console`][] section.

## Class: `CountQueuingStrategy`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`CountQueuingStrategy`][].

## `Crypto`

<!-- YAML
added:
  - v17.6.0
  - v16.15.0
changes:
  - version: v23.0.0
    pr-url: https://github.com/nodejs/node/pull/52564
    description: No longer experimental.
  - version: v19.0.0
    pr-url: https://github.com/nodejs/node/pull/42083
    description: No longer behind `--experimental-global-webcrypto` CLI flag.
-->

> Stability: 2 - Stable.

A browser-compatible implementation of {Crypto}. This global is available
only if the Node.js binary was compiled with including support for the
`node:crypto` module.

## `crypto`

<!-- YAML
added:
  - v17.6.0
  - v16.15.0
changes:
  - version: v23.0.0
    pr-url: https://github.com/nodejs/node/pull/52564
    description: No longer experimental.
  - version: v19.0.0
    pr-url: https://github.com/nodejs/node/pull/42083
    description: No longer behind `--experimental-global-webcrypto` CLI flag.
-->

> Stability: 2 - Stable.

A browser-compatible implementation of the [Web Crypto API][].

## `CryptoKey`

<!-- YAML
added:
  - v17.6.0
  - v16.15.0
changes:
  - version: v23.0.0
    pr-url: https://github.com/nodejs/node/pull/52564
    description: No longer experimental.
  - version: v19.0.0
    pr-url: https://github.com/nodejs/node/pull/42083
    description: No longer behind `--experimental-global-webcrypto` CLI flag.
-->

> Stability: 2 - Stable.

A browser-compatible implementation of {CryptoKey}. This global is available
only if the Node.js binary was compiled with including support for the
`node:crypto` module.

## `CustomEvent`

<!-- YAML
added:
  - v18.7.0
  - v16.17.0
changes:
  - version: v23.0.0
    pr-url: https://github.com/nodejs/node/pull/52723
    description: No longer experimental.
  - version:
    - v22.1.0
    - v20.13.0
    pr-url: https://github.com/nodejs/node/pull/52618
    description: CustomEvent is now stable.
  - version: v19.0.0
    pr-url: https://github.com/nodejs/node/pull/44860
    description: No longer behind `--experimental-global-customevent` CLI flag.
-->

> Stability: 2 - Stable

<!-- type=global -->

A browser-compatible implementation of the [`CustomEvent` Web API][].

## Class: `DecompressionStream`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`DecompressionStream`][].

## `Event`

<!-- YAML
added: v15.0.0
changes:
  - version: v15.4.0
    pr-url: https://github.com/nodejs/node/pull/35949
    description: No longer experimental.
-->

<!-- type=global -->

A browser-compatible implementation of the `Event` class. See
[`EventTarget` and `Event` API][] for more details.

## `EventSource`

<!-- YAML
added:
  - v22.3.0
  - v20.18.0
-->

> Stability: 1 - Experimental. Enable this API with the [`--experimental-eventsource`][]
> CLI flag.

A browser-compatible implementation of the [`EventSource`][] class.

## `EventTarget`

<!-- YAML
added: v15.0.0
changes:
  - version: v15.4.0
    pr-url: https://github.com/nodejs/node/pull/35949
    description: No longer experimental.
-->

<!-- type=global -->

A browser-compatible implementation of the `EventTarget` class. See
[`EventTarget` and `Event` API][] for more details.

## `exports`

This variable may appear to be global but is not. See [`exports`][].

## `fetch`

<!-- YAML
added:
  - v17.5.0
  - v16.15.0
changes:
  - version:
    - v21.0.0
    pr-url: https://github.com/nodejs/node/pull/45684
    description: No longer experimental.
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41811
    description: No longer behind `--experimental-fetch` CLI flag.
-->

> Stability: 2 - Stable

A browser-compatible implementation of the [`fetch()`][] function.

## Class: `File`

<!-- YAML
added: v20.0.0
-->

<!-- type=global -->

See {File}.

## Class `FormData`

<!-- YAML
added:
  - v17.6.0
  - v16.15.0
changes:
  - version:
    - v21.0.0
    pr-url: https://github.com/nodejs/node/pull/45684
    description: No longer experimental.
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41811
    description: No longer behind `--experimental-fetch` CLI flag.
-->

> Stability: 2 - Stable

A browser-compatible implementation of {FormData}.

## `global`

<!-- YAML
added: v0.1.27
-->

<!-- type=global -->

> Stability: 3 - Legacy. Use [`globalThis`][] instead.

* {Object} The global namespace object.

In browsers, the top-level scope has traditionally been the global scope. This
means that `var something` will define a new global variable, except within
ECMAScript modules. In Node.js, this is different. The top-level scope is not
the global scope; `var something` inside a Node.js module will be local to that
module, regardless of whether it is a [CommonJS module][] or an
[ECMAScript module][].

## Class `Headers`

<!-- YAML
added:
  - v17.5.0
  - v16.15.0
changes:
  - version:
    - v21.0.0
    pr-url: https://github.com/nodejs/node/pull/45684
    description: No longer experimental.
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41811
    description: No longer behind `--experimental-fetch` CLI flag.
-->

> Stability: 2 - Stable

A browser-compatible implementation of {Headers}.

## `localStorage`

<!-- YAML
added: v22.4.0
-->

> Stability: 1.0 - Early development.

A browser-compatible implementation of [`localStorage`][]. Data is stored
unencrypted in the file specified by the [`--localstorage-file`][] CLI flag.
The maximum amount of data that can be stored is 10 MB.
Any modification of this data outside of the Web Storage API is not supported.
Enable this API with the [`--experimental-webstorage`][] CLI flag.
`localStorage` data is not stored per user or per request when used in the context
of a server, it is shared across all users and requests.

## `MessageChannel`

<!-- YAML
added: v15.0.0
-->

<!-- type=global -->

The `MessageChannel` class. See [`MessageChannel`][] for more details.

## `MessageEvent`

<!-- YAML
added: v15.0.0
-->

<!-- type=global -->

The `MessageEvent` class. See [`MessageEvent`][] for more details.

## `MessagePort`

<!-- YAML
added: v15.0.0
-->

<!-- type=global -->

The `MessagePort` class. See [`MessagePort`][] for more details.

## `module`

This variable may appear to be global but is not. See [`module`][].

## `Navigator`

<!-- YAML
added: v21.0.0
-->

> Stability: 1.1 - Active development. Disable this API with the
> [`--no-experimental-global-navigator`][] CLI flag.

A partial implementation of the [Navigator API][].

## `navigator`

<!-- YAML
added: v21.0.0
-->

> Stability: 1.1 - Active development. Disable this API with the
> [`--no-experimental-global-navigator`][] CLI flag.

A partial implementation of [`window.navigator`][].

### `navigator.hardwareConcurrency`

<!-- YAML
added: v21.0.0
-->

* {number}

The `navigator.hardwareConcurrency` read-only property returns the number of
logical processors available to the current Node.js instance.

```js
console.log(`This process is running on ${navigator.hardwareConcurrency} logical processors`);
```

### `navigator.language`

<!-- YAML
added: v21.2.0
-->

* {string}

The `navigator.language` read-only property returns a string representing the
preferred language of the Node.js instance. The language will be determined by
the ICU library used by Node.js at runtime based on the
default language of the operating system.

The value is representing the language version as defined in [RFC 5646][].

The fallback value on builds without ICU is `'en-US'`.

```js
console.log(`The preferred language of the Node.js instance has the tag '${navigator.language}'`);
```

### `navigator.languages`

<!-- YAML
added: v21.2.0
-->

* {Array<string>}

The `navigator.languages` read-only property returns an array of strings
representing the preferred languages of the Node.js instance.
By default `navigator.languages` contains only the value of
`navigator.language`, which will be determined by the ICU library used by
Node.js at runtime based on the default language of the operating system.

The fallback value on builds without ICU is `['en-US']`.

```js
console.log(`The preferred languages are '${navigator.languages}'`);
```

### `navigator.platform`

<!-- YAML
added: v21.2.0
-->

* {string}

The `navigator.platform` read-only property returns a string identifying the
platform on which the Node.js instance is running.

```js
console.log(`This process is running on ${navigator.platform}`);
```

### `navigator.userAgent`

<!-- YAML
added: v21.1.0
-->

* {string}

The `navigator.userAgent` read-only property returns user agent
consisting of the runtime name and major version number.

```js
console.log(`The user-agent is ${navigator.userAgent}`); // Prints "Node.js/21"
```

## `PerformanceEntry`

<!-- YAML
added: v19.0.0
-->

<!-- type=global -->

The `PerformanceEntry` class. See [`PerformanceEntry`][] for more details.

## `PerformanceMark`

<!-- YAML
added: v19.0.0
-->

<!-- type=global -->

The `PerformanceMark` class. See [`PerformanceMark`][] for more details.

## `PerformanceMeasure`

<!-- YAML
added: v19.0.0
-->

<!-- type=global -->

The `PerformanceMeasure` class. See [`PerformanceMeasure`][] for more details.

## `PerformanceObserver`

<!-- YAML
added: v19.0.0
-->

<!-- type=global -->

The `PerformanceObserver` class. See [`PerformanceObserver`][] for more details.

## `PerformanceObserverEntryList`

<!-- YAML
added: v19.0.0
-->

<!-- type=global -->

The `PerformanceObserverEntryList` class. See
[`PerformanceObserverEntryList`][] for more details.

## `PerformanceResourceTiming`

<!-- YAML
added: v19.0.0
-->

<!-- type=global -->

The `PerformanceResourceTiming` class. See [`PerformanceResourceTiming`][] for
more details.

## `performance`

<!-- YAML
added: v16.0.0
-->

The [`perf_hooks.performance`][] object.

## `process`

<!-- YAML
added: v0.1.7
-->

<!-- type=global -->

* {Object}

The process object. See the [`process` object][] section.

## `queueMicrotask(callback)`

<!-- YAML
added: v11.0.0
-->

<!-- type=global -->

* `callback` {Function} Function to be queued.

The `queueMicrotask()` method queues a microtask to invoke `callback`. If
`callback` throws an exception, the [`process` object][] `'uncaughtException'`
event will be emitted.

The microtask queue is managed by V8 and may be used in a similar manner to
the [`process.nextTick()`][] queue, which is managed by Node.js. The
`process.nextTick()` queue is always processed before the microtask queue
within each turn of the Node.js event loop.

```js
// Here, `queueMicrotask()` is used to ensure the 'load' event is always
// emitted asynchronously, and therefore consistently. Using
// `process.nextTick()` here would result in the 'load' event always emitting
// before any other promise jobs.

DataHandler.prototype.load = async function load(key) {
  const hit = this._cache.get(key);
  if (hit !== undefined) {
    queueMicrotask(() => {
      this.emit('load', hit);
    });
    return;
  }

  const data = await fetchData(key);
  this._cache.set(key, data);
  this.emit('load', data);
};
```

## Class: `ReadableByteStreamController`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`ReadableByteStreamController`][].

## Class: `ReadableStream`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`ReadableStream`][].

## Class: `ReadableStreamBYOBReader`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`ReadableStreamBYOBReader`][].

## Class: `ReadableStreamBYOBRequest`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`ReadableStreamBYOBRequest`][].

## Class: `ReadableStreamDefaultController`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`ReadableStreamDefaultController`][].

## Class: `ReadableStreamDefaultReader`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`ReadableStreamDefaultReader`][].

## `require()`

This variable may appear to be global but is not. See [`require()`][].

## `Response`

<!-- YAML
added:
  - v17.5.0
  - v16.15.0
changes:
  - version:
    - v21.0.0
    pr-url: https://github.com/nodejs/node/pull/45684
    description: No longer experimental.
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41811
    description: No longer behind `--experimental-fetch` CLI flag.
-->

> Stability: 2 - Stable

A browser-compatible implementation of {Response}.

## `Request`

<!-- YAML
added:
  - v17.5.0
  - v16.15.0
changes:
  - version:
    - v21.0.0
    pr-url: https://github.com/nodejs/node/pull/45684
    description: No longer experimental.
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41811
    description: No longer behind `--experimental-fetch` CLI flag.
-->

> Stability: 2 - Stable

A browser-compatible implementation of {Request}.

## `sessionStorage`

<!-- YAML
added: v22.4.0
-->

> Stability: 1.0 - Early development.

A browser-compatible implementation of [`sessionStorage`][]. Data is stored in
memory, with a storage quota of 10 MB. `sessionStorage` data persists only within
the currently running process, and is not shared between workers.

## `setImmediate(callback[, ...args])`

<!-- YAML
added: v0.9.1
-->

<!-- type=global -->

[`setImmediate`][] is described in the [timers][] section.

## `setInterval(callback, delay[, ...args])`

<!-- YAML
added: v0.0.1
-->

<!-- type=global -->

[`setInterval`][] is described in the [timers][] section.

## `setTimeout(callback, delay[, ...args])`

<!-- YAML
added: v0.0.1
-->

<!-- type=global -->

[`setTimeout`][] is described in the [timers][] section.

## Class: `Storage`

<!-- YAML
added: v22.4.0
-->

> Stability: 1.0 - Early development.

A browser-compatible implementation of [`Storage`][]. Enable this API with the
[`--experimental-webstorage`][] CLI flag.

## `structuredClone(value[, options])`

<!-- YAML
added: v17.0.0
-->

<!-- type=global -->

The WHATWG [`structuredClone`][] method.

## `SubtleCrypto`

<!-- YAML
added:
  - v17.6.0
  - v16.15.0
changes:
  - version: v19.0.0
    pr-url: https://github.com/nodejs/node/pull/42083
    description: No longer behind `--experimental-global-webcrypto` CLI flag.
-->

> Stability: 2 - Stable.

A browser-compatible implementation of {SubtleCrypto}. This global is available
only if the Node.js binary was compiled with including support for the
`node:crypto` module.

## `DOMException`

<!-- YAML
added: v17.0.0
-->

<!-- type=global -->

The WHATWG `DOMException` class. See [`DOMException`][] for more details.

## `TextDecoder`

<!-- YAML
added: v11.0.0
-->

<!-- type=global -->

The WHATWG `TextDecoder` class. See the [`TextDecoder`][] section.

## Class: `TextDecoderStream`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`TextDecoderStream`][].

## `TextEncoder`

<!-- YAML
added: v11.0.0
-->

<!-- type=global -->

The WHATWG `TextEncoder` class. See the [`TextEncoder`][] section.

## Class: `TextEncoderStream`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`TextEncoderStream`][].

## Class: `TransformStream`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`TransformStream`][].

## Class: `TransformStreamDefaultController`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`TransformStreamDefaultController`][].

## `URL`

<!-- YAML
added: v10.0.0
-->

<!-- type=global -->

The WHATWG `URL` class. See the [`URL`][] section.

## `URLSearchParams`

<!-- YAML
added: v10.0.0
-->

<!-- type=global -->

The WHATWG `URLSearchParams` class. See the [`URLSearchParams`][] section.

## `WebAssembly`

<!-- YAML
added: v8.0.0
-->

<!-- type=global -->

* {Object}

The object that acts as the namespace for all W3C
[WebAssembly][webassembly-org] related functionality. See the
[Mozilla Developer Network][webassembly-mdn] for usage and compatibility.

## `WebSocket`

<!-- YAML
added:
  - v21.0.0
  - v20.10.0
changes:
  - version: v22.4.0
    pr-url: https://github.com/nodejs/node/pull/53352
    description: No longer experimental.
  - version: v22.0.0
    pr-url: https://github.com/nodejs/node/pull/51594
    description: No longer behind `--experimental-websocket` CLI flag.
-->

> Stability: 2 - Stable.

A browser-compatible implementation of [`WebSocket`][]. Disable this API
with the [`--no-experimental-websocket`][] CLI flag.

## Class: `WritableStream`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`WritableStream`][].

## Class: `WritableStreamDefaultController`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`WritableStreamDefaultController`][].

## Class: `WritableStreamDefaultWriter`

<!-- YAML
added: v18.0.0
-->

> Stability: 1 - Experimental.

A browser-compatible implementation of [`WritableStreamDefaultWriter`][].

[CommonJS module]: modules.md
[CommonJS modules]: modules.md
[ECMAScript module]: esm.md
[Navigator API]: https://html.spec.whatwg.org/multipage/system-state.html#the-navigator-object
[RFC 5646]: https://www.rfc-editor.org/rfc/rfc5646.txt
[Web Crypto API]: webcrypto.md
[`--experimental-eventsource`]: cli.md#--experimental-eventsource
[`--experimental-webstorage`]: cli.md#--experimental-webstorage
[`--localstorage-file`]: cli.md#--localstorage-filefile
[`--no-experimental-global-navigator`]: cli.md#--no-experimental-global-navigator
[`--no-experimental-websocket`]: cli.md#--no-experimental-websocket
[`AbortController`]: https://developer.mozilla.org/en-US/docs/Web/API/AbortController
[`ByteLengthQueuingStrategy`]: webstreams.md#class-bytelengthqueuingstrategy
[`CloseEvent`]: https://developer.mozilla.org/en-US/docs/Web/API/CloseEvent/CloseEvent
[`CompressionStream`]: webstreams.md#class-compressionstream
[`CountQueuingStrategy`]: webstreams.md#class-countqueuingstrategy
[`CustomEvent` Web API]: https://dom.spec.whatwg.org/#customevent
[`DOMException`]: https://developer.mozilla.org/en-US/docs/Web/API/DOMException
[`DecompressionStream`]: webstreams.md#class-decompressionstream
[`EventSource`]: https://developer.mozilla.org/en-US/docs/Web/API/EventSource
[`EventTarget` and `Event` API]: events.md#eventtarget-and-event-api
[`MessageChannel`]: worker_threads.md#class-messagechannel
[`MessageEvent`]: https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent/MessageEvent
[`MessagePort`]: worker_threads.md#class-messageport
[`PerformanceEntry`]: perf_hooks.md#class-performanceentry
[`PerformanceMark`]: perf_hooks.md#class-performancemark
[`PerformanceMeasure`]: perf_hooks.md#class-performancemeasure
[`PerformanceObserverEntryList`]: perf_hooks.md#class-performanceobserverentrylist
[`PerformanceObserver`]: perf_hooks.md#class-performanceobserver
[`PerformanceResourceTiming`]: perf_hooks.md#class-performanceresourcetiming
[`ReadableByteStreamController`]: webstreams.md#class-readablebytestreamcontroller
[`ReadableStreamBYOBReader`]: webstreams.md#class-readablestreambyobreader
[`ReadableStreamBYOBRequest`]: webstreams.md#class-readablestreambyobrequest
[`ReadableStreamDefaultController`]: webstreams.md#class-readablestreamdefaultcontroller
[`ReadableStreamDefaultReader`]: webstreams.md#class-readablestreamdefaultreader
[`ReadableStream`]: webstreams.md#class-readablestream
[`Storage`]: https://developer.mozilla.org/en-US/docs/Web/API/Storage
[`TextDecoderStream`]: webstreams.md#class-textdecoderstream
[`TextDecoder`]: util.md#class-utiltextdecoder
[`TextEncoderStream`]: webstreams.md#class-textencoderstream
[`TextEncoder`]: util.md#class-utiltextencoder
[`TransformStreamDefaultController`]: webstreams.md#class-transformstreamdefaultcontroller
[`TransformStream`]: webstreams.md#class-transformstream
[`URLSearchParams`]: url.md#class-urlsearchparams
[`URL`]: url.md#class-url
[`WebSocket`]: https://developer.mozilla.org/en-US/docs/Web/API/WebSocket
[`WritableStreamDefaultController`]: webstreams.md#class-writablestreamdefaultcontroller
[`WritableStreamDefaultWriter`]: webstreams.md#class-writablestreamdefaultwriter
[`WritableStream`]: webstreams.md#class-writablestream
[`__dirname`]: modules.md#__dirname
[`__filename`]: modules.md#__filename
[`abortSignal.reason`]: #abortsignalreason
[`buffer.atob()`]: buffer.md#bufferatobdata
[`buffer.btoa()`]: buffer.md#bufferbtoadata
[`clearImmediate`]: timers.md#clearimmediateimmediate
[`clearInterval`]: timers.md#clearintervaltimeout
[`clearTimeout`]: timers.md#cleartimeouttimeout
[`console`]: console.md
[`exports`]: modules.md#exports
[`fetch()`]: https://developer.mozilla.org/en-US/docs/Web/API/fetch
[`globalThis`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/globalThis
[`localStorage`]: https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage
[`module`]: modules.md#module
[`perf_hooks.performance`]: perf_hooks.md#perf_hooksperformance
[`process.nextTick()`]: process.md#processnexttickcallback-args
[`process` object]: process.md#process
[`require()`]: modules.md#requireid
[`sessionStorage`]: https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage
[`setImmediate`]: timers.md#setimmediatecallback-args
[`setInterval`]: timers.md#setintervalcallback-delay-args
[`setTimeout`]: timers.md#settimeoutcallback-delay-args
[`structuredClone`]: https://developer.mozilla.org/en-US/docs/Web/API/structuredClone
[`window.navigator`]: https://developer.mozilla.org/en-US/docs/Web/API/Window/navigator
[buffer section]: buffer.md
[built-in objects]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects
[timers]: timers.md
[webassembly-mdn]: https://developer.mozilla.org/en-US/docs/WebAssembly
[webassembly-org]: https://webassembly.org


# Console

<!--introduced_in=v0.10.13-->

> Stability: 2 - Stable

<!-- source_link=lib/console.js -->

The `node:console` module provides a simple debugging console that is similar to
the JavaScript console mechanism provided by web browsers.

The module exports two specific components:

* A `Console` class with methods such as `console.log()`, `console.error()`, and
  `console.warn()` that can be used to write to any Node.js stream.
* A global `console` instance configured to write to [`process.stdout`][] and
  [`process.stderr`][]. The global `console` can be used without calling
  `require('node:console')`.

_**Warning**_: The global console object's methods are neither consistently
synchronous like the browser APIs they resemble, nor are they consistently
asynchronous like all other Node.js streams. Programs that desire to depend
on the synchronous / asynchronous behavior of the console functions should
first figure out the nature of console's backing stream. This is because the
stream is dependent on the underlying platform and standard stream
configuration of the current process. See the [note on process I/O][] for
more information.

Example using the global `console`:

```js
console.log('hello world');
// Prints: hello world, to stdout
console.log('hello %s', 'world');
// Prints: hello world, to stdout
console.error(new Error('Whoops, something bad happened'));
// Prints error message and stack trace to stderr:
//   Error: Whoops, something bad happened
//     at [eval]:5:15
//     at Script.runInThisContext (node:vm:132:18)
//     at Object.runInThisContext (node:vm:309:38)
//     at node:internal/process/execution:77:19
//     at [eval]-wrapper:6:22
//     at evalScript (node:internal/process/execution:76:60)
//     at node:internal/main/eval_string:23:3

const name = 'Will Robinson';
console.warn(`Danger ${name}! Danger!`);
// Prints: Danger Will Robinson! Danger!, to stderr
```

Example using the `Console` class:

```js
const out = getStreamSomehow();
const err = getStreamSomehow();
const myConsole = new console.Console(out, err);

myConsole.log('hello world');
// Prints: hello world, to out
myConsole.log('hello %s', 'world');
// Prints: hello world, to out
myConsole.error(new Error('Whoops, something bad happened'));
// Prints: [Error: Whoops, something bad happened], to err

const name = 'Will Robinson';
myConsole.warn(`Danger ${name}! Danger!`);
// Prints: Danger Will Robinson! Danger!, to err
```

## Class: `Console`

<!-- YAML
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9744
    description: Errors that occur while writing to the underlying streams
                 will now be ignored by default.
-->

<!--type=class-->

The `Console` class can be used to create a simple logger with configurable
output streams and can be accessed using either `require('node:console').Console`
or `console.Console` (or their destructured counterparts):

```mjs
import { Console } from 'node:console';
```

```cjs
const { Console } = require('node:console');
```

```js
const { Console } = console;
```

### `new Console(stdout[, stderr][, ignoreErrors])`

### `new Console(options)`

<!-- YAML
changes:
  - version:
     - v14.2.0
     - v12.17.0
    pr-url: https://github.com/nodejs/node/pull/32964
    description: The `groupIndentation` option was introduced.
  - version: v11.7.0
    pr-url: https://github.com/nodejs/node/pull/24978
    description: The `inspectOptions` option is introduced.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19372
    description: The `Console` constructor now supports an `options` argument,
                 and the `colorMode` option was introduced.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9744
    description: The `ignoreErrors` option was introduced.
-->

* `options` {Object}
  * `stdout` {stream.Writable}
  * `stderr` {stream.Writable}
  * `ignoreErrors` {boolean} Ignore errors when writing to the underlying
    streams. **Default:** `true`.
  * `colorMode` {boolean|string} Set color support for this `Console` instance.
    Setting to `true` enables coloring while inspecting values. Setting to
    `false` disables coloring while inspecting values. Setting to
    `'auto'` makes color support depend on the value of the `isTTY` property
    and the value returned by `getColorDepth()` on the respective stream. This
    option can not be used, if `inspectOptions.colors` is set as well.
    **Default:** `'auto'`.
  * `inspectOptions` {Object} Specifies options that are passed along to
    [`util.inspect()`][].
  * `groupIndentation` {number} Set group indentation.
    **Default:** `2`.

Creates a new `Console` with one or two writable stream instances. `stdout` is a
writable stream to print log or info output. `stderr` is used for warning or
error output. If `stderr` is not provided, `stdout` is used for `stderr`.

```mjs
import { createWriteStream } from 'node:fs';
import { Console } from 'node:console';
// Alternatively
// const { Console } = console;

const output = createWriteStream('./stdout.log');
const errorOutput = createWriteStream('./stderr.log');
// Custom simple logger
const logger = new Console({ stdout: output, stderr: errorOutput });
// use it like console
const count = 5;
logger.log('count: %d', count);
// In stdout.log: count 5
```

```cjs
const fs = require('node:fs');
const { Console } = require('node:console');
// Alternatively
// const { Console } = console;

const output = fs.createWriteStream('./stdout.log');
const errorOutput = fs.createWriteStream('./stderr.log');
// Custom simple logger
const logger = new Console({ stdout: output, stderr: errorOutput });
// use it like console
const count = 5;
logger.log('count: %d', count);
// In stdout.log: count 5
```

The global `console` is a special `Console` whose output is sent to
[`process.stdout`][] and [`process.stderr`][]. It is equivalent to calling:

```js
new Console({ stdout: process.stdout, stderr: process.stderr });
```

### `console.assert(value[, ...message])`

<!-- YAML
added: v0.1.101
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17706
    description: The implementation is now spec compliant and does not throw
                 anymore.
-->

* `value` {any} The value tested for being truthy.
* `...message` {any} All arguments besides `value` are used as error message.

`console.assert()` writes a message if `value` is [falsy][] or omitted. It only
writes a message and does not otherwise affect execution. The output always
starts with `"Assertion failed"`. If provided, `message` is formatted using
[`util.format()`][].

If `value` is [truthy][], nothing happens.

```js
console.assert(true, 'does nothing');

console.assert(false, 'Whoops %s work', 'didn\'t');
// Assertion failed: Whoops didn't work

console.assert();
// Assertion failed
```

### `console.clear()`

<!-- YAML
added: v8.3.0
-->

When `stdout` is a TTY, calling `console.clear()` will attempt to clear the
TTY. When `stdout` is not a TTY, this method does nothing.

The specific operation of `console.clear()` can vary across operating systems
and terminal types. For most Linux operating systems, `console.clear()`
operates similarly to the `clear` shell command. On Windows, `console.clear()`
will clear only the output in the current terminal viewport for the Node.js
binary.

### `console.count([label])`

<!-- YAML
added: v8.3.0
-->

* `label` {string} The display label for the counter. **Default:** `'default'`.

Maintains an internal counter specific to `label` and outputs to `stdout` the
number of times `console.count()` has been called with the given `label`.

<!-- eslint-skip -->

```js
> console.count()
default: 1
undefined
> console.count('default')
default: 2
undefined
> console.count('abc')
abc: 1
undefined
> console.count('xyz')
xyz: 1
undefined
> console.count('abc')
abc: 2
undefined
> console.count()
default: 3
undefined
>
```

### `console.countReset([label])`

<!-- YAML
added: v8.3.0
-->

* `label` {string} The display label for the counter. **Default:** `'default'`.

Resets the internal counter specific to `label`.

<!-- eslint-skip -->

```js
> console.count('abc');
abc: 1
undefined
> console.countReset('abc');
undefined
> console.count('abc');
abc: 1
undefined
>
```

### `console.debug(data[, ...args])`

<!-- YAML
added: v8.0.0
changes:
  - version: v8.10.0
    pr-url: https://github.com/nodejs/node/pull/17033
    description: "`console.debug` is now an alias for `console.log`."
-->

* `data` {any}
* `...args` {any}

The `console.debug()` function is an alias for [`console.log()`][].

### `console.dir(obj[, options])`

<!-- YAML
added: v0.1.101
-->

* `obj` {any}
* `options` {Object}
  * `showHidden` {boolean} If `true` then the object's non-enumerable and symbol
    properties will be shown too. **Default:** `false`.
  * `depth` {number} Tells [`util.inspect()`][] how many times to recurse while
    formatting the object. This is useful for inspecting large complicated
    objects. To make it recurse indefinitely, pass `null`. **Default:** `2`.
  * `colors` {boolean} If `true`, then the output will be styled with ANSI color
    codes. Colors are customizable;
    see [customizing `util.inspect()` colors][]. **Default:** `false`.

Uses [`util.inspect()`][] on `obj` and prints the resulting string to `stdout`.
This function bypasses any custom `inspect()` function defined on `obj`.

### `console.dirxml(...data)`

<!-- YAML
added: v8.0.0
changes:
  - version: v9.3.0
    pr-url: https://github.com/nodejs/node/pull/17152
    description: "`console.dirxml` now calls `console.log` for its arguments."
-->

* `...data` {any}

This method calls `console.log()` passing it the arguments received.
This method does not produce any XML formatting.

### `console.error([data][, ...args])`

<!-- YAML
added: v0.1.100
-->

* `data` {any}
* `...args` {any}

Prints to `stderr` with newline. Multiple arguments can be passed, with the
first used as the primary message and all additional used as substitution
values similar to printf(3) (the arguments are all passed to
[`util.format()`][]).

```js
const code = 5;
console.error('error #%d', code);
// Prints: error #5, to stderr
console.error('error', code);
// Prints: error 5, to stderr
```

If formatting elements (e.g. `%d`) are not found in the first string then
[`util.inspect()`][] is called on each argument and the resulting string
values are concatenated. See [`util.format()`][] for more information.

### `console.group([...label])`

<!-- YAML
added: v8.5.0
-->

* `...label` {any}

Increases indentation of subsequent lines by spaces for `groupIndentation`
length.

If one or more `label`s are provided, those are printed first without the
additional indentation.

### `console.groupCollapsed()`

<!-- YAML
  added: v8.5.0
-->

An alias for [`console.group()`][].

### `console.groupEnd()`

<!-- YAML
added: v8.5.0
-->

Decreases indentation of subsequent lines by spaces for `groupIndentation`
length.

### `console.info([data][, ...args])`

<!-- YAML
added: v0.1.100
-->

* `data` {any}
* `...args` {any}

The `console.info()` function is an alias for [`console.log()`][].

### `console.log([data][, ...args])`

<!-- YAML
added: v0.1.100
-->

* `data` {any}
* `...args` {any}

Prints to `stdout` with newline. Multiple arguments can be passed, with the
first used as the primary message and all additional used as substitution
values similar to printf(3) (the arguments are all passed to
[`util.format()`][]).

```js
const count = 5;
console.log('count: %d', count);
// Prints: count: 5, to stdout
console.log('count:', count);
// Prints: count: 5, to stdout
```

See [`util.format()`][] for more information.

### `console.table(tabularData[, properties])`

<!-- YAML
added: v10.0.0
-->

* `tabularData` {any}
* `properties` {string\[]} Alternate properties for constructing the table.

Try to construct a table with the columns of the properties of `tabularData`
(or use `properties`) and rows of `tabularData` and log it. Falls back to just
logging the argument if it can't be parsed as tabular.

```js
// These can't be parsed as tabular data
console.table(Symbol());
// Symbol()

console.table(undefined);
// undefined

console.table([{ a: 1, b: 'Y' }, { a: 'Z', b: 2 }]);
// ┌─────────┬─────┬─────┐
// │ (index) │ a   │ b   │
// ├─────────┼─────┼─────┤
// │ 0       │ 1   │ 'Y' │
// │ 1       │ 'Z' │ 2   │
// └─────────┴─────┴─────┘

console.table([{ a: 1, b: 'Y' }, { a: 'Z', b: 2 }], ['a']);
// ┌─────────┬─────┐
// │ (index) │ a   │
// ├─────────┼─────┤
// │ 0       │ 1   │
// │ 1       │ 'Z' │
// └─────────┴─────┘
```

### `console.time([label])`

<!-- YAML
added: v0.1.104
-->

* `label` {string} **Default:** `'default'`

Starts a timer that can be used to compute the duration of an operation. Timers
are identified by a unique `label`. Use the same `label` when calling
[`console.timeEnd()`][] to stop the timer and output the elapsed time in
suitable time units to `stdout`. For example, if the elapsed
time is 3869ms, `console.timeEnd()` displays "3.869s".

### `console.timeEnd([label])`

<!-- YAML
added: v0.1.104
changes:
  - version: v13.0.0
    pr-url: https://github.com/nodejs/node/pull/29251
    description: The elapsed time is displayed with a suitable time unit.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5901
    description: This method no longer supports multiple calls that don't map
                 to individual `console.time()` calls; see below for details.
-->

* `label` {string} **Default:** `'default'`

Stops a timer that was previously started by calling [`console.time()`][] and
prints the result to `stdout`:

```js
console.time('bunch-of-stuff');
// Do a bunch of stuff.
console.timeEnd('bunch-of-stuff');
// Prints: bunch-of-stuff: 225.438ms
```

### `console.timeLog([label][, ...data])`

<!-- YAML
added: v10.7.0
-->

* `label` {string} **Default:** `'default'`
* `...data` {any}

For a timer that was previously started by calling [`console.time()`][], prints
the elapsed time and other `data` arguments to `stdout`:

```js
console.time('process');
const value = expensiveProcess1(); // Returns 42
console.timeLog('process', value);
// Prints "process: 365.227ms 42".
doExpensiveProcess2(value);
console.timeEnd('process');
```

### `console.trace([message][, ...args])`

<!-- YAML
added: v0.1.104
-->

* `message` {any}
* `...args` {any}

Prints to `stderr` the string `'Trace: '`, followed by the [`util.format()`][]
formatted message and stack trace to the current position in the code.

```js
console.trace('Show me');
// Prints: (stack trace will vary based on where trace is called)
//  Trace: Show me
//    at repl:2:9
//    at REPLServer.defaultEval (repl.js:248:27)
//    at bound (domain.js:287:14)
//    at REPLServer.runBound [as eval] (domain.js:300:12)
//    at REPLServer.<anonymous> (repl.js:412:12)
//    at emitOne (events.js:82:20)
//    at REPLServer.emit (events.js:169:7)
//    at REPLServer.Interface._onLine (readline.js:210:10)
//    at REPLServer.Interface._line (readline.js:549:8)
//    at REPLServer.Interface._ttyWrite (readline.js:826:14)
```

### `console.warn([data][, ...args])`

<!-- YAML
added: v0.1.100
-->

* `data` {any}
* `...args` {any}

The `console.warn()` function is an alias for [`console.error()`][].

## Inspector only methods

The following methods are exposed by the V8 engine in the general API but do
not display anything unless used in conjunction with the [inspector][]
(`--inspect` flag).

### `console.profile([label])`

<!-- YAML
added: v8.0.0
-->

* `label` {string}

This method does not display anything unless used in the inspector. The
`console.profile()` method starts a JavaScript CPU profile with an optional
label until [`console.profileEnd()`][] is called. The profile is then added to
the **Profile** panel of the inspector.

```js
console.profile('MyLabel');
// Some code
console.profileEnd('MyLabel');
// Adds the profile 'MyLabel' to the Profiles panel of the inspector.
```

### `console.profileEnd([label])`

<!-- YAML
added: v8.0.0
-->

* `label` {string}

This method does not display anything unless used in the inspector. Stops the
current JavaScript CPU profiling session if one has been started and prints
the report to the **Profiles** panel of the inspector. See
[`console.profile()`][] for an example.

If this method is called without a label, the most recently started profile is
stopped.

### `console.timeStamp([label])`

<!-- YAML
added: v8.0.0
-->

* `label` {string}

This method does not display anything unless used in the inspector. The
`console.timeStamp()` method adds an event with the label `'label'` to the
**Timeline** panel of the inspector.

[`console.error()`]: #consoleerrordata-args
[`console.group()`]: #consolegrouplabel
[`console.log()`]: #consolelogdata-args
[`console.profile()`]: #consoleprofilelabel
[`console.profileEnd()`]: #consoleprofileendlabel
[`console.time()`]: #consoletimelabel
[`console.timeEnd()`]: #consoletimeendlabel
[`process.stderr`]: process.md#processstderr
[`process.stdout`]: process.md#processstdout
[`util.format()`]: util.md#utilformatformat-args
[`util.inspect()`]: util.md#utilinspectobject-options
[customizing `util.inspect()` colors]: util.md#customizing-utilinspect-colors
[falsy]: https://developer.mozilla.org/en-US/docs/Glossary/Falsy
[inspector]: debugger.md
[note on process I/O]: process.md#a-note-on-process-io
[truthy]: https://developer.mozilla.org/en-US/docs/Glossary/Truthy

# Timers

<!--introduced_in=v0.10.0-->

> Stability: 2 - Stable

<!-- source_link=lib/timers.js -->

The `timer` module exposes a global API for scheduling functions to
be called at some future period of time. Because the timer functions are
globals, there is no need to call `require('node:timers')` to use the API.

The timer functions within Node.js implement a similar API as the timers API
provided by Web Browsers but use a different internal implementation that is
built around the Node.js [Event Loop][].

## Class: `Immediate`

This object is created internally and is returned from [`setImmediate()`][]. It
can be passed to [`clearImmediate()`][] in order to cancel the scheduled
actions.

By default, when an immediate is scheduled, the Node.js event loop will continue
running as long as the immediate is active. The `Immediate` object returned by
[`setImmediate()`][] exports both `immediate.ref()` and `immediate.unref()`
functions that can be used to control this default behavior.

### `immediate.hasRef()`

<!-- YAML
added: v11.0.0
-->

* Returns: {boolean}

If true, the `Immediate` object will keep the Node.js event loop active.

### `immediate.ref()`

<!-- YAML
added: v9.7.0
-->

* Returns: {Immediate} a reference to `immediate`

When called, requests that the Node.js event loop _not_ exit so long as the
`Immediate` is active. Calling `immediate.ref()` multiple times will have no
effect.

By default, all `Immediate` objects are "ref'ed", making it normally unnecessary
to call `immediate.ref()` unless `immediate.unref()` had been called previously.

### `immediate.unref()`

<!-- YAML
added: v9.7.0
-->

* Returns: {Immediate} a reference to `immediate`

When called, the active `Immediate` object will not require the Node.js event
loop to remain active. If there is no other activity keeping the event loop
running, the process may exit before the `Immediate` object's callback is
invoked. Calling `immediate.unref()` multiple times will have no effect.

### `immediate[Symbol.dispose]()`

<!-- YAML
added:
 - v20.5.0
 - v18.18.0
-->

> Stability: 1 - Experimental

Cancels the immediate. This is similar to calling `clearImmediate()`.

## Class: `Timeout`

This object is created internally and is returned from [`setTimeout()`][] and
[`setInterval()`][]. It can be passed to either [`clearTimeout()`][] or
[`clearInterval()`][] in order to cancel the scheduled actions.

By default, when a timer is scheduled using either [`setTimeout()`][] or
[`setInterval()`][], the Node.js event loop will continue running as long as the
timer is active. Each of the `Timeout` objects returned by these functions
export both `timeout.ref()` and `timeout.unref()` functions that can be used to
control this default behavior.

### `timeout.close()`

<!-- YAML
added: v0.9.1
-->

> Stability: 3 - Legacy: Use [`clearTimeout()`][] instead.

* Returns: {Timeout} a reference to `timeout`

Cancels the timeout.

### `timeout.hasRef()`

<!-- YAML
added: v11.0.0
-->

* Returns: {boolean}

If true, the `Timeout` object will keep the Node.js event loop active.

### `timeout.ref()`

<!-- YAML
added: v0.9.1
-->

* Returns: {Timeout} a reference to `timeout`

When called, requests that the Node.js event loop _not_ exit so long as the
`Timeout` is active. Calling `timeout.ref()` multiple times will have no effect.

By default, all `Timeout` objects are "ref'ed", making it normally unnecessary
to call `timeout.ref()` unless `timeout.unref()` had been called previously.

### `timeout.refresh()`

<!-- YAML
added: v10.2.0
-->

* Returns: {Timeout} a reference to `timeout`

Sets the timer's start time to the current time, and reschedules the timer to
call its callback at the previously specified duration adjusted to the current
time. This is useful for refreshing a timer without allocating a new
JavaScript object.

Using this on a timer that has already called its callback will reactivate the
timer.

### `timeout.unref()`

<!-- YAML
added: v0.9.1
-->

* Returns: {Timeout} a reference to `timeout`

When called, the active `Timeout` object will not require the Node.js event loop
to remain active. If there is no other activity keeping the event loop running,
the process may exit before the `Timeout` object's callback is invoked. Calling
`timeout.unref()` multiple times will have no effect.

### `timeout[Symbol.toPrimitive]()`

<!-- YAML
added:
  - v14.9.0
  - v12.19.0
-->

* Returns: {integer} a number that can be used to reference this `timeout`

Coerce a `Timeout` to a primitive. The primitive can be used to
clear the `Timeout`. The primitive can only be used in the
same thread where the timeout was created. Therefore, to use it
across [`worker_threads`][] it must first be passed to the correct
thread. This allows enhanced compatibility with browser
`setTimeout()` and `setInterval()` implementations.

### `timeout[Symbol.dispose]()`

<!-- YAML
added:
 - v20.5.0
 - v18.18.0
-->

> Stability: 1 - Experimental

Cancels the timeout.

## Scheduling timers

A timer in Node.js is an internal construct that calls a given function after
a certain period of time. When a timer's function is called varies depending on
which method was used to create the timer and what other work the Node.js
event loop is doing.

### `setImmediate(callback[, ...args])`

<!-- YAML
added: v0.9.1
changes:
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41678
    description: Passing an invalid callback to the `callback` argument
                 now throws `ERR_INVALID_ARG_TYPE` instead of
                 `ERR_INVALID_CALLBACK`.
-->

* `callback` {Function} The function to call at the end of this turn of
  the Node.js [Event Loop][]
* `...args` {any} Optional arguments to pass when the `callback` is called.
* Returns: {Immediate} for use with [`clearImmediate()`][]

Schedules the "immediate" execution of the `callback` after I/O events'
callbacks.

When multiple calls to `setImmediate()` are made, the `callback` functions are
queued for execution in the order in which they are created. The entire callback
queue is processed every event loop iteration. If an immediate timer is queued
from inside an executing callback, that timer will not be triggered until the
next event loop iteration.

If `callback` is not a function, a [`TypeError`][] will be thrown.

This method has a custom variant for promises that is available using
[`timersPromises.setImmediate()`][].

### `setInterval(callback[, delay[, ...args]])`

<!-- YAML
added: v0.0.1
changes:
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41678
    description: Passing an invalid callback to the `callback` argument
                 now throws `ERR_INVALID_ARG_TYPE` instead of
                 `ERR_INVALID_CALLBACK`.
-->

* `callback` {Function} The function to call when the timer elapses.
* `delay` {number} The number of milliseconds to wait before calling the
  `callback`. **Default:** `1`.
* `...args` {any} Optional arguments to pass when the `callback` is called.
* Returns: {Timeout} for use with [`clearInterval()`][]

Schedules repeated execution of `callback` every `delay` milliseconds.

When `delay` is larger than `2147483647` or less than `1` or `NaN`, the `delay`
will be set to `1`. Non-integer delays are truncated to an integer.

If `callback` is not a function, a [`TypeError`][] will be thrown.

This method has a custom variant for promises that is available using
[`timersPromises.setInterval()`][].

### `setTimeout(callback[, delay[, ...args]])`

<!-- YAML
added: v0.0.1
changes:
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41678
    description: Passing an invalid callback to the `callback` argument
                 now throws `ERR_INVALID_ARG_TYPE` instead of
                 `ERR_INVALID_CALLBACK`.
-->

* `callback` {Function} The function to call when the timer elapses.
* `delay` {number} The number of milliseconds to wait before calling the
  `callback`. **Default:** `1`.
* `...args` {any} Optional arguments to pass when the `callback` is called.
* Returns: {Timeout} for use with [`clearTimeout()`][]

Schedules execution of a one-time `callback` after `delay` milliseconds.

The `callback` will likely not be invoked in precisely `delay` milliseconds.
Node.js makes no guarantees about the exact timing of when callbacks will fire,
nor of their ordering. The callback will be called as close as possible to the
time specified.

When `delay` is larger than `2147483647` or less than `1` or `NaN`, the `delay`
will be set to `1`. Non-integer delays are truncated to an integer.

If `callback` is not a function, a [`TypeError`][] will be thrown.

This method has a custom variant for promises that is available using
[`timersPromises.setTimeout()`][].

## Cancelling timers

The [`setImmediate()`][], [`setInterval()`][], and [`setTimeout()`][] methods
each return objects that represent the scheduled timers. These can be used to
cancel the timer and prevent it from triggering.

For the promisified variants of [`setImmediate()`][] and [`setTimeout()`][],
an [`AbortController`][] may be used to cancel the timer. When canceled, the
returned Promises will be rejected with an `'AbortError'`.

For `setImmediate()`:

```mjs
import { setImmediate as setImmediatePromise } from 'node:timers/promises';

const ac = new AbortController();
const signal = ac.signal;

// We do not `await` the promise so `ac.abort()` is called concurrently.
setImmediatePromise('foobar', { signal })
  .then(console.log)
  .catch((err) => {
    if (err.name === 'AbortError')
      console.error('The immediate was aborted');
  });

ac.abort();
```

```cjs
const { setImmediate: setImmediatePromise } = require('node:timers/promises');

const ac = new AbortController();
const signal = ac.signal;

setImmediatePromise('foobar', { signal })
  .then(console.log)
  .catch((err) => {
    if (err.name === 'AbortError')
      console.error('The immediate was aborted');
  });

ac.abort();
```

For `setTimeout()`:

```mjs
import { setTimeout as setTimeoutPromise } from 'node:timers/promises';

const ac = new AbortController();
const signal = ac.signal;

// We do not `await` the promise so `ac.abort()` is called concurrently.
setTimeoutPromise(1000, 'foobar', { signal })
  .then(console.log)
  .catch((err) => {
    if (err.name === 'AbortError')
      console.error('The timeout was aborted');
  });

ac.abort();
```

```cjs
const { setTimeout: setTimeoutPromise } = require('node:timers/promises');

const ac = new AbortController();
const signal = ac.signal;

setTimeoutPromise(1000, 'foobar', { signal })
  .then(console.log)
  .catch((err) => {
    if (err.name === 'AbortError')
      console.error('The timeout was aborted');
  });

ac.abort();
```

### `clearImmediate(immediate)`

<!-- YAML
added: v0.9.1
-->

* `immediate` {Immediate} An `Immediate` object as returned by
  [`setImmediate()`][].

Cancels an `Immediate` object created by [`setImmediate()`][].

### `clearInterval(timeout)`

<!-- YAML
added: v0.0.1
-->

* `timeout` {Timeout|string|number} A `Timeout` object as returned by [`setInterval()`][]
  or the [primitive][] of the `Timeout` object as a string or a number.

Cancels a `Timeout` object created by [`setInterval()`][].

### `clearTimeout(timeout)`

<!-- YAML
added: v0.0.1
-->

* `timeout` {Timeout|string|number} A `Timeout` object as returned by [`setTimeout()`][]
  or the [primitive][] of the `Timeout` object as a string or a number.

Cancels a `Timeout` object created by [`setTimeout()`][].

## Timers Promises API

<!-- YAML
added: v15.0.0
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/38112
    description: Graduated from experimental.
-->

The `timers/promises` API provides an alternative set of timer functions
that return `Promise` objects. The API is accessible via
`require('node:timers/promises')`.

```mjs
import {
  setTimeout,
  setImmediate,
  setInterval,
} from 'node:timers/promises';
```

```cjs
const {
  setTimeout,
  setImmediate,
  setInterval,
} = require('node:timers/promises');
```

### `timersPromises.setTimeout([delay[, value[, options]]])`

<!-- YAML
added: v15.0.0
-->

* `delay` {number} The number of milliseconds to wait before fulfilling the
  promise. **Default:** `1`.
* `value` {any} A value with which the promise is fulfilled.
* `options` {Object}
  * `ref` {boolean} Set to `false` to indicate that the scheduled `Timeout`
    should not require the Node.js event loop to remain active.
    **Default:** `true`.
  * `signal` {AbortSignal} An optional `AbortSignal` that can be used to
    cancel the scheduled `Timeout`.

```mjs
import {
  setTimeout,
} from 'node:timers/promises';

const res = await setTimeout(100, 'result');

console.log(res);  // Prints 'result'
```

```cjs
const {
  setTimeout,
} = require('node:timers/promises');

setTimeout(100, 'result').then((res) => {
  console.log(res);  // Prints 'result'
});
```

### `timersPromises.setImmediate([value[, options]])`

<!-- YAML
added: v15.0.0
-->

* `value` {any} A value with which the promise is fulfilled.
* `options` {Object}
  * `ref` {boolean} Set to `false` to indicate that the scheduled `Immediate`
    should not require the Node.js event loop to remain active.
    **Default:** `true`.
  * `signal` {AbortSignal} An optional `AbortSignal` that can be used to
    cancel the scheduled `Immediate`.

```mjs
import {
  setImmediate,
} from 'node:timers/promises';

const res = await setImmediate('result');

console.log(res);  // Prints 'result'
```

```cjs
const {
  setImmediate,
} = require('node:timers/promises');

setImmediate('result').then((res) => {
  console.log(res);  // Prints 'result'
});
```

### `timersPromises.setInterval([delay[, value[, options]]])`

<!-- YAML
added: v15.9.0
-->

Returns an async iterator that generates values in an interval of `delay` ms.
If `ref` is `true`, you need to call `next()` of async iterator explicitly
or implicitly to keep the event loop alive.

* `delay` {number} The number of milliseconds to wait between iterations.
  **Default:** `1`.
* `value` {any} A value with which the iterator returns.
* `options` {Object}
  * `ref` {boolean} Set to `false` to indicate that the scheduled `Timeout`
    between iterations should not require the Node.js event loop to
    remain active.
    **Default:** `true`.
  * `signal` {AbortSignal} An optional `AbortSignal` that can be used to
    cancel the scheduled `Timeout` between operations.

```mjs
import {
  setInterval,
} from 'node:timers/promises';

const interval = 100;
for await (const startTime of setInterval(interval, Date.now())) {
  const now = Date.now();
  console.log(now);
  if ((now - startTime) > 1000)
    break;
}
console.log(Date.now());
```

```cjs
const {
  setInterval,
} = require('node:timers/promises');
const interval = 100;

(async function() {
  for await (const startTime of setInterval(interval, Date.now())) {
    const now = Date.now();
    console.log(now);
    if ((now - startTime) > 1000)
      break;
  }
  console.log(Date.now());
})();
```

### `timersPromises.scheduler.wait(delay[, options])`

<!-- YAML
added:
  - v17.3.0
  - v16.14.0
-->

> Stability: 1 - Experimental

* `delay` {number} The number of milliseconds to wait before resolving the
  promise.
* `options` {Object}
  * `ref` {boolean} Set to `false` to indicate that the scheduled `Timeout`
    should not require the Node.js event loop to remain active.
    **Default:** `true`.
  * `signal` {AbortSignal} An optional `AbortSignal` that can be used to
    cancel waiting.
* Returns: {Promise}

An experimental API defined by the [Scheduling APIs][] draft specification
being developed as a standard Web Platform API.

Calling `timersPromises.scheduler.wait(delay, options)` is equivalent
to calling `timersPromises.setTimeout(delay, undefined, options)`.

```mjs
import { scheduler } from 'node:timers/promises';

await scheduler.wait(1000); // Wait one second before continuing
```

### `timersPromises.scheduler.yield()`

<!-- YAML
added:
  - v17.3.0
  - v16.14.0
-->

> Stability: 1 - Experimental

* Returns: {Promise}

An experimental API defined by the [Scheduling APIs][] draft specification
being developed as a standard Web Platform API.

Calling `timersPromises.scheduler.yield()` is equivalent to calling
`timersPromises.setImmediate()` with no arguments.

[Event Loop]: https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/#setimmediate-vs-settimeout
[Scheduling APIs]: https://github.com/WICG/scheduling-apis
[`AbortController`]: globals.md#class-abortcontroller
[`TypeError`]: errors.md#class-typeerror
[`clearImmediate()`]: #clearimmediateimmediate
[`clearInterval()`]: #clearintervaltimeout
[`clearTimeout()`]: #cleartimeouttimeout
[`setImmediate()`]: #setimmediatecallback-args
[`setInterval()`]: #setintervalcallback-delay-args
[`setTimeout()`]: #settimeoutcallback-delay-args
[`timersPromises.setImmediate()`]: #timerspromisessetimmediatevalue-options
[`timersPromises.setInterval()`]: #timerspromisessetintervaldelay-value-options
[`timersPromises.setTimeout()`]: #timerspromisessettimeoutdelay-value-options
[`worker_threads`]: worker_threads.md
[primitive]: #timeoutsymboltoprimitive

# String decoder

<!--introduced_in=v0.10.0-->

> Stability: 2 - Stable

<!-- source_link=lib/string_decoder.js -->

The `node:string_decoder` module provides an API for decoding `Buffer` objects
into strings in a manner that preserves encoded multi-byte UTF-8 and UTF-16
characters. It can be accessed using:

```mjs
import { StringDecoder } from 'node:string_decoder';
```

```cjs
const { StringDecoder } = require('node:string_decoder');
```

The following example shows the basic use of the `StringDecoder` class.

```mjs
import { StringDecoder } from 'node:string_decoder';
import { Buffer } from 'node:buffer';
const decoder = new StringDecoder('utf8');

const cent = Buffer.from([0xC2, 0xA2]);
console.log(decoder.write(cent)); // Prints: ¢

const euro = Buffer.from([0xE2, 0x82, 0xAC]);
console.log(decoder.write(euro)); // Prints: €
```

```cjs
const { StringDecoder } = require('node:string_decoder');
const decoder = new StringDecoder('utf8');

const cent = Buffer.from([0xC2, 0xA2]);
console.log(decoder.write(cent)); // Prints: ¢

const euro = Buffer.from([0xE2, 0x82, 0xAC]);
console.log(decoder.write(euro)); // Prints: €
```

When a `Buffer` instance is written to the `StringDecoder` instance, an
internal buffer is used to ensure that the decoded string does not contain
any incomplete multibyte characters. These are held in the buffer until the
next call to `stringDecoder.write()` or until `stringDecoder.end()` is called.

In the following example, the three UTF-8 encoded bytes of the European Euro
symbol (`€`) are written over three separate operations:

```mjs
import { StringDecoder } from 'node:string_decoder';
import { Buffer } from 'node:buffer';
const decoder = new StringDecoder('utf8');

decoder.write(Buffer.from([0xE2]));
decoder.write(Buffer.from([0x82]));
console.log(decoder.end(Buffer.from([0xAC]))); // Prints: €
```

```cjs
const { StringDecoder } = require('node:string_decoder');
const decoder = new StringDecoder('utf8');

decoder.write(Buffer.from([0xE2]));
decoder.write(Buffer.from([0x82]));
console.log(decoder.end(Buffer.from([0xAC]))); // Prints: €
```

## Class: `StringDecoder`

### `new StringDecoder([encoding])`

<!-- YAML
added: v0.1.99
-->

* `encoding` {string} The character [encoding][] the `StringDecoder` will use.
  **Default:** `'utf8'`.

Creates a new `StringDecoder` instance.

### `stringDecoder.end([buffer])`

<!-- YAML
added: v0.9.3
-->

* `buffer` {string|Buffer|TypedArray|DataView} The bytes to decode.
* Returns: {string}

Returns any remaining input stored in the internal buffer as a string. Bytes
representing incomplete UTF-8 and UTF-16 characters will be replaced with
substitution characters appropriate for the character encoding.

If the `buffer` argument is provided, one final call to `stringDecoder.write()`
is performed before returning the remaining input.
After `end()` is called, the `stringDecoder` object can be reused for new input.

### `stringDecoder.write(buffer)`

<!-- YAML
added: v0.1.99
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9618
    description: Each invalid character is now replaced by a single replacement
                 character instead of one for each individual byte.
-->

* `buffer` {string|Buffer|TypedArray|DataView} The bytes to decode.
* Returns: {string}

Returns a decoded string, ensuring that any incomplete multibyte characters at
the end of the `Buffer`, or `TypedArray`, or `DataView` are omitted from the
returned string and stored in an internal buffer for the next call to
`stringDecoder.write()` or `stringDecoder.end()`.

[encoding]: buffer.md#buffers-and-character-encodings

# Path

<!--introduced_in=v0.10.0-->

> Stability: 2 - Stable

<!-- source_link=lib/path.js -->

The `node:path` module provides utilities for working with file and directory
paths. It can be accessed using:

```cjs
const path = require('node:path');
```

```mjs
import path from 'node:path';
```

## Windows vs. POSIX

The default operation of the `node:path` module varies based on the operating
system on which a Node.js application is running. Specifically, when running on
a Windows operating system, the `node:path` module will assume that
Windows-style paths are being used.

So using `path.basename()` might yield different results on POSIX and Windows:

On POSIX:

```js
path.basename('C:\\temp\\myfile.html');
// Returns: 'C:\\temp\\myfile.html'
```

On Windows:

```js
path.basename('C:\\temp\\myfile.html');
// Returns: 'myfile.html'
```

To achieve consistent results when working with Windows file paths on any
operating system, use [`path.win32`][]:

On POSIX and Windows:

```js
path.win32.basename('C:\\temp\\myfile.html');
// Returns: 'myfile.html'
```

To achieve consistent results when working with POSIX file paths on any
operating system, use [`path.posix`][]:

On POSIX and Windows:

```js
path.posix.basename('/tmp/myfile.html');
// Returns: 'myfile.html'
```

On Windows Node.js follows the concept of per-drive working directory.
This behavior can be observed when using a drive path without a backslash. For
example, `path.resolve('C:\\')` can potentially return a different result than
`path.resolve('C:')`. For more information, see
[this MSDN page][MSDN-Rel-Path].

## `path.basename(path[, suffix])`

<!-- YAML
added: v0.1.25
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: Passing a non-string as the `path` argument will throw now.
-->

* `path` {string}
* `suffix` {string} An optional suffix to remove
* Returns: {string}

The `path.basename()` method returns the last portion of a `path`, similar to
the Unix `basename` command. Trailing [directory separators][`path.sep`] are
ignored.

```js
path.basename('/foo/bar/baz/asdf/quux.html');
// Returns: 'quux.html'

path.basename('/foo/bar/baz/asdf/quux.html', '.html');
// Returns: 'quux'
```

Although Windows usually treats file names, including file extensions, in a
case-insensitive manner, this function does not. For example, `C:\\foo.html` and
`C:\\foo.HTML` refer to the same file, but `basename` treats the extension as a
case-sensitive string:

```js
path.win32.basename('C:\\foo.html', '.html');
// Returns: 'foo'

path.win32.basename('C:\\foo.HTML', '.html');
// Returns: 'foo.HTML'
```

A [`TypeError`][] is thrown if `path` is not a string or if `suffix` is given
and is not a string.

## `path.delimiter`

<!-- YAML
added: v0.9.3
-->

* {string}

Provides the platform-specific path delimiter:

* `;` for Windows
* `:` for POSIX

For example, on POSIX:

```js
console.log(process.env.PATH);
// Prints: '/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin'

process.env.PATH.split(path.delimiter);
// Returns: ['/usr/bin', '/bin', '/usr/sbin', '/sbin', '/usr/local/bin']
```

On Windows:

```js
console.log(process.env.PATH);
// Prints: 'C:\Windows\system32;C:\Windows;C:\Program Files\node\'

process.env.PATH.split(path.delimiter);
// Returns ['C:\\Windows\\system32', 'C:\\Windows', 'C:\\Program Files\\node\\']
```

## `path.dirname(path)`

<!-- YAML
added: v0.1.16
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: Passing a non-string as the `path` argument will throw now.
-->

* `path` {string}
* Returns: {string}

The `path.dirname()` method returns the directory name of a `path`, similar to
the Unix `dirname` command. Trailing directory separators are ignored, see
[`path.sep`][].

```js
path.dirname('/foo/bar/baz/asdf/quux');
// Returns: '/foo/bar/baz/asdf'
```

A [`TypeError`][] is thrown if `path` is not a string.

## `path.extname(path)`

<!-- YAML
added: v0.1.25
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: Passing a non-string as the `path` argument will throw now.
-->

* `path` {string}
* Returns: {string}

The `path.extname()` method returns the extension of the `path`, from the last
occurrence of the `.` (period) character to end of string in the last portion of
the `path`. If there is no `.` in the last portion of the `path`, or if
there are no `.` characters other than the first character of
the basename of `path` (see `path.basename()`) , an empty string is returned.

```js
path.extname('index.html');
// Returns: '.html'

path.extname('index.coffee.md');
// Returns: '.md'

path.extname('index.');
// Returns: '.'

path.extname('index');
// Returns: ''

path.extname('.index');
// Returns: ''

path.extname('.index.md');
// Returns: '.md'
```

A [`TypeError`][] is thrown if `path` is not a string.

## `path.format(pathObject)`

<!-- YAML
added: v0.11.15
changes:
  - version: v19.0.0
    pr-url: https://github.com/nodejs/node/pull/44349
    description: The dot will be added if it is not specified in `ext`.
-->

* `pathObject` {Object} Any JavaScript object having the following properties:
  * `dir` {string}
  * `root` {string}
  * `base` {string}
  * `name` {string}
  * `ext` {string}
* Returns: {string}

The `path.format()` method returns a path string from an object. This is the
opposite of [`path.parse()`][].

When providing properties to the `pathObject` remember that there are
combinations where one property has priority over another:

* `pathObject.root` is ignored if `pathObject.dir` is provided
* `pathObject.ext` and `pathObject.name` are ignored if `pathObject.base` exists

For example, on POSIX:

```js
// If `dir`, `root` and `base` are provided,
// `${dir}${path.sep}${base}`
// will be returned. `root` is ignored.
path.format({
  root: '/ignored',
  dir: '/home/user/dir',
  base: 'file.txt',
});
// Returns: '/home/user/dir/file.txt'

// `root` will be used if `dir` is not specified.
// If only `root` is provided or `dir` is equal to `root` then the
// platform separator will not be included. `ext` will be ignored.
path.format({
  root: '/',
  base: 'file.txt',
  ext: 'ignored',
});
// Returns: '/file.txt'

// `name` + `ext` will be used if `base` is not specified.
path.format({
  root: '/',
  name: 'file',
  ext: '.txt',
});
// Returns: '/file.txt'

// The dot will be added if it is not specified in `ext`.
path.format({
  root: '/',
  name: 'file',
  ext: 'txt',
});
// Returns: '/file.txt'
```

On Windows:

```js
path.format({
  dir: 'C:\\path\\dir',
  base: 'file.txt',
});
// Returns: 'C:\\path\\dir\\file.txt'
```

## `path.matchesGlob(path, pattern)`

<!-- YAML
added:
  - v22.5.0
  - v20.17.0
-->

> Stability: 1 - Experimental

* `path` {string} The path to glob-match against.
* `pattern` {string} The glob to check the path against.
* Returns: {boolean} Whether or not the `path` matched the `pattern`.

The `path.matchesGlob()` method determines if `path` matches the `pattern`.

For example:

```js
path.matchesGlob('/foo/bar', '/foo/*'); // true
path.matchesGlob('/foo/bar*', 'foo/bird'); // false
```

A [`TypeError`][] is thrown if `path` or `pattern` are not strings.

## `path.isAbsolute(path)`

<!-- YAML
added: v0.11.2
-->

* `path` {string}
* Returns: {boolean}

The `path.isAbsolute()` method determines if `path` is an absolute path.

If the given `path` is a zero-length string, `false` will be returned.

For example, on POSIX:

```js
path.isAbsolute('/foo/bar'); // true
path.isAbsolute('/baz/..');  // true
path.isAbsolute('qux/');     // false
path.isAbsolute('.');        // false
```

On Windows:

```js
path.isAbsolute('//server');    // true
path.isAbsolute('\\\\server');  // true
path.isAbsolute('C:/foo/..');   // true
path.isAbsolute('C:\\foo\\..'); // true
path.isAbsolute('bar\\baz');    // false
path.isAbsolute('bar/baz');     // false
path.isAbsolute('.');           // false
```

A [`TypeError`][] is thrown if `path` is not a string.

## `path.join([...paths])`

<!-- YAML
added: v0.1.16
-->

* `...paths` {string} A sequence of path segments
* Returns: {string}

The `path.join()` method joins all given `path` segments together using the
platform-specific separator as a delimiter, then normalizes the resulting path.

Zero-length `path` segments are ignored. If the joined path string is a
zero-length string then `'.'` will be returned, representing the current
working directory.

```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// Returns: '/foo/bar/baz/asdf'

path.join('foo', {}, 'bar');
// Throws 'TypeError: Path must be a string. Received {}'
```

A [`TypeError`][] is thrown if any of the path segments is not a string.

## `path.normalize(path)`

<!-- YAML
added: v0.1.23
-->

* `path` {string}
* Returns: {string}

The `path.normalize()` method normalizes the given `path`, resolving `'..'` and
`'.'` segments.

When multiple, sequential path segment separation characters are found (e.g.
`/` on POSIX and either `\` or `/` on Windows), they are replaced by a single
instance of the platform-specific path segment separator (`/` on POSIX and
`\` on Windows). Trailing separators are preserved.

If the `path` is a zero-length string, `'.'` is returned, representing the
current working directory.

On POSIX, the types of normalization applied by this function do not strictly
adhere to the POSIX specification. For example, this function will replace two
leading forward slashes with a single slash as if it was a regular absolute
path, whereas a few POSIX systems assign special meaning to paths beginning with
exactly two forward slashes. Similarly, other substitutions performed by this
function, such as removing `..` segments, may change how the underlying system
resolves the path.

For example, on POSIX:

```js
path.normalize('/foo/bar//baz/asdf/quux/..');
// Returns: '/foo/bar/baz/asdf'
```

On Windows:

```js
path.normalize('C:\\temp\\\\foo\\bar\\..\\');
// Returns: 'C:\\temp\\foo\\'
```

Since Windows recognizes multiple path separators, both separators will be
replaced by instances of the Windows preferred separator (`\`):

```js
path.win32.normalize('C:////temp\\\\/\\/\\/foo/bar');
// Returns: 'C:\\temp\\foo\\bar'
```

A [`TypeError`][] is thrown if `path` is not a string.

## `path.parse(path)`

<!-- YAML
added: v0.11.15
-->

* `path` {string}
* Returns: {Object}

The `path.parse()` method returns an object whose properties represent
significant elements of the `path`. Trailing directory separators are ignored,
see [`path.sep`][].

The returned object will have the following properties:

* `dir` {string}
* `root` {string}
* `base` {string}
* `name` {string}
* `ext` {string}

For example, on POSIX:

```js
path.parse('/home/user/dir/file.txt');
// Returns:
// { root: '/',
//   dir: '/home/user/dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
```

```text
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
"  /    home/user/dir / file  .txt "
└──────┴──────────────┴──────┴─────┘
(All spaces in the "" line should be ignored. They are purely for formatting.)
```

On Windows:

```js
path.parse('C:\\path\\dir\\file.txt');
// Returns:
// { root: 'C:\\',
//   dir: 'C:\\path\\dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
```

```text
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
" C:\      path\dir   \ file  .txt "
└──────┴──────────────┴──────┴─────┘
(All spaces in the "" line should be ignored. They are purely for formatting.)
```

A [`TypeError`][] is thrown if `path` is not a string.

## `path.posix`

<!-- YAML
added: v0.11.15
changes:
  - version: v15.3.0
    pr-url: https://github.com/nodejs/node/pull/34962
    description: Exposed as `require('path/posix')`.
-->

* {Object}

The `path.posix` property provides access to POSIX specific implementations
of the `path` methods.

The API is accessible via `require('node:path').posix` or `require('node:path/posix')`.

## `path.relative(from, to)`

<!-- YAML
added: v0.5.0
changes:
  - version: v6.8.0
    pr-url: https://github.com/nodejs/node/pull/8523
    description: On Windows, the leading slashes for UNC paths are now included
                 in the return value.
-->

* `from` {string}
* `to` {string}
* Returns: {string}

The `path.relative()` method returns the relative path from `from` to `to` based
on the current working directory. If `from` and `to` each resolve to the same
path (after calling `path.resolve()` on each), a zero-length string is returned.

If a zero-length string is passed as `from` or `to`, the current working
directory will be used instead of the zero-length strings.

For example, on POSIX:

```js
path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb');
// Returns: '../../impl/bbb'
```

On Windows:

```js
path.relative('C:\\orandea\\test\\aaa', 'C:\\orandea\\impl\\bbb');
// Returns: '..\\..\\impl\\bbb'
```

A [`TypeError`][] is thrown if either `from` or `to` is not a string.

## `path.resolve([...paths])`

<!-- YAML
added: v0.3.4
-->

* `...paths` {string} A sequence of paths or path segments
* Returns: {string}

The `path.resolve()` method resolves a sequence of paths or path segments into
an absolute path.

The given sequence of paths is processed from right to left, with each
subsequent `path` prepended until an absolute path is constructed.
For instance, given the sequence of path segments: `/foo`, `/bar`, `baz`,
calling `path.resolve('/foo', '/bar', 'baz')` would return `/bar/baz`
because `'baz'` is not an absolute path but `'/bar' + '/' + 'baz'` is.

If, after processing all given `path` segments, an absolute path has not yet
been generated, the current working directory is used.

The resulting path is normalized and trailing slashes are removed unless the
path is resolved to the root directory.

Zero-length `path` segments are ignored.

If no `path` segments are passed, `path.resolve()` will return the absolute path
of the current working directory.

```js
path.resolve('/foo/bar', './baz');
// Returns: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// Returns: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// If the current working directory is /home/myself/node,
// this returns '/home/myself/node/wwwroot/static_files/gif/image.gif'
```

A [`TypeError`][] is thrown if any of the arguments is not a string.

## `path.sep`

<!-- YAML
added: v0.7.9
-->

* {string}

Provides the platform-specific path segment separator:

* `\` on Windows
* `/` on POSIX

For example, on POSIX:

```js
'foo/bar/baz'.split(path.sep);
// Returns: ['foo', 'bar', 'baz']
```

On Windows:

```js
'foo\\bar\\baz'.split(path.sep);
// Returns: ['foo', 'bar', 'baz']
```

On Windows, both the forward slash (`/`) and backward slash (`\`) are accepted
as path segment separators; however, the `path` methods only add backward
slashes (`\`).

## `path.toNamespacedPath(path)`

<!-- YAML
added: v9.0.0
-->

* `path` {string}
* Returns: {string}

On Windows systems only, returns an equivalent [namespace-prefixed path][] for
the given `path`. If `path` is not a string, `path` will be returned without
modifications.

This method is meaningful only on Windows systems. On POSIX systems, the
method is non-operational and always returns `path` without modifications.

## `path.win32`

<!-- YAML
added: v0.11.15
changes:
  - version: v15.3.0
    pr-url: https://github.com/nodejs/node/pull/34962
    description: Exposed as `require('path/win32')`.
-->

* {Object}

The `path.win32` property provides access to Windows-specific implementations
of the `path` methods.

The API is accessible via `require('node:path').win32` or `require('node:path/win32')`.

[MSDN-Rel-Path]: https://docs.microsoft.com/en-us/windows/desktop/FileIO/naming-a-file#fully-qualified-vs-relative-paths
[`TypeError`]: errors.md#class-typeerror
[`path.parse()`]: #pathparsepath
[`path.posix`]: #pathposix
[`path.sep`]: #pathsep
[`path.win32`]: #pathwin32
[namespace-prefixed path]: https://docs.microsoft.com/en-us/windows/desktop/FileIO/naming-a-file#namespaces

# OS

<!--introduced_in=v0.10.0-->

> Stability: 2 - Stable

<!-- source_link=lib/os.js -->

The `node:os` module provides operating system-related utility methods and
properties. It can be accessed using:

```mjs
import os from 'node:os';
```

```cjs
const os = require('node:os');
```

## `os.EOL`

<!-- YAML
added: v0.7.8
-->

* {string}

The operating system-specific end-of-line marker.

* `\n` on POSIX
* `\r\n` on Windows

## `os.availableParallelism()`

<!-- YAML
added:
  - v19.4.0
  - v18.14.0
-->

* Returns: {integer}

Returns an estimate of the default amount of parallelism a program should use.
Always returns a value greater than zero.

This function is a small wrapper about libuv's [`uv_available_parallelism()`][].

## `os.arch()`

<!-- YAML
added: v0.5.0
-->

* Returns: {string}

Returns the operating system CPU architecture for which the Node.js binary was
compiled. Possible values are `'arm'`, `'arm64'`, `'ia32'`, `'loong64'`,
`'mips'`, `'mipsel'`, `'ppc64'`, `'riscv64'`, `'s390'`, `'s390x'`,
and `'x64'`.

The return value is equivalent to [`process.arch`][].

## `os.constants`

<!-- YAML
added: v6.3.0
-->

* {Object}

Contains commonly used operating system-specific constants for error codes,
process signals, and so on. The specific constants defined are described in
[OS constants](#os-constants).

## `os.cpus()`

<!-- YAML
added: v0.3.3
-->

* Returns: {Object\[]}

Returns an array of objects containing information about each logical CPU core.
The array will be empty if no CPU information is available, such as if the
`/proc` file system is unavailable.

The properties included on each object include:

* `model` {string}
* `speed` {number} (in MHz)
* `times` {Object}
  * `user` {number} The number of milliseconds the CPU has spent in user mode.
  * `nice` {number} The number of milliseconds the CPU has spent in nice mode.
  * `sys` {number} The number of milliseconds the CPU has spent in sys mode.
  * `idle` {number} The number of milliseconds the CPU has spent in idle mode.
  * `irq` {number} The number of milliseconds the CPU has spent in irq mode.

<!-- eslint-disable @stylistic/js/semi -->

```js
[
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 252020,
      nice: 0,
      sys: 30340,
      idle: 1070356870,
      irq: 0,
    },
  },
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 306960,
      nice: 0,
      sys: 26980,
      idle: 1071569080,
      irq: 0,
    },
  },
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 248450,
      nice: 0,
      sys: 21750,
      idle: 1070919370,
      irq: 0,
    },
  },
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 256880,
      nice: 0,
      sys: 19430,
      idle: 1070905480,
      irq: 20,
    },
  },
]
```

`nice` values are POSIX-only. On Windows, the `nice` values of all processors
are always 0.

`os.cpus().length` should not be used to calculate the amount of parallelism
available to an application. Use
[`os.availableParallelism()`](#osavailableparallelism) for this purpose.

## `os.devNull`

<!-- YAML
added:
  - v16.3.0
  - v14.18.0
-->

* {string}

The platform-specific file path of the null device.

* `\\.\nul` on Windows
* `/dev/null` on POSIX

## `os.endianness()`

<!-- YAML
added: v0.9.4
-->

* Returns: {string}

Returns a string identifying the endianness of the CPU for which the Node.js
binary was compiled.

Possible values are `'BE'` for big endian and `'LE'` for little endian.

## `os.freemem()`

<!-- YAML
added: v0.3.3
-->

* Returns: {integer}

Returns the amount of free system memory in bytes as an integer.

## `os.getPriority([pid])`

<!-- YAML
added: v10.10.0
-->

* `pid` {integer} The process ID to retrieve scheduling priority for.
  **Default:** `0`.
* Returns: {integer}

Returns the scheduling priority for the process specified by `pid`. If `pid` is
not provided or is `0`, the priority of the current process is returned.

## `os.homedir()`

<!-- YAML
added: v2.3.0
-->

* Returns: {string}

Returns the string path of the current user's home directory.

On POSIX, it uses the `$HOME` environment variable if defined. Otherwise it
uses the [effective UID][EUID] to look up the user's home directory.

On Windows, it uses the `USERPROFILE` environment variable if defined.
Otherwise it uses the path to the profile directory of the current user.

## `os.hostname()`

<!-- YAML
added: v0.3.3
-->

* Returns: {string}

Returns the host name of the operating system as a string.

## `os.loadavg()`

<!-- YAML
added: v0.3.3
-->

* Returns: {number\[]}

Returns an array containing the 1, 5, and 15 minute load averages.

The load average is a measure of system activity calculated by the operating
system and expressed as a fractional number.

The load average is a Unix-specific concept. On Windows, the return value is
always `[0, 0, 0]`.

## `os.machine()`

<!-- YAML
added:
  - v18.9.0
  - v16.18.0
-->

* Returns: {string}

Returns the machine type as a string, such as `arm`, `arm64`, `aarch64`,
`mips`, `mips64`, `ppc64`, `ppc64le`, `s390`, `s390x`, `i386`, `i686`, `x86_64`.

On POSIX systems, the machine type is determined by calling
[`uname(3)`][]. On Windows, `RtlGetVersion()` is used, and if it is not
available, `GetVersionExW()` will be used. See
<https://en.wikipedia.org/wiki/Uname#Examples> for more information.

## `os.networkInterfaces()`

<!-- YAML
added: v0.6.0
changes:
  - version: v18.4.0
    pr-url: https://github.com/nodejs/node/pull/43054
    description: The `family` property now returns a string instead of a number.
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41431
    description: The `family` property now returns a number instead of a string.
-->

* Returns: {Object}

Returns an object containing network interfaces that have been assigned a
network address.

Each key on the returned object identifies a network interface. The associated
value is an array of objects that each describe an assigned network address.

The properties available on the assigned network address object include:

* `address` {string} The assigned IPv4 or IPv6 address
* `netmask` {string} The IPv4 or IPv6 network mask
* `family` {string} Either `IPv4` or `IPv6`
* `mac` {string} The MAC address of the network interface
* `internal` {boolean} `true` if the network interface is a loopback or
  similar interface that is not remotely accessible; otherwise `false`
* `scopeid` {number} The numeric IPv6 scope ID (only specified when `family`
  is `IPv6`)
* `cidr` {string} The assigned IPv4 or IPv6 address with the routing prefix
  in CIDR notation. If the `netmask` is invalid, this property is set
  to `null`.

<!-- eslint-skip -->

```js
{
  lo: [
    {
      address: '127.0.0.1',
      netmask: '255.0.0.0',
      family: 'IPv4',
      mac: '00:00:00:00:00:00',
      internal: true,
      cidr: '127.0.0.1/8'
    },
    {
      address: '::1',
      netmask: 'ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff',
      family: 'IPv6',
      mac: '00:00:00:00:00:00',
      scopeid: 0,
      internal: true,
      cidr: '::1/128'
    }
  ],
  eth0: [
    {
      address: '192.168.1.108',
      netmask: '255.255.255.0',
      family: 'IPv4',
      mac: '01:02:03:0a:0b:0c',
      internal: false,
      cidr: '192.168.1.108/24'
    },
    {
      address: 'fe80::a00:27ff:fe4e:66a1',
      netmask: 'ffff:ffff:ffff:ffff::',
      family: 'IPv6',
      mac: '01:02:03:0a:0b:0c',
      scopeid: 1,
      internal: false,
      cidr: 'fe80::a00:27ff:fe4e:66a1/64'
    }
  ]
}
```

## `os.platform()`

<!-- YAML
added: v0.5.0
-->

* Returns: {string}

Returns a string identifying the operating system platform for which
the Node.js binary was compiled. The value is set at compile time.
Possible values are `'aix'`, `'darwin'`, `'freebsd'`,`'linux'`,
`'openbsd'`, `'sunos'`, and `'win32'`.

The return value is equivalent to [`process.platform`][].

The value `'android'` may also be returned if Node.js is built on the Android
operating system. [Android support is experimental][Android building].

## `os.release()`

<!-- YAML
added: v0.3.3
-->

* Returns: {string}

Returns the operating system as a string.

On POSIX systems, the operating system release is determined by calling
[`uname(3)`][]. On Windows, `GetVersionExW()` is used. See
<https://en.wikipedia.org/wiki/Uname#Examples> for more information.

## `os.setPriority([pid, ]priority)`

<!-- YAML
added: v10.10.0
-->

* `pid` {integer} The process ID to set scheduling priority for.
  **Default:** `0`.
* `priority` {integer} The scheduling priority to assign to the process.

Attempts to set the scheduling priority for the process specified by `pid`. If
`pid` is not provided or is `0`, the process ID of the current process is used.

The `priority` input must be an integer between `-20` (high priority) and `19`
(low priority). Due to differences between Unix priority levels and Windows
priority classes, `priority` is mapped to one of six priority constants in
`os.constants.priority`. When retrieving a process priority level, this range
mapping may cause the return value to be slightly different on Windows. To avoid
confusion, set `priority` to one of the priority constants.

On Windows, setting priority to `PRIORITY_HIGHEST` requires elevated user
privileges. Otherwise the set priority will be silently reduced to
`PRIORITY_HIGH`.

## `os.tmpdir()`

<!-- YAML
added: v0.9.9
changes:
  - version: v2.0.0
    pr-url: https://github.com/nodejs/node/pull/747
    description: This function is now cross-platform consistent and no longer
                 returns a path with a trailing slash on any platform.
-->

* Returns: {string}

Returns the operating system's default directory for temporary files as a
string.

On Windows, the result can be overridden by `TEMP` and `TMP` environment variables, and
`TEMP` takes precedence over `TMP`. If neither is set, it defaults to `%SystemRoot%\temp`
or `%windir%\temp`.

On non-Windows platforms, `TMPDIR`, `TMP` and `TEMP` environment variables will be checked
to override the result of this method, in the described order. If none of them is set, it
defaults to `/tmp`.

Some operating system distributions would either configure `TMPDIR` (non-Windows) or
`TEMP` and `TMP` (Windows) by default without additional configurations by the system
administrators. The result of `os.tmpdir()` typically reflects the system preference
unless it's explicitly overridden by the users.

## `os.totalmem()`

<!-- YAML
added: v0.3.3
-->

* Returns: {integer}

Returns the total amount of system memory in bytes as an integer.

## `os.type()`

<!-- YAML
added: v0.3.3
-->

* Returns: {string}

Returns the operating system name as returned by [`uname(3)`][]. For example, it
returns `'Linux'` on Linux, `'Darwin'` on macOS, and `'Windows_NT'` on Windows.

See <https://en.wikipedia.org/wiki/Uname#Examples> for additional information
about the output of running [`uname(3)`][] on various operating systems.

## `os.uptime()`

<!-- YAML
added: v0.3.3
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/20129
    description: The result of this function no longer contains a fraction
                 component on Windows.
-->

* Returns: {integer}

Returns the system uptime in number of seconds.

## `os.userInfo([options])`

<!-- YAML
added: v6.0.0
-->

* `options` {Object}
  * `encoding` {string} Character encoding used to interpret resulting strings.
    If `encoding` is set to `'buffer'`, the `username`, `shell`, and `homedir`
    values will be `Buffer` instances. **Default:** `'utf8'`.
* Returns: {Object}

Returns information about the currently effective user. On POSIX platforms,
this is typically a subset of the password file. The returned object includes
the `username`, `uid`, `gid`, `shell`, and `homedir`. On Windows, the `uid` and
`gid` fields are `-1`, and `shell` is `null`.

The value of `homedir` returned by `os.userInfo()` is provided by the operating
system. This differs from the result of `os.homedir()`, which queries
environment variables for the home directory before falling back to the
operating system response.

Throws a [`SystemError`][] if a user has no `username` or `homedir`.

## `os.version()`

<!-- YAML
added:
 - v13.11.0
 - v12.17.0
-->

* Returns: {string}

Returns a string identifying the kernel version.

On POSIX systems, the operating system release is determined by calling
[`uname(3)`][]. On Windows, `RtlGetVersion()` is used, and if it is not
available, `GetVersionExW()` will be used. See
<https://en.wikipedia.org/wiki/Uname#Examples> for more information.

## OS constants

The following constants are exported by `os.constants`.

Not all constants will be available on every operating system.

### Signal constants

<!-- YAML
changes:
  - version: v5.11.0
    pr-url: https://github.com/nodejs/node/pull/6093
    description: Added support for `SIGINFO`.
-->

The following signal constants are exported by `os.constants.signals`.

<table>
  <tr>
    <th>Constant</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>SIGHUP</code></td>
    <td>Sent to indicate when a controlling terminal is closed or a parent
    process exits.</td>
  </tr>
  <tr>
    <td><code>SIGINT</code></td>
    <td>Sent to indicate when a user wishes to interrupt a process
    (<kbd>Ctrl</kbd>+<kbd>C</kbd>).</td>
  </tr>
  <tr>
    <td><code>SIGQUIT</code></td>
    <td>Sent to indicate when a user wishes to terminate a process and perform a
    core dump.</td>
  </tr>
  <tr>
    <td><code>SIGILL</code></td>
    <td>Sent to a process to notify that it has attempted to perform an illegal,
    malformed, unknown, or privileged instruction.</td>
  </tr>
  <tr>
    <td><code>SIGTRAP</code></td>
    <td>Sent to a process when an exception has occurred.</td>
  </tr>
  <tr>
    <td><code>SIGABRT</code></td>
    <td>Sent to a process to request that it abort.</td>
  </tr>
  <tr>
    <td><code>SIGIOT</code></td>
    <td>Synonym for <code>SIGABRT</code></td>
  </tr>
  <tr>
    <td><code>SIGBUS</code></td>
    <td>Sent to a process to notify that it has caused a bus error.</td>
  </tr>
  <tr>
    <td><code>SIGFPE</code></td>
    <td>Sent to a process to notify that it has performed an illegal arithmetic
    operation.</td>
  </tr>
  <tr>
    <td><code>SIGKILL</code></td>
    <td>Sent to a process to terminate it immediately.</td>
  </tr>
  <tr>
    <td><code>SIGUSR1</code> <code>SIGUSR2</code></td>
    <td>Sent to a process to identify user-defined conditions.</td>
  </tr>
  <tr>
    <td><code>SIGSEGV</code></td>
    <td>Sent to a process to notify of a segmentation fault.</td>
  </tr>
  <tr>
    <td><code>SIGPIPE</code></td>
    <td>Sent to a process when it has attempted to write to a disconnected
    pipe.</td>
  </tr>
  <tr>
    <td><code>SIGALRM</code></td>
    <td>Sent to a process when a system timer elapses.</td>
  </tr>
  <tr>
    <td><code>SIGTERM</code></td>
    <td>Sent to a process to request termination.</td>
  </tr>
  <tr>
    <td><code>SIGCHLD</code></td>
    <td>Sent to a process when a child process terminates.</td>
  </tr>
  <tr>
    <td><code>SIGSTKFLT</code></td>
    <td>Sent to a process to indicate a stack fault on a coprocessor.</td>
  </tr>
  <tr>
    <td><code>SIGCONT</code></td>
    <td>Sent to instruct the operating system to continue a paused process.</td>
  </tr>
  <tr>
    <td><code>SIGSTOP</code></td>
    <td>Sent to instruct the operating system to halt a process.</td>
  </tr>
  <tr>
    <td><code>SIGTSTP</code></td>
    <td>Sent to a process to request it to stop.</td>
  </tr>
  <tr>
    <td><code>SIGBREAK</code></td>
    <td>Sent to indicate when a user wishes to interrupt a process.</td>
  </tr>
  <tr>
    <td><code>SIGTTIN</code></td>
    <td>Sent to a process when it reads from the TTY while in the
    background.</td>
  </tr>
  <tr>
    <td><code>SIGTTOU</code></td>
    <td>Sent to a process when it writes to the TTY while in the
    background.</td>
  </tr>
  <tr>
    <td><code>SIGURG</code></td>
    <td>Sent to a process when a socket has urgent data to read.</td>
  </tr>
  <tr>
    <td><code>SIGXCPU</code></td>
    <td>Sent to a process when it has exceeded its limit on CPU usage.</td>
  </tr>
  <tr>
    <td><code>SIGXFSZ</code></td>
    <td>Sent to a process when it grows a file larger than the maximum
    allowed.</td>
  </tr>
  <tr>
    <td><code>SIGVTALRM</code></td>
    <td>Sent to a process when a virtual timer has elapsed.</td>
  </tr>
  <tr>
    <td><code>SIGPROF</code></td>
    <td>Sent to a process when a system timer has elapsed.</td>
  </tr>
  <tr>
    <td><code>SIGWINCH</code></td>
    <td>Sent to a process when the controlling terminal has changed its
    size.</td>
  </tr>
  <tr>
    <td><code>SIGIO</code></td>
    <td>Sent to a process when I/O is available.</td>
  </tr>
  <tr>
    <td><code>SIGPOLL</code></td>
    <td>Synonym for <code>SIGIO</code></td>
  </tr>
  <tr>
    <td><code>SIGLOST</code></td>
    <td>Sent to a process when a file lock has been lost.</td>
  </tr>
  <tr>
    <td><code>SIGPWR</code></td>
    <td>Sent to a process to notify of a power failure.</td>
  </tr>
  <tr>
    <td><code>SIGINFO</code></td>
    <td>Synonym for <code>SIGPWR</code></td>
  </tr>
  <tr>
    <td><code>SIGSYS</code></td>
    <td>Sent to a process to notify of a bad argument.</td>
  </tr>
  <tr>
    <td><code>SIGUNUSED</code></td>
    <td>Synonym for <code>SIGSYS</code></td>
  </tr>
</table>

### Error constants

The following error constants are exported by `os.constants.errno`.

#### POSIX error constants

<table>
  <tr>
    <th>Constant</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>E2BIG</code></td>
    <td>Indicates that the list of arguments is longer than expected.</td>
  </tr>
  <tr>
    <td><code>EACCES</code></td>
    <td>Indicates that the operation did not have sufficient permissions.</td>
  </tr>
  <tr>
    <td><code>EADDRINUSE</code></td>
    <td>Indicates that the network address is already in use.</td>
  </tr>
  <tr>
    <td><code>EADDRNOTAVAIL</code></td>
    <td>Indicates that the network address is currently unavailable for
    use.</td>
  </tr>
  <tr>
    <td><code>EAFNOSUPPORT</code></td>
    <td>Indicates that the network address family is not supported.</td>
  </tr>
  <tr>
    <td><code>EAGAIN</code></td>
    <td>Indicates that there is no data available and to try the
    operation again later.</td>
  </tr>
  <tr>
    <td><code>EALREADY</code></td>
    <td>Indicates that the socket already has a pending connection in
    progress.</td>
  </tr>
  <tr>
    <td><code>EBADF</code></td>
    <td>Indicates that a file descriptor is not valid.</td>
  </tr>
  <tr>
    <td><code>EBADMSG</code></td>
    <td>Indicates an invalid data message.</td>
  </tr>
  <tr>
    <td><code>EBUSY</code></td>
    <td>Indicates that a device or resource is busy.</td>
  </tr>
  <tr>
    <td><code>ECANCELED</code></td>
    <td>Indicates that an operation was canceled.</td>
  </tr>
  <tr>
    <td><code>ECHILD</code></td>
    <td>Indicates that there are no child processes.</td>
  </tr>
  <tr>
    <td><code>ECONNABORTED</code></td>
    <td>Indicates that the network connection has been aborted.</td>
  </tr>
  <tr>
    <td><code>ECONNREFUSED</code></td>
    <td>Indicates that the network connection has been refused.</td>
  </tr>
  <tr>
    <td><code>ECONNRESET</code></td>
    <td>Indicates that the network connection has been reset.</td>
  </tr>
  <tr>
    <td><code>EDEADLK</code></td>
    <td>Indicates that a resource deadlock has been avoided.</td>
  </tr>
  <tr>
    <td><code>EDESTADDRREQ</code></td>
    <td>Indicates that a destination address is required.</td>
  </tr>
  <tr>
    <td><code>EDOM</code></td>
    <td>Indicates that an argument is out of the domain of the function.</td>
  </tr>
  <tr>
    <td><code>EDQUOT</code></td>
    <td>Indicates that the disk quota has been exceeded.</td>
  </tr>
  <tr>
    <td><code>EEXIST</code></td>
    <td>Indicates that the file already exists.</td>
  </tr>
  <tr>
    <td><code>EFAULT</code></td>
    <td>Indicates an invalid pointer address.</td>
  </tr>
  <tr>
    <td><code>EFBIG</code></td>
    <td>Indicates that the file is too large.</td>
  </tr>
  <tr>
    <td><code>EHOSTUNREACH</code></td>
    <td>Indicates that the host is unreachable.</td>
  </tr>
  <tr>
    <td><code>EIDRM</code></td>
    <td>Indicates that the identifier has been removed.</td>
  </tr>
  <tr>
    <td><code>EILSEQ</code></td>
    <td>Indicates an illegal byte sequence.</td>
  </tr>
  <tr>
    <td><code>EINPROGRESS</code></td>
    <td>Indicates that an operation is already in progress.</td>
  </tr>
  <tr>
    <td><code>EINTR</code></td>
    <td>Indicates that a function call was interrupted.</td>
  </tr>
  <tr>
    <td><code>EINVAL</code></td>
    <td>Indicates that an invalid argument was provided.</td>
  </tr>
  <tr>
    <td><code>EIO</code></td>
    <td>Indicates an otherwise unspecified I/O error.</td>
  </tr>
  <tr>
    <td><code>EISCONN</code></td>
    <td>Indicates that the socket is connected.</td>
  </tr>
  <tr>
    <td><code>EISDIR</code></td>
    <td>Indicates that the path is a directory.</td>
  </tr>
  <tr>
    <td><code>ELOOP</code></td>
    <td>Indicates too many levels of symbolic links in a path.</td>
  </tr>
  <tr>
    <td><code>EMFILE</code></td>
    <td>Indicates that there are too many open files.</td>
  </tr>
  <tr>
    <td><code>EMLINK</code></td>
    <td>Indicates that there are too many hard links to a file.</td>
  </tr>
  <tr>
    <td><code>EMSGSIZE</code></td>
    <td>Indicates that the provided message is too long.</td>
  </tr>
  <tr>
    <td><code>EMULTIHOP</code></td>
    <td>Indicates that a multihop was attempted.</td>
  </tr>
  <tr>
    <td><code>ENAMETOOLONG</code></td>
    <td>Indicates that the filename is too long.</td>
  </tr>
  <tr>
    <td><code>ENETDOWN</code></td>
    <td>Indicates that the network is down.</td>
  </tr>
  <tr>
    <td><code>ENETRESET</code></td>
    <td>Indicates that the connection has been aborted by the network.</td>
  </tr>
  <tr>
    <td><code>ENETUNREACH</code></td>
    <td>Indicates that the network is unreachable.</td>
  </tr>
  <tr>
    <td><code>ENFILE</code></td>
    <td>Indicates too many open files in the system.</td>
  </tr>
  <tr>
    <td><code>ENOBUFS</code></td>
    <td>Indicates that no buffer space is available.</td>
  </tr>
  <tr>
    <td><code>ENODATA</code></td>
    <td>Indicates that no message is available on the stream head read
    queue.</td>
  </tr>
  <tr>
    <td><code>ENODEV</code></td>
    <td>Indicates that there is no such device.</td>
  </tr>
  <tr>
    <td><code>ENOENT</code></td>
    <td>Indicates that there is no such file or directory.</td>
  </tr>
  <tr>
    <td><code>ENOEXEC</code></td>
    <td>Indicates an exec format error.</td>
  </tr>
  <tr>
    <td><code>ENOLCK</code></td>
    <td>Indicates that there are no locks available.</td>
  </tr>
  <tr>
    <td><code>ENOLINK</code></td>
    <td>Indications that a link has been severed.</td>
  </tr>
  <tr>
    <td><code>ENOMEM</code></td>
    <td>Indicates that there is not enough space.</td>
  </tr>
  <tr>
    <td><code>ENOMSG</code></td>
    <td>Indicates that there is no message of the desired type.</td>
  </tr>
  <tr>
    <td><code>ENOPROTOOPT</code></td>
    <td>Indicates that a given protocol is not available.</td>
  </tr>
  <tr>
    <td><code>ENOSPC</code></td>
    <td>Indicates that there is no space available on the device.</td>
  </tr>
  <tr>
    <td><code>ENOSR</code></td>
    <td>Indicates that there are no stream resources available.</td>
  </tr>
  <tr>
    <td><code>ENOSTR</code></td>
    <td>Indicates that a given resource is not a stream.</td>
  </tr>
  <tr>
    <td><code>ENOSYS</code></td>
    <td>Indicates that a function has not been implemented.</td>
  </tr>
  <tr>
    <td><code>ENOTCONN</code></td>
    <td>Indicates that the socket is not connected.</td>
  </tr>
  <tr>
    <td><code>ENOTDIR</code></td>
    <td>Indicates that the path is not a directory.</td>
  </tr>
  <tr>
    <td><code>ENOTEMPTY</code></td>
    <td>Indicates that the directory is not empty.</td>
  </tr>
  <tr>
    <td><code>ENOTSOCK</code></td>
    <td>Indicates that the given item is not a socket.</td>
  </tr>
  <tr>
    <td><code>ENOTSUP</code></td>
    <td>Indicates that a given operation is not supported.</td>
  </tr>
  <tr>
    <td><code>ENOTTY</code></td>
    <td>Indicates an inappropriate I/O control operation.</td>
  </tr>
  <tr>
    <td><code>ENXIO</code></td>
    <td>Indicates no such device or address.</td>
  </tr>
  <tr>
    <td><code>EOPNOTSUPP</code></td>
    <td>Indicates that an operation is not supported on the socket. Although
    <code>ENOTSUP</code> and <code>EOPNOTSUPP</code> have the same value
    on Linux, according to POSIX.1 these error values should be distinct.)</td>
  </tr>
  <tr>
    <td><code>EOVERFLOW</code></td>
    <td>Indicates that a value is too large to be stored in a given data
    type.</td>
  </tr>
  <tr>
    <td><code>EPERM</code></td>
    <td>Indicates that the operation is not permitted.</td>
  </tr>
  <tr>
    <td><code>EPIPE</code></td>
    <td>Indicates a broken pipe.</td>
  </tr>
  <tr>
    <td><code>EPROTO</code></td>
    <td>Indicates a protocol error.</td>
  </tr>
  <tr>
    <td><code>EPROTONOSUPPORT</code></td>
    <td>Indicates that a protocol is not supported.</td>
  </tr>
  <tr>
    <td><code>EPROTOTYPE</code></td>
    <td>Indicates the wrong type of protocol for a socket.</td>
  </tr>
  <tr>
    <td><code>ERANGE</code></td>
    <td>Indicates that the results are too large.</td>
  </tr>
  <tr>
    <td><code>EROFS</code></td>
    <td>Indicates that the file system is read only.</td>
  </tr>
  <tr>
    <td><code>ESPIPE</code></td>
    <td>Indicates an invalid seek operation.</td>
  </tr>
  <tr>
    <td><code>ESRCH</code></td>
    <td>Indicates that there is no such process.</td>
  </tr>
  <tr>
    <td><code>ESTALE</code></td>
    <td>Indicates that the file handle is stale.</td>
  </tr>
  <tr>
    <td><code>ETIME</code></td>
    <td>Indicates an expired timer.</td>
  </tr>
  <tr>
    <td><code>ETIMEDOUT</code></td>
    <td>Indicates that the connection timed out.</td>
  </tr>
  <tr>
    <td><code>ETXTBSY</code></td>
    <td>Indicates that a text file is busy.</td>
  </tr>
  <tr>
    <td><code>EWOULDBLOCK</code></td>
    <td>Indicates that the operation would block.</td>
  </tr>
  <tr>
    <td><code>EXDEV</code></td>
    <td>Indicates an improper link.</td>
  </tr>
</table>

#### Windows-specific error constants

The following error codes are specific to the Windows operating system.

<table>
  <tr>
    <th>Constant</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>WSAEINTR</code></td>
    <td>Indicates an interrupted function call.</td>
  </tr>
  <tr>
    <td><code>WSAEBADF</code></td>
    <td>Indicates an invalid file handle.</td>
  </tr>
  <tr>
    <td><code>WSAEACCES</code></td>
    <td>Indicates insufficient permissions to complete the operation.</td>
  </tr>
  <tr>
    <td><code>WSAEFAULT</code></td>
    <td>Indicates an invalid pointer address.</td>
  </tr>
  <tr>
    <td><code>WSAEINVAL</code></td>
    <td>Indicates that an invalid argument was passed.</td>
  </tr>
  <tr>
    <td><code>WSAEMFILE</code></td>
    <td>Indicates that there are too many open files.</td>
  </tr>
  <tr>
    <td><code>WSAEWOULDBLOCK</code></td>
    <td>Indicates that a resource is temporarily unavailable.</td>
  </tr>
  <tr>
    <td><code>WSAEINPROGRESS</code></td>
    <td>Indicates that an operation is currently in progress.</td>
  </tr>
  <tr>
    <td><code>WSAEALREADY</code></td>
    <td>Indicates that an operation is already in progress.</td>
  </tr>
  <tr>
    <td><code>WSAENOTSOCK</code></td>
    <td>Indicates that the resource is not a socket.</td>
  </tr>
  <tr>
    <td><code>WSAEDESTADDRREQ</code></td>
    <td>Indicates that a destination address is required.</td>
  </tr>
  <tr>
    <td><code>WSAEMSGSIZE</code></td>
    <td>Indicates that the message size is too long.</td>
  </tr>
  <tr>
    <td><code>WSAEPROTOTYPE</code></td>
    <td>Indicates the wrong protocol type for the socket.</td>
  </tr>
  <tr>
    <td><code>WSAENOPROTOOPT</code></td>
    <td>Indicates a bad protocol option.</td>
  </tr>
  <tr>
    <td><code>WSAEPROTONOSUPPORT</code></td>
    <td>Indicates that the protocol is not supported.</td>
  </tr>
  <tr>
    <td><code>WSAESOCKTNOSUPPORT</code></td>
    <td>Indicates that the socket type is not supported.</td>
  </tr>
  <tr>
    <td><code>WSAEOPNOTSUPP</code></td>
    <td>Indicates that the operation is not supported.</td>
  </tr>
  <tr>
    <td><code>WSAEPFNOSUPPORT</code></td>
    <td>Indicates that the protocol family is not supported.</td>
  </tr>
  <tr>
    <td><code>WSAEAFNOSUPPORT</code></td>
    <td>Indicates that the address family is not supported.</td>
  </tr>
  <tr>
    <td><code>WSAEADDRINUSE</code></td>
    <td>Indicates that the network address is already in use.</td>
  </tr>
  <tr>
    <td><code>WSAEADDRNOTAVAIL</code></td>
    <td>Indicates that the network address is not available.</td>
  </tr>
  <tr>
    <td><code>WSAENETDOWN</code></td>
    <td>Indicates that the network is down.</td>
  </tr>
  <tr>
    <td><code>WSAENETUNREACH</code></td>
    <td>Indicates that the network is unreachable.</td>
  </tr>
  <tr>
    <td><code>WSAENETRESET</code></td>
    <td>Indicates that the network connection has been reset.</td>
  </tr>
  <tr>
    <td><code>WSAECONNABORTED</code></td>
    <td>Indicates that the connection has been aborted.</td>
  </tr>
  <tr>
    <td><code>WSAECONNRESET</code></td>
    <td>Indicates that the connection has been reset by the peer.</td>
  </tr>
  <tr>
    <td><code>WSAENOBUFS</code></td>
    <td>Indicates that there is no buffer space available.</td>
  </tr>
  <tr>
    <td><code>WSAEISCONN</code></td>
    <td>Indicates that the socket is already connected.</td>
  </tr>
  <tr>
    <td><code>WSAENOTCONN</code></td>
    <td>Indicates that the socket is not connected.</td>
  </tr>
  <tr>
    <td><code>WSAESHUTDOWN</code></td>
    <td>Indicates that data cannot be sent after the socket has been
    shutdown.</td>
  </tr>
  <tr>
    <td><code>WSAETOOMANYREFS</code></td>
    <td>Indicates that there are too many references.</td>
  </tr>
  <tr>
    <td><code>WSAETIMEDOUT</code></td>
    <td>Indicates that the connection has timed out.</td>
  </tr>
  <tr>
    <td><code>WSAECONNREFUSED</code></td>
    <td>Indicates that the connection has been refused.</td>
  </tr>
  <tr>
    <td><code>WSAELOOP</code></td>
    <td>Indicates that a name cannot be translated.</td>
  </tr>
  <tr>
    <td><code>WSAENAMETOOLONG</code></td>
    <td>Indicates that a name was too long.</td>
  </tr>
  <tr>
    <td><code>WSAEHOSTDOWN</code></td>
    <td>Indicates that a network host is down.</td>
  </tr>
  <tr>
    <td><code>WSAEHOSTUNREACH</code></td>
    <td>Indicates that there is no route to a network host.</td>
  </tr>
  <tr>
    <td><code>WSAENOTEMPTY</code></td>
    <td>Indicates that the directory is not empty.</td>
  </tr>
  <tr>
    <td><code>WSAEPROCLIM</code></td>
    <td>Indicates that there are too many processes.</td>
  </tr>
  <tr>
    <td><code>WSAEUSERS</code></td>
    <td>Indicates that the user quota has been exceeded.</td>
  </tr>
  <tr>
    <td><code>WSAEDQUOT</code></td>
    <td>Indicates that the disk quota has been exceeded.</td>
  </tr>
  <tr>
    <td><code>WSAESTALE</code></td>
    <td>Indicates a stale file handle reference.</td>
  </tr>
  <tr>
    <td><code>WSAEREMOTE</code></td>
    <td>Indicates that the item is remote.</td>
  </tr>
  <tr>
    <td><code>WSASYSNOTREADY</code></td>
    <td>Indicates that the network subsystem is not ready.</td>
  </tr>
  <tr>
    <td><code>WSAVERNOTSUPPORTED</code></td>
    <td>Indicates that the <code>winsock.dll</code> version is out of
    range.</td>
  </tr>
  <tr>
    <td><code>WSANOTINITIALISED</code></td>
    <td>Indicates that successful WSAStartup has not yet been performed.</td>
  </tr>
  <tr>
    <td><code>WSAEDISCON</code></td>
    <td>Indicates that a graceful shutdown is in progress.</td>
  </tr>
  <tr>
    <td><code>WSAENOMORE</code></td>
    <td>Indicates that there are no more results.</td>
  </tr>
  <tr>
    <td><code>WSAECANCELLED</code></td>
    <td>Indicates that an operation has been canceled.</td>
  </tr>
  <tr>
    <td><code>WSAEINVALIDPROCTABLE</code></td>
    <td>Indicates that the procedure call table is invalid.</td>
  </tr>
  <tr>
    <td><code>WSAEINVALIDPROVIDER</code></td>
    <td>Indicates an invalid service provider.</td>
  </tr>
  <tr>
    <td><code>WSAEPROVIDERFAILEDINIT</code></td>
    <td>Indicates that the service provider failed to initialized.</td>
  </tr>
  <tr>
    <td><code>WSASYSCALLFAILURE</code></td>
    <td>Indicates a system call failure.</td>
  </tr>
  <tr>
    <td><code>WSASERVICE_NOT_FOUND</code></td>
    <td>Indicates that a service was not found.</td>
  </tr>
  <tr>
    <td><code>WSATYPE_NOT_FOUND</code></td>
    <td>Indicates that a class type was not found.</td>
  </tr>
  <tr>
    <td><code>WSA_E_NO_MORE</code></td>
    <td>Indicates that there are no more results.</td>
  </tr>
  <tr>
    <td><code>WSA_E_CANCELLED</code></td>
    <td>Indicates that the call was canceled.</td>
  </tr>
  <tr>
    <td><code>WSAEREFUSED</code></td>
    <td>Indicates that a database query was refused.</td>
  </tr>
</table>

### dlopen constants

If available on the operating system, the following constants
are exported in `os.constants.dlopen`. See dlopen(3) for detailed
information.

<table>
  <tr>
    <th>Constant</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>RTLD_LAZY</code></td>
    <td>Perform lazy binding. Node.js sets this flag by default.</td>
  </tr>
  <tr>
    <td><code>RTLD_NOW</code></td>
    <td>Resolve all undefined symbols in the library before dlopen(3)
    returns.</td>
  </tr>
  <tr>
    <td><code>RTLD_GLOBAL</code></td>
    <td>Symbols defined by the library will be made available for symbol
    resolution of subsequently loaded libraries.</td>
  </tr>
  <tr>
    <td><code>RTLD_LOCAL</code></td>
    <td>The converse of <code>RTLD_GLOBAL</code>. This is the default behavior
    if neither flag is specified.</td>
  </tr>
  <tr>
    <td><code>RTLD_DEEPBIND</code></td>
    <td>Make a self-contained library use its own symbols in preference to
    symbols from previously loaded libraries.</td>
  </tr>
</table>

### Priority constants

<!-- YAML
added: v10.10.0
-->

The following process scheduling constants are exported by
`os.constants.priority`.

<table>
  <tr>
    <th>Constant</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>PRIORITY_LOW</code></td>
    <td>The lowest process scheduling priority. This corresponds to
    <code>IDLE_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>19</code> on all other platforms.</td>
  </tr>
  <tr>
    <td><code>PRIORITY_BELOW_NORMAL</code></td>
    <td>The process scheduling priority above <code>PRIORITY_LOW</code> and
    below <code>PRIORITY_NORMAL</code>. This corresponds to
    <code>BELOW_NORMAL_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>10</code> on all other platforms.</td>
  </tr>
  <tr>
    <td><code>PRIORITY_NORMAL</code></td>
    <td>The default process scheduling priority. This corresponds to
    <code>NORMAL_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>0</code> on all other platforms.</td>
  </tr>
  <tr>
    <td><code>PRIORITY_ABOVE_NORMAL</code></td>
    <td>The process scheduling priority above <code>PRIORITY_NORMAL</code> and
    below <code>PRIORITY_HIGH</code>. This corresponds to
    <code>ABOVE_NORMAL_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>-7</code> on all other platforms.</td>
  </tr>
  <tr>
    <td><code>PRIORITY_HIGH</code></td>
    <td>The process scheduling priority above <code>PRIORITY_ABOVE_NORMAL</code>
    and below <code>PRIORITY_HIGHEST</code>. This corresponds to
    <code>HIGH_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>-14</code> on all other platforms.</td>
  </tr>
  <tr>
    <td><code>PRIORITY_HIGHEST</code></td>
    <td>The highest process scheduling priority. This corresponds to
    <code>REALTIME_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>-20</code> on all other platforms.</td>
  </tr>
</table>

### libuv constants

<table>
  <tr>
    <th>Constant</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>UV_UDP_REUSEADDR</code></td>
    <td></td>
  </tr>
</table>

[Android building]: https://github.com/nodejs/node/blob/HEAD/BUILDING.md#android
[EUID]: https://en.wikipedia.org/wiki/User_identifier#Effective_user_ID
[`SystemError`]: errors.md#class-systemerror
[`process.arch`]: process.md#processarch
[`process.platform`]: process.md#processplatform
[`uname(3)`]: https://linux.die.net/man/3/uname
[`uv_available_parallelism()`]: https://docs.libuv.org/en/v1.x/misc.html#c.uv_available_parallelism

# Assert

<!--introduced_in=v0.1.21-->

> Stability: 2 - Stable

<!-- source_link=lib/assert.js -->

The `node:assert` module provides a set of assertion functions for verifying
invariants.

## Strict assertion mode

<!-- YAML
added: v9.9.0
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/34001
    description: Exposed as `require('node:assert/strict')`.
  - version:
      - v13.9.0
      - v12.16.2
    pr-url: https://github.com/nodejs/node/pull/31635
    description: Changed "strict mode" to "strict assertion mode" and "legacy
                 mode" to "legacy assertion mode" to avoid confusion with the
                 more usual meaning of "strict mode".
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17615
    description: Added error diffs to the strict assertion mode.
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17002
    description: Added strict assertion mode to the assert module.
-->

In strict assertion mode, non-strict methods behave like their corresponding
strict methods. For example, [`assert.deepEqual()`][] will behave like
[`assert.deepStrictEqual()`][].

In strict assertion mode, error messages for objects display a diff. In legacy
assertion mode, error messages for objects display the objects, often truncated.

To use strict assertion mode:

```mjs
import { strict as assert } from 'node:assert';
```

```cjs
const assert = require('node:assert').strict;
```

```mjs
import assert from 'node:assert/strict';
```

```cjs
const assert = require('node:assert/strict');
```

Example error diff:

```mjs
import { strict as assert } from 'node:assert';

assert.deepEqual([[[1, 2, 3]], 4, 5], [[[1, 2, '3']], 4, 5]);
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected ... Lines skipped
//
//   [
//     [
// ...
//       2,
// +     3
// -     '3'
//     ],
// ...
//     5
//   ]
```

```cjs
const assert = require('node:assert/strict');

assert.deepEqual([[[1, 2, 3]], 4, 5], [[[1, 2, '3']], 4, 5]);
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected ... Lines skipped
//
//   [
//     [
// ...
//       2,
// +     3
// -     '3'
//     ],
// ...
//     5
//   ]
```

To deactivate the colors, use the `NO_COLOR` or `NODE_DISABLE_COLORS`
environment variables. This will also deactivate the colors in the REPL. For
more on color support in terminal environments, read the tty
[`getColorDepth()`][] documentation.

## Legacy assertion mode

Legacy assertion mode uses the [`==` operator][] in:

* [`assert.deepEqual()`][]
* [`assert.equal()`][]
* [`assert.notDeepEqual()`][]
* [`assert.notEqual()`][]

To use legacy assertion mode:

```mjs
import assert from 'node:assert';
```

```cjs
const assert = require('node:assert');
```

Legacy assertion mode may have surprising results, especially when using
[`assert.deepEqual()`][]:

```cjs
// WARNING: This does not throw an AssertionError in legacy assertion mode!
assert.deepEqual(/a/gi, new Date());
```

## Class: assert.AssertionError

* Extends: {errors.Error}

Indicates the failure of an assertion. All errors thrown by the `node:assert`
module will be instances of the `AssertionError` class.

### `new assert.AssertionError(options)`

<!-- YAML
added: v0.1.21
-->

* `options` {Object}
  * `message` {string} If provided, the error message is set to this value.
  * `actual` {any} The `actual` property on the error instance.
  * `expected` {any} The `expected` property on the error instance.
  * `operator` {string} The `operator` property on the error instance.
  * `stackStartFn` {Function} If provided, the generated stack trace omits
    frames before this function.

A subclass of `Error` that indicates the failure of an assertion.

All instances contain the built-in `Error` properties (`message` and `name`)
and:

* `actual` {any} Set to the `actual` argument for methods such as
  [`assert.strictEqual()`][].
* `expected` {any} Set to the `expected` value for methods such as
  [`assert.strictEqual()`][].
* `generatedMessage` {boolean} Indicates if the message was auto-generated
  (`true`) or not.
* `code` {string} Value is always `ERR_ASSERTION` to show that the error is an
  assertion error.
* `operator` {string} Set to the passed in operator value.

```mjs
import assert from 'node:assert';

// Generate an AssertionError to compare the error message later:
const { message } = new assert.AssertionError({
  actual: 1,
  expected: 2,
  operator: 'strictEqual',
});

// Verify error output:
try {
  assert.strictEqual(1, 2);
} catch (err) {
  assert(err instanceof assert.AssertionError);
  assert.strictEqual(err.message, message);
  assert.strictEqual(err.name, 'AssertionError');
  assert.strictEqual(err.actual, 1);
  assert.strictEqual(err.expected, 2);
  assert.strictEqual(err.code, 'ERR_ASSERTION');
  assert.strictEqual(err.operator, 'strictEqual');
  assert.strictEqual(err.generatedMessage, true);
}
```

```cjs
const assert = require('node:assert');

// Generate an AssertionError to compare the error message later:
const { message } = new assert.AssertionError({
  actual: 1,
  expected: 2,
  operator: 'strictEqual',
});

// Verify error output:
try {
  assert.strictEqual(1, 2);
} catch (err) {
  assert(err instanceof assert.AssertionError);
  assert.strictEqual(err.message, message);
  assert.strictEqual(err.name, 'AssertionError');
  assert.strictEqual(err.actual, 1);
  assert.strictEqual(err.expected, 2);
  assert.strictEqual(err.code, 'ERR_ASSERTION');
  assert.strictEqual(err.operator, 'strictEqual');
  assert.strictEqual(err.generatedMessage, true);
}
```

## Class: `assert.CallTracker`

<!-- YAML
added:
  - v14.2.0
  - v12.19.0
changes:
  - version: v20.1.0
    pr-url: https://github.com/nodejs/node/pull/47740
    description: the `assert.CallTracker` class has been deprecated and will be
                  removed in a future version.
-->

> Stability: 0 - Deprecated

This feature is deprecated and will be removed in a future version.
Please consider using alternatives such as the
[`mock`][] helper function.

### `new assert.CallTracker()`

<!-- YAML
added:
  - v14.2.0
  - v12.19.0
-->

Creates a new [`CallTracker`][] object which can be used to track if functions
were called a specific number of times. The `tracker.verify()` must be called
for the verification to take place. The usual pattern would be to call it in a
[`process.on('exit')`][] handler.

```mjs
import assert from 'node:assert';
import process from 'node:process';

const tracker = new assert.CallTracker();

function func() {}

// callsfunc() must be called exactly 1 time before tracker.verify().
const callsfunc = tracker.calls(func, 1);

callsfunc();

// Calls tracker.verify() and verifies if all tracker.calls() functions have
// been called exact times.
process.on('exit', () => {
  tracker.verify();
});
```

```cjs
const assert = require('node:assert');
const process = require('node:process');

const tracker = new assert.CallTracker();

function func() {}

// callsfunc() must be called exactly 1 time before tracker.verify().
const callsfunc = tracker.calls(func, 1);

callsfunc();

// Calls tracker.verify() and verifies if all tracker.calls() functions have
// been called exact times.
process.on('exit', () => {
  tracker.verify();
});
```

### `tracker.calls([fn][, exact])`

<!-- YAML
added:
  - v14.2.0
  - v12.19.0
-->

* `fn` {Function} **Default:** A no-op function.
* `exact` {number} **Default:** `1`.
* Returns: {Function} A function that wraps `fn`.

The wrapper function is expected to be called exactly `exact` times. If the
function has not been called exactly `exact` times when
[`tracker.verify()`][] is called, then [`tracker.verify()`][] will throw an
error.

```mjs
import assert from 'node:assert';

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}

// Returns a function that wraps func() that must be called exact times
// before tracker.verify().
const callsfunc = tracker.calls(func);
```

```cjs
const assert = require('node:assert');

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}

// Returns a function that wraps func() that must be called exact times
// before tracker.verify().
const callsfunc = tracker.calls(func);
```

### `tracker.getCalls(fn)`

<!-- YAML
added:
  - v18.8.0
  - v16.18.0
-->

* `fn` {Function}

* Returns: {Array} An array with all the calls to a tracked function.

* Object {Object}
  * `thisArg` {Object}
  * `arguments` {Array} the arguments passed to the tracked function

```mjs
import assert from 'node:assert';

const tracker = new assert.CallTracker();

function func() {}
const callsfunc = tracker.calls(func);
callsfunc(1, 2, 3);

assert.deepStrictEqual(tracker.getCalls(callsfunc),
                       [{ thisArg: undefined, arguments: [1, 2, 3] }]);
```

```cjs
const assert = require('node:assert');

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}
const callsfunc = tracker.calls(func);
callsfunc(1, 2, 3);

assert.deepStrictEqual(tracker.getCalls(callsfunc),
                       [{ thisArg: undefined, arguments: [1, 2, 3] }]);
```

### `tracker.report()`

<!-- YAML
added:
  - v14.2.0
  - v12.19.0
-->

* Returns: {Array} An array of objects containing information about the wrapper
  functions returned by [`tracker.calls()`][].
* Object {Object}
  * `message` {string}
  * `actual` {number} The actual number of times the function was called.
  * `expected` {number} The number of times the function was expected to be
    called.
  * `operator` {string} The name of the function that is wrapped.
  * `stack` {Object} A stack trace of the function.

The arrays contains information about the expected and actual number of calls of
the functions that have not been called the expected number of times.

```mjs
import assert from 'node:assert';

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}

// Returns a function that wraps func() that must be called exact times
// before tracker.verify().
const callsfunc = tracker.calls(func, 2);

// Returns an array containing information on callsfunc()
console.log(tracker.report());
// [
//  {
//    message: 'Expected the func function to be executed 2 time(s) but was
//    executed 0 time(s).',
//    actual: 0,
//    expected: 2,
//    operator: 'func',
//    stack: stack trace
//  }
// ]
```

```cjs
const assert = require('node:assert');

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}

// Returns a function that wraps func() that must be called exact times
// before tracker.verify().
const callsfunc = tracker.calls(func, 2);

// Returns an array containing information on callsfunc()
console.log(tracker.report());
// [
//  {
//    message: 'Expected the func function to be executed 2 time(s) but was
//    executed 0 time(s).',
//    actual: 0,
//    expected: 2,
//    operator: 'func',
//    stack: stack trace
//  }
// ]
```

### `tracker.reset([fn])`

<!-- YAML
added:
  - v18.8.0
  - v16.18.0
-->

* `fn` {Function} a tracked function to reset.

Reset calls of the call tracker.
If a tracked function is passed as an argument, the calls will be reset for it.
If no arguments are passed, all tracked functions will be reset.

```mjs
import assert from 'node:assert';

const tracker = new assert.CallTracker();

function func() {}
const callsfunc = tracker.calls(func);

callsfunc();
// Tracker was called once
assert.strictEqual(tracker.getCalls(callsfunc).length, 1);

tracker.reset(callsfunc);
assert.strictEqual(tracker.getCalls(callsfunc).length, 0);
```

```cjs
const assert = require('node:assert');

const tracker = new assert.CallTracker();

function func() {}
const callsfunc = tracker.calls(func);

callsfunc();
// Tracker was called once
assert.strictEqual(tracker.getCalls(callsfunc).length, 1);

tracker.reset(callsfunc);
assert.strictEqual(tracker.getCalls(callsfunc).length, 0);
```

### `tracker.verify()`

<!-- YAML
added:
  - v14.2.0
  - v12.19.0
-->

Iterates through the list of functions passed to
[`tracker.calls()`][] and will throw an error for functions that
have not been called the expected number of times.

```mjs
import assert from 'node:assert';

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}

// Returns a function that wraps func() that must be called exact times
// before tracker.verify().
const callsfunc = tracker.calls(func, 2);

callsfunc();

// Will throw an error since callsfunc() was only called once.
tracker.verify();
```

```cjs
const assert = require('node:assert');

// Creates call tracker.
const tracker = new assert.CallTracker();

function func() {}

// Returns a function that wraps func() that must be called exact times
// before tracker.verify().
const callsfunc = tracker.calls(func, 2);

callsfunc();

// Will throw an error since callsfunc() was only called once.
tracker.verify();
```

## `assert(value[, message])`

<!-- YAML
added: v0.5.9
-->

* `value` {any} The input that is checked for being truthy.
* `message` {string|Error}

An alias of [`assert.ok()`][].

## `assert.deepEqual(actual, expected[, message])`

<!-- YAML
added: v0.1.21
changes:
  - version:
      - v22.2.0
      - v20.15.0
    pr-url: https://github.com/nodejs/node/pull/51805
    description: Error cause and errors properties are now compared as well.
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41020
    description: Regular expressions lastIndex property is now compared as well.
  - version:
      - v16.0.0
      - v14.18.0
    pr-url: https://github.com/nodejs/node/pull/38113
    description: In Legacy assertion mode, changed status from Deprecated to
                 Legacy.
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/30766
    description: NaN is now treated as being identical if both sides are
                 NaN.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/25008
    description: The type tags are now properly compared and there are a couple
                 minor comparison adjustments to make the check less surprising.
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15001
    description: The `Error` names and messages are now properly compared.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12142
    description: The `Set` and `Map` content is also compared.
  - version:
      - v6.4.0
      - v4.7.1
    pr-url: https://github.com/nodejs/node/pull/8002
    description: Typed array slices are handled correctly now.
  - version:
      - v6.1.0
      - v4.5.0
    pr-url: https://github.com/nodejs/node/pull/6432
    description: Objects with circular references can be used as inputs now.
  - version:
      - v5.10.1
      - v4.4.3
    pr-url: https://github.com/nodejs/node/pull/5910
    description: Handle non-`Uint8Array` typed arrays correctly.
-->

* `actual` {any}
* `expected` {any}
* `message` {string|Error}

**Strict assertion mode**

An alias of [`assert.deepStrictEqual()`][].

**Legacy assertion mode**

> Stability: 3 - Legacy: Use [`assert.deepStrictEqual()`][] instead.

Tests for deep equality between the `actual` and `expected` parameters. Consider
using [`assert.deepStrictEqual()`][] instead. [`assert.deepEqual()`][] can have
surprising results.

_Deep equality_ means that the enumerable "own" properties of child objects
are also recursively evaluated by the following rules.

### Comparison details

* Primitive values are compared with the [`==` operator][],
  with the exception of `NaN`. It is treated as being identical in case
  both sides are `NaN`.
* [Type tags][Object.prototype.toString()] of objects should be the same.
* Only [enumerable "own" properties][] are considered.
* [`Error`][] names, messages, causes, and errors are always compared,
  even if these are not enumerable properties.
* [Object wrappers][] are compared both as objects and unwrapped values.
* `Object` properties are compared unordered.
* [`Map`][] keys and [`Set`][] items are compared unordered.
* Recursion stops when both sides differ or both sides encounter a circular
  reference.
* Implementation does not test the [`[[Prototype]]`][prototype-spec] of
  objects.
* [`Symbol`][] properties are not compared.
* [`WeakMap`][] and [`WeakSet`][] comparison does not rely on their values
  but only on their instances.
* [`RegExp`][] lastIndex, flags, and source are always compared, even if these
  are not enumerable properties.

The following example does not throw an [`AssertionError`][] because the
primitives are compared using the [`==` operator][].

```mjs
import assert from 'node:assert';
// WARNING: This does not throw an AssertionError!

assert.deepEqual('+00000000', false);
```

```cjs
const assert = require('node:assert');
// WARNING: This does not throw an AssertionError!

assert.deepEqual('+00000000', false);
```

"Deep" equality means that the enumerable "own" properties of child objects
are evaluated also:

```mjs
import assert from 'node:assert';

const obj1 = {
  a: {
    b: 1,
  },
};
const obj2 = {
  a: {
    b: 2,
  },
};
const obj3 = {
  a: {
    b: 1,
  },
};
const obj4 = { __proto__: obj1 };

assert.deepEqual(obj1, obj1);
// OK

// Values of b are different:
assert.deepEqual(obj1, obj2);
// AssertionError: { a: { b: 1 } } deepEqual { a: { b: 2 } }

assert.deepEqual(obj1, obj3);
// OK

// Prototypes are ignored:
assert.deepEqual(obj1, obj4);
// AssertionError: { a: { b: 1 } } deepEqual {}
```

```cjs
const assert = require('node:assert');

const obj1 = {
  a: {
    b: 1,
  },
};
const obj2 = {
  a: {
    b: 2,
  },
};
const obj3 = {
  a: {
    b: 1,
  },
};
const obj4 = { __proto__: obj1 };

assert.deepEqual(obj1, obj1);
// OK

// Values of b are different:
assert.deepEqual(obj1, obj2);
// AssertionError: { a: { b: 1 } } deepEqual { a: { b: 2 } }

assert.deepEqual(obj1, obj3);
// OK

// Prototypes are ignored:
assert.deepEqual(obj1, obj4);
// AssertionError: { a: { b: 1 } } deepEqual {}
```

If the values are not equal, an [`AssertionError`][] is thrown with a `message`
property set equal to the value of the `message` parameter. If the `message`
parameter is undefined, a default error message is assigned. If the `message`
parameter is an instance of an [`Error`][] then it will be thrown instead of the
[`AssertionError`][].

## `assert.deepStrictEqual(actual, expected[, message])`

<!-- YAML
added: v1.2.0
changes:
  - version:
    - v22.2.0
    - v20.15.0
    pr-url: https://github.com/nodejs/node/pull/51805
    description: Error cause and errors properties are now compared as well.
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41020
    description: Regular expressions lastIndex property is now compared as well.
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15169
    description: Enumerable symbol properties are now compared.
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15036
    description: The `NaN` is now compared using the
              [SameValueZero](https://tc39.github.io/ecma262/#sec-samevaluezero)
              comparison.
  - version: v8.5.0
    pr-url: https://github.com/nodejs/node/pull/15001
    description: The `Error` names and messages are now properly compared.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12142
    description: The `Set` and `Map` content is also compared.
  - version:
    - v6.4.0
    - v4.7.1
    pr-url: https://github.com/nodejs/node/pull/8002
    description: Typed array slices are handled correctly now.
  - version: v6.1.0
    pr-url: https://github.com/nodejs/node/pull/6432
    description: Objects with circular references can be used as inputs now.
  - version:
    - v5.10.1
    - v4.4.3
    pr-url: https://github.com/nodejs/node/pull/5910
    description: Handle non-`Uint8Array` typed arrays correctly.
-->

* `actual` {any}
* `expected` {any}
* `message` {string|Error}

Tests for deep equality between the `actual` and `expected` parameters.
"Deep" equality means that the enumerable "own" properties of child objects
are recursively evaluated also by the following rules.

### Comparison details

* Primitive values are compared using [`Object.is()`][].
* [Type tags][Object.prototype.toString()] of objects should be the same.
* [`[[Prototype]]`][prototype-spec] of objects are compared using
  the [`===` operator][].
* Only [enumerable "own" properties][] are considered.
* [`Error`][] names, messages, causes, and errors are always compared,
  even if these are not enumerable properties.
  `errors` is also compared.
* Enumerable own [`Symbol`][] properties are compared as well.
* [Object wrappers][] are compared both as objects and unwrapped values.
* `Object` properties are compared unordered.
* [`Map`][] keys and [`Set`][] items are compared unordered.
* Recursion stops when both sides differ or both sides encounter a circular
  reference.
* [`WeakMap`][] and [`WeakSet`][] instances are **not** compared structurally.
  They are only equal if they reference the same object. Any comparison between
  different `WeakMap` or `WeakSet` instances will result in inequality,
  even if they contain the same entries.
* [`RegExp`][] lastIndex, flags, and source are always compared, even if these
  are not enumerable properties.

```mjs
import assert from 'node:assert/strict';

// This fails because 1 !== '1'.
assert.deepStrictEqual({ a: 1 }, { a: '1' });
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected
//
//   {
// +   a: 1
// -   a: '1'
//   }

// The following objects don't have own properties
const date = new Date();
const object = {};
const fakeDate = {};
Object.setPrototypeOf(fakeDate, Date.prototype);

// Different [[Prototype]]:
assert.deepStrictEqual(object, fakeDate);
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected
//
// + {}
// - Date {}

// Different type tags:
assert.deepStrictEqual(date, fakeDate);
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected
//
// + 2018-04-26T00:49:08.604Z
// - Date {}

assert.deepStrictEqual(NaN, NaN);
// OK because Object.is(NaN, NaN) is true.

// Different unwrapped numbers:
assert.deepStrictEqual(new Number(1), new Number(2));
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected
//
// + [Number: 1]
// - [Number: 2]

assert.deepStrictEqual(new String('foo'), Object('foo'));
// OK because the object and the string are identical when unwrapped.

assert.deepStrictEqual(-0, -0);
// OK

// Different zeros:
assert.deepStrictEqual(0, -0);
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected
//
// + 0
// - -0

const symbol1 = Symbol();
const symbol2 = Symbol();
assert.deepStrictEqual({ [symbol1]: 1 }, { [symbol1]: 1 });
// OK, because it is the same symbol on both objects.

assert.deepStrictEqual({ [symbol1]: 1 }, { [symbol2]: 1 });
// AssertionError [ERR_ASSERTION]: Inputs identical but not reference equal:
//
// {
//   Symbol(): 1
// }

const weakMap1 = new WeakMap();
const weakMap2 = new WeakMap();
const obj = {};

weakMap1.set(obj, 'value');
weakMap2.set(obj, 'value');

// Comparing different instances fails, even with same contents
assert.deepStrictEqual(weakMap1, weakMap2);
// AssertionError: Values have same structure but are not reference-equal:
//
// WeakMap {
//   <items unknown>
// }

// Comparing the same instance to itself succeeds
assert.deepStrictEqual(weakMap1, weakMap1);
// OK

const weakSet1 = new WeakSet();
const weakSet2 = new WeakSet();
weakSet1.add(obj);
weakSet2.add(obj);

// Comparing different instances fails, even with same contents
assert.deepStrictEqual(weakSet1, weakSet2);
// AssertionError: Values have same structure but are not reference-equal:
// + actual - expected
//
// WeakSet {
//   <items unknown>
// }

// Comparing the same instance to itself succeeds
assert.deepStrictEqual(weakSet1, weakSet1);
// OK
```

```cjs
const assert = require('node:assert/strict');

// This fails because 1 !== '1'.
assert.deepStrictEqual({ a: 1 }, { a: '1' });
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected
//
//   {
// +   a: 1
// -   a: '1'
//   }

// The following objects don't have own properties
const date = new Date();
const object = {};
const fakeDate = {};
Object.setPrototypeOf(fakeDate, Date.prototype);

// Different [[Prototype]]:
assert.deepStrictEqual(object, fakeDate);
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected
//
// + {}
// - Date {}

// Different type tags:
assert.deepStrictEqual(date, fakeDate);
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected
//
// + 2018-04-26T00:49:08.604Z
// - Date {}

assert.deepStrictEqual(NaN, NaN);
// OK because Object.is(NaN, NaN) is true.

// Different unwrapped numbers:
assert.deepStrictEqual(new Number(1), new Number(2));
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected
//
// + [Number: 1]
// - [Number: 2]

assert.deepStrictEqual(new String('foo'), Object('foo'));
// OK because the object and the string are identical when unwrapped.

assert.deepStrictEqual(-0, -0);
// OK

// Different zeros:
assert.deepStrictEqual(0, -0);
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected
//
// + 0
// - -0

const symbol1 = Symbol();
const symbol2 = Symbol();
assert.deepStrictEqual({ [symbol1]: 1 }, { [symbol1]: 1 });
// OK, because it is the same symbol on both objects.

assert.deepStrictEqual({ [symbol1]: 1 }, { [symbol2]: 1 });
// AssertionError [ERR_ASSERTION]: Inputs identical but not reference equal:
//
// {
//   Symbol(): 1
// }

const weakMap1 = new WeakMap();
const weakMap2 = new WeakMap();
const obj = {};

weakMap1.set(obj, 'value');
weakMap2.set(obj, 'value');

// Comparing different instances fails, even with same contents
assert.deepStrictEqual(weakMap1, weakMap2);
// AssertionError: Values have same structure but are not reference-equal:
//
// WeakMap {
//   <items unknown>
// }

// Comparing the same instance to itself succeeds
assert.deepStrictEqual(weakMap1, weakMap1);
// OK

const weakSet1 = new WeakSet();
const weakSet2 = new WeakSet();
weakSet1.add(obj);
weakSet2.add(obj);

// Comparing different instances fails, even with same contents
assert.deepStrictEqual(weakSet1, weakSet2);
// AssertionError: Values have same structure but are not reference-equal:
// + actual - expected
//
// WeakSet {
//   <items unknown>
// }

// Comparing the same instance to itself succeeds
assert.deepStrictEqual(weakSet1, weakSet1);
// OK
```

If the values are not equal, an [`AssertionError`][] is thrown with a `message`
property set equal to the value of the `message` parameter. If the `message`
parameter is undefined, a default error message is assigned. If the `message`
parameter is an instance of an [`Error`][] then it will be thrown instead of the
`AssertionError`.

## `assert.doesNotMatch(string, regexp[, message])`

<!-- YAML
added:
  - v13.6.0
  - v12.16.0
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/38111
    description: This API is no longer experimental.
-->

* `string` {string}
* `regexp` {RegExp}
* `message` {string|Error}

Expects the `string` input not to match the regular expression.

```mjs
import assert from 'node:assert/strict';

assert.doesNotMatch('I will fail', /fail/);
// AssertionError [ERR_ASSERTION]: The input was expected to not match the ...

assert.doesNotMatch(123, /pass/);
// AssertionError [ERR_ASSERTION]: The "string" argument must be of type string.

assert.doesNotMatch('I will pass', /different/);
// OK
```

```cjs
const assert = require('node:assert/strict');

assert.doesNotMatch('I will fail', /fail/);
// AssertionError [ERR_ASSERTION]: The input was expected to not match the ...

assert.doesNotMatch(123, /pass/);
// AssertionError [ERR_ASSERTION]: The "string" argument must be of type string.

assert.doesNotMatch('I will pass', /different/);
// OK
```

If the values do match, or if the `string` argument is of another type than
`string`, an [`AssertionError`][] is thrown with a `message` property set equal
to the value of the `message` parameter. If the `message` parameter is
undefined, a default error message is assigned. If the `message` parameter is an
instance of an [`Error`][] then it will be thrown instead of the
[`AssertionError`][].

## `assert.doesNotReject(asyncFn[, error][, message])`

<!-- YAML
added: v10.0.0
-->

* `asyncFn` {Function|Promise}
* `error` {RegExp|Function}
* `message` {string}

Awaits the `asyncFn` promise or, if `asyncFn` is a function, immediately
calls the function and awaits the returned promise to complete. It will then
check that the promise is not rejected.

If `asyncFn` is a function and it throws an error synchronously,
`assert.doesNotReject()` will return a rejected `Promise` with that error. If
the function does not return a promise, `assert.doesNotReject()` will return a
rejected `Promise` with an [`ERR_INVALID_RETURN_VALUE`][] error. In both cases
the error handler is skipped.

Using `assert.doesNotReject()` is actually not useful because there is little
benefit in catching a rejection and then rejecting it again. Instead, consider
adding a comment next to the specific code path that should not reject and keep
error messages as expressive as possible.

If specified, `error` can be a [`Class`][], [`RegExp`][], or a validation
function. See [`assert.throws()`][] for more details.

Besides the async nature to await the completion behaves identically to
[`assert.doesNotThrow()`][].

```mjs
import assert from 'node:assert/strict';

await assert.doesNotReject(
  async () => {
    throw new TypeError('Wrong value');
  },
  SyntaxError,
);
```

```cjs
const assert = require('node:assert/strict');

(async () => {
  await assert.doesNotReject(
    async () => {
      throw new TypeError('Wrong value');
    },
    SyntaxError,
  );
})();
```

```mjs
import assert from 'node:assert/strict';

assert.doesNotReject(Promise.reject(new TypeError('Wrong value')))
  .then(() => {
    // ...
  });
```

```cjs
const assert = require('node:assert/strict');

assert.doesNotReject(Promise.reject(new TypeError('Wrong value')))
  .then(() => {
    // ...
  });
```

## `assert.doesNotThrow(fn[, error][, message])`

<!-- YAML
added: v0.1.21
changes:
  - version:
    - v5.11.0
    - v4.4.5
    pr-url: https://github.com/nodejs/node/pull/2407
    description: The `message` parameter is respected now.
  - version: v4.2.0
    pr-url: https://github.com/nodejs/node/pull/3276
    description: The `error` parameter can now be an arrow function.
-->

* `fn` {Function}
* `error` {RegExp|Function}
* `message` {string}

Asserts that the function `fn` does not throw an error.

Using `assert.doesNotThrow()` is actually not useful because there
is no benefit in catching an error and then rethrowing it. Instead, consider
adding a comment next to the specific code path that should not throw and keep
error messages as expressive as possible.

When `assert.doesNotThrow()` is called, it will immediately call the `fn`
function.

If an error is thrown and it is the same type as that specified by the `error`
parameter, then an [`AssertionError`][] is thrown. If the error is of a
different type, or if the `error` parameter is undefined, the error is
propagated back to the caller.

If specified, `error` can be a [`Class`][], [`RegExp`][], or a validation
function. See [`assert.throws()`][] for more details.

The following, for instance, will throw the [`TypeError`][] because there is no
matching error type in the assertion:

```mjs
import assert from 'node:assert/strict';

assert.doesNotThrow(
  () => {
    throw new TypeError('Wrong value');
  },
  SyntaxError,
);
```

```cjs
const assert = require('node:assert/strict');

assert.doesNotThrow(
  () => {
    throw new TypeError('Wrong value');
  },
  SyntaxError,
);
```

However, the following will result in an [`AssertionError`][] with the message
'Got unwanted exception...':

```mjs
import assert from 'node:assert/strict';

assert.doesNotThrow(
  () => {
    throw new TypeError('Wrong value');
  },
  TypeError,
);
```

```cjs
const assert = require('node:assert/strict');

assert.doesNotThrow(
  () => {
    throw new TypeError('Wrong value');
  },
  TypeError,
);
```

If an [`AssertionError`][] is thrown and a value is provided for the `message`
parameter, the value of `message` will be appended to the [`AssertionError`][]
message:

```mjs
import assert from 'node:assert/strict';

assert.doesNotThrow(
  () => {
    throw new TypeError('Wrong value');
  },
  /Wrong value/,
  'Whoops',
);
// Throws: AssertionError: Got unwanted exception: Whoops
```

```cjs
const assert = require('node:assert/strict');

assert.doesNotThrow(
  () => {
    throw new TypeError('Wrong value');
  },
  /Wrong value/,
  'Whoops',
);
// Throws: AssertionError: Got unwanted exception: Whoops
```

## `assert.equal(actual, expected[, message])`

<!-- YAML
added: v0.1.21
changes:
  - version:
      - v16.0.0
      - v14.18.0
    pr-url: https://github.com/nodejs/node/pull/38113
    description: In Legacy assertion mode, changed status from Deprecated to
                 Legacy.
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/30766
    description: NaN is now treated as being identical if both sides are
                 NaN.
-->

* `actual` {any}
* `expected` {any}
* `message` {string|Error}

**Strict assertion mode**

An alias of [`assert.strictEqual()`][].

**Legacy assertion mode**

> Stability: 3 - Legacy: Use [`assert.strictEqual()`][] instead.

Tests shallow, coercive equality between the `actual` and `expected` parameters
using the [`==` operator][]. `NaN` is specially handled
and treated as being identical if both sides are `NaN`.

```mjs
import assert from 'node:assert';

assert.equal(1, 1);
// OK, 1 == 1
assert.equal(1, '1');
// OK, 1 == '1'
assert.equal(NaN, NaN);
// OK

assert.equal(1, 2);
// AssertionError: 1 == 2
assert.equal({ a: { b: 1 } }, { a: { b: 1 } });
// AssertionError: { a: { b: 1 } } == { a: { b: 1 } }
```

```cjs
const assert = require('node:assert');

assert.equal(1, 1);
// OK, 1 == 1
assert.equal(1, '1');
// OK, 1 == '1'
assert.equal(NaN, NaN);
// OK

assert.equal(1, 2);
// AssertionError: 1 == 2
assert.equal({ a: { b: 1 } }, { a: { b: 1 } });
// AssertionError: { a: { b: 1 } } == { a: { b: 1 } }
```

If the values are not equal, an [`AssertionError`][] is thrown with a `message`
property set equal to the value of the `message` parameter. If the `message`
parameter is undefined, a default error message is assigned. If the `message`
parameter is an instance of an [`Error`][] then it will be thrown instead of the
`AssertionError`.

## `assert.fail([message])`

<!-- YAML
added: v0.1.21
-->

* `message` {string|Error} **Default:** `'Failed'`

Throws an [`AssertionError`][] with the provided error message or a default
error message. If the `message` parameter is an instance of an [`Error`][] then
it will be thrown instead of the [`AssertionError`][].

```mjs
import assert from 'node:assert/strict';

assert.fail();
// AssertionError [ERR_ASSERTION]: Failed

assert.fail('boom');
// AssertionError [ERR_ASSERTION]: boom

assert.fail(new TypeError('need array'));
// TypeError: need array
```

```cjs
const assert = require('node:assert/strict');

assert.fail();
// AssertionError [ERR_ASSERTION]: Failed

assert.fail('boom');
// AssertionError [ERR_ASSERTION]: boom

assert.fail(new TypeError('need array'));
// TypeError: need array
```

Using `assert.fail()` with more than two arguments is possible but deprecated.
See below for further details.

## `assert.fail(actual, expected[, message[, operator[, stackStartFn]]])`

<!-- YAML
added: v0.1.21
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18418
    description: Calling `assert.fail()` with more than one argument is
                 deprecated and emits a warning.
-->

> Stability: 0 - Deprecated: Use `assert.fail([message])` or other assert
> functions instead.

* `actual` {any}
* `expected` {any}
* `message` {string|Error}
* `operator` {string} **Default:** `'!='`
* `stackStartFn` {Function} **Default:** `assert.fail`

If `message` is falsy, the error message is set as the values of `actual` and
`expected` separated by the provided `operator`. If just the two `actual` and
`expected` arguments are provided, `operator` will default to `'!='`. If
`message` is provided as third argument it will be used as the error message and
the other arguments will be stored as properties on the thrown object. If
`stackStartFn` is provided, all stack frames above that function will be
removed from stacktrace (see [`Error.captureStackTrace`][]). If no arguments are
given, the default message `Failed` will be used.

```mjs
import assert from 'node:assert/strict';

assert.fail('a', 'b');
// AssertionError [ERR_ASSERTION]: 'a' != 'b'

assert.fail(1, 2, undefined, '>');
// AssertionError [ERR_ASSERTION]: 1 > 2

assert.fail(1, 2, 'fail');
// AssertionError [ERR_ASSERTION]: fail

assert.fail(1, 2, 'whoops', '>');
// AssertionError [ERR_ASSERTION]: whoops

assert.fail(1, 2, new TypeError('need array'));
// TypeError: need array
```

```cjs
const assert = require('node:assert/strict');

assert.fail('a', 'b');
// AssertionError [ERR_ASSERTION]: 'a' != 'b'

assert.fail(1, 2, undefined, '>');
// AssertionError [ERR_ASSERTION]: 1 > 2

assert.fail(1, 2, 'fail');
// AssertionError [ERR_ASSERTION]: fail

assert.fail(1, 2, 'whoops', '>');
// AssertionError [ERR_ASSERTION]: whoops

assert.fail(1, 2, new TypeError('need array'));
// TypeError: need array
```

In the last three cases `actual`, `expected`, and `operator` have no
influence on the error message.

Example use of `stackStartFn` for truncating the exception's stacktrace:

```mjs
import assert from 'node:assert/strict';

function suppressFrame() {
  assert.fail('a', 'b', undefined, '!==', suppressFrame);
}
suppressFrame();
// AssertionError [ERR_ASSERTION]: 'a' !== 'b'
//     at repl:1:1
//     at ContextifyScript.Script.runInThisContext (vm.js:44:33)
//     ...
```

```cjs
const assert = require('node:assert/strict');

function suppressFrame() {
  assert.fail('a', 'b', undefined, '!==', suppressFrame);
}
suppressFrame();
// AssertionError [ERR_ASSERTION]: 'a' !== 'b'
//     at repl:1:1
//     at ContextifyScript.Script.runInThisContext (vm.js:44:33)
//     ...
```

## `assert.ifError(value)`

<!-- YAML
added: v0.1.97
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18247
    description: Instead of throwing the original error it is now wrapped into
                 an [`AssertionError`][] that contains the full stack trace.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18247
    description: Value may now only be `undefined` or `null`. Before all falsy
                 values were handled the same as `null` and did not throw.
-->

* `value` {any}

Throws `value` if `value` is not `undefined` or `null`. This is useful when
testing the `error` argument in callbacks. The stack trace contains all frames
from the error passed to `ifError()` including the potential new frames for
`ifError()` itself.

```mjs
import assert from 'node:assert/strict';

assert.ifError(null);
// OK
assert.ifError(0);
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: 0
assert.ifError('error');
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: 'error'
assert.ifError(new Error());
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: Error

// Create some random error frames.
let err;
(function errorFrame() {
  err = new Error('test error');
})();

(function ifErrorFrame() {
  assert.ifError(err);
})();
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: test error
//     at ifErrorFrame
//     at errorFrame
```

```cjs
const assert = require('node:assert/strict');

assert.ifError(null);
// OK
assert.ifError(0);
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: 0
assert.ifError('error');
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: 'error'
assert.ifError(new Error());
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: Error

// Create some random error frames.
let err;
(function errorFrame() {
  err = new Error('test error');
})();

(function ifErrorFrame() {
  assert.ifError(err);
})();
// AssertionError [ERR_ASSERTION]: ifError got unwanted exception: test error
//     at ifErrorFrame
//     at errorFrame
```

## `assert.match(string, regexp[, message])`

<!-- YAML
added:
  - v13.6.0
  - v12.16.0
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/38111
    description: This API is no longer experimental.
-->

* `string` {string}
* `regexp` {RegExp}
* `message` {string|Error}

Expects the `string` input to match the regular expression.

```mjs
import assert from 'node:assert/strict';

assert.match('I will fail', /pass/);
// AssertionError [ERR_ASSERTION]: The input did not match the regular ...

assert.match(123, /pass/);
// AssertionError [ERR_ASSERTION]: The "string" argument must be of type string.

assert.match('I will pass', /pass/);
// OK
```

```cjs
const assert = require('node:assert/strict');

assert.match('I will fail', /pass/);
// AssertionError [ERR_ASSERTION]: The input did not match the regular ...

assert.match(123, /pass/);
// AssertionError [ERR_ASSERTION]: The "string" argument must be of type string.

assert.match('I will pass', /pass/);
// OK
```

If the values do not match, or if the `string` argument is of another type than
`string`, an [`AssertionError`][] is thrown with a `message` property set equal
to the value of the `message` parameter. If the `message` parameter is
undefined, a default error message is assigned. If the `message` parameter is an
instance of an [`Error`][] then it will be thrown instead of the
[`AssertionError`][].

## `assert.notDeepEqual(actual, expected[, message])`

<!-- YAML
added: v0.1.21
changes:
  - version:
      - v16.0.0
      - v14.18.0
    pr-url: https://github.com/nodejs/node/pull/38113
    description: In Legacy assertion mode, changed status from Deprecated to
                 Legacy.
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/30766
    description: NaN is now treated as being identical if both sides are
                 NaN.
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15001
    description: The `Error` names and messages are now properly compared.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12142
    description: The `Set` and `Map` content is also compared.
  - version:
      - v6.4.0
      - v4.7.1
    pr-url: https://github.com/nodejs/node/pull/8002
    description: Typed array slices are handled correctly now.
  - version:
      - v6.1.0
      - v4.5.0
    pr-url: https://github.com/nodejs/node/pull/6432
    description: Objects with circular references can be used as inputs now.
  - version:
      - v5.10.1
      - v4.4.3
    pr-url: https://github.com/nodejs/node/pull/5910
    description: Handle non-`Uint8Array` typed arrays correctly.
-->

* `actual` {any}
* `expected` {any}
* `message` {string|Error}

**Strict assertion mode**

An alias of [`assert.notDeepStrictEqual()`][].

**Legacy assertion mode**

> Stability: 3 - Legacy: Use [`assert.notDeepStrictEqual()`][] instead.

Tests for any deep inequality. Opposite of [`assert.deepEqual()`][].

```mjs
import assert from 'node:assert';

const obj1 = {
  a: {
    b: 1,
  },
};
const obj2 = {
  a: {
    b: 2,
  },
};
const obj3 = {
  a: {
    b: 1,
  },
};
const obj4 = { __proto__: obj1 };

assert.notDeepEqual(obj1, obj1);
// AssertionError: { a: { b: 1 } } notDeepEqual { a: { b: 1 } }

assert.notDeepEqual(obj1, obj2);
// OK

assert.notDeepEqual(obj1, obj3);
// AssertionError: { a: { b: 1 } } notDeepEqual { a: { b: 1 } }

assert.notDeepEqual(obj1, obj4);
// OK
```

```cjs
const assert = require('node:assert');

const obj1 = {
  a: {
    b: 1,
  },
};
const obj2 = {
  a: {
    b: 2,
  },
};
const obj3 = {
  a: {
    b: 1,
  },
};
const obj4 = { __proto__: obj1 };

assert.notDeepEqual(obj1, obj1);
// AssertionError: { a: { b: 1 } } notDeepEqual { a: { b: 1 } }

assert.notDeepEqual(obj1, obj2);
// OK

assert.notDeepEqual(obj1, obj3);
// AssertionError: { a: { b: 1 } } notDeepEqual { a: { b: 1 } }

assert.notDeepEqual(obj1, obj4);
// OK
```

If the values are deeply equal, an [`AssertionError`][] is thrown with a
`message` property set equal to the value of the `message` parameter. If the
`message` parameter is undefined, a default error message is assigned. If the
`message` parameter is an instance of an [`Error`][] then it will be thrown
instead of the `AssertionError`.

## `assert.notDeepStrictEqual(actual, expected[, message])`

<!-- YAML
added: v1.2.0
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15398
    description: The `-0` and `+0` are not considered equal anymore.
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15036
    description: The `NaN` is now compared using the
              [SameValueZero](https://tc39.github.io/ecma262/#sec-samevaluezero)
              comparison.
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15001
    description: The `Error` names and messages are now properly compared.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12142
    description: The `Set` and `Map` content is also compared.
  - version:
    - v6.4.0
    - v4.7.1
    pr-url: https://github.com/nodejs/node/pull/8002
    description: Typed array slices are handled correctly now.
  - version: v6.1.0
    pr-url: https://github.com/nodejs/node/pull/6432
    description: Objects with circular references can be used as inputs now.
  - version:
    - v5.10.1
    - v4.4.3
    pr-url: https://github.com/nodejs/node/pull/5910
    description: Handle non-`Uint8Array` typed arrays correctly.
-->

* `actual` {any}
* `expected` {any}
* `message` {string|Error}

Tests for deep strict inequality. Opposite of [`assert.deepStrictEqual()`][].

```mjs
import assert from 'node:assert/strict';

assert.notDeepStrictEqual({ a: 1 }, { a: '1' });
// OK
```

```cjs
const assert = require('node:assert/strict');

assert.notDeepStrictEqual({ a: 1 }, { a: '1' });
// OK
```

If the values are deeply and strictly equal, an [`AssertionError`][] is thrown
with a `message` property set equal to the value of the `message` parameter. If
the `message` parameter is undefined, a default error message is assigned. If
the `message` parameter is an instance of an [`Error`][] then it will be thrown
instead of the [`AssertionError`][].

## `assert.notEqual(actual, expected[, message])`

<!-- YAML
added: v0.1.21
changes:
  - version:
      - v16.0.0
      - v14.18.0
    pr-url: https://github.com/nodejs/node/pull/38113
    description: In Legacy assertion mode, changed status from Deprecated to
                 Legacy.
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/30766
    description: NaN is now treated as being identical if both sides are
                 NaN.
-->

* `actual` {any}
* `expected` {any}
* `message` {string|Error}

**Strict assertion mode**

An alias of [`assert.notStrictEqual()`][].

**Legacy assertion mode**

> Stability: 3 - Legacy: Use [`assert.notStrictEqual()`][] instead.

Tests shallow, coercive inequality with the [`!=` operator][]. `NaN` is
specially handled and treated as being identical if both sides are `NaN`.

```mjs
import assert from 'node:assert';

assert.notEqual(1, 2);
// OK

assert.notEqual(1, 1);
// AssertionError: 1 != 1

assert.notEqual(1, '1');
// AssertionError: 1 != '1'
```

```cjs
const assert = require('node:assert');

assert.notEqual(1, 2);
// OK

assert.notEqual(1, 1);
// AssertionError: 1 != 1

assert.notEqual(1, '1');
// AssertionError: 1 != '1'
```

If the values are equal, an [`AssertionError`][] is thrown with a `message`
property set equal to the value of the `message` parameter. If the `message`
parameter is undefined, a default error message is assigned. If the `message`
parameter is an instance of an [`Error`][] then it will be thrown instead of the
`AssertionError`.

## `assert.notStrictEqual(actual, expected[, message])`

<!-- YAML
added: v0.1.21
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17003
    description: Used comparison changed from Strict Equality to `Object.is()`.
-->

* `actual` {any}
* `expected` {any}
* `message` {string|Error}

Tests strict inequality between the `actual` and `expected` parameters as
determined by [`Object.is()`][].

```mjs
import assert from 'node:assert/strict';

assert.notStrictEqual(1, 2);
// OK

assert.notStrictEqual(1, 1);
// AssertionError [ERR_ASSERTION]: Expected "actual" to be strictly unequal to:
//
// 1

assert.notStrictEqual(1, '1');
// OK
```

```cjs
const assert = require('node:assert/strict');

assert.notStrictEqual(1, 2);
// OK

assert.notStrictEqual(1, 1);
// AssertionError [ERR_ASSERTION]: Expected "actual" to be strictly unequal to:
//
// 1

assert.notStrictEqual(1, '1');
// OK
```

If the values are strictly equal, an [`AssertionError`][] is thrown with a
`message` property set equal to the value of the `message` parameter. If the
`message` parameter is undefined, a default error message is assigned. If the
`message` parameter is an instance of an [`Error`][] then it will be thrown
instead of the `AssertionError`.

## `assert.ok(value[, message])`

<!-- YAML
added: v0.1.21
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18319
    description: The `assert.ok()` (no arguments) will now use a predefined
                 error message.
-->

* `value` {any}
* `message` {string|Error}

Tests if `value` is truthy. It is equivalent to
`assert.equal(!!value, true, message)`.

If `value` is not truthy, an [`AssertionError`][] is thrown with a `message`
property set equal to the value of the `message` parameter. If the `message`
parameter is `undefined`, a default error message is assigned. If the `message`
parameter is an instance of an [`Error`][] then it will be thrown instead of the
`AssertionError`.
If no arguments are passed in at all `message` will be set to the string:
``'No value argument passed to `assert.ok()`'``.

Be aware that in the `repl` the error message will be different to the one
thrown in a file! See below for further details.

```mjs
import assert from 'node:assert/strict';

assert.ok(true);
// OK
assert.ok(1);
// OK

assert.ok();
// AssertionError: No value argument passed to `assert.ok()`

assert.ok(false, 'it\'s false');
// AssertionError: it's false

// In the repl:
assert.ok(typeof 123 === 'string');
// AssertionError: false == true

// In a file (e.g. test.js):
assert.ok(typeof 123 === 'string');
// AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(typeof 123 === 'string')

assert.ok(false);
// AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(false)

assert.ok(0);
// AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(0)
```

```cjs
const assert = require('node:assert/strict');

assert.ok(true);
// OK
assert.ok(1);
// OK

assert.ok();
// AssertionError: No value argument passed to `assert.ok()`

assert.ok(false, 'it\'s false');
// AssertionError: it's false

// In the repl:
assert.ok(typeof 123 === 'string');
// AssertionError: false == true

// In a file (e.g. test.js):
assert.ok(typeof 123 === 'string');
// AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(typeof 123 === 'string')

assert.ok(false);
// AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(false)

assert.ok(0);
// AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(0)
```

```mjs
import assert from 'node:assert/strict';

// Using `assert()` works the same:
assert(0);
// AssertionError: The expression evaluated to a falsy value:
//
//   assert(0)
```

```cjs
const assert = require('node:assert');

// Using `assert()` works the same:
assert(0);
// AssertionError: The expression evaluated to a falsy value:
//
//   assert(0)
```

## `assert.rejects(asyncFn[, error][, message])`

<!-- YAML
added: v10.0.0
-->

* `asyncFn` {Function|Promise}
* `error` {RegExp|Function|Object|Error}
* `message` {string}

Awaits the `asyncFn` promise or, if `asyncFn` is a function, immediately
calls the function and awaits the returned promise to complete. It will then
check that the promise is rejected.

If `asyncFn` is a function and it throws an error synchronously,
`assert.rejects()` will return a rejected `Promise` with that error. If the
function does not return a promise, `assert.rejects()` will return a rejected
`Promise` with an [`ERR_INVALID_RETURN_VALUE`][] error. In both cases the error
handler is skipped.

Besides the async nature to await the completion behaves identically to
[`assert.throws()`][].

If specified, `error` can be a [`Class`][], [`RegExp`][], a validation function,
an object where each property will be tested for, or an instance of error where
each property will be tested for including the non-enumerable `message` and
`name` properties.

If specified, `message` will be the message provided by the [`AssertionError`][]
if the `asyncFn` fails to reject.

```mjs
import assert from 'node:assert/strict';

await assert.rejects(
  async () => {
    throw new TypeError('Wrong value');
  },
  {
    name: 'TypeError',
    message: 'Wrong value',
  },
);
```

```cjs
const assert = require('node:assert/strict');

(async () => {
  await assert.rejects(
    async () => {
      throw new TypeError('Wrong value');
    },
    {
      name: 'TypeError',
      message: 'Wrong value',
    },
  );
})();
```

```mjs
import assert from 'node:assert/strict';

await assert.rejects(
  async () => {
    throw new TypeError('Wrong value');
  },
  (err) => {
    assert.strictEqual(err.name, 'TypeError');
    assert.strictEqual(err.message, 'Wrong value');
    return true;
  },
);
```

```cjs
const assert = require('node:assert/strict');

(async () => {
  await assert.rejects(
    async () => {
      throw new TypeError('Wrong value');
    },
    (err) => {
      assert.strictEqual(err.name, 'TypeError');
      assert.strictEqual(err.message, 'Wrong value');
      return true;
    },
  );
})();
```

```mjs
import assert from 'node:assert/strict';

assert.rejects(
  Promise.reject(new Error('Wrong value')),
  Error,
).then(() => {
  // ...
});
```

```cjs
const assert = require('node:assert/strict');

assert.rejects(
  Promise.reject(new Error('Wrong value')),
  Error,
).then(() => {
  // ...
});
```

`error` cannot be a string. If a string is provided as the second
argument, then `error` is assumed to be omitted and the string will be used for
`message` instead. This can lead to easy-to-miss mistakes. Please read the
example in [`assert.throws()`][] carefully if using a string as the second
argument gets considered.

## `assert.strictEqual(actual, expected[, message])`

<!-- YAML
added: v0.1.21
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17003
    description: Used comparison changed from Strict Equality to `Object.is()`.
-->

* `actual` {any}
* `expected` {any}
* `message` {string|Error}

Tests strict equality between the `actual` and `expected` parameters as
determined by [`Object.is()`][].

```mjs
import assert from 'node:assert/strict';

assert.strictEqual(1, 2);
// AssertionError [ERR_ASSERTION]: Expected inputs to be strictly equal:
//
// 1 !== 2

assert.strictEqual(1, 1);
// OK

assert.strictEqual('Hello foobar', 'Hello World!');
// AssertionError [ERR_ASSERTION]: Expected inputs to be strictly equal:
// + actual - expected
//
// + 'Hello foobar'
// - 'Hello World!'
//          ^

const apples = 1;
const oranges = 2;
assert.strictEqual(apples, oranges, `apples ${apples} !== oranges ${oranges}`);
// AssertionError [ERR_ASSERTION]: apples 1 !== oranges 2

assert.strictEqual(1, '1', new TypeError('Inputs are not identical'));
// TypeError: Inputs are not identical
```

```cjs
const assert = require('node:assert/strict');

assert.strictEqual(1, 2);
// AssertionError [ERR_ASSERTION]: Expected inputs to be strictly equal:
//
// 1 !== 2

assert.strictEqual(1, 1);
// OK

assert.strictEqual('Hello foobar', 'Hello World!');
// AssertionError [ERR_ASSERTION]: Expected inputs to be strictly equal:
// + actual - expected
//
// + 'Hello foobar'
// - 'Hello World!'
//          ^

const apples = 1;
const oranges = 2;
assert.strictEqual(apples, oranges, `apples ${apples} !== oranges ${oranges}`);
// AssertionError [ERR_ASSERTION]: apples 1 !== oranges 2

assert.strictEqual(1, '1', new TypeError('Inputs are not identical'));
// TypeError: Inputs are not identical
```

If the values are not strictly equal, an [`AssertionError`][] is thrown with a
`message` property set equal to the value of the `message` parameter. If the
`message` parameter is undefined, a default error message is assigned. If the
`message` parameter is an instance of an [`Error`][] then it will be thrown
instead of the [`AssertionError`][].

## `assert.throws(fn[, error][, message])`

<!-- YAML
added: v0.1.21
changes:
  - version: v10.2.0
    pr-url: https://github.com/nodejs/node/pull/20485
    description: The `error` parameter can be an object containing regular
                 expressions now.
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17584
    description: The `error` parameter can now be an object as well.
  - version: v4.2.0
    pr-url: https://github.com/nodejs/node/pull/3276
    description: The `error` parameter can now be an arrow function.
-->

* `fn` {Function}
* `error` {RegExp|Function|Object|Error}
* `message` {string}

Expects the function `fn` to throw an error.

If specified, `error` can be a [`Class`][], [`RegExp`][], a validation function,
a validation object where each property will be tested for strict deep equality,
or an instance of error where each property will be tested for strict deep
equality including the non-enumerable `message` and `name` properties. When
using an object, it is also possible to use a regular expression, when
validating against a string property. See below for examples.

If specified, `message` will be appended to the message provided by the
`AssertionError` if the `fn` call fails to throw or in case the error validation
fails.

Custom validation object/error instance:

```mjs
import assert from 'node:assert/strict';

const err = new TypeError('Wrong value');
err.code = 404;
err.foo = 'bar';
err.info = {
  nested: true,
  baz: 'text',
};
err.reg = /abc/i;

assert.throws(
  () => {
    throw err;
  },
  {
    name: 'TypeError',
    message: 'Wrong value',
    info: {
      nested: true,
      baz: 'text',
    },
    // Only properties on the validation object will be tested for.
    // Using nested objects requires all properties to be present. Otherwise
    // the validation is going to fail.
  },
);

// Using regular expressions to validate error properties:
assert.throws(
  () => {
    throw err;
  },
  {
    // The `name` and `message` properties are strings and using regular
    // expressions on those will match against the string. If they fail, an
    // error is thrown.
    name: /^TypeError$/,
    message: /Wrong/,
    foo: 'bar',
    info: {
      nested: true,
      // It is not possible to use regular expressions for nested properties!
      baz: 'text',
    },
    // The `reg` property contains a regular expression and only if the
    // validation object contains an identical regular expression, it is going
    // to pass.
    reg: /abc/i,
  },
);

// Fails due to the different `message` and `name` properties:
assert.throws(
  () => {
    const otherErr = new Error('Not found');
    // Copy all enumerable properties from `err` to `otherErr`.
    for (const [key, value] of Object.entries(err)) {
      otherErr[key] = value;
    }
    throw otherErr;
  },
  // The error's `message` and `name` properties will also be checked when using
  // an error as validation object.
  err,
);
```

```cjs
const assert = require('node:assert/strict');

const err = new TypeError('Wrong value');
err.code = 404;
err.foo = 'bar';
err.info = {
  nested: true,
  baz: 'text',
};
err.reg = /abc/i;

assert.throws(
  () => {
    throw err;
  },
  {
    name: 'TypeError',
    message: 'Wrong value',
    info: {
      nested: true,
      baz: 'text',
    },
    // Only properties on the validation object will be tested for.
    // Using nested objects requires all properties to be present. Otherwise
    // the validation is going to fail.
  },
);

// Using regular expressions to validate error properties:
assert.throws(
  () => {
    throw err;
  },
  {
    // The `name` and `message` properties are strings and using regular
    // expressions on those will match against the string. If they fail, an
    // error is thrown.
    name: /^TypeError$/,
    message: /Wrong/,
    foo: 'bar',
    info: {
      nested: true,
      // It is not possible to use regular expressions for nested properties!
      baz: 'text',
    },
    // The `reg` property contains a regular expression and only if the
    // validation object contains an identical regular expression, it is going
    // to pass.
    reg: /abc/i,
  },
);

// Fails due to the different `message` and `name` properties:
assert.throws(
  () => {
    const otherErr = new Error('Not found');
    // Copy all enumerable properties from `err` to `otherErr`.
    for (const [key, value] of Object.entries(err)) {
      otherErr[key] = value;
    }
    throw otherErr;
  },
  // The error's `message` and `name` properties will also be checked when using
  // an error as validation object.
  err,
);
```

Validate instanceof using constructor:

```mjs
import assert from 'node:assert/strict';

assert.throws(
  () => {
    throw new Error('Wrong value');
  },
  Error,
);
```

```cjs
const assert = require('node:assert/strict');

assert.throws(
  () => {
    throw new Error('Wrong value');
  },
  Error,
);
```

Validate error message using [`RegExp`][]:

Using a regular expression runs `.toString` on the error object, and will
therefore also include the error name.

```mjs
import assert from 'node:assert/strict';

assert.throws(
  () => {
    throw new Error('Wrong value');
  },
  /^Error: Wrong value$/,
);
```

```cjs
const assert = require('node:assert/strict');

assert.throws(
  () => {
    throw new Error('Wrong value');
  },
  /^Error: Wrong value$/,
);
```

Custom error validation:

The function must return `true` to indicate all internal validations passed.
It will otherwise fail with an [`AssertionError`][].

```mjs
import assert from 'node:assert/strict';

assert.throws(
  () => {
    throw new Error('Wrong value');
  },
  (err) => {
    assert(err instanceof Error);
    assert(/value/.test(err));
    // Avoid returning anything from validation functions besides `true`.
    // Otherwise, it's not clear what part of the validation failed. Instead,
    // throw an error about the specific validation that failed (as done in this
    // example) and add as much helpful debugging information to that error as
    // possible.
    return true;
  },
  'unexpected error',
);
```

```cjs
const assert = require('node:assert/strict');

assert.throws(
  () => {
    throw new Error('Wrong value');
  },
  (err) => {
    assert(err instanceof Error);
    assert(/value/.test(err));
    // Avoid returning anything from validation functions besides `true`.
    // Otherwise, it's not clear what part of the validation failed. Instead,
    // throw an error about the specific validation that failed (as done in this
    // example) and add as much helpful debugging information to that error as
    // possible.
    return true;
  },
  'unexpected error',
);
```

`error` cannot be a string. If a string is provided as the second
argument, then `error` is assumed to be omitted and the string will be used for
`message` instead. This can lead to easy-to-miss mistakes. Using the same
message as the thrown error message is going to result in an
`ERR_AMBIGUOUS_ARGUMENT` error. Please read the example below carefully if using
a string as the second argument gets considered:

```mjs
import assert from 'node:assert/strict';

function throwingFirst() {
  throw new Error('First');
}

function throwingSecond() {
  throw new Error('Second');
}

function notThrowing() {}

// The second argument is a string and the input function threw an Error.
// The first case will not throw as it does not match for the error message
// thrown by the input function!
assert.throws(throwingFirst, 'Second');
// In the next example the message has no benefit over the message from the
// error and since it is not clear if the user intended to actually match
// against the error message, Node.js throws an `ERR_AMBIGUOUS_ARGUMENT` error.
assert.throws(throwingSecond, 'Second');
// TypeError [ERR_AMBIGUOUS_ARGUMENT]

// The string is only used (as message) in case the function does not throw:
assert.throws(notThrowing, 'Second');
// AssertionError [ERR_ASSERTION]: Missing expected exception: Second

// If it was intended to match for the error message do this instead:
// It does not throw because the error messages match.
assert.throws(throwingSecond, /Second$/);

// If the error message does not match, an AssertionError is thrown.
assert.throws(throwingFirst, /Second$/);
// AssertionError [ERR_ASSERTION]
```

```cjs
const assert = require('node:assert/strict');

function throwingFirst() {
  throw new Error('First');
}

function throwingSecond() {
  throw new Error('Second');
}

function notThrowing() {}

// The second argument is a string and the input function threw an Error.
// The first case will not throw as it does not match for the error message
// thrown by the input function!
assert.throws(throwingFirst, 'Second');
// In the next example the message has no benefit over the message from the
// error and since it is not clear if the user intended to actually match
// against the error message, Node.js throws an `ERR_AMBIGUOUS_ARGUMENT` error.
assert.throws(throwingSecond, 'Second');
// TypeError [ERR_AMBIGUOUS_ARGUMENT]

// The string is only used (as message) in case the function does not throw:
assert.throws(notThrowing, 'Second');
// AssertionError [ERR_ASSERTION]: Missing expected exception: Second

// If it was intended to match for the error message do this instead:
// It does not throw because the error messages match.
assert.throws(throwingSecond, /Second$/);

// If the error message does not match, an AssertionError is thrown.
assert.throws(throwingFirst, /Second$/);
// AssertionError [ERR_ASSERTION]
```

Due to the confusing error-prone notation, avoid a string as the second
argument.

## `assert.partialDeepStrictEqual(actual, expected[, message])`

<!-- YAML
added:
  - v23.4.0
  - v22.13.0
-->

> Stability: 1.0 - Early development

* `actual` {any}
* `expected` {any}
* `message` {string|Error}

[`assert.partialDeepStrictEqual()`][] Asserts the equivalence between the `actual` and `expected` parameters through a
deep comparison, ensuring that all properties in the `expected` parameter are
present in the `actual` parameter with equivalent values, not allowing type coercion.
The main difference with [`assert.deepStrictEqual()`][] is that [`assert.partialDeepStrictEqual()`][] does not require
all properties in the `actual` parameter to be present in the `expected` parameter.
This method should always pass the same test cases as [`assert.deepStrictEqual()`][], behaving as a super set of it.

```mjs
import assert from 'node:assert';

assert.partialDeepStrictEqual({ a: 1, b: 2 }, { a: 1, b: 2 });
// OK

assert.partialDeepStrictEqual({ a: { b: { c: 1 } } }, { a: { b: { c: 1 } } });
// OK

assert.partialDeepStrictEqual({ a: 1, b: 2, c: 3 }, { a: 1, b: 2 });
// OK

assert.partialDeepStrictEqual(new Set(['value1', 'value2']), new Set(['value1', 'value2']));
// OK

assert.partialDeepStrictEqual(new Map([['key1', 'value1']]), new Map([['key1', 'value1']]));
// OK

assert.partialDeepStrictEqual(new Uint8Array([1, 2, 3]), new Uint8Array([1, 2, 3]));
// OK

assert.partialDeepStrictEqual(/abc/, /abc/);
// OK

assert.partialDeepStrictEqual([{ a: 5 }, { b: 5 }], [{ a: 5 }]);
// OK

assert.partialDeepStrictEqual(new Set([{ a: 1 }, { b: 1 }]), new Set([{ a: 1 }]));
// OK

assert.partialDeepStrictEqual(new Date(0), new Date(0));
// OK

assert.partialDeepStrictEqual({ a: 1 }, { a: 1, b: 2 });
// AssertionError

assert.partialDeepStrictEqual({ a: 1, b: '2' }, { a: 1, b: 2 });
// AssertionError

assert.partialDeepStrictEqual({ a: { b: 2 } }, { a: { b: '2' } });
// AssertionError
```

```cjs
const assert = require('node:assert');

assert.partialDeepStrictEqual({ a: 1, b: 2 }, { a: 1, b: 2 });
// OK

assert.partialDeepStrictEqual({ a: { b: { c: 1 } } }, { a: { b: { c: 1 } } });
// OK

assert.partialDeepStrictEqual({ a: 1, b: 2, c: 3 }, { a: 1, b: 2 });
// OK

assert.partialDeepStrictEqual([{ a: 5 }, { b: 5 }], [{ a: 5 }]);
// OK

assert.partialDeepStrictEqual(new Set([{ a: 1 }, { b: 1 }]), new Set([{ a: 1 }]));
// OK

assert.partialDeepStrictEqual({ a: 1 }, { a: 1, b: 2 });
// AssertionError

assert.partialDeepStrictEqual({ a: 1, b: '2' }, { a: 1, b: 2 });
// AssertionError

assert.partialDeepStrictEqual({ a: { b: 2 } }, { a: { b: '2' } });
// AssertionError
```

[Object wrappers]: https://developer.mozilla.org/en-US/docs/Glossary/Primitive#Primitive_wrapper_objects_in_JavaScript
[Object.prototype.toString()]: https://tc39.github.io/ecma262/#sec-object.prototype.tostring
[`!=` operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Inequality
[`===` operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality
[`==` operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Equality
[`AssertionError`]: #class-assertassertionerror
[`CallTracker`]: #class-assertcalltracker
[`Class`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes
[`ERR_INVALID_RETURN_VALUE`]: errors.md#err_invalid_return_value
[`Error.captureStackTrace`]: errors.md#errorcapturestacktracetargetobject-constructoropt
[`Error`]: errors.md#class-error
[`Map`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map
[`Object.is()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is
[`RegExp`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions
[`Set`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set
[`Symbol`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol
[`TypeError`]: errors.md#class-typeerror
[`WeakMap`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap
[`WeakSet`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet
[`assert.deepEqual()`]: #assertdeepequalactual-expected-message
[`assert.deepStrictEqual()`]: #assertdeepstrictequalactual-expected-message
[`assert.doesNotThrow()`]: #assertdoesnotthrowfn-error-message
[`assert.equal()`]: #assertequalactual-expected-message
[`assert.notDeepEqual()`]: #assertnotdeepequalactual-expected-message
[`assert.notDeepStrictEqual()`]: #assertnotdeepstrictequalactual-expected-message
[`assert.notEqual()`]: #assertnotequalactual-expected-message
[`assert.notStrictEqual()`]: #assertnotstrictequalactual-expected-message
[`assert.ok()`]: #assertokvalue-message
[`assert.partialDeepStrictEqual()`]: #assertpartialdeepstrictequalactual-expected-message
[`assert.strictEqual()`]: #assertstrictequalactual-expected-message
[`assert.throws()`]: #assertthrowsfn-error-message
[`getColorDepth()`]: tty.md#writestreamgetcolordepthenv
[`mock`]: test.md#mocking
[`process.on('exit')`]: process.md#event-exit
[`tracker.calls()`]: #trackercallsfn-exact
[`tracker.verify()`]: #trackerverify
[enumerable "own" properties]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties
[prototype-spec]: https://tc39.github.io/ecma262/#sec-ordinary-object-internal-methods-and-internal-slots

# Test runner

<!--introduced_in=v18.0.0-->

<!-- YAML
added:
  - v18.0.0
  - v16.17.0
changes:
  - version: v20.0.0
    pr-url: https://github.com/nodejs/node/pull/46983
    description: The test runner is now stable.
-->

> Stability: 2 - Stable

<!-- source_link=lib/test.js -->

The `node:test` module facilitates the creation of JavaScript tests.
To access it:

```mjs
import test from 'node:test';
```

```cjs
const test = require('node:test');
```

This module is only available under the `node:` scheme.

Tests created via the `test` module consist of a single function that is
processed in one of three ways:

1. A synchronous function that is considered failing if it throws an exception,
   and is considered passing otherwise.
2. A function that returns a `Promise` that is considered failing if the
   `Promise` rejects, and is considered passing if the `Promise` fulfills.
3. A function that receives a callback function. If the callback receives any
   truthy value as its first argument, the test is considered failing. If a
   falsy value is passed as the first argument to the callback, the test is
   considered passing. If the test function receives a callback function and
   also returns a `Promise`, the test will fail.

The following example illustrates how tests are written using the
`test` module.

```js
test('synchronous passing test', (t) => {
  // This test passes because it does not throw an exception.
  assert.strictEqual(1, 1);
});

test('synchronous failing test', (t) => {
  // This test fails because it throws an exception.
  assert.strictEqual(1, 2);
});

test('asynchronous passing test', async (t) => {
  // This test passes because the Promise returned by the async
  // function is settled and not rejected.
  assert.strictEqual(1, 1);
});

test('asynchronous failing test', async (t) => {
  // This test fails because the Promise returned by the async
  // function is rejected.
  assert.strictEqual(1, 2);
});

test('failing test using Promises', (t) => {
  // Promises can be used directly as well.
  return new Promise((resolve, reject) => {
    setImmediate(() => {
      reject(new Error('this will cause the test to fail'));
    });
  });
});

test('callback passing test', (t, done) => {
  // done() is the callback function. When the setImmediate() runs, it invokes
  // done() with no arguments.
  setImmediate(done);
});

test('callback failing test', (t, done) => {
  // When the setImmediate() runs, done() is invoked with an Error object and
  // the test fails.
  setImmediate(() => {
    done(new Error('callback failure'));
  });
});
```

If any tests fail, the process exit code is set to `1`.

## Subtests

The test context's `test()` method allows subtests to be created.
It allows you to structure your tests in a hierarchical manner,
where you can create nested tests within a larger test.
This method behaves identically to the top level `test()` function.
The following example demonstrates the creation of a
top level test with two subtests.

```js
test('top level test', async (t) => {
  t.test('subtest 1', (t) => {
    assert.strictEqual(1, 1);
  });

  t.test('subtest 2', (t) => {
    assert.strictEqual(2, 2);
  });
});
```

> **Note:** `beforeEach` and `afterEach` hooks are triggered
> between each subtest execution.

Any subtest failures cause the parent test to fail.

## Skipping tests

Individual tests can be skipped by passing the `skip` option to the test, or by
calling the test context's `skip()` method as shown in the
following example.

```js
// The skip option is used, but no message is provided.
test('skip option', { skip: true }, (t) => {
  // This code is never executed.
});

// The skip option is used, and a message is provided.
test('skip option with message', { skip: 'this is skipped' }, (t) => {
  // This code is never executed.
});

test('skip() method', (t) => {
  // Make sure to return here as well if the test contains additional logic.
  t.skip();
});

test('skip() method with message', (t) => {
  // Make sure to return here as well if the test contains additional logic.
  t.skip('this is skipped');
});
```

## TODO tests

Individual tests can be marked as flaky or incomplete by passing the `todo`
option to the test, or by calling the test context's `todo()` method, as shown
in the following example. These tests represent a pending implementation or bug
that needs to be fixed. TODO tests are executed, but are not treated as test
failures, and therefore do not affect the process exit code. If a test is marked
as both TODO and skipped, the TODO option is ignored.

```js
// The todo option is used, but no message is provided.
test('todo option', { todo: true }, (t) => {
  // This code is executed, but not treated as a failure.
  throw new Error('this does not fail the test');
});

// The todo option is used, and a message is provided.
test('todo option with message', { todo: 'this is a todo test' }, (t) => {
  // This code is executed.
});

test('todo() method', (t) => {
  t.todo();
});

test('todo() method with message', (t) => {
  t.todo('this is a todo test and is not treated as a failure');
  throw new Error('this does not fail the test');
});
```

## `describe()` and `it()` aliases

Suites and tests can also be written using the `describe()` and `it()`
functions. [`describe()`][] is an alias for [`suite()`][], and [`it()`][] is an
alias for [`test()`][].

```js
describe('A thing', () => {
  it('should work', () => {
    assert.strictEqual(1, 1);
  });

  it('should be ok', () => {
    assert.strictEqual(2, 2);
  });

  describe('a nested thing', () => {
    it('should work', () => {
      assert.strictEqual(3, 3);
    });
  });
});
```

`describe()` and `it()` are imported from the `node:test` module.

```mjs
import { describe, it } from 'node:test';
```

```cjs
const { describe, it } = require('node:test');
```

## `only` tests

If Node.js is started with the [`--test-only`][] command-line option, or test
isolation is disabled, it is possible to skip all tests except for a selected
subset by passing the `only` option to the tests that should run. When a test
with the `only` option is set, all subtests are also run.
If a suite has the `only` option set, all tests within the suite are run,
unless it has descendants with the `only` option set, in which case only those
tests are run.

When using [subtests][] within a `test()`/`it()`, it is required to mark
all ancestor tests with the `only` option to run only a
selected subset of tests.

The test context's `runOnly()`
method can be used to implement the same behavior at the subtest level. Tests
that are not executed are omitted from the test runner output.

```js
// Assume Node.js is run with the --test-only command-line option.
// The suite's 'only' option is set, so these tests are run.
test('this test is run', { only: true }, async (t) => {
  // Within this test, all subtests are run by default.
  t.test('running subtest');

  // The test context can be updated to run subtests with the 'only' option.
  t.runOnly(true);
  t.test('this subtest is now skipped');
  t.test('this subtest is run', { only: true });

  // Switch the context back to execute all tests.
  t.runOnly(false);
  t.test('this subtest is now run');

  // Explicitly do not run these tests.
  t.test('skipped subtest 3', { only: false });
  t.test('skipped subtest 4', { skip: true });
});

// The 'only' option is not set, so this test is skipped.
test('this test is not run', () => {
  // This code is not run.
  throw new Error('fail');
});

describe('a suite', () => {
  // The 'only' option is set, so this test is run.
  it('this test is run', { only: true }, () => {
    // This code is run.
  });

  it('this test is not run', () => {
    // This code is not run.
    throw new Error('fail');
  });
});

describe.only('a suite', () => {
  // The 'only' option is set, so this test is run.
  it('this test is run', () => {
    // This code is run.
  });

  it('this test is run', () => {
    // This code is run.
  });
});
```

## Filtering tests by name

The [`--test-name-pattern`][] command-line option can be used to only run
tests whose name matches the provided pattern, and the
[`--test-skip-pattern`][] option can be used to skip tests whose name
matches the provided pattern. Test name patterns are interpreted as
JavaScript regular expressions. The `--test-name-pattern` and
`--test-skip-pattern` options can be specified multiple times in order to run
nested tests. For each test that is executed, any corresponding test hooks,
such as `beforeEach()`, are also run. Tests that are not executed are omitted
from the test runner output.

Given the following test file, starting Node.js with the
`--test-name-pattern="test [1-3]"` option would cause the test runner to execute
`test 1`, `test 2`, and `test 3`. If `test 1` did not match the test name
pattern, then its subtests would not execute, despite matching the pattern. The
same set of tests could also be executed by passing `--test-name-pattern`
multiple times (e.g. `--test-name-pattern="test 1"`,
`--test-name-pattern="test 2"`, etc.).

```js
test('test 1', async (t) => {
  t.test('test 2');
  t.test('test 3');
});

test('Test 4', async (t) => {
  t.test('Test 5');
  t.test('test 6');
});
```

Test name patterns can also be specified using regular expression literals. This
allows regular expression flags to be used. In the previous example, starting
Node.js with `--test-name-pattern="/test [4-5]/i"` (or `--test-skip-pattern="/test [4-5]/i"`)
would match `Test 4` and `Test 5` because the pattern is case-insensitive.

To match a single test with a pattern, you can prefix it with all its ancestor
test names separated by space, to ensure it is unique.
For example, given the following test file:

```js
describe('test 1', (t) => {
  it('some test');
});

describe('test 2', (t) => {
  it('some test');
});
```

Starting Node.js with `--test-name-pattern="test 1 some test"` would match
only `some test` in `test 1`.

Test name patterns do not change the set of files that the test runner executes.

If both `--test-name-pattern` and `--test-skip-pattern` are supplied,
tests must satisfy **both** requirements in order to be executed.

## Extraneous asynchronous activity

Once a test function finishes executing, the results are reported as quickly
as possible while maintaining the order of the tests. However, it is possible
for the test function to generate asynchronous activity that outlives the test
itself. The test runner handles this type of activity, but does not delay the
reporting of test results in order to accommodate it.

In the following example, a test completes with two `setImmediate()`
operations still outstanding. The first `setImmediate()` attempts to create a
new subtest. Because the parent test has already finished and output its
results, the new subtest is immediately marked as failed, and reported later
to the {TestsStream}.

The second `setImmediate()` creates an `uncaughtException` event.
`uncaughtException` and `unhandledRejection` events originating from a completed
test are marked as failed by the `test` module and reported as diagnostic
warnings at the top level by the {TestsStream}.

```js
test('a test that creates asynchronous activity', (t) => {
  setImmediate(() => {
    t.test('subtest that is created too late', (t) => {
      throw new Error('error1');
    });
  });

  setImmediate(() => {
    throw new Error('error2');
  });

  // The test finishes after this line.
});
```

## Watch mode

<!-- YAML
added:
  - v19.2.0
  - v18.13.0
-->

> Stability: 1 - Experimental

The Node.js test runner supports running in watch mode by passing the `--watch` flag:

```bash
node --test --watch
```

In watch mode, the test runner will watch for changes to test files and
their dependencies. When a change is detected, the test runner will
rerun the tests affected by the change.
The test runner will continue to run until the process is terminated.

## Running tests from the command line

The Node.js test runner can be invoked from the command line by passing the
[`--test`][] flag:

```bash
node --test
```

By default, Node.js will run all files matching these patterns:

* `**/*.test.{cjs,mjs,js}`
* `**/*-test.{cjs,mjs,js}`
* `**/*_test.{cjs,mjs,js}`
* `**/test-*.{cjs,mjs,js}`
* `**/test.{cjs,mjs,js}`
* `**/test/**/*.{cjs,mjs,js}`

Unless [`--no-experimental-strip-types`][] is supplied, the following
additional patterns are also matched:

* `**/*.test.{cts,mts,ts}`
* `**/*-test.{cts,mts,ts}`
* `**/*_test.{cts,mts,ts}`
* `**/test-*.{cts,mts,ts}`
* `**/test.{cts,mts,ts}`
* `**/test/**/*.{cts,mts,ts}`

Alternatively, one or more glob patterns can be provided as the
final argument(s) to the Node.js command, as shown below.
Glob patterns follow the behavior of [`glob(7)`][].
The glob patterns should be enclosed in double quotes on the command line to
prevent shell expansion, which can reduce portability across systems.

```bash
node --test "**/*.test.js" "**/*.spec.js"
```

Matching files are executed as test files.
More information on the test file execution can be found
in the [test runner execution model][] section.

### Test runner execution model

When process-level test isolation is enabled, each matching test file is
executed in a separate child process. The maximum number of child processes
running at any time is controlled by the [`--test-concurrency`][] flag. If the
child process finishes with an exit code of 0, the test is considered passing.
Otherwise, the test is considered to be a failure. Test files must be executable
by Node.js, but are not required to use the `node:test` module internally.

Each test file is executed as if it was a regular script. That is, if the test
file itself uses `node:test` to define tests, all of those tests will be
executed within a single application thread, regardless of the value of the
`concurrency` option of [`test()`][].

When process-level test isolation is disabled, each matching test file is
imported into the test runner process. Once all test files have been loaded, the
top level tests are executed with a concurrency of one. Because the test files
are all run within the same context, it is possible for tests to interact with
each other in ways that are not possible when isolation is enabled. For example,
if a test relies on global state, it is possible for that state to be modified
by a test originating from another file.

## Collecting code coverage

> Stability: 1 - Experimental

When Node.js is started with the [`--experimental-test-coverage`][]
command-line flag, code coverage is collected and statistics are reported once
all tests have completed. If the [`NODE_V8_COVERAGE`][] environment variable is
used to specify a code coverage directory, the generated V8 coverage files are
written to that directory. Node.js core modules and files within
`node_modules/` directories are, by default, not included in the coverage report.
However, they can be explicitly included via the [`--test-coverage-include`][] flag.
By default all the matching test files are excluded from the coverage report.
Exclusions can be overridden by using the [`--test-coverage-exclude`][] flag.
If coverage is enabled, the coverage report is sent to any [test reporters][] via
the `'test:coverage'` event.

Coverage can be disabled on a series of lines using the following
comment syntax:

```js
/* node:coverage disable */
if (anAlwaysFalseCondition) {
  // Code in this branch will never be executed, but the lines are ignored for
  // coverage purposes. All lines following the 'disable' comment are ignored
  // until a corresponding 'enable' comment is encountered.
  console.log('this is never executed');
}
/* node:coverage enable */
```

Coverage can also be disabled for a specified number of lines. After the
specified number of lines, coverage will be automatically reenabled. If the
number of lines is not explicitly provided, a single line is ignored.

```js
/* node:coverage ignore next */
if (anAlwaysFalseCondition) { console.log('this is never executed'); }

/* node:coverage ignore next 3 */
if (anAlwaysFalseCondition) {
  console.log('this is never executed');
}
```

### Coverage reporters

The tap and spec reporters will print a summary of the coverage statistics.
There is also an lcov reporter that will generate an lcov file which can be
used as an in depth coverage report.

```bash
node --test --experimental-test-coverage --test-reporter=lcov --test-reporter-destination=lcov.info
```

* No test results are reported by this reporter.
* This reporter should ideally be used alongside another reporter.

## Mocking

The `node:test` module supports mocking during testing via a top-level `mock`
object. The following example creates a spy on a function that adds two numbers
together. The spy is then used to assert that the function was called as
expected.

```mjs
import assert from 'node:assert';
import { mock, test } from 'node:test';

test('spies on a function', () => {
  const sum = mock.fn((a, b) => {
    return a + b;
  });

  assert.strictEqual(sum.mock.callCount(), 0);
  assert.strictEqual(sum(3, 4), 7);
  assert.strictEqual(sum.mock.callCount(), 1);

  const call = sum.mock.calls[0];
  assert.deepStrictEqual(call.arguments, [3, 4]);
  assert.strictEqual(call.result, 7);
  assert.strictEqual(call.error, undefined);

  // Reset the globally tracked mocks.
  mock.reset();
});
```

```cjs
'use strict';
const assert = require('node:assert');
const { mock, test } = require('node:test');

test('spies on a function', () => {
  const sum = mock.fn((a, b) => {
    return a + b;
  });

  assert.strictEqual(sum.mock.callCount(), 0);
  assert.strictEqual(sum(3, 4), 7);
  assert.strictEqual(sum.mock.callCount(), 1);

  const call = sum.mock.calls[0];
  assert.deepStrictEqual(call.arguments, [3, 4]);
  assert.strictEqual(call.result, 7);
  assert.strictEqual(call.error, undefined);

  // Reset the globally tracked mocks.
  mock.reset();
});
```

The same mocking functionality is also exposed on the [`TestContext`][] object
of each test. The following example creates a spy on an object method using the
API exposed on the `TestContext`. The benefit of mocking via the test context is
that the test runner will automatically restore all mocked functionality once
the test finishes.

```js
test('spies on an object method', (t) => {
  const number = {
    value: 5,
    add(a) {
      return this.value + a;
    },
  };

  t.mock.method(number, 'add');
  assert.strictEqual(number.add.mock.callCount(), 0);
  assert.strictEqual(number.add(3), 8);
  assert.strictEqual(number.add.mock.callCount(), 1);

  const call = number.add.mock.calls[0];

  assert.deepStrictEqual(call.arguments, [3]);
  assert.strictEqual(call.result, 8);
  assert.strictEqual(call.target, undefined);
  assert.strictEqual(call.this, number);
});
```

### Timers

Mocking timers is a technique commonly used in software testing to simulate and
control the behavior of timers, such as `setInterval` and `setTimeout`,
without actually waiting for the specified time intervals.

Refer to the [`MockTimers`][] class for a full list of methods and features.

This allows developers to write more reliable and
predictable tests for time-dependent functionality.

The example below shows how to mock `setTimeout`.
Using `.enable({ apis: ['setTimeout'] });`
it will mock the `setTimeout` functions in the [node:timers](./timers.md) and
[node:timers/promises](./timers.md#timers-promises-api) modules,
as well as from the Node.js global context.

**Note:** Destructuring functions such as
`import { setTimeout } from 'node:timers'`
is currently not supported by this API.

```mjs
import assert from 'node:assert';
import { mock, test } from 'node:test';

test('mocks setTimeout to be executed synchronously without having to actually wait for it', () => {
  const fn = mock.fn();

  // Optionally choose what to mock
  mock.timers.enable({ apis: ['setTimeout'] });
  setTimeout(fn, 9999);
  assert.strictEqual(fn.mock.callCount(), 0);

  // Advance in time
  mock.timers.tick(9999);
  assert.strictEqual(fn.mock.callCount(), 1);

  // Reset the globally tracked mocks.
  mock.timers.reset();

  // If you call reset mock instance, it will also reset timers instance
  mock.reset();
});
```

```cjs
const assert = require('node:assert');
const { mock, test } = require('node:test');

test('mocks setTimeout to be executed synchronously without having to actually wait for it', () => {
  const fn = mock.fn();

  // Optionally choose what to mock
  mock.timers.enable({ apis: ['setTimeout'] });
  setTimeout(fn, 9999);
  assert.strictEqual(fn.mock.callCount(), 0);

  // Advance in time
  mock.timers.tick(9999);
  assert.strictEqual(fn.mock.callCount(), 1);

  // Reset the globally tracked mocks.
  mock.timers.reset();

  // If you call reset mock instance, it will also reset timers instance
  mock.reset();
});
```

The same mocking functionality is also exposed in the mock property on the [`TestContext`][] object
of each test. The benefit of mocking via the test context is
that the test runner will automatically restore all mocked timers
functionality once the test finishes.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
  const fn = context.mock.fn();

  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['setTimeout'] });
  setTimeout(fn, 9999);
  assert.strictEqual(fn.mock.callCount(), 0);

  // Advance in time
  context.mock.timers.tick(9999);
  assert.strictEqual(fn.mock.callCount(), 1);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
  const fn = context.mock.fn();

  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['setTimeout'] });
  setTimeout(fn, 9999);
  assert.strictEqual(fn.mock.callCount(), 0);

  // Advance in time
  context.mock.timers.tick(9999);
  assert.strictEqual(fn.mock.callCount(), 1);
});
```

### Dates

The mock timers API also allows the mocking of the `Date` object. This is a
useful feature for testing time-dependent functionality, or to simulate
internal calendar functions such as `Date.now()`.

The dates implementation is also part of the [`MockTimers`][] class. Refer to it
for a full list of methods and features.

**Note:** Dates and timers are dependent when mocked together. This means that
if you have both the `Date` and `setTimeout` mocked, advancing the time will
also advance the mocked date as they simulate a single internal clock.

The example below show how to mock the `Date` object and obtain the current
`Date.now()` value.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('mocks the Date object', (context) => {
  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['Date'] });
  // If not specified, the initial date will be based on 0 in the UNIX epoch
  assert.strictEqual(Date.now(), 0);

  // Advance in time will also advance the date
  context.mock.timers.tick(9999);
  assert.strictEqual(Date.now(), 9999);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('mocks the Date object', (context) => {
  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['Date'] });
  // If not specified, the initial date will be based on 0 in the UNIX epoch
  assert.strictEqual(Date.now(), 0);

  // Advance in time will also advance the date
  context.mock.timers.tick(9999);
  assert.strictEqual(Date.now(), 9999);
});
```

If there is no initial epoch set, the initial date will be based on 0 in the
Unix epoch. This is January 1st, 1970, 00:00:00 UTC. You can set an initial date
by passing a `now` property to the `.enable()` method. This value will be used
as the initial date for the mocked `Date` object. It can either be a positive
integer, or another Date object.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('mocks the Date object with initial time', (context) => {
  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['Date'], now: 100 });
  assert.strictEqual(Date.now(), 100);

  // Advance in time will also advance the date
  context.mock.timers.tick(200);
  assert.strictEqual(Date.now(), 300);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('mocks the Date object with initial time', (context) => {
  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['Date'], now: 100 });
  assert.strictEqual(Date.now(), 100);

  // Advance in time will also advance the date
  context.mock.timers.tick(200);
  assert.strictEqual(Date.now(), 300);
});
```

You can use the `.setTime()` method to manually move the mocked date to another
time. This method only accepts a positive integer.

**Note:** This method will execute any mocked timers that are in the past
from the new time.

In the below example we are setting a new time for the mocked date.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('sets the time of a date object', (context) => {
  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['Date'], now: 100 });
  assert.strictEqual(Date.now(), 100);

  // Advance in time will also advance the date
  context.mock.timers.setTime(1000);
  context.mock.timers.tick(200);
  assert.strictEqual(Date.now(), 1200);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('sets the time of a date object', (context) => {
  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['Date'], now: 100 });
  assert.strictEqual(Date.now(), 100);

  // Advance in time will also advance the date
  context.mock.timers.setTime(1000);
  context.mock.timers.tick(200);
  assert.strictEqual(Date.now(), 1200);
});
```

If you have any timer that's set to run in the past, it will be executed as if
the `.tick()` method has been called. This is useful if you want to test
time-dependent functionality that's already in the past.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('runs timers as setTime passes ticks', (context) => {
  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
  const fn = context.mock.fn();
  setTimeout(fn, 1000);

  context.mock.timers.setTime(800);
  // Timer is not executed as the time is not yet reached
  assert.strictEqual(fn.mock.callCount(), 0);
  assert.strictEqual(Date.now(), 800);

  context.mock.timers.setTime(1200);
  // Timer is executed as the time is now reached
  assert.strictEqual(fn.mock.callCount(), 1);
  assert.strictEqual(Date.now(), 1200);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('runs timers as setTime passes ticks', (context) => {
  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
  const fn = context.mock.fn();
  setTimeout(fn, 1000);

  context.mock.timers.setTime(800);
  // Timer is not executed as the time is not yet reached
  assert.strictEqual(fn.mock.callCount(), 0);
  assert.strictEqual(Date.now(), 800);

  context.mock.timers.setTime(1200);
  // Timer is executed as the time is now reached
  assert.strictEqual(fn.mock.callCount(), 1);
  assert.strictEqual(Date.now(), 1200);
});
```

Using `.runAll()` will execute all timers that are currently in the queue. This
will also advance the mocked date to the time of the last timer that was
executed as if the time has passed.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('runs timers as setTime passes ticks', (context) => {
  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
  const fn = context.mock.fn();
  setTimeout(fn, 1000);
  setTimeout(fn, 2000);
  setTimeout(fn, 3000);

  context.mock.timers.runAll();
  // All timers are executed as the time is now reached
  assert.strictEqual(fn.mock.callCount(), 3);
  assert.strictEqual(Date.now(), 3000);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('runs timers as setTime passes ticks', (context) => {
  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
  const fn = context.mock.fn();
  setTimeout(fn, 1000);
  setTimeout(fn, 2000);
  setTimeout(fn, 3000);

  context.mock.timers.runAll();
  // All timers are executed as the time is now reached
  assert.strictEqual(fn.mock.callCount(), 3);
  assert.strictEqual(Date.now(), 3000);
});
```

## Snapshot testing

<!-- YAML
added: v22.3.0
changes:
  - version: v23.4.0
    pr-url: https://github.com/nodejs/node/pull/55897
    description: Snapsnot testing is no longer experimental.
-->

Snapshot tests allow arbitrary values to be serialized into string values and
compared against a set of known good values. The known good values are known as
snapshots, and are stored in a snapshot file. Snapshot files are managed by the
test runner, but are designed to be human readable to aid in debugging. Best
practice is for snapshot files to be checked into source control along with your
test files.

Snapshot files are generated by starting Node.js with the
[`--test-update-snapshots`][] command-line flag. A separate snapshot file is
generated for each test file. By default, the snapshot file has the same name
as the test file with a `.snapshot` file extension. This behavior can be
configured using the `snapshot.setResolveSnapshotPath()` function. Each
snapshot assertion corresponds to an export in the snapshot file.

An example snapshot test is shown below. The first time this test is executed,
it will fail because the corresponding snapshot file does not exist.

```js
// test.js
suite('suite of snapshot tests', () => {
  test('snapshot test', (t) => {
    t.assert.snapshot({ value1: 1, value2: 2 });
    t.assert.snapshot(5);
  });
});
```

Generate the snapshot file by running the test file with
`--test-update-snapshots`. The test should pass, and a file named
`test.js.snapshot` is created in the same directory as the test file. The
contents of the snapshot file are shown below. Each snapshot is identified by
the full name of test and a counter to differentiate between snapshots in the
same test.

```js
exports[`suite of snapshot tests > snapshot test 1`] = `
{
  "value1": 1,
  "value2": 2
}
`;

exports[`suite of snapshot tests > snapshot test 2`] = `
5
`;
```

Once the snapshot file is created, run the tests again without the
`--test-update-snapshots` flag. The tests should pass now.

## Test reporters

<!-- YAML
added:
  - v19.6.0
  - v18.15.0
changes:
  - version:
    - v19.9.0
    - v18.17.0
    pr-url: https://github.com/nodejs/node/pull/47238
    description: Reporters are now exposed at `node:test/reporters`.
-->

The `node:test` module supports passing [`--test-reporter`][]
flags for the test runner to use a specific reporter.

The following built-reporters are supported:

* `spec`
  The `spec` reporter outputs the test results in a human-readable format. This
  is the default reporter.

* `tap`
  The `tap` reporter outputs the test results in the [TAP][] format.

* `dot`
  The `dot` reporter outputs the test results in a compact format,
  where each passing test is represented by a `.`,
  and each failing test is represented by a `X`.

* `junit`
  The junit reporter outputs test results in a jUnit XML format

* `lcov`
  The `lcov` reporter outputs test coverage when used with the
  [`--experimental-test-coverage`][] flag.

The exact output of these reporters is subject to change between versions of
Node.js, and should not be relied on programmatically. If programmatic access
to the test runner's output is required, use the events emitted by the
{TestsStream}.

The reporters are available via the `node:test/reporters` module:

```mjs
import { tap, spec, dot, junit, lcov } from 'node:test/reporters';
```

```cjs
const { tap, spec, dot, junit, lcov } = require('node:test/reporters');
```

### Custom reporters

[`--test-reporter`][] can be used to specify a path to custom reporter.
A custom reporter is a module that exports a value
accepted by [stream.compose][].
Reporters should transform events emitted by a {TestsStream}

Example of a custom reporter using {stream.Transform}:

```mjs
import { Transform } from 'node:stream';

const customReporter = new Transform({
  writableObjectMode: true,
  transform(event, encoding, callback) {
    switch (event.type) {
      case 'test:dequeue':
        callback(null, `test ${event.data.name} dequeued`);
        break;
      case 'test:enqueue':
        callback(null, `test ${event.data.name} enqueued`);
        break;
      case 'test:watch:drained':
        callback(null, 'test watch queue drained');
        break;
      case 'test:start':
        callback(null, `test ${event.data.name} started`);
        break;
      case 'test:pass':
        callback(null, `test ${event.data.name} passed`);
        break;
      case 'test:fail':
        callback(null, `test ${event.data.name} failed`);
        break;
      case 'test:plan':
        callback(null, 'test plan');
        break;
      case 'test:diagnostic':
      case 'test:stderr':
      case 'test:stdout':
        callback(null, event.data.message);
        break;
      case 'test:coverage': {
        const { totalLineCount } = event.data.summary.totals;
        callback(null, `total line count: ${totalLineCount}\n`);
        break;
      }
    }
  },
});

export default customReporter;
```

```cjs
const { Transform } = require('node:stream');

const customReporter = new Transform({
  writableObjectMode: true,
  transform(event, encoding, callback) {
    switch (event.type) {
      case 'test:dequeue':
        callback(null, `test ${event.data.name} dequeued`);
        break;
      case 'test:enqueue':
        callback(null, `test ${event.data.name} enqueued`);
        break;
      case 'test:watch:drained':
        callback(null, 'test watch queue drained');
        break;
      case 'test:start':
        callback(null, `test ${event.data.name} started`);
        break;
      case 'test:pass':
        callback(null, `test ${event.data.name} passed`);
        break;
      case 'test:fail':
        callback(null, `test ${event.data.name} failed`);
        break;
      case 'test:plan':
        callback(null, 'test plan');
        break;
      case 'test:diagnostic':
      case 'test:stderr':
      case 'test:stdout':
        callback(null, event.data.message);
        break;
      case 'test:coverage': {
        const { totalLineCount } = event.data.summary.totals;
        callback(null, `total line count: ${totalLineCount}\n`);
        break;
      }
    }
  },
});

module.exports = customReporter;
```

Example of a custom reporter using a generator function:

```mjs
export default async function * customReporter(source) {
  for await (const event of source) {
    switch (event.type) {
      case 'test:dequeue':
        yield `test ${event.data.name} dequeued\n`;
        break;
      case 'test:enqueue':
        yield `test ${event.data.name} enqueued\n`;
        break;
      case 'test:watch:drained':
        yield 'test watch queue drained\n';
        break;
      case 'test:start':
        yield `test ${event.data.name} started\n`;
        break;
      case 'test:pass':
        yield `test ${event.data.name} passed\n`;
        break;
      case 'test:fail':
        yield `test ${event.data.name} failed\n`;
        break;
      case 'test:plan':
        yield 'test plan\n';
        break;
      case 'test:diagnostic':
      case 'test:stderr':
      case 'test:stdout':
        yield `${event.data.message}\n`;
        break;
      case 'test:coverage': {
        const { totalLineCount } = event.data.summary.totals;
        yield `total line count: ${totalLineCount}\n`;
        break;
      }
    }
  }
}
```

```cjs
module.exports = async function * customReporter(source) {
  for await (const event of source) {
    switch (event.type) {
      case 'test:dequeue':
        yield `test ${event.data.name} dequeued\n`;
        break;
      case 'test:enqueue':
        yield `test ${event.data.name} enqueued\n`;
        break;
      case 'test:watch:drained':
        yield 'test watch queue drained\n';
        break;
      case 'test:start':
        yield `test ${event.data.name} started\n`;
        break;
      case 'test:pass':
        yield `test ${event.data.name} passed\n`;
        break;
      case 'test:fail':
        yield `test ${event.data.name} failed\n`;
        break;
      case 'test:plan':
        yield 'test plan\n';
        break;
      case 'test:diagnostic':
      case 'test:stderr':
      case 'test:stdout':
        yield `${event.data.message}\n`;
        break;
      case 'test:coverage': {
        const { totalLineCount } = event.data.summary.totals;
        yield `total line count: ${totalLineCount}\n`;
        break;
      }
    }
  }
};
```

The value provided to `--test-reporter` should be a string like one used in an
`import()` in JavaScript code, or a value provided for [`--import`][].

### Multiple reporters

The [`--test-reporter`][] flag can be specified multiple times to report test
results in several formats. In this situation
it is required to specify a destination for each reporter
using [`--test-reporter-destination`][].
Destination can be `stdout`, `stderr`, or a file path.
Reporters and destinations are paired according
to the order they were specified.

In the following example, the `spec` reporter will output to `stdout`,
and the `dot` reporter will output to `file.txt`:

```bash
node --test-reporter=spec --test-reporter=dot --test-reporter-destination=stdout --test-reporter-destination=file.txt
```

When a single reporter is specified, the destination will default to `stdout`,
unless a destination is explicitly provided.

## `run([options])`

<!-- YAML
added:
  - v18.9.0
  - v16.19.0
changes:
  - version: v23.0.0
    pr-url: https://github.com/nodejs/node/pull/54705
    description: Added the `cwd` option.
  - version:
    - v23.0.0
    - v22.10.0
    pr-url: https://github.com/nodejs/node/pull/53937
    description: Added coverage options.
  - version: v22.8.0
    pr-url: https://github.com/nodejs/node/pull/53927
    description: Added the `isolation` option.
  - version: v22.6.0
    pr-url: https://github.com/nodejs/node/pull/53866
    description: Added the `globPatterns` option.
  - version:
    - v22.0.0
    - v20.14.0
    pr-url: https://github.com/nodejs/node/pull/52038
    description: Added the `forceExit` option.
  - version:
    - v20.1.0
    - v18.17.0
    pr-url: https://github.com/nodejs/node/pull/47628
    description: Add a testNamePatterns option.
-->

* `options` {Object} Configuration options for running tests. The following
  properties are supported:
  * `concurrency` {number|boolean} If a number is provided,
    then that many test processes would run in parallel, where each process
    corresponds to one test file.
    If `true`, it would run `os.availableParallelism() - 1` test files in
    parallel.
    If `false`, it would only run one test file at a time.
    **Default:** `false`.
  * `cwd`: {string} Specifies the current working directory to be used by the test runner.
    Serves as the base path for resolving files according to the [test runner execution model][].
    **Default:** `process.cwd()`.
  * `files`: {Array} An array containing the list of files to run.
    **Default:** matching files from [test runner execution model][].
  * `forceExit`: {boolean} Configures the test runner to exit the process once
    all known tests have finished executing even if the event loop would
    otherwise remain active. **Default:** `false`.
  * `globPatterns`: {Array} An array containing the list of glob patterns to
    match test files. This option cannot be used together with `files`.
    **Default:** matching files from [test runner execution model][].
  * `inspectPort` {number|Function} Sets inspector port of test child process.
    This can be a number, or a function that takes no arguments and returns a
    number. If a nullish value is provided, each process gets its own port,
    incremented from the primary's `process.debugPort`. This option is ignored
    if the `isolation` option is set to `'none'` as no child processes are
    spawned. **Default:** `undefined`.
  * `isolation` {string} Configures the type of test isolation. If set to
    `'process'`, each test file is run in a separate child process. If set to
    `'none'`, all test files run in the current process. **Default:**
    `'process'`.
  * `only`: {boolean} If truthy, the test context will only run tests that
    have the `only` option set
  * `setup` {Function} A function that accepts the `TestsStream` instance
    and can be used to setup listeners before any tests are run.
    **Default:** `undefined`.
  * `execArgv` {Array} An array of CLI flags to pass to the `node` executable when
    spawning the subprocesses. This option has no effect when `isolation` is `'none`'.
    **Default:** `[]`
  * `argv` {Array} An array of CLI flags to pass to each test file when spawning the
    subprocesses. This option has no effect when `isolation` is `'none'`.
    **Default:** `[]`.
  * `signal` {AbortSignal} Allows aborting an in-progress test execution.
  * `testNamePatterns` {string|RegExp|Array} A String, RegExp or a RegExp Array,
    that can be used to only run tests whose name matches the provided pattern.
    Test name patterns are interpreted as JavaScript regular expressions.
    For each test that is executed, any corresponding test hooks, such as
    `beforeEach()`, are also run.
    **Default:** `undefined`.
  * `testSkipPatterns` {string|RegExp|Array} A String, RegExp or a RegExp Array,
    that can be used to exclude running tests whose name matches the provided pattern.
    Test name patterns are interpreted as JavaScript regular expressions.
    For each test that is executed, any corresponding test hooks, such as
    `beforeEach()`, are also run.
    **Default:** `undefined`.
  * `timeout` {number} A number of milliseconds the test execution will
    fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.
  * `watch` {boolean} Whether to run in watch mode or not. **Default:** `false`.
  * `shard` {Object} Running tests in a specific shard. **Default:** `undefined`.
    * `index` {number} is a positive integer between 1 and `<total>`
      that specifies the index of the shard to run. This option is _required_.
    * `total` {number} is a positive integer that specifies the total number
      of shards to split the test files to. This option is _required_.
  * `coverage` {boolean} enable [code coverage][] collection.
    **Default:** `false`.
  * `coverageExcludeGlobs` {string|Array} Excludes specific files from code coverage
    using a glob pattern, which can match both absolute and relative file paths.
    This property is only applicable when `coverage` was set to `true`.
    If both `coverageExcludeGlobs` and `coverageIncludeGlobs` are provided,
    files must meet **both** criteria to be included in the coverage report.
    **Default:** `undefined`.
  * `coverageIncludeGlobs` {string|Array} Includes specific files in code coverage
    using a glob pattern, which can match both absolute and relative file paths.
    This property is only applicable when `coverage` was set to `true`.
    If both `coverageExcludeGlobs` and `coverageIncludeGlobs` are provided,
    files must meet **both** criteria to be included in the coverage report.
    **Default:** `undefined`.
  * `lineCoverage` {number} Require a minimum percent of covered lines. If code
    coverage does not reach the threshold specified, the process will exit with code `1`.
    **Default:** `0`.
  * `branchCoverage` {number} Require a minimum percent of covered branches. If code
    coverage does not reach the threshold specified, the process will exit with code `1`.
    **Default:** `0`.
  * `functionCoverage` {number} Require a minimum percent of covered functions. If code
    coverage does not reach the threshold specified, the process will exit with code `1`.
    **Default:** `0`.
* Returns: {TestsStream}

**Note:** `shard` is used to horizontally parallelize test running across
machines or processes, ideal for large-scale executions across varied
environments. It's incompatible with `watch` mode, tailored for rapid
code iteration by automatically rerunning tests on file changes.

```mjs
import { tap } from 'node:test/reporters';
import { run } from 'node:test';
import process from 'node:process';
import path from 'node:path';

run({ files: [path.resolve('./tests/test.js')] })
 .on('test:fail', () => {
   process.exitCode = 1;
 })
 .compose(tap)
 .pipe(process.stdout);
```

```cjs
const { tap } = require('node:test/reporters');
const { run } = require('node:test');
const path = require('node:path');

run({ files: [path.resolve('./tests/test.js')] })
 .on('test:fail', () => {
   process.exitCode = 1;
 })
 .compose(tap)
 .pipe(process.stdout);
```

## `suite([name][, options][, fn])`

<!-- YAML
added:
  - v22.0.0
  - v20.13.0
changes:
  - version:
    - REPLACEME
    pr-url: https://github.com/nodejs/node/pull/56664
    description: This function no longer returns a `Promise`.
-->

* `name` {string} The name of the suite, which is displayed when reporting test
  results. **Default:** The `name` property of `fn`, or `'<anonymous>'` if `fn`
  does not have a name.
* `options` {Object} Optional configuration options for the suite.
  This supports the same options as `test([name][, options][, fn])`.
* `fn` {Function|AsyncFunction} The suite function declaring nested tests and
  suites. The first argument to this function is a [`SuiteContext`][] object.
  **Default:** A no-op function.

The `suite()` function is imported from the `node:test` module.

## `suite.skip([name][, options][, fn])`

<!-- YAML
added:
  - v22.0.0
  - v20.13.0
-->

Shorthand for skipping a suite. This is the same as
[`suite([name], { skip: true }[, fn])`][suite options].

## `suite.todo([name][, options][, fn])`

<!-- YAML
added:
  - v22.0.0
  - v20.13.0
-->

Shorthand for marking a suite as `TODO`. This is the same as
[`suite([name], { todo: true }[, fn])`][suite options].

## `suite.only([name][, options][, fn])`

<!-- YAML
added:
  - v22.0.0
  - v20.13.0
-->

Shorthand for marking a suite as `only`. This is the same as
[`suite([name], { only: true }[, fn])`][suite options].

## `test([name][, options][, fn])`

<!-- YAML
added:
  - v18.0.0
  - v16.17.0
changes:
  - version:
    - REPLACEME
    pr-url: https://github.com/nodejs/node/pull/56664
    description: This function no longer returns a `Promise`.
  - version:
    - v20.2.0
    - v18.17.0
    pr-url: https://github.com/nodejs/node/pull/47909
    description: Added the `skip`, `todo`, and `only` shorthands.
  - version:
    - v18.8.0
    - v16.18.0
    pr-url: https://github.com/nodejs/node/pull/43554
    description: Add a `signal` option.
  - version:
    - v18.7.0
    - v16.17.0
    pr-url: https://github.com/nodejs/node/pull/43505
    description: Add a `timeout` option.
-->

* `name` {string} The name of the test, which is displayed when reporting test
  results. **Default:** The `name` property of `fn`, or `'<anonymous>'` if `fn`
  does not have a name.
* `options` {Object} Configuration options for the test. The following
  properties are supported:
  * `concurrency` {number|boolean} If a number is provided,
    then that many tests would run in parallel within the application thread.
    If `true`, all scheduled asynchronous tests run concurrently within the
    thread. If `false`, only one test runs at a time.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `false`.
  * `only` {boolean} If truthy, and the test context is configured to run
    `only` tests, then this test will be run. Otherwise, the test is skipped.
    **Default:** `false`.
  * `signal` {AbortSignal} Allows aborting an in-progress test.
  * `skip` {boolean|string} If truthy, the test is skipped. If a string is
    provided, that string is displayed in the test results as the reason for
    skipping the test. **Default:** `false`.
  * `todo` {boolean|string} If truthy, the test marked as `TODO`. If a string
    is provided, that string is displayed in the test results as the reason why
    the test is `TODO`. **Default:** `false`.
  * `timeout` {number} A number of milliseconds the test will fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.
  * `plan` {number} The number of assertions and subtests expected to be run in the test.
    If the number of assertions run in the test does not match the number
    specified in the plan, the test will fail.
    **Default:** `undefined`.
* `fn` {Function|AsyncFunction} The function under test. The first argument
  to this function is a [`TestContext`][] object. If the test uses callbacks,
  the callback function is passed as the second argument. **Default:** A no-op
  function.

The `test()` function is the value imported from the `test` module. Each
invocation of this function results in reporting the test to the {TestsStream}.

The `TestContext` object passed to the `fn` argument can be used to perform
actions related to the current test. Examples include skipping the test, adding
additional diagnostic information, or creating subtests.

The `timeout` option can be used to fail the test if it takes longer than
`timeout` milliseconds to complete. However, it is not a reliable mechanism for
canceling tests because a running test might block the application thread and
thus prevent the scheduled cancellation.

## `test.skip([name][, options][, fn])`

Shorthand for skipping a test,
same as [`test([name], { skip: true }[, fn])`][it options].

## `test.todo([name][, options][, fn])`

Shorthand for marking a test as `TODO`,
same as [`test([name], { todo: true }[, fn])`][it options].

## `test.only([name][, options][, fn])`

Shorthand for marking a test as `only`,
same as [`test([name], { only: true }[, fn])`][it options].

## `describe([name][, options][, fn])`

Alias for [`suite()`][].

The `describe()` function is imported from the `node:test` module.

## `describe.skip([name][, options][, fn])`

Shorthand for skipping a suite. This is the same as
[`describe([name], { skip: true }[, fn])`][describe options].

## `describe.todo([name][, options][, fn])`

Shorthand for marking a suite as `TODO`. This is the same as
[`describe([name], { todo: true }[, fn])`][describe options].

## `describe.only([name][, options][, fn])`

<!-- YAML
added:
  - v19.8.0
  - v18.15.0
-->

Shorthand for marking a suite as `only`. This is the same as
[`describe([name], { only: true }[, fn])`][describe options].

## `it([name][, options][, fn])`

<!-- YAML
added:
  - v18.6.0
  - v16.17.0
changes:
  - version:
    - v19.8.0
    - v18.16.0
    pr-url: https://github.com/nodejs/node/pull/46889
    description: Calling `it()` is now equivalent to calling `test()`.
-->

Alias for [`test()`][].

The `it()` function is imported from the `node:test` module.

## `it.skip([name][, options][, fn])`

Shorthand for skipping a test,
same as [`it([name], { skip: true }[, fn])`][it options].

## `it.todo([name][, options][, fn])`

Shorthand for marking a test as `TODO`,
same as [`it([name], { todo: true }[, fn])`][it options].

## `it.only([name][, options][, fn])`

<!-- YAML
added:
  - v19.8.0
  - v18.15.0
-->

Shorthand for marking a test as `only`,
same as [`it([name], { only: true }[, fn])`][it options].

## `before([fn][, options])`

<!-- YAML
added:
  - v18.8.0
  - v16.18.0
-->

* `fn` {Function|AsyncFunction} The hook function.
  If the hook uses callbacks,
  the callback function is passed as the second argument. **Default:** A no-op
  function.
* `options` {Object} Configuration options for the hook. The following
  properties are supported:
  * `signal` {AbortSignal} Allows aborting an in-progress hook.
  * `timeout` {number} A number of milliseconds the hook will fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.

This function creates a hook that runs before executing a suite.

```js
describe('tests', async () => {
  before(() => console.log('about to run some test'));
  it('is a subtest', () => {
    assert.ok('some relevant assertion here');
  });
});
```

## `after([fn][, options])`

<!-- YAML
added:
 - v18.8.0
 - v16.18.0
-->

* `fn` {Function|AsyncFunction} The hook function.
  If the hook uses callbacks,
  the callback function is passed as the second argument. **Default:** A no-op
  function.
* `options` {Object} Configuration options for the hook. The following
  properties are supported:
  * `signal` {AbortSignal} Allows aborting an in-progress hook.
  * `timeout` {number} A number of milliseconds the hook will fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.

This function creates a hook that runs after executing a suite.

```js
describe('tests', async () => {
  after(() => console.log('finished running tests'));
  it('is a subtest', () => {
    assert.ok('some relevant assertion here');
  });
});
```

**Note:** The `after` hook is guaranteed to run,
even if tests within the suite fail.

## `beforeEach([fn][, options])`

<!-- YAML
added:
  - v18.8.0
  - v16.18.0
-->

* `fn` {Function|AsyncFunction} The hook function.
  If the hook uses callbacks,
  the callback function is passed as the second argument. **Default:** A no-op
  function.
* `options` {Object} Configuration options for the hook. The following
  properties are supported:
  * `signal` {AbortSignal} Allows aborting an in-progress hook.
  * `timeout` {number} A number of milliseconds the hook will fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.

This function creates a hook that runs before each test in the current suite.

```js
describe('tests', async () => {
  beforeEach(() => console.log('about to run a test'));
  it('is a subtest', () => {
    assert.ok('some relevant assertion here');
  });
});
```

## `afterEach([fn][, options])`

<!-- YAML
added:
  - v18.8.0
  - v16.18.0
-->

* `fn` {Function|AsyncFunction} The hook function.
  If the hook uses callbacks,
  the callback function is passed as the second argument. **Default:** A no-op
  function.
* `options` {Object} Configuration options for the hook. The following
  properties are supported:
  * `signal` {AbortSignal} Allows aborting an in-progress hook.
  * `timeout` {number} A number of milliseconds the hook will fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.

This function creates a hook that runs after each test in the current suite.
The `afterEach()` hook is run even if the test fails.

```js
describe('tests', async () => {
  afterEach(() => console.log('finished running a test'));
  it('is a subtest', () => {
    assert.ok('some relevant assertion here');
  });
});
```

## `assert`

<!-- YAML
added: v23.7.0
-->

An object whose methods are used to configure available assertions on the
`TestContext` objects in the current process. The methods from `node:assert`
and snapshot testing functions are available by default.

It is possible to apply the same configuration to all files by placing common
configuration code in a module
preloaded with `--require` or `--import`.

### `assert.register(name, fn)`

<!-- YAML
added: v23.7.0
-->

Defines a new assertion function with the provided name and function. If an
assertion already exists with the same name, it is overwritten.

## `snapshot`

<!-- YAML
added: v22.3.0
-->

An object whose methods are used to configure default snapshot settings in the
current process. It is possible to apply the same configuration to all files by
placing common configuration code in a module preloaded with `--require` or
`--import`.

### `snapshot.setDefaultSnapshotSerializers(serializers)`

<!-- YAML
added: v22.3.0
-->

* `serializers` {Array} An array of synchronous functions used as the default
  serializers for snapshot tests.

This function is used to customize the default serialization mechanism used by
the test runner. By default, the test runner performs serialization by calling
`JSON.stringify(value, null, 2)` on the provided value. `JSON.stringify()` does
have limitations regarding circular structures and supported data types. If a
more robust serialization mechanism is required, this function should be used.

### `snapshot.setResolveSnapshotPath(fn)`

<!-- YAML
added: v22.3.0
-->

* `fn` {Function} A function used to compute the location of the snapshot file.
  The function receives the path of the test file as its only argument. If the
  test is not associated with a file (for example in the REPL), the input is
  undefined. `fn()` must return a string specifying the location of the snapshot
  snapshot file.

This function is used to customize the location of the snapshot file used for
snapshot testing. By default, the snapshot filename is the same as the entry
point filename with a `.snapshot` file extension.

## Class: `MockFunctionContext`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

The `MockFunctionContext` class is used to inspect or manipulate the behavior of
mocks created via the [`MockTracker`][] APIs.

### `ctx.calls`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

* {Array}

A getter that returns a copy of the internal array used to track calls to the
mock. Each entry in the array is an object with the following properties.

* `arguments` {Array} An array of the arguments passed to the mock function.
* `error` {any} If the mocked function threw then this property contains the
  thrown value. **Default:** `undefined`.
* `result` {any} The value returned by the mocked function.
* `stack` {Error} An `Error` object whose stack can be used to determine the
  callsite of the mocked function invocation.
* `target` {Function|undefined} If the mocked function is a constructor, this
  field contains the class being constructed. Otherwise this will be
  `undefined`.
* `this` {any} The mocked function's `this` value.

### `ctx.callCount()`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

* Returns: {integer} The number of times that this mock has been invoked.

This function returns the number of times that this mock has been invoked. This
function is more efficient than checking `ctx.calls.length` because `ctx.calls`
is a getter that creates a copy of the internal call tracking array.

### `ctx.mockImplementation(implementation)`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

* `implementation` {Function|AsyncFunction} The function to be used as the
  mock's new implementation.

This function is used to change the behavior of an existing mock.

The following example creates a mock function using `t.mock.fn()`, calls the
mock function, and then changes the mock implementation to a different function.

```js
test('changes a mock behavior', (t) => {
  let cnt = 0;

  function addOne() {
    cnt++;
    return cnt;
  }

  function addTwo() {
    cnt += 2;
    return cnt;
  }

  const fn = t.mock.fn(addOne);

  assert.strictEqual(fn(), 1);
  fn.mock.mockImplementation(addTwo);
  assert.strictEqual(fn(), 3);
  assert.strictEqual(fn(), 5);
});
```

### `ctx.mockImplementationOnce(implementation[, onCall])`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

* `implementation` {Function|AsyncFunction} The function to be used as the
  mock's implementation for the invocation number specified by `onCall`.
* `onCall` {integer} The invocation number that will use `implementation`. If
  the specified invocation has already occurred then an exception is thrown.
  **Default:** The number of the next invocation.

This function is used to change the behavior of an existing mock for a single
invocation. Once invocation `onCall` has occurred, the mock will revert to
whatever behavior it would have used had `mockImplementationOnce()` not been
called.

The following example creates a mock function using `t.mock.fn()`, calls the
mock function, changes the mock implementation to a different function for the
next invocation, and then resumes its previous behavior.

```js
test('changes a mock behavior once', (t) => {
  let cnt = 0;

  function addOne() {
    cnt++;
    return cnt;
  }

  function addTwo() {
    cnt += 2;
    return cnt;
  }

  const fn = t.mock.fn(addOne);

  assert.strictEqual(fn(), 1);
  fn.mock.mockImplementationOnce(addTwo);
  assert.strictEqual(fn(), 3);
  assert.strictEqual(fn(), 4);
});
```

### `ctx.resetCalls()`

<!-- YAML
added:
  - v19.3.0
  - v18.13.0
-->

Resets the call history of the mock function.

### `ctx.restore()`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

Resets the implementation of the mock function to its original behavior. The
mock can still be used after calling this function.

## Class: `MockModuleContext`

<!-- YAML
added:
  - v22.3.0
  - v20.18.0
-->

> Stability: 1.0 - Early development

The `MockModuleContext` class is used to manipulate the behavior of module mocks
created via the [`MockTracker`][] APIs.

### `ctx.restore()`

<!-- YAML
added:
  - v22.3.0
  - v20.18.0
-->

Resets the implementation of the mock module.

## Class: `MockTracker`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

The `MockTracker` class is used to manage mocking functionality. The test runner
module provides a top level `mock` export which is a `MockTracker` instance.
Each test also provides its own `MockTracker` instance via the test context's
`mock` property.

### `mock.fn([original[, implementation]][, options])`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

* `original` {Function|AsyncFunction} An optional function to create a mock on.
  **Default:** A no-op function.
* `implementation` {Function|AsyncFunction} An optional function used as the
  mock implementation for `original`. This is useful for creating mocks that
  exhibit one behavior for a specified number of calls and then restore the
  behavior of `original`. **Default:** The function specified by `original`.
* `options` {Object} Optional configuration options for the mock function. The
  following properties are supported:
  * `times` {integer} The number of times that the mock will use the behavior of
    `implementation`. Once the mock function has been called `times` times, it
    will automatically restore the behavior of `original`. This value must be an
    integer greater than zero. **Default:** `Infinity`.
* Returns: {Proxy} The mocked function. The mocked function contains a special
  `mock` property, which is an instance of [`MockFunctionContext`][], and can
  be used for inspecting and changing the behavior of the mocked function.

This function is used to create a mock function.

The following example creates a mock function that increments a counter by one
on each invocation. The `times` option is used to modify the mock behavior such
that the first two invocations add two to the counter instead of one.

```js
test('mocks a counting function', (t) => {
  let cnt = 0;

  function addOne() {
    cnt++;
    return cnt;
  }

  function addTwo() {
    cnt += 2;
    return cnt;
  }

  const fn = t.mock.fn(addOne, addTwo, { times: 2 });

  assert.strictEqual(fn(), 2);
  assert.strictEqual(fn(), 4);
  assert.strictEqual(fn(), 5);
  assert.strictEqual(fn(), 6);
});
```

### `mock.getter(object, methodName[, implementation][, options])`

<!-- YAML
added:
  - v19.3.0
  - v18.13.0
-->

This function is syntax sugar for [`MockTracker.method`][] with `options.getter`
set to `true`.

### `mock.method(object, methodName[, implementation][, options])`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

* `object` {Object} The object whose method is being mocked.
* `methodName` {string|symbol} The identifier of the method on `object` to mock.
  If `object[methodName]` is not a function, an error is thrown.
* `implementation` {Function|AsyncFunction} An optional function used as the
  mock implementation for `object[methodName]`. **Default:** The original method
  specified by `object[methodName]`.
* `options` {Object} Optional configuration options for the mock method. The
  following properties are supported:
  * `getter` {boolean} If `true`, `object[methodName]` is treated as a getter.
    This option cannot be used with the `setter` option. **Default:** false.
  * `setter` {boolean} If `true`, `object[methodName]` is treated as a setter.
    This option cannot be used with the `getter` option. **Default:** false.
  * `times` {integer} The number of times that the mock will use the behavior of
    `implementation`. Once the mocked method has been called `times` times, it
    will automatically restore the original behavior. This value must be an
    integer greater than zero. **Default:** `Infinity`.
* Returns: {Proxy} The mocked method. The mocked method contains a special
  `mock` property, which is an instance of [`MockFunctionContext`][], and can
  be used for inspecting and changing the behavior of the mocked method.

This function is used to create a mock on an existing object method. The
following example demonstrates how a mock is created on an existing object
method.

```js
test('spies on an object method', (t) => {
  const number = {
    value: 5,
    subtract(a) {
      return this.value - a;
    },
  };

  t.mock.method(number, 'subtract');
  assert.strictEqual(number.subtract.mock.callCount(), 0);
  assert.strictEqual(number.subtract(3), 2);
  assert.strictEqual(number.subtract.mock.callCount(), 1);

  const call = number.subtract.mock.calls[0];

  assert.deepStrictEqual(call.arguments, [3]);
  assert.strictEqual(call.result, 2);
  assert.strictEqual(call.error, undefined);
  assert.strictEqual(call.target, undefined);
  assert.strictEqual(call.this, number);
});
```

### `mock.module(specifier[, options])`

<!-- YAML
added:
  - v22.3.0
  - v20.18.0
-->

> Stability: 1.0 - Early development

* `specifier` {string|URL} A string identifying the module to mock.
* `options` {Object} Optional configuration options for the mock module. The
  following properties are supported:
  * `cache` {boolean} If `false`, each call to `require()` or `import()`
    generates a new mock module. If `true`, subsequent calls will return the same
    module mock, and the mock module is inserted into the CommonJS cache.
    **Default:** false.
  * `defaultExport` {any} An optional value used as the mocked module's default
    export. If this value is not provided, ESM mocks do not include a default
    export. If the mock is a CommonJS or builtin module, this setting is used as
    the value of `module.exports`. If this value is not provided, CJS and builtin
    mocks use an empty object as the value of `module.exports`.
  * `namedExports` {Object} An optional object whose keys and values are used to
    create the named exports of the mock module. If the mock is a CommonJS or
    builtin module, these values are copied onto `module.exports`. Therefore, if a
    mock is created with both named exports and a non-object default export, the
    mock will throw an exception when used as a CJS or builtin module.
* Returns: {MockModuleContext} An object that can be used to manipulate the mock.

This function is used to mock the exports of ECMAScript modules, CommonJS
modules, and Node.js builtin modules. Any references to the original module
prior to mocking are not impacted. In order to enable module mocking, Node.js must
be started with the [`--experimental-test-module-mocks`][] command-line flag.

The following example demonstrates how a mock is created for a module.

```js
test('mocks a builtin module in both module systems', async (t) => {
  // Create a mock of 'node:readline' with a named export named 'fn', which
  // does not exist in the original 'node:readline' module.
  const mock = t.mock.module('node:readline', {
    namedExports: { fn() { return 42; } },
  });

  let esmImpl = await import('node:readline');
  let cjsImpl = require('node:readline');

  // cursorTo() is an export of the original 'node:readline' module.
  assert.strictEqual(esmImpl.cursorTo, undefined);
  assert.strictEqual(cjsImpl.cursorTo, undefined);
  assert.strictEqual(esmImpl.fn(), 42);
  assert.strictEqual(cjsImpl.fn(), 42);

  mock.restore();

  // The mock is restored, so the original builtin module is returned.
  esmImpl = await import('node:readline');
  cjsImpl = require('node:readline');

  assert.strictEqual(typeof esmImpl.cursorTo, 'function');
  assert.strictEqual(typeof cjsImpl.cursorTo, 'function');
  assert.strictEqual(esmImpl.fn, undefined);
  assert.strictEqual(cjsImpl.fn, undefined);
});
```

### `mock.reset()`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

This function restores the default behavior of all mocks that were previously
created by this `MockTracker` and disassociates the mocks from the
`MockTracker` instance. Once disassociated, the mocks can still be used, but the
`MockTracker` instance can no longer be used to reset their behavior or
otherwise interact with them.

After each test completes, this function is called on the test context's
`MockTracker`. If the global `MockTracker` is used extensively, calling this
function manually is recommended.

### `mock.restoreAll()`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

This function restores the default behavior of all mocks that were previously
created by this `MockTracker`. Unlike `mock.reset()`, `mock.restoreAll()` does
not disassociate the mocks from the `MockTracker` instance.

### `mock.setter(object, methodName[, implementation][, options])`

<!-- YAML
added:
  - v19.3.0
  - v18.13.0
-->

This function is syntax sugar for [`MockTracker.method`][] with `options.setter`
set to `true`.

## Class: `MockTimers`

<!-- YAML
added:
  - v20.4.0
  - v18.19.0
changes:
  - version: v23.1.0
    pr-url: https://github.com/nodejs/node/pull/55398
    description: The Mock Timers is now stable.
-->

> Stability: 2 - Stable

Mocking timers is a technique commonly used in software testing to simulate and
control the behavior of timers, such as `setInterval` and `setTimeout`,
without actually waiting for the specified time intervals.

MockTimers is also able to mock the `Date` object.

The [`MockTracker`][] provides a top-level `timers` export
which is a `MockTimers` instance.

### `timers.enable([enableOptions])`

<!-- YAML
added:
  - v20.4.0
  - v18.19.0
changes:
  - version:
    - v21.2.0
    - v20.11.0
    pr-url: https://github.com/nodejs/node/pull/48638
    description: Updated parameters to be an option object with available APIs
                 and the default initial epoch.
-->

Enables timer mocking for the specified timers.

* `enableOptions` {Object} Optional configuration options for enabling timer
  mocking. The following properties are supported:
  * `apis` {Array} An optional array containing the timers to mock.
    The currently supported timer values are `'setInterval'`, `'setTimeout'`, `'setImmediate'`,
    and `'Date'`. **Default:** `['setInterval', 'setTimeout', 'setImmediate', 'Date']`.
    If no array is provided, all time related APIs (`'setInterval'`, `'clearInterval'`,
    `'setTimeout'`, `'clearTimeout'`, `'setImmediate'`, `'clearImmediate'`, and
    `'Date'`) will be mocked by default.
  * `now` {number | Date} An optional number or Date object representing the
    initial time (in milliseconds) to use as the value
    for `Date.now()`. **Default:** `0`.

**Note:** When you enable mocking for a specific timer, its associated
clear function will also be implicitly mocked.

**Note:** Mocking `Date` will affect the behavior of the mocked timers
as they use the same internal clock.

Example usage without setting initial time:

```mjs
import { mock } from 'node:test';
mock.timers.enable({ apis: ['setInterval'] });
```

```cjs
const { mock } = require('node:test');
mock.timers.enable({ apis: ['setInterval'] });
```

The above example enables mocking for the `setInterval` timer and
implicitly mocks the `clearInterval` function. Only the `setInterval`
and `clearInterval` functions from [node:timers](./timers.md),
[node:timers/promises](./timers.md#timers-promises-api), and
`globalThis` will be mocked.

Example usage with initial time set

```mjs
import { mock } from 'node:test';
mock.timers.enable({ apis: ['Date'], now: 1000 });
```

```cjs
const { mock } = require('node:test');
mock.timers.enable({ apis: ['Date'], now: 1000 });
```

Example usage with initial Date object as time set

```mjs
import { mock } from 'node:test';
mock.timers.enable({ apis: ['Date'], now: new Date() });
```

```cjs
const { mock } = require('node:test');
mock.timers.enable({ apis: ['Date'], now: new Date() });
```

Alternatively, if you call `mock.timers.enable()` without any parameters:

All timers (`'setInterval'`, `'clearInterval'`, `'setTimeout'`, `'clearTimeout'`,
`'setImmediate'`, and `'clearImmediate'`) will be mocked. The `setInterval`,
`clearInterval`, `setTimeout`, `clearTimeout`, `setImmediate`, and
`clearImmediate` functions from `node:timers`, `node:timers/promises`, and
`globalThis` will be mocked. As well as the global `Date` object.

### `timers.reset()`

<!-- YAML
added:
  - v20.4.0
  - v18.19.0
-->

This function restores the default behavior of all mocks that were previously
created by this  `MockTimers` instance and disassociates the mocks
from the  `MockTracker` instance.

**Note:** After each test completes, this function is called on
the test context's  `MockTracker`.

```mjs
import { mock } from 'node:test';
mock.timers.reset();
```

```cjs
const { mock } = require('node:test');
mock.timers.reset();
```

### `timers[Symbol.dispose]()`

Calls `timers.reset()`.

### `timers.tick([milliseconds])`

<!-- YAML
added:
  - v20.4.0
  - v18.19.0
-->

Advances time for all mocked timers.

* `milliseconds` {number} The amount of time, in milliseconds,
  to advance the timers. **Default:** `1`.

**Note:** This diverges from how `setTimeout` in Node.js behaves and accepts
only positive numbers. In Node.js, `setTimeout` with negative numbers is
only supported for web compatibility reasons.

The following example mocks a `setTimeout` function and
by using `.tick` advances in
time triggering all pending timers.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
  const fn = context.mock.fn();

  context.mock.timers.enable({ apis: ['setTimeout'] });

  setTimeout(fn, 9999);

  assert.strictEqual(fn.mock.callCount(), 0);

  // Advance in time
  context.mock.timers.tick(9999);

  assert.strictEqual(fn.mock.callCount(), 1);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
  const fn = context.mock.fn();
  context.mock.timers.enable({ apis: ['setTimeout'] });

  setTimeout(fn, 9999);
  assert.strictEqual(fn.mock.callCount(), 0);

  // Advance in time
  context.mock.timers.tick(9999);

  assert.strictEqual(fn.mock.callCount(), 1);
});
```

Alternatively, the `.tick` function can be called many times

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
  const fn = context.mock.fn();
  context.mock.timers.enable({ apis: ['setTimeout'] });
  const nineSecs = 9000;
  setTimeout(fn, nineSecs);

  const threeSeconds = 3000;
  context.mock.timers.tick(threeSeconds);
  context.mock.timers.tick(threeSeconds);
  context.mock.timers.tick(threeSeconds);

  assert.strictEqual(fn.mock.callCount(), 1);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
  const fn = context.mock.fn();
  context.mock.timers.enable({ apis: ['setTimeout'] });
  const nineSecs = 9000;
  setTimeout(fn, nineSecs);

  const threeSeconds = 3000;
  context.mock.timers.tick(threeSeconds);
  context.mock.timers.tick(threeSeconds);
  context.mock.timers.tick(threeSeconds);

  assert.strictEqual(fn.mock.callCount(), 1);
});
```

Advancing time using `.tick` will also advance the time for any `Date` object
created after the mock was enabled (if `Date` was also set to be mocked).

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
  const fn = context.mock.fn();

  context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
  setTimeout(fn, 9999);

  assert.strictEqual(fn.mock.callCount(), 0);
  assert.strictEqual(Date.now(), 0);

  // Advance in time
  context.mock.timers.tick(9999);
  assert.strictEqual(fn.mock.callCount(), 1);
  assert.strictEqual(Date.now(), 9999);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
  const fn = context.mock.fn();
  context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });

  setTimeout(fn, 9999);
  assert.strictEqual(fn.mock.callCount(), 0);
  assert.strictEqual(Date.now(), 0);

  // Advance in time
  context.mock.timers.tick(9999);
  assert.strictEqual(fn.mock.callCount(), 1);
  assert.strictEqual(Date.now(), 9999);
});
```

#### Using clear functions

As mentioned, all clear functions from timers (`clearTimeout`, `clearInterval`,and
`clearImmediate`) are implicitly mocked. Take a look at this example using `setTimeout`:

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
  const fn = context.mock.fn();

  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['setTimeout'] });
  const id = setTimeout(fn, 9999);

  // Implicitly mocked as well
  clearTimeout(id);
  context.mock.timers.tick(9999);

  // As that setTimeout was cleared the mock function will never be called
  assert.strictEqual(fn.mock.callCount(), 0);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
  const fn = context.mock.fn();

  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['setTimeout'] });
  const id = setTimeout(fn, 9999);

  // Implicitly mocked as well
  clearTimeout(id);
  context.mock.timers.tick(9999);

  // As that setTimeout was cleared the mock function will never be called
  assert.strictEqual(fn.mock.callCount(), 0);
});
```

#### Working with Node.js timers modules

Once you enable mocking timers, [node:timers](./timers.md),
[node:timers/promises](./timers.md#timers-promises-api) modules,
and timers from the Node.js global context are enabled:

**Note:** Destructuring functions such as
`import { setTimeout } from 'node:timers'` is currently
not supported by this API.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';
import nodeTimers from 'node:timers';
import nodeTimersPromises from 'node:timers/promises';

test('mocks setTimeout to be executed synchronously without having to actually wait for it', async (context) => {
  const globalTimeoutObjectSpy = context.mock.fn();
  const nodeTimerSpy = context.mock.fn();
  const nodeTimerPromiseSpy = context.mock.fn();

  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['setTimeout'] });
  setTimeout(globalTimeoutObjectSpy, 9999);
  nodeTimers.setTimeout(nodeTimerSpy, 9999);

  const promise = nodeTimersPromises.setTimeout(9999).then(nodeTimerPromiseSpy);

  // Advance in time
  context.mock.timers.tick(9999);
  assert.strictEqual(globalTimeoutObjectSpy.mock.callCount(), 1);
  assert.strictEqual(nodeTimerSpy.mock.callCount(), 1);
  await promise;
  assert.strictEqual(nodeTimerPromiseSpy.mock.callCount(), 1);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');
const nodeTimers = require('node:timers');
const nodeTimersPromises = require('node:timers/promises');

test('mocks setTimeout to be executed synchronously without having to actually wait for it', async (context) => {
  const globalTimeoutObjectSpy = context.mock.fn();
  const nodeTimerSpy = context.mock.fn();
  const nodeTimerPromiseSpy = context.mock.fn();

  // Optionally choose what to mock
  context.mock.timers.enable({ apis: ['setTimeout'] });
  setTimeout(globalTimeoutObjectSpy, 9999);
  nodeTimers.setTimeout(nodeTimerSpy, 9999);

  const promise = nodeTimersPromises.setTimeout(9999).then(nodeTimerPromiseSpy);

  // Advance in time
  context.mock.timers.tick(9999);
  assert.strictEqual(globalTimeoutObjectSpy.mock.callCount(), 1);
  assert.strictEqual(nodeTimerSpy.mock.callCount(), 1);
  await promise;
  assert.strictEqual(nodeTimerPromiseSpy.mock.callCount(), 1);
});
```

In Node.js, `setInterval` from [node:timers/promises](./timers.md#timers-promises-api)
is an `AsyncGenerator` and is also supported by this API:

```mjs
import assert from 'node:assert';
import { test } from 'node:test';
import nodeTimersPromises from 'node:timers/promises';
test('should tick five times testing a real use case', async (context) => {
  context.mock.timers.enable({ apis: ['setInterval'] });

  const expectedIterations = 3;
  const interval = 1000;
  const startedAt = Date.now();
  async function run() {
    const times = [];
    for await (const time of nodeTimersPromises.setInterval(interval, startedAt)) {
      times.push(time);
      if (times.length === expectedIterations) break;
    }
    return times;
  }

  const r = run();
  context.mock.timers.tick(interval);
  context.mock.timers.tick(interval);
  context.mock.timers.tick(interval);

  const timeResults = await r;
  assert.strictEqual(timeResults.length, expectedIterations);
  for (let it = 1; it < expectedIterations; it++) {
    assert.strictEqual(timeResults[it - 1], startedAt + (interval * it));
  }
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');
const nodeTimersPromises = require('node:timers/promises');
test('should tick five times testing a real use case', async (context) => {
  context.mock.timers.enable({ apis: ['setInterval'] });

  const expectedIterations = 3;
  const interval = 1000;
  const startedAt = Date.now();
  async function run() {
    const times = [];
    for await (const time of nodeTimersPromises.setInterval(interval, startedAt)) {
      times.push(time);
      if (times.length === expectedIterations) break;
    }
    return times;
  }

  const r = run();
  context.mock.timers.tick(interval);
  context.mock.timers.tick(interval);
  context.mock.timers.tick(interval);

  const timeResults = await r;
  assert.strictEqual(timeResults.length, expectedIterations);
  for (let it = 1; it < expectedIterations; it++) {
    assert.strictEqual(timeResults[it - 1], startedAt + (interval * it));
  }
});
```

### `timers.runAll()`

<!-- YAML
added:
  - v20.4.0
  - v18.19.0
-->

Triggers all pending mocked timers immediately. If the `Date` object is also
mocked, it will also advance the `Date` object to the furthest timer's time.

The example below triggers all pending timers immediately,
causing them to execute without any delay.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('runAll functions following the given order', (context) => {
  context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
  const results = [];
  setTimeout(() => results.push(1), 9999);

  // Notice that if both timers have the same timeout,
  // the order of execution is guaranteed
  setTimeout(() => results.push(3), 8888);
  setTimeout(() => results.push(2), 8888);

  assert.deepStrictEqual(results, []);

  context.mock.timers.runAll();
  assert.deepStrictEqual(results, [3, 2, 1]);
  // The Date object is also advanced to the furthest timer's time
  assert.strictEqual(Date.now(), 9999);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('runAll functions following the given order', (context) => {
  context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
  const results = [];
  setTimeout(() => results.push(1), 9999);

  // Notice that if both timers have the same timeout,
  // the order of execution is guaranteed
  setTimeout(() => results.push(3), 8888);
  setTimeout(() => results.push(2), 8888);

  assert.deepStrictEqual(results, []);

  context.mock.timers.runAll();
  assert.deepStrictEqual(results, [3, 2, 1]);
  // The Date object is also advanced to the furthest timer's time
  assert.strictEqual(Date.now(), 9999);
});
```

**Note:** The `runAll()` function is specifically designed for
triggering timers in the context of timer mocking.
It does not have any effect on real-time system
clocks or actual timers outside of the mocking environment.

### `timers.setTime(milliseconds)`

<!-- YAML
added:
  - v21.2.0
  - v20.11.0
-->

Sets the current Unix timestamp that will be used as reference for any mocked
`Date` objects.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('runAll functions following the given order', (context) => {
  const now = Date.now();
  const setTime = 1000;
  // Date.now is not mocked
  assert.deepStrictEqual(Date.now(), now);

  context.mock.timers.enable({ apis: ['Date'] });
  context.mock.timers.setTime(setTime);
  // Date.now is now 1000
  assert.strictEqual(Date.now(), setTime);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('setTime replaces current time', (context) => {
  const now = Date.now();
  const setTime = 1000;
  // Date.now is not mocked
  assert.deepStrictEqual(Date.now(), now);

  context.mock.timers.enable({ apis: ['Date'] });
  context.mock.timers.setTime(setTime);
  // Date.now is now 1000
  assert.strictEqual(Date.now(), setTime);
});
```

#### Dates and Timers working together

Dates and timer objects are dependent on each other. If you use `setTime()` to
pass the current time to the mocked `Date` object, the set timers with
`setTimeout` and `setInterval` will **not** be affected.

However, the `tick` method **will** advanced the mocked `Date` object.

```mjs
import assert from 'node:assert';
import { test } from 'node:test';

test('runAll functions following the given order', (context) => {
  context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
  const results = [];
  setTimeout(() => results.push(1), 9999);

  assert.deepStrictEqual(results, []);
  context.mock.timers.setTime(12000);
  assert.deepStrictEqual(results, []);
  // The date is advanced but the timers don't tick
  assert.strictEqual(Date.now(), 12000);
});
```

```cjs
const assert = require('node:assert');
const { test } = require('node:test');

test('runAll functions following the given order', (context) => {
  context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
  const results = [];
  setTimeout(() => results.push(1), 9999);

  assert.deepStrictEqual(results, []);
  context.mock.timers.setTime(12000);
  assert.deepStrictEqual(results, []);
  // The date is advanced but the timers don't tick
  assert.strictEqual(Date.now(), 12000);
});
```

## Class: `TestsStream`

<!-- YAML
added:
  - v18.9.0
  - v16.19.0
changes:
  - version:
    - v20.0.0
    - v19.9.0
    - v18.17.0
    pr-url: https://github.com/nodejs/node/pull/47094
    description: added type to test:pass and test:fail events for when the test is a suite.
-->

* Extends {Readable}

A successful call to [`run()`][] method will return a new {TestsStream}
object, streaming a series of events representing the execution of the tests.
`TestsStream` will emit events, in the order of the tests definition

Some of the events are guaranteed to be emitted in the same order as the tests
are defined, while others are emitted in the order that the tests execute.

### Event: `'test:coverage'`

* `data` {Object}
  * `summary` {Object} An object containing the coverage report.
    * `files` {Array} An array of coverage reports for individual files. Each
      report is an object with the following schema:
      * `path` {string} The absolute path of the file.
      * `totalLineCount` {number} The total number of lines.
      * `totalBranchCount` {number} The total number of branches.
      * `totalFunctionCount` {number} The total number of functions.
      * `coveredLineCount` {number} The number of covered lines.
      * `coveredBranchCount` {number} The number of covered branches.
      * `coveredFunctionCount` {number} The number of covered functions.
      * `coveredLinePercent` {number} The percentage of lines covered.
      * `coveredBranchPercent` {number} The percentage of branches covered.
      * `coveredFunctionPercent` {number} The percentage of functions covered.
      * `functions` {Array} An array of functions representing function
        coverage.
        * `name` {string} The name of the function.
        * `line` {number} The line number where the function is defined.
        * `count` {number} The number of times the function was called.
      * `branches` {Array} An array of branches representing branch coverage.
        * `line` {number} The line number where the branch is defined.
        * `count` {number} The number of times the branch was taken.
      * `lines` {Array} An array of lines representing line
        numbers and the number of times they were covered.
        * `line` {number} The line number.
        * `count` {number} The number of times the line was covered.
    * `thresholds` {Object} An object containing whether or not the coverage for
      each coverage type.
      * `function` {number} The function coverage threshold.
      * `branch` {number} The branch coverage threshold.
      * `line` {number} The line coverage threshold.
    * `totals` {Object} An object containing a summary of coverage for all
      files.
      * `totalLineCount` {number} The total number of lines.
      * `totalBranchCount` {number} The total number of branches.
      * `totalFunctionCount` {number} The total number of functions.
      * `coveredLineCount` {number} The number of covered lines.
      * `coveredBranchCount` {number} The number of covered branches.
      * `coveredFunctionCount` {number} The number of covered functions.
      * `coveredLinePercent` {number} The percentage of lines covered.
      * `coveredBranchPercent` {number} The percentage of branches covered.
      * `coveredFunctionPercent` {number} The percentage of functions covered.
    * `workingDirectory` {string} The working directory when code coverage
      began. This is useful for displaying relative path names in case the tests
      changed the working directory of the Node.js process.
  * `nesting` {number} The nesting level of the test.

Emitted when code coverage is enabled and all tests have completed.

### Event: `'test:complete'`

* `data` {Object}
  * `column` {number|undefined} The column number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `details` {Object} Additional execution metadata.
    * `passed` {boolean} Whether the test passed or not.
    * `duration_ms` {number} The duration of the test in milliseconds.
    * `error` {Error|undefined} An error wrapping the error thrown by the test
      if it did not pass.
      * `cause` {Error} The actual error thrown by the test.
    * `type` {string|undefined} The type of the test, used to denote whether
      this is a suite.
  * `file` {string|undefined} The path of the test file,
    `undefined` if test was run through the REPL.
  * `line` {number|undefined} The line number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `name` {string} The test name.
  * `nesting` {number} The nesting level of the test.
  * `testNumber` {number} The ordinal number of the test.
  * `todo` {string|boolean|undefined} Present if [`context.todo`][] is called
  * `skip` {string|boolean|undefined} Present if [`context.skip`][] is called

Emitted when a test completes its execution.
This event is not emitted in the same order as the tests are
defined.
The corresponding declaration ordered events are `'test:pass'` and `'test:fail'`.

### Event: `'test:dequeue'`

* `data` {Object}
  * `column` {number|undefined} The column number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `file` {string|undefined} The path of the test file,
    `undefined` if test was run through the REPL.
  * `line` {number|undefined} The line number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `name` {string} The test name.
  * `nesting` {number} The nesting level of the test.
  * `type` {string} The test type. Either `'suite'` or `'test'`.

Emitted when a test is dequeued, right before it is executed.
This event is not guaranteed to be emitted in the same order as the tests are
defined. The corresponding declaration ordered event is `'test:start'`.

### Event: `'test:diagnostic'`

* `data` {Object}
  * `column` {number|undefined} The column number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `file` {string|undefined} The path of the test file,
    `undefined` if test was run through the REPL.
  * `line` {number|undefined} The line number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `message` {string} The diagnostic message.
  * `nesting` {number} The nesting level of the test.

Emitted when [`context.diagnostic`][] is called.
This event is guaranteed to be emitted in the same order as the tests are
defined.

### Event: `'test:enqueue'`

* `data` {Object}
  * `column` {number|undefined} The column number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `file` {string|undefined} The path of the test file,
    `undefined` if test was run through the REPL.
  * `line` {number|undefined} The line number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `name` {string} The test name.
  * `nesting` {number} The nesting level of the test.
  * `type` {string} The test type. Either `'suite'` or `'test'`.

Emitted when a test is enqueued for execution.

### Event: `'test:fail'`

* `data` {Object}
  * `column` {number|undefined} The column number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `details` {Object} Additional execution metadata.
    * `duration_ms` {number} The duration of the test in milliseconds.
    * `error` {Error} An error wrapping the error thrown by the test.
      * `cause` {Error} The actual error thrown by the test.
    * `type` {string|undefined} The type of the test, used to denote whether
      this is a suite.
  * `file` {string|undefined} The path of the test file,
    `undefined` if test was run through the REPL.
  * `line` {number|undefined} The line number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `name` {string} The test name.
  * `nesting` {number} The nesting level of the test.
  * `testNumber` {number} The ordinal number of the test.
  * `todo` {string|boolean|undefined} Present if [`context.todo`][] is called
  * `skip` {string|boolean|undefined} Present if [`context.skip`][] is called

Emitted when a test fails.
This event is guaranteed to be emitted in the same order as the tests are
defined.
The corresponding execution ordered event is `'test:complete'`.

### Event: `'test:pass'`

* `data` {Object}
  * `column` {number|undefined} The column number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `details` {Object} Additional execution metadata.
    * `duration_ms` {number} The duration of the test in milliseconds.
    * `type` {string|undefined} The type of the test, used to denote whether
      this is a suite.
  * `file` {string|undefined} The path of the test file,
    `undefined` if test was run through the REPL.
  * `line` {number|undefined} The line number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `name` {string} The test name.
  * `nesting` {number} The nesting level of the test.
  * `testNumber` {number} The ordinal number of the test.
  * `todo` {string|boolean|undefined} Present if [`context.todo`][] is called
  * `skip` {string|boolean|undefined} Present if [`context.skip`][] is called

Emitted when a test passes.
This event is guaranteed to be emitted in the same order as the tests are
defined.
The corresponding execution ordered event is `'test:complete'`.

### Event: `'test:plan'`

* `data` {Object}
  * `column` {number|undefined} The column number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `file` {string|undefined} The path of the test file,
    `undefined` if test was run through the REPL.
  * `line` {number|undefined} The line number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `nesting` {number} The nesting level of the test.
  * `count` {number} The number of subtests that have ran.

Emitted when all subtests have completed for a given test.
This event is guaranteed to be emitted in the same order as the tests are
defined.

### Event: `'test:start'`

* `data` {Object}
  * `column` {number|undefined} The column number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `file` {string|undefined} The path of the test file,
    `undefined` if test was run through the REPL.
  * `line` {number|undefined} The line number where the test is defined, or
    `undefined` if the test was run through the REPL.
  * `name` {string} The test name.
  * `nesting` {number} The nesting level of the test.

Emitted when a test starts reporting its own and its subtests status.
This event is guaranteed to be emitted in the same order as the tests are
defined.
The corresponding execution ordered event is `'test:dequeue'`.

### Event: `'test:stderr'`

* `data` {Object}
  * `file` {string} The path of the test file.
  * `message` {string} The message written to `stderr`.

Emitted when a running test writes to `stderr`.
This event is only emitted if `--test` flag is passed.
This event is not guaranteed to be emitted in the same order as the tests are
defined.

### Event: `'test:stdout'`

* `data` {Object}
  * `file` {string} The path of the test file.
  * `message` {string} The message written to `stdout`.

Emitted when a running test writes to `stdout`.
This event is only emitted if `--test` flag is passed.
This event is not guaranteed to be emitted in the same order as the tests are
defined.

### Event: `'test:summary'`

* `data` {Object}
  * `counts` {Object} An object containing the counts of various test results.
    * `cancelled` {number} The total number of cancelled tests.
    * `failed` {number} The total number of failed tests.
    * `passed` {number} The total number of passed tests.
    * `skipped` {number} The total number of skipped tests.
    * `suites` {number} The total number of suites run.
    * `tests` {number} The total number of tests run, excluding suites.
    * `todo` {number} The total number of TODO tests.
    * `topLevel` {number} The total number of top level tests and suites.
  * `duration_ms` {number} The duration of the test run in milliseconds.
  * `file` {string|undefined} The path of the test file that generated the
    summary. If the summary corresponds to multiple files, this value is
    `undefined`.
  * `success` {boolean} Indicates whether or not the test run is considered
    successful or not. If any error condition occurs, such as a failing test or
    unmet coverage threshold, this value will be set to `false`.

Emitted when a test run completes. This event contains metrics pertaining to
the completed test run, and is useful for determining if a test run passed or
failed. If process-level test isolation is used, a `'test:summary'` event is
generated for each test file in addition to a final cumulative summary.

### Event: `'test:watch:drained'`

Emitted when no more tests are queued for execution in watch mode.

## Class: `TestContext`

<!-- YAML
added:
  - v18.0.0
  - v16.17.0
changes:
  - version:
    - v20.1.0
    - v18.17.0
    pr-url: https://github.com/nodejs/node/pull/47586
    description: The `before` function was added to TestContext.
-->

An instance of `TestContext` is passed to each test function in order to
interact with the test runner. However, the `TestContext` constructor is not
exposed as part of the API.

### `context.before([fn][, options])`

<!-- YAML
added:
  - v20.1.0
  - v18.17.0
-->

* `fn` {Function|AsyncFunction} The hook function. The first argument
  to this function is a [`TestContext`][] object. If the hook uses callbacks,
  the callback function is passed as the second argument. **Default:** A no-op
  function.
* `options` {Object} Configuration options for the hook. The following
  properties are supported:
  * `signal` {AbortSignal} Allows aborting an in-progress hook.
  * `timeout` {number} A number of milliseconds the hook will fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.

This function is used to create a hook running before
subtest of the current test.

### `context.beforeEach([fn][, options])`

<!-- YAML
added:
  - v18.8.0
  - v16.18.0
-->

* `fn` {Function|AsyncFunction} The hook function. The first argument
  to this function is a [`TestContext`][] object. If the hook uses callbacks,
  the callback function is passed as the second argument. **Default:** A no-op
  function.
* `options` {Object} Configuration options for the hook. The following
  properties are supported:
  * `signal` {AbortSignal} Allows aborting an in-progress hook.
  * `timeout` {number} A number of milliseconds the hook will fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.

This function is used to create a hook running
before each subtest of the current test.

```js
test('top level test', async (t) => {
  t.beforeEach((t) => t.diagnostic(`about to run ${t.name}`));
  t.test('This is a subtest', (t) => {
    assert.ok('some relevant assertion here');
  });
});
```

### `context.after([fn][, options])`

<!-- YAML
added:
  - v19.3.0
  - v18.13.0
-->

* `fn` {Function|AsyncFunction} The hook function. The first argument
  to this function is a [`TestContext`][] object. If the hook uses callbacks,
  the callback function is passed as the second argument. **Default:** A no-op
  function.
* `options` {Object} Configuration options for the hook. The following
  properties are supported:
  * `signal` {AbortSignal} Allows aborting an in-progress hook.
  * `timeout` {number} A number of milliseconds the hook will fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.

This function is used to create a hook that runs after the current test
finishes.

```js
test('top level test', async (t) => {
  t.after((t) => t.diagnostic(`finished running ${t.name}`));
  assert.ok('some relevant assertion here');
});
```

### `context.afterEach([fn][, options])`

<!-- YAML
added:
  - v18.8.0
  - v16.18.0
-->

* `fn` {Function|AsyncFunction} The hook function. The first argument
  to this function is a [`TestContext`][] object. If the hook uses callbacks,
  the callback function is passed as the second argument. **Default:** A no-op
  function.
* `options` {Object} Configuration options for the hook. The following
  properties are supported:
  * `signal` {AbortSignal} Allows aborting an in-progress hook.
  * `timeout` {number} A number of milliseconds the hook will fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.

This function is used to create a hook running
after each subtest of the current test.

```js
test('top level test', async (t) => {
  t.afterEach((t) => t.diagnostic(`finished running ${t.name}`));
  t.test('This is a subtest', (t) => {
    assert.ok('some relevant assertion here');
  });
});
```

### `context.assert`

<!-- YAML
added:
  - v22.2.0
  - v20.15.0
-->

An object containing assertion methods bound to `context`. The top-level
functions from the `node:assert` module are exposed here for the purpose of
creating test plans.

```js
test('test', (t) => {
  t.plan(1);
  t.assert.strictEqual(true, true);
});
```

#### `context.assert.fileSnapshot(value, path[, options])`

<!-- YAML
added: v23.7.0
-->

* `value` {any} A value to serialize to a string. If Node.js was started with
  the [`--test-update-snapshots`][] flag, the serialized value is written to
  `path`. Otherwise, the serialized value is compared to the contents of the
  existing snapshot file.
* `path` {string} The file where the serialized `value` is written.
* `options` {Object} Optional configuration options. The following properties
  are supported:
  * `serializers` {Array} An array of synchronous functions used to serialize
    `value` into a string. `value` is passed as the only argument to the first
    serializer function. The return value of each serializer is passed as input
    to the next serializer. Once all serializers have run, the resulting value
    is coerced to a string. **Default:** If no serializers are provided, the
    test runner's default serializers are used.

This function serializes `value` and writes it to the file specified by `path`.

```js
test('snapshot test with default serialization', (t) => {
  t.assert.fileSnapshot({ value1: 1, value2: 2 }, './snapshots/snapshot.json');
});
```

This function differs from `context.assert.snapshot()` in the following ways:

* The snapshot file path is explicitly provided by the user.
* Each snapshot file is limited to a single snapshot value.
* No additional escaping is performed by the test runner.

These differences allow snapshot files to better support features such as syntax
highlighting.

#### `context.assert.snapshot(value[, options])`

<!-- YAML
added: v22.3.0
-->

* `value` {any} A value to serialize to a string. If Node.js was started with
  the [`--test-update-snapshots`][] flag, the serialized value is written to
  the snapshot file. Otherwise, the serialized value is compared to the
  corresponding value in the existing snapshot file.
* `options` {Object} Optional configuration options. The following properties
  are supported:
  * `serializers` {Array} An array of synchronous functions used to serialize
    `value` into a string. `value` is passed as the only argument to the first
    serializer function. The return value of each serializer is passed as input
    to the next serializer. Once all serializers have run, the resulting value
    is coerced to a string. **Default:** If no serializers are provided, the
    test runner's default serializers are used.

This function implements assertions for snapshot testing.

```js
test('snapshot test with default serialization', (t) => {
  t.assert.snapshot({ value1: 1, value2: 2 });
});

test('snapshot test with custom serialization', (t) => {
  t.assert.snapshot({ value3: 3, value4: 4 }, {
    serializers: [(value) => JSON.stringify(value)],
  });
});
```

### `context.diagnostic(message)`

<!-- YAML
added:
  - v18.0.0
  - v16.17.0
-->

* `message` {string} Message to be reported.

This function is used to write diagnostics to the output. Any diagnostic
information is included at the end of the test's results. This function does
not return a value.

```js
test('top level test', (t) => {
  t.diagnostic('A diagnostic message');
});
```

### `context.filePath`

<!-- YAML
added:
  - v22.6.0
  - v20.16.0
-->

The absolute path of the test file that created the current test. If a test file
imports additional modules that generate tests, the imported tests will return
the path of the root test file.

### `context.fullName`

<!-- YAML
added: v22.3.0
-->

The name of the test and each of its ancestors, separated by `>`.

### `context.name`

<!-- YAML
added:
  - v18.8.0
  - v16.18.0
-->

The name of the test.

### `context.plan(count)`

<!-- YAML
added:
  - v22.2.0
  - v20.15.0
changes:
  - version:
    - v23.4.0
    - v22.13.0
    pr-url: https://github.com/nodejs/node/pull/55895
    description: This function is no longer experimental.
-->

* `count` {number} The number of assertions and subtests that are expected to run.

This function is used to set the number of assertions and subtests that are expected to run
within the test. If the number of assertions and subtests that run does not match the
expected count, the test will fail.

> Note: To make sure assertions are tracked, `t.assert` must be used instead of `assert` directly.

```js
test('top level test', (t) => {
  t.plan(2);
  t.assert.ok('some relevant assertion here');
  t.test('subtest', () => {});
});
```

When working with asynchronous code, the `plan` function can be used to ensure that the
correct number of assertions are run:

```js
test('planning with streams', (t, done) => {
  function* generate() {
    yield 'a';
    yield 'b';
    yield 'c';
  }
  const expected = ['a', 'b', 'c'];
  t.plan(expected.length);
  const stream = Readable.from(generate());
  stream.on('data', (chunk) => {
    t.assert.strictEqual(chunk, expected.shift());
  });

  stream.on('end', () => {
    done();
  });
});
```

### `context.runOnly(shouldRunOnlyTests)`

<!-- YAML
added:
  - v18.0.0
  - v16.17.0
-->

* `shouldRunOnlyTests` {boolean} Whether or not to run `only` tests.

If `shouldRunOnlyTests` is truthy, the test context will only run tests that
have the `only` option set. Otherwise, all tests are run. If Node.js was not
started with the [`--test-only`][] command-line option, this function is a
no-op.

```js
test('top level test', (t) => {
  // The test context can be set to run subtests with the 'only' option.
  t.runOnly(true);
  t.test('this subtest is now skipped');
  t.test('this subtest is run', { only: true });
});
```

### `context.signal`

<!-- YAML
added:
  - v18.7.0
  - v16.17.0
-->

* Type: {AbortSignal}

Can be used to abort test subtasks when the test has been aborted.

```js
test('top level test', async (t) => {
  await fetch('some/uri', { signal: t.signal });
});
```

### `context.skip([message])`

<!-- YAML
added:
  - v18.0.0
  - v16.17.0
-->

* `message` {string} Optional skip message.

This function causes the test's output to indicate the test as skipped. If
`message` is provided, it is included in the output. Calling `skip()` does
not terminate execution of the test function. This function does not return a
value.

```js
test('top level test', (t) => {
  // Make sure to return here as well if the test contains additional logic.
  t.skip('this is skipped');
});
```

### `context.todo([message])`

<!-- YAML
added:
  - v18.0.0
  - v16.17.0
-->

* `message` {string} Optional `TODO` message.

This function adds a `TODO` directive to the test's output. If `message` is
provided, it is included in the output. Calling `todo()` does not terminate
execution of the test function. This function does not return a value.

```js
test('top level test', (t) => {
  // This test is marked as `TODO`
  t.todo('this is a todo');
});
```

### `context.test([name][, options][, fn])`

<!-- YAML
added:
  - v18.0.0
  - v16.17.0
changes:
  - version:
    - REPLACEME
    pr-url: https://github.com/nodejs/node/pull/56664
    description: This function no longer returns a `Promise`.
  - version:
    - v18.8.0
    - v16.18.0
    pr-url: https://github.com/nodejs/node/pull/43554
    description: Add a `signal` option.
  - version:
    - v18.7.0
    - v16.17.0
    pr-url: https://github.com/nodejs/node/pull/43505
    description: Add a `timeout` option.
-->

* `name` {string} The name of the subtest, which is displayed when reporting
  test results. **Default:** The `name` property of `fn`, or `'<anonymous>'` if
  `fn` does not have a name.
* `options` {Object} Configuration options for the subtest. The following
  properties are supported:
  * `concurrency` {number|boolean|null} If a number is provided,
    then that many tests would run in parallel within the application thread.
    If `true`, it would run all subtests in parallel.
    If `false`, it would only run one test at a time.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `null`.
  * `only` {boolean} If truthy, and the test context is configured to run
    `only` tests, then this test will be run. Otherwise, the test is skipped.
    **Default:** `false`.
  * `signal` {AbortSignal} Allows aborting an in-progress test.
  * `skip` {boolean|string} If truthy, the test is skipped. If a string is
    provided, that string is displayed in the test results as the reason for
    skipping the test. **Default:** `false`.
  * `todo` {boolean|string} If truthy, the test marked as `TODO`. If a string
    is provided, that string is displayed in the test results as the reason why
    the test is `TODO`. **Default:** `false`.
  * `timeout` {number} A number of milliseconds the test will fail after.
    If unspecified, subtests inherit this value from their parent.
    **Default:** `Infinity`.
  * `plan` {number} The number of assertions and subtests expected to be run in the test.
    If the number of assertions run in the test does not match the number
    specified in the plan, the test will fail.
    **Default:** `undefined`.
* `fn` {Function|AsyncFunction} The function under test. The first argument
  to this function is a [`TestContext`][] object. If the test uses callbacks,
  the callback function is passed as the second argument. **Default:** A no-op
  function.

This function is used to create subtests under the current test. This function
behaves in the same fashion as the top level [`test()`][] function.

```js
test('top level test', async (t) => {
  t.test(
    'This is a subtest',
    { only: false, skip: false, concurrency: 1, todo: false, plan: 1 },
    (t) => {
      t.assert.ok('some relevant assertion here');
    },
  );
});
```

### `context.waitFor(condition[, options])`

<!-- YAML
added: v23.7.0
-->

* `condition` {Function|AsyncFunction} An assertion function that is invoked
  periodically until it completes successfully or the defined polling timeout
  elapses. Successful completion is defined as not throwing or rejecting. This
  function does not accept any arguments, and is allowed to return any value.
* `options` {Object} An optional configuration object for the polling operation.
  The following properties are supported:
  * `interval` {number} The number of milliseconds to wait after an unsuccessful
    invocation of `condition` before trying again. **Default:** `50`.
  * `timeout` {number} The poll timeout in milliseconds. If `condition` has not
    succeeded by the time this elapses, an error occurs. **Default:** `1000`.
* Returns: {Promise} Fulfilled with the value returned by `condition`.

This method polls a `condition` function until that function either returns
successfully or the operation times out.

## Class: `SuiteContext`

<!-- YAML
added:
  - v18.7.0
  - v16.17.0
-->

An instance of `SuiteContext` is passed to each suite function in order to
interact with the test runner. However, the `SuiteContext` constructor is not
exposed as part of the API.

### `context.filePath`

<!-- YAML
added: v22.6.0
-->

The absolute path of the test file that created the current suite. If a test
file imports additional modules that generate suites, the imported suites will
return the path of the root test file.

### `context.name`

<!-- YAML
added:
  - v18.8.0
  - v16.18.0
-->

The name of the suite.

### `context.signal`

<!-- YAML
added:
  - v18.7.0
  - v16.17.0
-->

* Type: {AbortSignal}

Can be used to abort test subtasks when the test has been aborted.

[TAP]: https://testanything.org/
[`--experimental-test-coverage`]: cli.md#--experimental-test-coverage
[`--experimental-test-module-mocks`]: cli.md#--experimental-test-module-mocks
[`--import`]: cli.md#--importmodule
[`--no-experimental-strip-types`]: cli.md#--no-experimental-strip-types
[`--test-concurrency`]: cli.md#--test-concurrency
[`--test-coverage-exclude`]: cli.md#--test-coverage-exclude
[`--test-coverage-include`]: cli.md#--test-coverage-include
[`--test-name-pattern`]: cli.md#--test-name-pattern
[`--test-only`]: cli.md#--test-only
[`--test-reporter-destination`]: cli.md#--test-reporter-destination
[`--test-reporter`]: cli.md#--test-reporter
[`--test-skip-pattern`]: cli.md#--test-skip-pattern
[`--test-update-snapshots`]: cli.md#--test-update-snapshots
[`--test`]: cli.md#--test
[`MockFunctionContext`]: #class-mockfunctioncontext
[`MockTimers`]: #class-mocktimers
[`MockTracker.method`]: #mockmethodobject-methodname-implementation-options
[`MockTracker`]: #class-mocktracker
[`NODE_V8_COVERAGE`]: cli.md#node_v8_coveragedir
[`SuiteContext`]: #class-suitecontext
[`TestContext`]: #class-testcontext
[`context.diagnostic`]: #contextdiagnosticmessage
[`context.skip`]: #contextskipmessage
[`context.todo`]: #contexttodomessage
[`describe()`]: #describename-options-fn
[`glob(7)`]: https://man7.org/linux/man-pages/man7/glob.7.html
[`it()`]: #itname-options-fn
[`run()`]: #runoptions
[`suite()`]: #suitename-options-fn
[`test()`]: #testname-options-fn
[code coverage]: #collecting-code-coverage
[describe options]: #describename-options-fn
[it options]: #testname-options-fn
[stream.compose]: stream.md#streamcomposestreams
[subtests]: #subtests
[suite options]: #suitename-options-fn
[test reporters]: #test-reporters
[test runner execution model]: #test-runner-execution-model

# Util

<!--introduced_in=v0.10.0-->

> Stability: 2 - Stable

<!-- source_link=lib/util.js -->

The `node:util` module supports the needs of Node.js internal APIs. Many of the
utilities are useful for application and module developers as well. To access
it:

```js
const util = require('node:util');
```

## `util.callbackify(original)`

<!-- YAML
added: v8.2.0
-->

* `original` {Function} An `async` function
* Returns: {Function} a callback style function

Takes an `async` function (or a function that returns a `Promise`) and returns a
function following the error-first callback style, i.e. taking
an `(err, value) => ...` callback as the last argument. In the callback, the
first argument will be the rejection reason (or `null` if the `Promise`
resolved), and the second argument will be the resolved value.

```js
const util = require('node:util');

async function fn() {
  return 'hello world';
}
const callbackFunction = util.callbackify(fn);

callbackFunction((err, ret) => {
  if (err) throw err;
  console.log(ret);
});
```

Will print:

```text
hello world
```

The callback is executed asynchronously, and will have a limited stack trace.
If the callback throws, the process will emit an [`'uncaughtException'`][]
event, and if not handled will exit.

Since `null` has a special meaning as the first argument to a callback, if a
wrapped function rejects a `Promise` with a falsy value as a reason, the value
is wrapped in an `Error` with the original value stored in a field named
`reason`.

```js
function fn() {
  return Promise.reject(null);
}
const callbackFunction = util.callbackify(fn);

callbackFunction((err, ret) => {
  // When the Promise was rejected with `null` it is wrapped with an Error and
  // the original value is stored in `reason`.
  err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
});
```

## `util.debuglog(section[, callback])`

<!-- YAML
added: v0.11.3
-->

* `section` {string} A string identifying the portion of the application for
  which the `debuglog` function is being created.
* `callback` {Function} A callback invoked the first time the logging function
  is called with a function argument that is a more optimized logging function.
* Returns: {Function} The logging function

The `util.debuglog()` method is used to create a function that conditionally
writes debug messages to `stderr` based on the existence of the `NODE_DEBUG`
environment variable. If the `section` name appears within the value of that
environment variable, then the returned function operates similar to
[`console.error()`][]. If not, then the returned function is a no-op.

```js
const util = require('node:util');
const debuglog = util.debuglog('foo');

debuglog('hello from foo [%d]', 123);
```

If this program is run with `NODE_DEBUG=foo` in the environment, then
it will output something like:

```console
FOO 3245: hello from foo [123]
```

where `3245` is the process id. If it is not run with that
environment variable set, then it will not print anything.

The `section` supports wildcard also:

```js
const util = require('node:util');
const debuglog = util.debuglog('foo-bar');

debuglog('hi there, it\'s foo-bar [%d]', 2333);
```

if it is run with `NODE_DEBUG=foo*` in the environment, then it will output
something like:

```console
FOO-BAR 3257: hi there, it's foo-bar [2333]
```

Multiple comma-separated `section` names may be specified in the `NODE_DEBUG`
environment variable: `NODE_DEBUG=fs,net,tls`.

The optional `callback` argument can be used to replace the logging function
with a different function that doesn't have any initialization or
unnecessary wrapping.

```js
const util = require('node:util');
let debuglog = util.debuglog('internals', (debug) => {
  // Replace with a logging function that optimizes out
  // testing if the section is enabled
  debuglog = debug;
});
```

### `debuglog().enabled`

<!-- YAML
added: v14.9.0
-->

* {boolean}

The `util.debuglog().enabled` getter is used to create a test that can be used
in conditionals based on the existence of the `NODE_DEBUG` environment variable.
If the `section` name appears within the value of that environment variable,
then the returned value will be `true`. If not, then the returned value will be
`false`.

```js
const util = require('node:util');
const enabled = util.debuglog('foo').enabled;
if (enabled) {
  console.log('hello from foo [%d]', 123);
}
```

If this program is run with `NODE_DEBUG=foo` in the environment, then it will
output something like:

```console
hello from foo [123]
```

## `util.debug(section)`

<!-- YAML
added: v14.9.0
-->

Alias for `util.debuglog`. Usage allows for readability of that doesn't imply
logging when only using `util.debuglog().enabled`.

## `util.deprecate(fn, msg[, code])`

<!-- YAML
added: v0.8.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/16393
    description: Deprecation warnings are only emitted once for each code.
-->

* `fn` {Function} The function that is being deprecated.
* `msg` {string} A warning message to display when the deprecated function is
  invoked.
* `code` {string} A deprecation code. See the [list of deprecated APIs][] for a
  list of codes.
* Returns: {Function} The deprecated function wrapped to emit a warning.

The `util.deprecate()` method wraps `fn` (which may be a function or class) in
such a way that it is marked as deprecated.

```js
const util = require('node:util');

exports.obsoleteFunction = util.deprecate(() => {
  // Do something here.
}, 'obsoleteFunction() is deprecated. Use newShinyFunction() instead.');
```

When called, `util.deprecate()` will return a function that will emit a
`DeprecationWarning` using the [`'warning'`][] event. The warning will
be emitted and printed to `stderr` the first time the returned function is
called. After the warning is emitted, the wrapped function is called without
emitting a warning.

If the same optional `code` is supplied in multiple calls to `util.deprecate()`,
the warning will be emitted only once for that `code`.

```js
const util = require('node:util');

const fn1 = util.deprecate(someFunction, someMessage, 'DEP0001');
const fn2 = util.deprecate(someOtherFunction, someOtherMessage, 'DEP0001');
fn1(); // Emits a deprecation warning with code DEP0001
fn2(); // Does not emit a deprecation warning because it has the same code
```

If either the `--no-deprecation` or `--no-warnings` command-line flags are
used, or if the `process.noDeprecation` property is set to `true` _prior_ to
the first deprecation warning, the `util.deprecate()` method does nothing.

If the `--trace-deprecation` or `--trace-warnings` command-line flags are set,
or the `process.traceDeprecation` property is set to `true`, a warning and a
stack trace are printed to `stderr` the first time the deprecated function is
called.

If the `--throw-deprecation` command-line flag is set, or the
`process.throwDeprecation` property is set to `true`, then an exception will be
thrown when the deprecated function is called.

The `--throw-deprecation` command-line flag and `process.throwDeprecation`
property take precedence over `--trace-deprecation` and
`process.traceDeprecation`.

## `util.format(format[, ...args])`

<!-- YAML
added: v0.5.3
changes:
  - version: v12.11.0
    pr-url: https://github.com/nodejs/node/pull/29606
    description: The `%c` specifier is ignored now.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/23162
    description: The `format` argument is now only taken as such if it actually
                 contains format specifiers.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/23162
    description: If the `format` argument is not a format string, the output
                 string's formatting is no longer dependent on the type of the
                 first argument. This change removes previously present quotes
                 from strings that were being output when the first argument
                 was not a string.
  - version: v11.4.0
    pr-url: https://github.com/nodejs/node/pull/23708
    description: The `%d`, `%f`, and `%i` specifiers now support Symbols
                 properly.
  - version: v11.4.0
    pr-url: https://github.com/nodejs/node/pull/24806
    description: The `%o` specifier's `depth` has default depth of 4 again.
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/17907
    description: The `%o` specifier's `depth` option will now fall back to the
                 default depth.
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/22097
    description: The `%d` and `%i` specifiers now support BigInt.
  - version: v8.4.0
    pr-url: https://github.com/nodejs/node/pull/14558
    description: The `%o` and `%O` specifiers are supported now.
-->

* `format` {string} A `printf`-like format string.

The `util.format()` method returns a formatted string using the first argument
as a `printf`-like format string which can contain zero or more format
specifiers. Each specifier is replaced with the converted value from the
corresponding argument. Supported specifiers are:

* `%s`: `String` will be used to convert all values except `BigInt`, `Object`
  and `-0`. `BigInt` values will be represented with an `n` and Objects that
  have no user defined `toString` function are inspected using `util.inspect()`
  with options `{ depth: 0, colors: false, compact: 3 }`.
* `%d`: `Number` will be used to convert all values except `BigInt` and
  `Symbol`.
* `%i`: `parseInt(value, 10)` is used for all values except `BigInt` and
  `Symbol`.
* `%f`: `parseFloat(value)` is used for all values expect `Symbol`.
* `%j`: JSON. Replaced with the string `'[Circular]'` if the argument contains
  circular references.
* `%o`: `Object`. A string representation of an object with generic JavaScript
  object formatting. Similar to `util.inspect()` with options
  `{ showHidden: true, showProxy: true }`. This will show the full object
  including non-enumerable properties and proxies.
* `%O`: `Object`. A string representation of an object with generic JavaScript
  object formatting. Similar to `util.inspect()` without options. This will show
  the full object not including non-enumerable properties and proxies.
* `%c`: `CSS`. This specifier is ignored and will skip any CSS passed in.
* `%%`: single percent sign (`'%'`). This does not consume an argument.
* Returns: {string} The formatted string

If a specifier does not have a corresponding argument, it is not replaced:

```js
util.format('%s:%s', 'foo');
// Returns: 'foo:%s'
```

Values that are not part of the format string are formatted using
`util.inspect()` if their type is not `string`.

If there are more arguments passed to the `util.format()` method than the
number of specifiers, the extra arguments are concatenated to the returned
string, separated by spaces:

```js
util.format('%s:%s', 'foo', 'bar', 'baz');
// Returns: 'foo:bar baz'
```

If the first argument does not contain a valid format specifier, `util.format()`
returns a string that is the concatenation of all arguments separated by spaces:

```js
util.format(1, 2, 3);
// Returns: '1 2 3'
```

If only one argument is passed to `util.format()`, it is returned as it is
without any formatting:

```js
util.format('%% %s');
// Returns: '%% %s'
```

`util.format()` is a synchronous method that is intended as a debugging tool.
Some input values can have a significant performance overhead that can block the
event loop. Use this function with care and never in a hot code path.

## `util.formatWithOptions(inspectOptions, format[, ...args])`

<!-- YAML
added: v10.0.0
-->

* `inspectOptions` {Object}
* `format` {string}

This function is identical to [`util.format()`][], except in that it takes
an `inspectOptions` argument which specifies options that are passed along to
[`util.inspect()`][].

```js
util.formatWithOptions({ colors: true }, 'See object %O', { foo: 42 });
// Returns 'See object { foo: 42 }', where `42` is colored as a number
// when printed to a terminal.
```

## `util.getCallSites(frameCountOrOptions, [options])`

> Stability: 1.1 - Active development

<!-- YAML
added: v22.9.0
changes:
  - version: v23.7.0
    pr-url: https://github.com/nodejs/node/pull/56584
    description: Property `column` is deprecated in favor of `columnNumber`.
  - version: v23.7.0
    pr-url: https://github.com/nodejs/node/pull/56551
    description: Property `CallSite.scriptId` is exposed.
  - version:
    - v23.3.0
    - v22.12.0
    pr-url: https://github.com/nodejs/node/pull/55626
    description: The API is renamed from `util.getCallSite` to `util.getCallSites()`.
-->

* `frameCount` {number} Optional number of frames to capture as call site objects.
  **Default:** `10`. Allowable range is between 1 and 200.
* `options` {Object} Optional
  * `sourceMap` {boolean} Reconstruct the original location in the stacktrace from the source-map.
    Enabled by default with the flag `--enable-source-maps`.
* Returns: {Object\[]} An array of call site objects
  * `functionName` {string} Returns the name of the function associated with this call site.
  * `scriptName` {string} Returns the name of the resource that contains the script for the
    function for this call site.
  * `scriptId` {string} Returns the unique id of the script, as in Chrome DevTools protocol [`Runtime.ScriptId`][].
  * `lineNumber` {number} Returns the JavaScript script line number (1-based).
  * `columnNumber` {number} Returns the JavaScript script column number (1-based).

Returns an array of call site objects containing the stack of
the caller function.

```js
const util = require('node:util');

function exampleFunction() {
  const callSites = util.getCallSites();

  console.log('Call Sites:');
  callSites.forEach((callSite, index) => {
    console.log(`CallSite ${index + 1}:`);
    console.log(`Function Name: ${callSite.functionName}`);
    console.log(`Script Name: ${callSite.scriptName}`);
    console.log(`Line Number: ${callSite.lineNumber}`);
    console.log(`Column Number: ${callSite.columnNumber}`);
  });
  // CallSite 1:
  // Function Name: exampleFunction
  // Script Name: /home/example.js
  // Line Number: 5
  // Column Number: 26

  // CallSite 2:
  // Function Name: anotherFunction
  // Script Name: /home/example.js
  // Line Number: 22
  // Column Number: 3

  // ...
}

// A function to simulate another stack layer
function anotherFunction() {
  exampleFunction();
}

anotherFunction();
```

It is possible to reconstruct the original locations by setting the option `sourceMap` to `true`.
If the source map is not available, the original location will be the same as the current location.
When the `--enable-source-maps` flag is enabled, for example when using `--experimental-transform-types`,
`sourceMap` will be true by default.

```ts
import util from 'node:util';

interface Foo {
  foo: string;
}

const callSites = util.getCallSites({ sourceMap: true });

// With sourceMap:
// Function Name: ''
// Script Name: example.js
// Line Number: 7
// Column Number: 26

// Without sourceMap:
// Function Name: ''
// Script Name: example.js
// Line Number: 2
// Column Number: 26
```

## `util.getSystemErrorName(err)`

<!-- YAML
added: v9.7.0
-->

* `err` {number}
* Returns: {string}

Returns the string name for a numeric error code that comes from a Node.js API.
The mapping between error codes and error names is platform-dependent.
See [Common System Errors][] for the names of common errors.

```js
fs.access('file/that/does/not/exist', (err) => {
  const name = util.getSystemErrorName(err.errno);
  console.error(name);  // ENOENT
});
```

## `util.getSystemErrorMap()`

<!-- YAML
added:
  - v16.0.0
  - v14.17.0
-->

* Returns: {Map}

Returns a Map of all system error codes available from the Node.js API.
The mapping between error codes and error names is platform-dependent.
See [Common System Errors][] for the names of common errors.

```js
fs.access('file/that/does/not/exist', (err) => {
  const errorMap = util.getSystemErrorMap();
  const name = errorMap.get(err.errno);
  console.error(name);  // ENOENT
});
```

## `util.getSystemErrorMessage(err)`

<!-- YAML
added:
  - v23.1.0
  - v22.12.0
-->

* `err` {number}
* Returns: {string}

Returns the string message for a numeric error code that comes from a Node.js
API.
The mapping between error codes and string messages is platform-dependent.

```js
fs.access('file/that/does/not/exist', (err) => {
  const name = util.getSystemErrorMessage(err.errno);
  console.error(name);  // No such file or directory
});
```

## `util.inherits(constructor, superConstructor)`

<!-- YAML
added: v0.3.0
changes:
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3455
    description: The `constructor` parameter can refer to an ES6 class now.
-->

> Stability: 3 - Legacy: Use ES2015 class syntax and `extends` keyword instead.

* `constructor` {Function}
* `superConstructor` {Function}

Usage of `util.inherits()` is discouraged. Please use the ES6 `class` and
`extends` keywords to get language level inheritance support. Also note
that the two styles are [semantically incompatible][].

Inherit the prototype methods from one [constructor][] into another. The
prototype of `constructor` will be set to a new object created from
`superConstructor`.

This mainly adds some input validation on top of
`Object.setPrototypeOf(constructor.prototype, superConstructor.prototype)`.
As an additional convenience, `superConstructor` will be accessible
through the `constructor.super_` property.

```js
const util = require('node:util');
const EventEmitter = require('node:events');

function MyStream() {
  EventEmitter.call(this);
}

util.inherits(MyStream, EventEmitter);

MyStream.prototype.write = function(data) {
  this.emit('data', data);
};

const stream = new MyStream();

console.log(stream instanceof EventEmitter); // true
console.log(MyStream.super_ === EventEmitter); // true

stream.on('data', (data) => {
  console.log(`Received data: "${data}"`);
});
stream.write('It works!'); // Received data: "It works!"
```

ES6 example using `class` and `extends`:

```js
const EventEmitter = require('node:events');

class MyStream extends EventEmitter {
  write(data) {
    this.emit('data', data);
  }
}

const stream = new MyStream();

stream.on('data', (data) => {
  console.log(`Received data: "${data}"`);
});
stream.write('With ES6');
```

## `util.inspect(object[, options])`

## `util.inspect(object[, showHidden[, depth[, colors]]])`

<!-- YAML
added: v0.3.0
changes:
  - version:
    - v17.3.0
    - v16.14.0
    pr-url: https://github.com/nodejs/node/pull/41003
    description: The `numericSeparator` option is supported now.
  - version: v16.18.0
    pr-url: https://github.com/nodejs/node/pull/43576
    description: add support for `maxArrayLength` when inspecting `Set` and `Map`.
  - version:
    - v14.6.0
    - v12.19.0
    pr-url: https://github.com/nodejs/node/pull/33690
    description: If `object` is from a different `vm.Context` now, a custom
                 inspection function on it will not receive context-specific
                 arguments anymore.
  - version:
     - v13.13.0
     - v12.17.0
    pr-url: https://github.com/nodejs/node/pull/32392
    description: The `maxStringLength` option is supported now.
  - version:
     - v13.5.0
     - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/30768
    description: User defined prototype properties are inspected in case
                 `showHidden` is `true`.
  - version: v13.0.0
    pr-url: https://github.com/nodejs/node/pull/27685
    description: Circular references now include a marker to the reference.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/27109
    description: The `compact` options default is changed to `3` and the
                 `breakLength` options default is changed to `80`.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/24971
    description: Internal properties no longer appear in the context argument
                 of a custom inspection function.
  - version: v11.11.0
    pr-url: https://github.com/nodejs/node/pull/26269
    description: The `compact` option accepts numbers for a new output mode.
  - version: v11.7.0
    pr-url: https://github.com/nodejs/node/pull/25006
    description: ArrayBuffers now also show their binary contents.
  - version: v11.5.0
    pr-url: https://github.com/nodejs/node/pull/24852
    description: The `getters` option is supported now.
  - version: v11.4.0
    pr-url: https://github.com/nodejs/node/pull/24326
    description: The `depth` default changed back to `2`.
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22846
    description: The `depth` default changed to `20`.
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22756
    description: The inspection output is now limited to about 128 MiB. Data
                 above that size will not be fully inspected.
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/22788
    description: The `sorted` option is supported now.
  - version: v10.6.0
    pr-url: https://github.com/nodejs/node/pull/20725
    description: Inspecting linked lists and similar objects is now possible
                 up to the maximum call stack size.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19259
    description: The `WeakMap` and `WeakSet` entries can now be inspected
                 as well.
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17576
    description: The `compact` option is supported now.
  - version: v6.6.0
    pr-url: https://github.com/nodejs/node/pull/8174
    description: Custom inspection functions can now return `this`.
  - version: v6.3.0
    pr-url: https://github.com/nodejs/node/pull/7499
    description: The `breakLength` option is supported now.
  - version: v6.1.0
    pr-url: https://github.com/nodejs/node/pull/6334
    description: The `maxArrayLength` option is supported now; in particular,
                 long arrays are truncated by default.
  - version: v6.1.0
    pr-url: https://github.com/nodejs/node/pull/6465
    description: The `showProxy` option is supported now.
-->

* `object` {any} Any JavaScript primitive or `Object`.
* `options` {Object}
  * `showHidden` {boolean} If `true`, `object`'s non-enumerable symbols and
    properties are included in the formatted result. [`WeakMap`][] and
    [`WeakSet`][] entries are also included as well as user defined prototype
    properties (excluding method properties). **Default:** `false`.
  * `depth` {number} Specifies the number of times to recurse while formatting
    `object`. This is useful for inspecting large objects. To recurse up to
    the maximum call stack size pass `Infinity` or `null`.
    **Default:** `2`.
  * `colors` {boolean} If `true`, the output is styled with ANSI color
    codes. Colors are customizable. See [Customizing `util.inspect` colors][].
    **Default:** `false`.
  * `customInspect` {boolean} If `false`,
    `[util.inspect.custom](depth, opts, inspect)` functions are not invoked.
    **Default:** `true`.
  * `showProxy` {boolean} If `true`, `Proxy` inspection includes
    the [`target` and `handler`][] objects. **Default:** `false`.
  * `maxArrayLength` {integer} Specifies the maximum number of `Array`,
    [`TypedArray`][], [`Map`][], [`Set`][], [`WeakMap`][],
    and [`WeakSet`][] elements to include when formatting.
    Set to `null` or `Infinity` to show all elements. Set to `0` or
    negative to show no elements. **Default:** `100`.
  * `maxStringLength` {integer} Specifies the maximum number of characters to
    include when formatting. Set to `null` or `Infinity` to show all elements.
    Set to `0` or negative to show no characters. **Default:** `10000`.
  * `breakLength` {integer} The length at which input values are split across
    multiple lines. Set to `Infinity` to format the input as a single line
    (in combination with `compact` set to `true` or any number >= `1`).
    **Default:** `80`.
  * `compact` {boolean|integer} Setting this to `false` causes each object key
    to be displayed on a new line. It will break on new lines in text that is
    longer than `breakLength`. If set to a number, the most `n` inner elements
    are united on a single line as long as all properties fit into
    `breakLength`. Short array elements are also grouped together. For more
    information, see the example below. **Default:** `3`.
  * `sorted` {boolean|Function} If set to `true` or a function, all properties
    of an object, and `Set` and `Map` entries are sorted in the resulting
    string. If set to `true` the [default sort][] is used. If set to a function,
    it is used as a [compare function][].
  * `getters` {boolean|string} If set to `true`, getters are inspected. If set
    to `'get'`, only getters without a corresponding setter are inspected. If
    set to `'set'`, only getters with a corresponding setter are inspected.
    This might cause side effects depending on the getter function.
    **Default:** `false`.
  * `numericSeparator` {boolean} If set to `true`, an underscore is used to
    separate every three digits in all bigints and numbers.
    **Default:** `false`.
* Returns: {string} The representation of `object`.

The `util.inspect()` method returns a string representation of `object` that is
intended for debugging. The output of `util.inspect` may change at any time
and should not be depended upon programmatically. Additional `options` may be
passed that alter the result.
`util.inspect()` will use the constructor's name and/or `@@toStringTag` to make
an identifiable tag for an inspected value.

```js
class Foo {
  get [Symbol.toStringTag]() {
    return 'bar';
  }
}

class Bar {}

const baz = Object.create(null, { [Symbol.toStringTag]: { value: 'foo' } });

util.inspect(new Foo()); // 'Foo [bar] {}'
util.inspect(new Bar()); // 'Bar {}'
util.inspect(baz);       // '[foo] {}'
```

Circular references point to their anchor by using a reference index:

```js
const { inspect } = require('node:util');

const obj = {};
obj.a = [obj];
obj.b = {};
obj.b.inner = obj.b;
obj.b.obj = obj;

console.log(inspect(obj));
// <ref *1> {
//   a: [ [Circular *1] ],
//   b: <ref *2> { inner: [Circular *2], obj: [Circular *1] }
// }
```

The following example inspects all properties of the `util` object:

```js
const util = require('node:util');

console.log(util.inspect(util, { showHidden: true, depth: null }));
```

The following example highlights the effect of the `compact` option:

```js
const util = require('node:util');

const o = {
  a: [1, 2, [[
    'Lorem ipsum dolor sit amet,\nconsectetur adipiscing elit, sed do ' +
      'eiusmod \ntempor incididunt ut labore et dolore magna aliqua.',
    'test',
    'foo']], 4],
  b: new Map([['za', 1], ['zb', 'test']]),
};
console.log(util.inspect(o, { compact: true, depth: 5, breakLength: 80 }));

// { a:
//   [ 1,
//     2,
//     [ [ 'Lorem ipsum dolor sit amet,\nconsectetur [...]', // A long line
//           'test',
//           'foo' ] ],
//     4 ],
//   b: Map(2) { 'za' => 1, 'zb' => 'test' } }

// Setting `compact` to false or an integer creates more reader friendly output.
console.log(util.inspect(o, { compact: false, depth: 5, breakLength: 80 }));

// {
//   a: [
//     1,
//     2,
//     [
//       [
//         'Lorem ipsum dolor sit amet,\n' +
//           'consectetur adipiscing elit, sed do eiusmod \n' +
//           'tempor incididunt ut labore et dolore magna aliqua.',
//         'test',
//         'foo'
//       ]
//     ],
//     4
//   ],
//   b: Map(2) {
//     'za' => 1,
//     'zb' => 'test'
//   }
// }

// Setting `breakLength` to e.g. 150 will print the "Lorem ipsum" text in a
// single line.
```

The `showHidden` option allows [`WeakMap`][] and [`WeakSet`][] entries to be
inspected. If there are more entries than `maxArrayLength`, there is no
guarantee which entries are displayed. That means retrieving the same
[`WeakSet`][] entries twice may result in different output. Furthermore, entries
with no remaining strong references may be garbage collected at any time.

```js
const { inspect } = require('node:util');

const obj = { a: 1 };
const obj2 = { b: 2 };
const weakSet = new WeakSet([obj, obj2]);

console.log(inspect(weakSet, { showHidden: true }));
// WeakSet { { a: 1 }, { b: 2 } }
```

The `sorted` option ensures that an object's property insertion order does not
impact the result of `util.inspect()`.

```js
const { inspect } = require('node:util');
const assert = require('node:assert');

const o1 = {
  b: [2, 3, 1],
  a: '`a` comes before `b`',
  c: new Set([2, 3, 1]),
};
console.log(inspect(o1, { sorted: true }));
// { a: '`a` comes before `b`', b: [ 2, 3, 1 ], c: Set(3) { 1, 2, 3 } }
console.log(inspect(o1, { sorted: (a, b) => b.localeCompare(a) }));
// { c: Set(3) { 3, 2, 1 }, b: [ 2, 3, 1 ], a: '`a` comes before `b`' }

const o2 = {
  c: new Set([2, 1, 3]),
  a: '`a` comes before `b`',
  b: [2, 3, 1],
};
assert.strict.equal(
  inspect(o1, { sorted: true }),
  inspect(o2, { sorted: true }),
);
```

The `numericSeparator` option adds an underscore every three digits to all
numbers.

```js
const { inspect } = require('node:util');

const thousand = 1_000;
const million = 1_000_000;
const bigNumber = 123_456_789n;
const bigDecimal = 1_234.123_45;

console.log(inspect(thousand, { numericSeparator: true }));
// 1_000
console.log(inspect(million, { numericSeparator: true }));
// 1_000_000
console.log(inspect(bigNumber, { numericSeparator: true }));
// 123_456_789n
console.log(inspect(bigDecimal, { numericSeparator: true }));
// 1_234.123_45
```

`util.inspect()` is a synchronous method intended for debugging. Its maximum
output length is approximately 128 MiB. Inputs that result in longer output will
be truncated.

### Customizing `util.inspect` colors

<!-- type=misc -->

Color output (if enabled) of `util.inspect` is customizable globally
via the `util.inspect.styles` and `util.inspect.colors` properties.

`util.inspect.styles` is a map associating a style name to a color from
`util.inspect.colors`.

The default styles and associated colors are:

* `bigint`: `yellow`
* `boolean`: `yellow`
* `date`: `magenta`
* `module`: `underline`
* `name`: (no styling)
* `null`: `bold`
* `number`: `yellow`
* `regexp`: `red`
* `special`: `cyan` (e.g., `Proxies`)
* `string`: `green`
* `symbol`: `green`
* `undefined`: `grey`

Color styling uses ANSI control codes that may not be supported on all
terminals. To verify color support use [`tty.hasColors()`][].

Predefined control codes are listed below (grouped as "Modifiers", "Foreground
colors", and "Background colors").

#### Modifiers

Modifier support varies throughout different terminals. They will mostly be
ignored, if not supported.

* `reset` - Resets all (color) modifiers to their defaults
* **bold** - Make text bold
* _italic_ - Make text italic
* <span style="border-bottom: 1px;">underline</span> - Make text underlined
* ~~strikethrough~~ - Puts a horizontal line through the center of the text
  (Alias: `strikeThrough`, `crossedout`, `crossedOut`)
* `hidden` - Prints the text, but makes it invisible (Alias: conceal)
* <span style="opacity: 0.5;">dim</span> - Decreased color intensity (Alias:
  `faint`)
* <span style="border-top: 1px">overlined</span> - Make text overlined
* blink - Hides and shows the text in an interval
* <span style="filter: invert(100%)">inverse</span> - Swap foreground and
  background colors (Alias: `swapcolors`, `swapColors`)
* <span style="border-bottom: 1px double;">doubleunderline</span> - Make text
  double underlined (Alias: `doubleUnderline`)
* <span style="border: 1px">framed</span> - Draw a frame around the text

#### Foreground colors

* `black`
* `red`
* `green`
* `yellow`
* `blue`
* `magenta`
* `cyan`
* `white`
* `gray` (alias: `grey`, `blackBright`)
* `redBright`
* `greenBright`
* `yellowBright`
* `blueBright`
* `magentaBright`
* `cyanBright`
* `whiteBright`

#### Background colors

* `bgBlack`
* `bgRed`
* `bgGreen`
* `bgYellow`
* `bgBlue`
* `bgMagenta`
* `bgCyan`
* `bgWhite`
* `bgGray` (alias: `bgGrey`, `bgBlackBright`)
* `bgRedBright`
* `bgGreenBright`
* `bgYellowBright`
* `bgBlueBright`
* `bgMagentaBright`
* `bgCyanBright`
* `bgWhiteBright`

### Custom inspection functions on objects

<!-- type=misc -->

<!-- YAML
added: v0.1.97
changes:
  - version:
      - v17.3.0
      - v16.14.0
    pr-url: https://github.com/nodejs/node/pull/41019
    description: The inspect argument is added for more interoperability.
-->

Objects may also define their own
[`[util.inspect.custom](depth, opts, inspect)`][util.inspect.custom] function,
which `util.inspect()` will invoke and use the result of when inspecting
the object.

```js
const util = require('node:util');

class Box {
  constructor(value) {
    this.value = value;
  }

  [util.inspect.custom](depth, options, inspect) {
    if (depth < 0) {
      return options.stylize('[Box]', 'special');
    }

    const newOptions = Object.assign({}, options, {
      depth: options.depth === null ? null : options.depth - 1,
    });

    // Five space padding because that's the size of "Box< ".
    const padding = ' '.repeat(5);
    const inner = inspect(this.value, newOptions)
                  .replace(/\n/g, `\n${padding}`);
    return `${options.stylize('Box', 'special')}< ${inner} >`;
  }
}

const box = new Box(true);

util.inspect(box);
// Returns: "Box< true >"
```

Custom `[util.inspect.custom](depth, opts, inspect)` functions typically return
a string but may return a value of any type that will be formatted accordingly
by `util.inspect()`.

```js
const util = require('node:util');

const obj = { foo: 'this will not show up in the inspect() output' };
obj[util.inspect.custom] = (depth) => {
  return { bar: 'baz' };
};

util.inspect(obj);
// Returns: "{ bar: 'baz' }"
```

### `util.inspect.custom`

<!-- YAML
added: v6.6.0
changes:
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/20857
    description: This is now defined as a shared symbol.
-->

* {symbol} that can be used to declare custom inspect functions.

In addition to being accessible through `util.inspect.custom`, this
symbol is [registered globally][global symbol registry] and can be
accessed in any environment as `Symbol.for('nodejs.util.inspect.custom')`.

Using this allows code to be written in a portable fashion, so that the custom
inspect function is used in an Node.js environment and ignored in the browser.
The `util.inspect()` function itself is passed as third argument to the custom
inspect function to allow further portability.

```js
const customInspectSymbol = Symbol.for('nodejs.util.inspect.custom');

class Password {
  constructor(value) {
    this.value = value;
  }

  toString() {
    return 'xxxxxxxx';
  }

  [customInspectSymbol](depth, inspectOptions, inspect) {
    return `Password <${this.toString()}>`;
  }
}

const password = new Password('r0sebud');
console.log(password);
// Prints Password <xxxxxxxx>
```

See [Custom inspection functions on Objects][] for more details.

### `util.inspect.defaultOptions`

<!-- YAML
added: v6.4.0
-->

The `defaultOptions` value allows customization of the default options used by
`util.inspect`. This is useful for functions like `console.log` or
`util.format` which implicitly call into `util.inspect`. It shall be set to an
object containing one or more valid [`util.inspect()`][] options. Setting
option properties directly is also supported.

```js
const util = require('node:util');
const arr = Array(101).fill(0);

console.log(arr); // Logs the truncated array
util.inspect.defaultOptions.maxArrayLength = null;
console.log(arr); // logs the full array
```

## `util.isDeepStrictEqual(val1, val2)`

<!-- YAML
added: v9.0.0
-->

* `val1` {any}
* `val2` {any}
* Returns: {boolean}

Returns `true` if there is deep strict equality between `val1` and `val2`.
Otherwise, returns `false`.

See [`assert.deepStrictEqual()`][] for more information about deep strict
equality.

## Class: `util.MIMEType`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

> Stability: 1 - Experimental

An implementation of [the MIMEType class](https://bmeck.github.io/node-proposal-mime-api/).

In accordance with browser conventions, all properties of `MIMEType` objects
are implemented as getters and setters on the class prototype, rather than as
data properties on the object itself.

A MIME string is a structured string containing multiple meaningful
components. When parsed, a `MIMEType` object is returned containing
properties for each of these components.

### Constructor: `new MIMEType(input)`

* `input` {string} The input MIME to parse

Creates a new `MIMEType` object by parsing the `input`.

```mjs
import { MIMEType } from 'node:util';

const myMIME = new MIMEType('text/plain');
```

```cjs
const { MIMEType } = require('node:util');

const myMIME = new MIMEType('text/plain');
```

A `TypeError` will be thrown if the `input` is not a valid MIME. Note
that an effort will be made to coerce the given values into strings. For
instance:

```mjs
import { MIMEType } from 'node:util';
const myMIME = new MIMEType({ toString: () => 'text/plain' });
console.log(String(myMIME));
// Prints: text/plain
```

```cjs
const { MIMEType } = require('node:util');
const myMIME = new MIMEType({ toString: () => 'text/plain' });
console.log(String(myMIME));
// Prints: text/plain
```

### `mime.type`

* {string}

Gets and sets the type portion of the MIME.

```mjs
import { MIMEType } from 'node:util';

const myMIME = new MIMEType('text/javascript');
console.log(myMIME.type);
// Prints: text
myMIME.type = 'application';
console.log(myMIME.type);
// Prints: application
console.log(String(myMIME));
// Prints: application/javascript
```

```cjs
const { MIMEType } = require('node:util');

const myMIME = new MIMEType('text/javascript');
console.log(myMIME.type);
// Prints: text
myMIME.type = 'application';
console.log(myMIME.type);
// Prints: application
console.log(String(myMIME));
// Prints: application/javascript
```

### `mime.subtype`

* {string}

Gets and sets the subtype portion of the MIME.

```mjs
import { MIMEType } from 'node:util';

const myMIME = new MIMEType('text/ecmascript');
console.log(myMIME.subtype);
// Prints: ecmascript
myMIME.subtype = 'javascript';
console.log(myMIME.subtype);
// Prints: javascript
console.log(String(myMIME));
// Prints: text/javascript
```

```cjs
const { MIMEType } = require('node:util');

const myMIME = new MIMEType('text/ecmascript');
console.log(myMIME.subtype);
// Prints: ecmascript
myMIME.subtype = 'javascript';
console.log(myMIME.subtype);
// Prints: javascript
console.log(String(myMIME));
// Prints: text/javascript
```

### `mime.essence`

* {string}

Gets the essence of the MIME. This property is read only.
Use `mime.type` or `mime.subtype` to alter the MIME.

```mjs
import { MIMEType } from 'node:util';

const myMIME = new MIMEType('text/javascript;key=value');
console.log(myMIME.essence);
// Prints: text/javascript
myMIME.type = 'application';
console.log(myMIME.essence);
// Prints: application/javascript
console.log(String(myMIME));
// Prints: application/javascript;key=value
```

```cjs
const { MIMEType } = require('node:util');

const myMIME = new MIMEType('text/javascript;key=value');
console.log(myMIME.essence);
// Prints: text/javascript
myMIME.type = 'application';
console.log(myMIME.essence);
// Prints: application/javascript
console.log(String(myMIME));
// Prints: application/javascript;key=value
```

### `mime.params`

* {MIMEParams}

Gets the [`MIMEParams`][] object representing the
parameters of the MIME. This property is read-only. See
[`MIMEParams`][] documentation for details.

### `mime.toString()`

* Returns: {string}

The `toString()` method on the `MIMEType` object returns the serialized MIME.

Because of the need for standard compliance, this method does not allow users
to customize the serialization process of the MIME.

### `mime.toJSON()`

* Returns: {string}

Alias for [`mime.toString()`][].

This method is automatically called when an `MIMEType` object is serialized
with [`JSON.stringify()`][].

```mjs
import { MIMEType } from 'node:util';

const myMIMES = [
  new MIMEType('image/png'),
  new MIMEType('image/gif'),
];
console.log(JSON.stringify(myMIMES));
// Prints: ["image/png", "image/gif"]
```

```cjs
const { MIMEType } = require('node:util');

const myMIMES = [
  new MIMEType('image/png'),
  new MIMEType('image/gif'),
];
console.log(JSON.stringify(myMIMES));
// Prints: ["image/png", "image/gif"]
```

## Class: `util.MIMEParams`

<!-- YAML
added:
  - v19.1.0
  - v18.13.0
-->

The `MIMEParams` API provides read and write access to the parameters of a
`MIMEType`.

### Constructor: `new MIMEParams()`

Creates a new `MIMEParams` object by with empty parameters

```mjs
import { MIMEParams } from 'node:util';

const myParams = new MIMEParams();
```

```cjs
const { MIMEParams } = require('node:util');

const myParams = new MIMEParams();
```

### `mimeParams.delete(name)`

* `name` {string}

Remove all name-value pairs whose name is `name`.

### `mimeParams.entries()`

* Returns: {Iterator}

Returns an iterator over each of the name-value pairs in the parameters.
Each item of the iterator is a JavaScript `Array`. The first item of the array
is the `name`, the second item of the array is the `value`.

### `mimeParams.get(name)`

* `name` {string}
* Returns: {string | null} A string or `null` if there is no name-value pair
  with the given `name`.

Returns the value of the first name-value pair whose name is `name`. If there
are no such pairs, `null` is returned.

### `mimeParams.has(name)`

* `name` {string}
* Returns: {boolean}

Returns `true` if there is at least one name-value pair whose name is `name`.

### `mimeParams.keys()`

* Returns: {Iterator}

Returns an iterator over the names of each name-value pair.

```mjs
import { MIMEType } from 'node:util';

const { params } = new MIMEType('text/plain;foo=0;bar=1');
for (const name of params.keys()) {
  console.log(name);
}
// Prints:
//   foo
//   bar
```

```cjs
const { MIMEType } = require('node:util');

const { params } = new MIMEType('text/plain;foo=0;bar=1');
for (const name of params.keys()) {
  console.log(name);
}
// Prints:
//   foo
//   bar
```

### `mimeParams.set(name, value)`

* `name` {string}
* `value` {string}

Sets the value in the `MIMEParams` object associated with `name` to
`value`. If there are any pre-existing name-value pairs whose names are `name`,
set the first such pair's value to `value`.

```mjs
import { MIMEType } from 'node:util';

const { params } = new MIMEType('text/plain;foo=0;bar=1');
params.set('foo', 'def');
params.set('baz', 'xyz');
console.log(params.toString());
// Prints: foo=def;bar=1;baz=xyz
```

```cjs
const { MIMEType } = require('node:util');

const { params } = new MIMEType('text/plain;foo=0;bar=1');
params.set('foo', 'def');
params.set('baz', 'xyz');
console.log(params.toString());
// Prints: foo=def;bar=1;baz=xyz
```

### `mimeParams.values()`

* Returns: {Iterator}

Returns an iterator over the values of each name-value pair.

### `mimeParams[@@iterator]()`

* Returns: {Iterator}

Alias for [`mimeParams.entries()`][].

```mjs
import { MIMEType } from 'node:util';

const { params } = new MIMEType('text/plain;foo=bar;xyz=baz');
for (const [name, value] of params) {
  console.log(name, value);
}
// Prints:
//   foo bar
//   xyz baz
```

```cjs
const { MIMEType } = require('node:util');

const { params } = new MIMEType('text/plain;foo=bar;xyz=baz');
for (const [name, value] of params) {
  console.log(name, value);
}
// Prints:
//   foo bar
//   xyz baz
```

## `util.parseArgs([config])`

<!-- YAML
added:
  - v18.3.0
  - v16.17.0
changes:
  - version:
    - v22.4.0
    - v20.16.0
    pr-url: https://github.com/nodejs/node/pull/53107
    description: add support for allowing negative options in input `config`.
  - version:
    - v20.0.0
    pr-url: https://github.com/nodejs/node/pull/46718
    description: The API is no longer experimental.
  - version:
    - v18.11.0
    - v16.19.0
    pr-url: https://github.com/nodejs/node/pull/44631
    description: Add support for default values in input `config`.
  - version:
    - v18.7.0
    - v16.17.0
    pr-url: https://github.com/nodejs/node/pull/43459
    description: add support for returning detailed parse information
                 using `tokens` in input `config` and returned properties.
-->

* `config` {Object} Used to provide arguments for parsing and to configure
  the parser. `config` supports the following properties:
  * `args` {string\[]} array of argument strings. **Default:** `process.argv`
    with `execPath` and `filename` removed.
  * `options` {Object} Used to describe arguments known to the parser.
    Keys of `options` are the long names of options and values are an
    {Object} accepting the following properties:
    * `type` {string} Type of argument, which must be either `boolean` or `string`.
    * `multiple` {boolean} Whether this option can be provided multiple
      times. If `true`, all values will be collected in an array. If
      `false`, values for the option are last-wins. **Default:** `false`.
    * `short` {string} A single character alias for the option.
    * `default` {string | boolean | string\[] | boolean\[]} The default value to
      be used if (and only if) the option does not appear in the arguments to be
      parsed. It must be of the same type as the `type` property. When `multiple`
      is `true`, it must be an array.
  * `strict` {boolean} Should an error be thrown when unknown arguments
    are encountered, or when arguments are passed that do not match the
    `type` configured in `options`.
    **Default:** `true`.
  * `allowPositionals` {boolean} Whether this command accepts positional
    arguments.
    **Default:** `false` if `strict` is `true`, otherwise `true`.
  * `allowNegative` {boolean} If `true`, allows explicitly setting boolean
    options to `false` by prefixing the option name with `--no-`.
    **Default:** `false`.
  * `tokens` {boolean} Return the parsed tokens. This is useful for extending
    the built-in behavior, from adding additional checks through to reprocessing
    the tokens in different ways.
    **Default:** `false`.

* Returns: {Object} The parsed command line arguments:
  * `values` {Object} A mapping of parsed option names with their {string}
    or {boolean} values.
  * `positionals` {string\[]} Positional arguments.
  * `tokens` {Object\[] | undefined} See [parseArgs tokens](#parseargs-tokens)
    section. Only returned if `config` includes `tokens: true`.

Provides a higher level API for command-line argument parsing than interacting
with `process.argv` directly. Takes a specification for the expected arguments
and returns a structured object with the parsed options and positionals.

```mjs
import { parseArgs } from 'node:util';
const args = ['-f', '--bar', 'b'];
const options = {
  foo: {
    type: 'boolean',
    short: 'f',
  },
  bar: {
    type: 'string',
  },
};
const {
  values,
  positionals,
} = parseArgs({ args, options });
console.log(values, positionals);
// Prints: [Object: null prototype] { foo: true, bar: 'b' } []
```

```cjs
const { parseArgs } = require('node:util');
const args = ['-f', '--bar', 'b'];
const options = {
  foo: {
    type: 'boolean',
    short: 'f',
  },
  bar: {
    type: 'string',
  },
};
const {
  values,
  positionals,
} = parseArgs({ args, options });
console.log(values, positionals);
// Prints: [Object: null prototype] { foo: true, bar: 'b' } []
```

### `parseArgs` `tokens`

Detailed parse information is available for adding custom behaviors by
specifying `tokens: true` in the configuration.
The returned tokens have properties describing:

* all tokens
  * `kind` {string} One of 'option', 'positional', or 'option-terminator'.
  * `index` {number} Index of element in `args` containing token. So the
    source argument for a token is `args[token.index]`.
* option tokens
  * `name` {string} Long name of option.
  * `rawName` {string} How option used in args, like `-f` of `--foo`.
  * `value` {string | undefined} Option value specified in args.
    Undefined for boolean options.
  * `inlineValue` {boolean | undefined} Whether option value specified inline,
    like `--foo=bar`.
* positional tokens
  * `value` {string} The value of the positional argument in args (i.e. `args[index]`).
* option-terminator token

The returned tokens are in the order encountered in the input args. Options
that appear more than once in args produce a token for each use. Short option
groups like `-xy` expand to a token for each option. So `-xxx` produces
three tokens.

For example, to add support for a negated option like `--no-color` (which
`allowNegative` supports when the option is of `boolean` type), the returned
tokens can be reprocessed to change the value stored for the negated option.

```mjs
import { parseArgs } from 'node:util';

const options = {
  'color': { type: 'boolean' },
  'no-color': { type: 'boolean' },
  'logfile': { type: 'string' },
  'no-logfile': { type: 'boolean' },
};
const { values, tokens } = parseArgs({ options, tokens: true });

// Reprocess the option tokens and overwrite the returned values.
tokens
  .filter((token) => token.kind === 'option')
  .forEach((token) => {
    if (token.name.startsWith('no-')) {
      // Store foo:false for --no-foo
      const positiveName = token.name.slice(3);
      values[positiveName] = false;
      delete values[token.name];
    } else {
      // Resave value so last one wins if both --foo and --no-foo.
      values[token.name] = token.value ?? true;
    }
  });

const color = values.color;
const logfile = values.logfile ?? 'default.log';

console.log({ logfile, color });
```

```cjs
const { parseArgs } = require('node:util');

const options = {
  'color': { type: 'boolean' },
  'no-color': { type: 'boolean' },
  'logfile': { type: 'string' },
  'no-logfile': { type: 'boolean' },
};
const { values, tokens } = parseArgs({ options, tokens: true });

// Reprocess the option tokens and overwrite the returned values.
tokens
  .filter((token) => token.kind === 'option')
  .forEach((token) => {
    if (token.name.startsWith('no-')) {
      // Store foo:false for --no-foo
      const positiveName = token.name.slice(3);
      values[positiveName] = false;
      delete values[token.name];
    } else {
      // Resave value so last one wins if both --foo and --no-foo.
      values[token.name] = token.value ?? true;
    }
  });

const color = values.color;
const logfile = values.logfile ?? 'default.log';

console.log({ logfile, color });
```

Example usage showing negated options, and when an option is used
multiple ways then last one wins.

```console
$ node negate.js
{ logfile: 'default.log', color: undefined }
$ node negate.js --no-logfile --no-color
{ logfile: false, color: false }
$ node negate.js --logfile=test.log --color
{ logfile: 'test.log', color: true }
$ node negate.js --no-logfile --logfile=test.log --color --no-color
{ logfile: 'test.log', color: false }
```

## `util.parseEnv(content)`

> Stability: 1.1 - Active development

<!-- YAML
added:
  - v21.7.0
  - v20.12.0
-->

* `content` {string}

The raw contents of a `.env` file.

* Returns: {Object}

Given an example `.env` file:

```cjs
const { parseEnv } = require('node:util');

parseEnv('HELLO=world\nHELLO=oh my\n');
// Returns: { HELLO: 'oh my' }
```

```mjs
import { parseEnv } from 'node:util';

parseEnv('HELLO=world\nHELLO=oh my\n');
// Returns: { HELLO: 'oh my' }
```

## `util.promisify(original)`

<!-- YAML
added: v8.0.0
changes:
  - version: v20.8.0
    pr-url: https://github.com/nodejs/node/pull/49647
    description: Calling `promisify` on a function that returns a `Promise` is
                 deprecated.
-->

* `original` {Function}
* Returns: {Function}

Takes a function following the common error-first callback style, i.e. taking
an `(err, value) => ...` callback as the last argument, and returns a version
that returns promises.

```js
const util = require('node:util');
const fs = require('node:fs');

const stat = util.promisify(fs.stat);
stat('.').then((stats) => {
  // Do something with `stats`
}).catch((error) => {
  // Handle the error.
});
```

Or, equivalently using `async function`s:

```js
const util = require('node:util');
const fs = require('node:fs');

const stat = util.promisify(fs.stat);

async function callStat() {
  const stats = await stat('.');
  console.log(`This directory is owned by ${stats.uid}`);
}

callStat();
```

If there is an `original[util.promisify.custom]` property present, `promisify`
will return its value, see [Custom promisified functions][].

`promisify()` assumes that `original` is a function taking a callback as its
final argument in all cases. If `original` is not a function, `promisify()`
will throw an error. If `original` is a function but its last argument is not
an error-first callback, it will still be passed an error-first
callback as its last argument.

Using `promisify()` on class methods or other methods that use `this` may not
work as expected unless handled specially:

```js
const util = require('node:util');

class Foo {
  constructor() {
    this.a = 42;
  }

  bar(callback) {
    callback(null, this.a);
  }
}

const foo = new Foo();

const naiveBar = util.promisify(foo.bar);
// TypeError: Cannot read property 'a' of undefined
// naiveBar().then(a => console.log(a));

naiveBar.call(foo).then((a) => console.log(a)); // '42'

const bindBar = naiveBar.bind(foo);
bindBar().then((a) => console.log(a)); // '42'
```

### Custom promisified functions

Using the `util.promisify.custom` symbol one can override the return value of
[`util.promisify()`][]:

```js
const util = require('node:util');

function doSomething(foo, callback) {
  // ...
}

doSomething[util.promisify.custom] = (foo) => {
  return getPromiseSomehow();
};

const promisified = util.promisify(doSomething);
console.log(promisified === doSomething[util.promisify.custom]);
// prints 'true'
```

This can be useful for cases where the original function does not follow the
standard format of taking an error-first callback as the last argument.

For example, with a function that takes in
`(foo, onSuccessCallback, onErrorCallback)`:

```js
doSomething[util.promisify.custom] = (foo) => {
  return new Promise((resolve, reject) => {
    doSomething(foo, resolve, reject);
  });
};
```

If `promisify.custom` is defined but is not a function, `promisify()` will
throw an error.

### `util.promisify.custom`

<!-- YAML
added: v8.0.0
changes:
  - version:
      - v13.12.0
      - v12.16.2
    pr-url: https://github.com/nodejs/node/pull/31672
    description: This is now defined as a shared symbol.
-->

* {symbol} that can be used to declare custom promisified variants of functions,
  see [Custom promisified functions][].

In addition to being accessible through `util.promisify.custom`, this
symbol is [registered globally][global symbol registry] and can be
accessed in any environment as `Symbol.for('nodejs.util.promisify.custom')`.

For example, with a function that takes in
`(foo, onSuccessCallback, onErrorCallback)`:

```js
const kCustomPromisifiedSymbol = Symbol.for('nodejs.util.promisify.custom');

doSomething[kCustomPromisifiedSymbol] = (foo) => {
  return new Promise((resolve, reject) => {
    doSomething(foo, resolve, reject);
  });
};
```

## `util.stripVTControlCharacters(str)`

<!-- YAML
added: v16.11.0
-->

* `str` {string}
* Returns: {string}

Returns `str` with any ANSI escape codes removed.

```js
console.log(util.stripVTControlCharacters('\u001B[4mvalue\u001B[0m'));
// Prints "value"
```

## `util.styleText(format, text[, options])`

> Stability: 2 - Stable.

<!-- YAML
added:
  - v21.7.0
  - v20.12.0
changes:
  - version:
    - v23.5.0
    - v22.13.0
    pr-url: https://github.com/nodejs/node/pull/56265
    description: styleText is now stable.
  - version:
    - v22.8.0
    - v20.18.0
    pr-url: https://github.com/nodejs/node/pull/54389
    description: Respect isTTY and environment variables
      such as NO_COLORS, NODE_DISABLE_COLORS, and FORCE_COLOR.
-->

* `format` {string | Array} A text format or an Array
  of text formats defined in `util.inspect.colors`.
* `text` {string} The text to to be formatted.
* `options` {Object}
  * `validateStream` {boolean} When true, `stream` is checked to see if it can handle colors. **Default:** `true`.
  * `stream` {Stream} A stream that will be validated if it can be colored. **Default:** `process.stdout`.

This function returns a formatted text considering the `format` passed
for printing in a terminal. It is aware of the terminal's capabilities
and acts according to the configuration set via `NO_COLORS`,
`NODE_DISABLE_COLORS` and `FORCE_COLOR` environment variables.

```mjs
import { styleText } from 'node:util';
import { stderr } from 'node:process';

const successMessage = styleText('green', 'Success!');
console.log(successMessage);

const errorMessage = styleText(
  'red',
  'Error! Error!',
  // Validate if process.stderr has TTY
  { stream: stderr },
);
console.error(errorMessage);
```

```cjs
const { styleText } = require('node:util');
const { stderr } = require('node:process');

const successMessage = styleText('green', 'Success!');
console.log(successMessage);

const errorMessage = styleText(
  'red',
  'Error! Error!',
  // Validate if process.stderr has TTY
  { stream: stderr },
);
console.error(errorMessage);
```

`util.inspect.colors` also provides text formats such as `italic`, and
`underline` and you can combine both:

```cjs
console.log(
  util.styleText(['underline', 'italic'], 'My italic underlined message'),
);
```

When passing an array of formats, the order of the format applied
is left to right so the following style might overwrite the previous one.

```cjs
console.log(
  util.styleText(['red', 'green'], 'text'), // green
);
```

The full list of formats can be found in [modifiers][].

## Class: `util.TextDecoder`

<!-- YAML
added: v8.3.0
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22281
    description: The class is now available on the global object.
-->

An implementation of the [WHATWG Encoding Standard][] `TextDecoder` API.

```js
const decoder = new TextDecoder();
const u8arr = new Uint8Array([72, 101, 108, 108, 111]);
console.log(decoder.decode(u8arr)); // Hello
```

### WHATWG supported encodings

Per the [WHATWG Encoding Standard][], the encodings supported by the
`TextDecoder` API are outlined in the tables below. For each encoding,
one or more aliases may be used.

Different Node.js build configurations support different sets of encodings.
(see [Internationalization][])

#### Encodings supported by default (with full ICU data)

| Encoding           | Aliases                                                                                                                                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `'ibm866'`         | `'866'`, `'cp866'`, `'csibm866'`                                                                                                                                                                                                    |
| `'iso-8859-2'`     | `'csisolatin2'`, `'iso-ir-101'`, `'iso8859-2'`, `'iso88592'`, `'iso_8859-2'`, `'iso_8859-2:1987'`, `'l2'`, `'latin2'`                                                                                                               |
| `'iso-8859-3'`     | `'csisolatin3'`, `'iso-ir-109'`, `'iso8859-3'`, `'iso88593'`, `'iso_8859-3'`, `'iso_8859-3:1988'`, `'l3'`, `'latin3'`                                                                                                               |
| `'iso-8859-4'`     | `'csisolatin4'`, `'iso-ir-110'`, `'iso8859-4'`, `'iso88594'`, `'iso_8859-4'`, `'iso_8859-4:1988'`, `'l4'`, `'latin4'`                                                                                                               |
| `'iso-8859-5'`     | `'csisolatincyrillic'`, `'cyrillic'`, `'iso-ir-144'`, `'iso8859-5'`, `'iso88595'`, `'iso_8859-5'`, `'iso_8859-5:1988'`                                                                                                              |
| `'iso-8859-6'`     | `'arabic'`, `'asmo-708'`, `'csiso88596e'`, `'csiso88596i'`, `'csisolatinarabic'`, `'ecma-114'`, `'iso-8859-6-e'`, `'iso-8859-6-i'`, `'iso-ir-127'`, `'iso8859-6'`, `'iso88596'`, `'iso_8859-6'`, `'iso_8859-6:1987'`                |
| `'iso-8859-7'`     | `'csisolatingreek'`, `'ecma-118'`, `'elot_928'`, `'greek'`, `'greek8'`, `'iso-ir-126'`, `'iso8859-7'`, `'iso88597'`, `'iso_8859-7'`, `'iso_8859-7:1987'`, `'sun_eu_greek'`                                                          |
| `'iso-8859-8'`     | `'csiso88598e'`, `'csisolatinhebrew'`, `'hebrew'`, `'iso-8859-8-e'`, `'iso-ir-138'`, `'iso8859-8'`, `'iso88598'`, `'iso_8859-8'`, `'iso_8859-8:1988'`, `'visual'`                                                                   |
| `'iso-8859-8-i'`   | `'csiso88598i'`, `'logical'`                                                                                                                                                                                                        |
| `'iso-8859-10'`    | `'csisolatin6'`, `'iso-ir-157'`, `'iso8859-10'`, `'iso885910'`, `'l6'`, `'latin6'`                                                                                                                                                  |
| `'iso-8859-13'`    | `'iso8859-13'`, `'iso885913'`                                                                                                                                                                                                       |
| `'iso-8859-14'`    | `'iso8859-14'`, `'iso885914'`                                                                                                                                                                                                       |
| `'iso-8859-15'`    | `'csisolatin9'`, `'iso8859-15'`, `'iso885915'`, `'iso_8859-15'`, `'l9'`                                                                                                                                                             |
| `'koi8-r'`         | `'cskoi8r'`, `'koi'`, `'koi8'`, `'koi8_r'`                                                                                                                                                                                          |
| `'koi8-u'`         | `'koi8-ru'`                                                                                                                                                                                                                         |
| `'macintosh'`      | `'csmacintosh'`, `'mac'`, `'x-mac-roman'`                                                                                                                                                                                           |
| `'windows-874'`    | `'dos-874'`, `'iso-8859-11'`, `'iso8859-11'`, `'iso885911'`, `'tis-620'`                                                                                                                                                            |
| `'windows-1250'`   | `'cp1250'`, `'x-cp1250'`                                                                                                                                                                                                            |
| `'windows-1251'`   | `'cp1251'`, `'x-cp1251'`                                                                                                                                                                                                            |
| `'windows-1252'`   | `'ansi_x3.4-1968'`, `'ascii'`, `'cp1252'`, `'cp819'`, `'csisolatin1'`, `'ibm819'`, `'iso-8859-1'`, `'iso-ir-100'`, `'iso8859-1'`, `'iso88591'`, `'iso_8859-1'`, `'iso_8859-1:1987'`, `'l1'`, `'latin1'`, `'us-ascii'`, `'x-cp1252'` |
| `'windows-1253'`   | `'cp1253'`, `'x-cp1253'`                                                                                                                                                                                                            |
| `'windows-1254'`   | `'cp1254'`, `'csisolatin5'`, `'iso-8859-9'`, `'iso-ir-148'`, `'iso8859-9'`, `'iso88599'`, `'iso_8859-9'`, `'iso_8859-9:1989'`, `'l5'`, `'latin5'`, `'x-cp1254'`                                                                     |
| `'windows-1255'`   | `'cp1255'`, `'x-cp1255'`                                                                                                                                                                                                            |
| `'windows-1256'`   | `'cp1256'`, `'x-cp1256'`                                                                                                                                                                                                            |
| `'windows-1257'`   | `'cp1257'`, `'x-cp1257'`                                                                                                                                                                                                            |
| `'windows-1258'`   | `'cp1258'`, `'x-cp1258'`                                                                                                                                                                                                            |
| `'x-mac-cyrillic'` | `'x-mac-ukrainian'`                                                                                                                                                                                                                 |
| `'gbk'`            | `'chinese'`, `'csgb2312'`, `'csiso58gb231280'`, `'gb2312'`, `'gb_2312'`, `'gb_2312-80'`, `'iso-ir-58'`, `'x-gbk'`                                                                                                                   |
| `'gb18030'`        |                                                                                                                                                                                                                                     |
| `'big5'`           | `'big5-hkscs'`, `'cn-big5'`, `'csbig5'`, `'x-x-big5'`                                                                                                                                                                               |
| `'euc-jp'`         | `'cseucpkdfmtjapanese'`, `'x-euc-jp'`                                                                                                                                                                                               |
| `'iso-2022-jp'`    | `'csiso2022jp'`                                                                                                                                                                                                                     |
| `'shift_jis'`      | `'csshiftjis'`, `'ms932'`, `'ms_kanji'`, `'shift-jis'`, `'sjis'`, `'windows-31j'`, `'x-sjis'`                                                                                                                                       |
| `'euc-kr'`         | `'cseuckr'`, `'csksc56011987'`, `'iso-ir-149'`, `'korean'`, `'ks_c_5601-1987'`, `'ks_c_5601-1989'`, `'ksc5601'`, `'ksc_5601'`, `'windows-949'`                                                                                      |

#### Encodings supported when Node.js is built with the `small-icu` option

| Encoding     | Aliases                         |
| ------------ | ------------------------------- |
| `'utf-8'`    | `'unicode-1-1-utf-8'`, `'utf8'` |
| `'utf-16le'` | `'utf-16'`                      |
| `'utf-16be'` |                                 |

#### Encodings supported when ICU is disabled

| Encoding     | Aliases                         |
| ------------ | ------------------------------- |
| `'utf-8'`    | `'unicode-1-1-utf-8'`, `'utf8'` |
| `'utf-16le'` | `'utf-16'`                      |

The `'iso-8859-16'` encoding listed in the [WHATWG Encoding Standard][]
is not supported.

### `new TextDecoder([encoding[, options]])`

* `encoding` {string} Identifies the `encoding` that this `TextDecoder` instance
  supports. **Default:** `'utf-8'`.
* `options` {Object}
  * `fatal` {boolean} `true` if decoding failures are fatal.
    This option is not supported when ICU is disabled
    (see [Internationalization][]). **Default:** `false`.
  * `ignoreBOM` {boolean} When `true`, the `TextDecoder` will include the byte
    order mark in the decoded result. When `false`, the byte order mark will
    be removed from the output. This option is only used when `encoding` is
    `'utf-8'`, `'utf-16be'`, or `'utf-16le'`. **Default:** `false`.

Creates a new `TextDecoder` instance. The `encoding` may specify one of the
supported encodings or an alias.

The `TextDecoder` class is also available on the global object.

### `textDecoder.decode([input[, options]])`

* `input` {ArrayBuffer|DataView|TypedArray} An `ArrayBuffer`, `DataView`, or
  `TypedArray` instance containing the encoded data.
* `options` {Object}
  * `stream` {boolean} `true` if additional chunks of data are expected.
    **Default:** `false`.
* Returns: {string}

Decodes the `input` and returns a string. If `options.stream` is `true`, any
incomplete byte sequences occurring at the end of the `input` are buffered
internally and emitted after the next call to `textDecoder.decode()`.

If `textDecoder.fatal` is `true`, decoding errors that occur will result in a
`TypeError` being thrown.

### `textDecoder.encoding`

* {string}

The encoding supported by the `TextDecoder` instance.

### `textDecoder.fatal`

* {boolean}

The value will be `true` if decoding errors result in a `TypeError` being
thrown.

### `textDecoder.ignoreBOM`

* {boolean}

The value will be `true` if the decoding result will include the byte order
mark.

## Class: `util.TextEncoder`

<!-- YAML
added: v8.3.0
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22281
    description: The class is now available on the global object.
-->

An implementation of the [WHATWG Encoding Standard][] `TextEncoder` API. All
instances of `TextEncoder` only support UTF-8 encoding.

```js
const encoder = new TextEncoder();
const uint8array = encoder.encode('this is some data');
```

The `TextEncoder` class is also available on the global object.

### `textEncoder.encode([input])`

* `input` {string} The text to encode. **Default:** an empty string.
* Returns: {Uint8Array}

UTF-8 encodes the `input` string and returns a `Uint8Array` containing the
encoded bytes.

### `textEncoder.encodeInto(src, dest)`

<!-- YAML
added: v12.11.0
-->

* `src` {string} The text to encode.
* `dest` {Uint8Array} The array to hold the encode result.
* Returns: {Object}
  * `read` {number} The read Unicode code units of src.
  * `written` {number} The written UTF-8 bytes of dest.

UTF-8 encodes the `src` string to the `dest` Uint8Array and returns an object
containing the read Unicode code units and written UTF-8 bytes.

```js
const encoder = new TextEncoder();
const src = 'this is some data';
const dest = new Uint8Array(10);
const { read, written } = encoder.encodeInto(src, dest);
```

### `textEncoder.encoding`

* {string}

The encoding supported by the `TextEncoder` instance. Always set to `'utf-8'`.

## `util.toUSVString(string)`

<!-- YAML
added:
  - v16.8.0
  - v14.18.0
-->

* `string` {string}

Returns the `string` after replacing any surrogate code points
(or equivalently, any unpaired surrogate code units) with the
Unicode "replacement character" U+FFFD.

## `util.transferableAbortController()`

<!-- YAML
added: v18.11.0
-->

> Stability: 1 - Experimental

Creates and returns an {AbortController} instance whose {AbortSignal} is marked
as transferable and can be used with `structuredClone()` or `postMessage()`.

## `util.transferableAbortSignal(signal)`

<!-- YAML
added: v18.11.0
-->

> Stability: 1 - Experimental

* `signal` {AbortSignal}
* Returns: {AbortSignal}

Marks the given {AbortSignal} as transferable so that it can be used with
`structuredClone()` and `postMessage()`.

```js
const signal = transferableAbortSignal(AbortSignal.timeout(100));
const channel = new MessageChannel();
channel.port2.postMessage(signal, [signal]);
```

## `util.aborted(signal, resource)`

<!-- YAML
added:
 - v19.7.0
 - v18.16.0
-->

> Stability: 1 - Experimental

* `signal` {AbortSignal}
* `resource` {Object} Any non-null object tied to the abortable operation and held weakly.
  If `resource` is garbage collected before the `signal` aborts, the promise remains pending,
  allowing Node.js to stop tracking it.
  This helps prevent memory leaks in long-running or non-cancelable operations.
* Returns: {Promise}

Listens to abort event on the provided `signal` and returns a promise that resolves when the `signal` is aborted.
If `resource` is provided, it weakly references the operation's associated object,
so if `resource` is garbage collected before the `signal` aborts,
then returned promise shall remain pending.
This prevents memory leaks in long-running or non-cancelable operations.

```cjs
const { aborted } = require('node:util');

// Obtain an object with an abortable signal, like a custom resource or operation.
const dependent = obtainSomethingAbortable();

// Pass `dependent` as the resource, indicating the promise should only resolve
// if `dependent` is still in memory when the signal is aborted.
aborted(dependent.signal, dependent).then(() => {

  // This code runs when `dependent` is aborted.
  console.log('Dependent resource was aborted.');
});

// Simulate an event that triggers the abort.
dependent.on('event', () => {
  dependent.abort(); // This will cause the `aborted` promise to resolve.
});
```

```mjs
import { aborted } from 'node:util';

// Obtain an object with an abortable signal, like a custom resource or operation.
const dependent = obtainSomethingAbortable();

// Pass `dependent` as the resource, indicating the promise should only resolve
// if `dependent` is still in memory when the signal is aborted.
aborted(dependent.signal, dependent).then(() => {

  // This code runs when `dependent` is aborted.
  console.log('Dependent resource was aborted.');
});

// Simulate an event that triggers the abort.
dependent.on('event', () => {
  dependent.abort(); // This will cause the `aborted` promise to resolve.
});
```

## `util.types`

<!-- YAML
added: v10.0.0
changes:
  - version: v15.3.0
    pr-url: https://github.com/nodejs/node/pull/34055
    description: Exposed as `require('util/types')`.
-->

`util.types` provides type checks for different kinds of built-in objects.
Unlike `instanceof` or `Object.prototype.toString.call(value)`, these checks do
not inspect properties of the object that are accessible from JavaScript (like
their prototype), and usually have the overhead of calling into C++.

The result generally does not make any guarantees about what kinds of
properties or behavior a value exposes in JavaScript. They are primarily
useful for addon developers who prefer to do type checking in JavaScript.

The API is accessible via `require('node:util').types` or `require('node:util/types')`.

### `util.types.isAnyArrayBuffer(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`ArrayBuffer`][] or
[`SharedArrayBuffer`][] instance.

See also [`util.types.isArrayBuffer()`][] and
[`util.types.isSharedArrayBuffer()`][].

```js
util.types.isAnyArrayBuffer(new ArrayBuffer());  // Returns true
util.types.isAnyArrayBuffer(new SharedArrayBuffer());  // Returns true
```

### `util.types.isArrayBufferView(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is an instance of one of the [`ArrayBuffer`][]
views, such as typed array objects or [`DataView`][]. Equivalent to
[`ArrayBuffer.isView()`][].

```js
util.types.isArrayBufferView(new Int8Array());  // true
util.types.isArrayBufferView(Buffer.from('hello world')); // true
util.types.isArrayBufferView(new DataView(new ArrayBuffer(16)));  // true
util.types.isArrayBufferView(new ArrayBuffer());  // false
```

### `util.types.isArgumentsObject(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is an `arguments` object.

<!-- eslint-disable prefer-rest-params -->

```js
function foo() {
  util.types.isArgumentsObject(arguments);  // Returns true
}
```

### `util.types.isArrayBuffer(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`ArrayBuffer`][] instance.
This does _not_ include [`SharedArrayBuffer`][] instances. Usually, it is
desirable to test for both; See [`util.types.isAnyArrayBuffer()`][] for that.

```js
util.types.isArrayBuffer(new ArrayBuffer());  // Returns true
util.types.isArrayBuffer(new SharedArrayBuffer());  // Returns false
```

### `util.types.isAsyncFunction(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is an [async function][].
This only reports back what the JavaScript engine is seeing;
in particular, the return value may not match the original source code if
a transpilation tool was used.

```js
util.types.isAsyncFunction(function foo() {});  // Returns false
util.types.isAsyncFunction(async function foo() {});  // Returns true
```

### `util.types.isBigInt64Array(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a `BigInt64Array` instance.

```js
util.types.isBigInt64Array(new BigInt64Array());   // Returns true
util.types.isBigInt64Array(new BigUint64Array());  // Returns false
```

### `util.types.isBigIntObject(value)`

<!-- YAML
added: v10.4.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a BigInt object, e.g. created
by `Object(BigInt(123))`.

```js
util.types.isBigIntObject(Object(BigInt(123)));   // Returns true
util.types.isBigIntObject(BigInt(123));   // Returns false
util.types.isBigIntObject(123);  // Returns false
```

### `util.types.isBigUint64Array(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a `BigUint64Array` instance.

```js
util.types.isBigUint64Array(new BigInt64Array());   // Returns false
util.types.isBigUint64Array(new BigUint64Array());  // Returns true
```

### `util.types.isBooleanObject(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a boolean object, e.g. created
by `new Boolean()`.

```js
util.types.isBooleanObject(false);  // Returns false
util.types.isBooleanObject(true);   // Returns false
util.types.isBooleanObject(new Boolean(false)); // Returns true
util.types.isBooleanObject(new Boolean(true));  // Returns true
util.types.isBooleanObject(Boolean(false)); // Returns false
util.types.isBooleanObject(Boolean(true));  // Returns false
```

### `util.types.isBoxedPrimitive(value)`

<!-- YAML
added: v10.11.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is any boxed primitive object, e.g. created
by `new Boolean()`, `new String()` or `Object(Symbol())`.

For example:

```js
util.types.isBoxedPrimitive(false); // Returns false
util.types.isBoxedPrimitive(new Boolean(false)); // Returns true
util.types.isBoxedPrimitive(Symbol('foo')); // Returns false
util.types.isBoxedPrimitive(Object(Symbol('foo'))); // Returns true
util.types.isBoxedPrimitive(Object(BigInt(5))); // Returns true
```

### `util.types.isCryptoKey(value)`

<!-- YAML
added: v16.2.0
-->

* `value` {Object}
* Returns: {boolean}

Returns `true` if `value` is a {CryptoKey}, `false` otherwise.

### `util.types.isDataView(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`DataView`][] instance.

```js
const ab = new ArrayBuffer(20);
util.types.isDataView(new DataView(ab));  // Returns true
util.types.isDataView(new Float64Array());  // Returns false
```

See also [`ArrayBuffer.isView()`][].

### `util.types.isDate(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Date`][] instance.

```js
util.types.isDate(new Date());  // Returns true
```

### `util.types.isExternal(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a native `External` value.

A native `External` value is a special type of object that contains a
raw C++ pointer (`void*`) for access from native code, and has no other
properties. Such objects are created either by Node.js internals or native
addons. In JavaScript, they are [frozen][`Object.freeze()`] objects with a
`null` prototype.

```c
#include <js_native_api.h>
#include <stdlib.h>
napi_value result;
static napi_value MyNapi(napi_env env, napi_callback_info info) {
  int* raw = (int*) malloc(1024);
  napi_status status = napi_create_external(env, (void*) raw, NULL, NULL, &result);
  if (status != napi_ok) {
    napi_throw_error(env, NULL, "napi_create_external failed");
    return NULL;
  }
  return result;
}
...
DECLARE_NAPI_PROPERTY("myNapi", MyNapi)
...
```

```js
const native = require('napi_addon.node');
const data = native.myNapi();
util.types.isExternal(data); // returns true
util.types.isExternal(0); // returns false
util.types.isExternal(new String('foo')); // returns false
```

For further information on `napi_create_external`, refer to
[`napi_create_external()`][].

### `util.types.isFloat32Array(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Float32Array`][] instance.

```js
util.types.isFloat32Array(new ArrayBuffer());  // Returns false
util.types.isFloat32Array(new Float32Array());  // Returns true
util.types.isFloat32Array(new Float64Array());  // Returns false
```

### `util.types.isFloat64Array(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Float64Array`][] instance.

```js
util.types.isFloat64Array(new ArrayBuffer());  // Returns false
util.types.isFloat64Array(new Uint8Array());  // Returns false
util.types.isFloat64Array(new Float64Array());  // Returns true
```

### `util.types.isGeneratorFunction(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a generator function.
This only reports back what the JavaScript engine is seeing;
in particular, the return value may not match the original source code if
a transpilation tool was used.

```js
util.types.isGeneratorFunction(function foo() {});  // Returns false
util.types.isGeneratorFunction(function* foo() {});  // Returns true
```

### `util.types.isGeneratorObject(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a generator object as returned from a
built-in generator function.
This only reports back what the JavaScript engine is seeing;
in particular, the return value may not match the original source code if
a transpilation tool was used.

```js
function* foo() {}
const generator = foo();
util.types.isGeneratorObject(generator);  // Returns true
```

### `util.types.isInt8Array(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Int8Array`][] instance.

```js
util.types.isInt8Array(new ArrayBuffer());  // Returns false
util.types.isInt8Array(new Int8Array());  // Returns true
util.types.isInt8Array(new Float64Array());  // Returns false
```

### `util.types.isInt16Array(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Int16Array`][] instance.

```js
util.types.isInt16Array(new ArrayBuffer());  // Returns false
util.types.isInt16Array(new Int16Array());  // Returns true
util.types.isInt16Array(new Float64Array());  // Returns false
```

### `util.types.isInt32Array(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Int32Array`][] instance.

```js
util.types.isInt32Array(new ArrayBuffer());  // Returns false
util.types.isInt32Array(new Int32Array());  // Returns true
util.types.isInt32Array(new Float64Array());  // Returns false
```

### `util.types.isKeyObject(value)`

<!-- YAML
added: v16.2.0
-->

* `value` {Object}
* Returns: {boolean}

Returns `true` if `value` is a {KeyObject}, `false` otherwise.

### `util.types.isMap(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Map`][] instance.

```js
util.types.isMap(new Map());  // Returns true
```

### `util.types.isMapIterator(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is an iterator returned for a built-in
[`Map`][] instance.

```js
const map = new Map();
util.types.isMapIterator(map.keys());  // Returns true
util.types.isMapIterator(map.values());  // Returns true
util.types.isMapIterator(map.entries());  // Returns true
util.types.isMapIterator(map[Symbol.iterator]());  // Returns true
```

### `util.types.isModuleNamespaceObject(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is an instance of a [Module Namespace Object][].

```mjs
import * as ns from './a.js';

util.types.isModuleNamespaceObject(ns);  // Returns true
```

### `util.types.isNativeError(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value was returned by the constructor of a
[built-in `Error` type][].

```js
console.log(util.types.isNativeError(new Error()));  // true
console.log(util.types.isNativeError(new TypeError()));  // true
console.log(util.types.isNativeError(new RangeError()));  // true
```

Subclasses of the native error types are also native errors:

```js
class MyError extends Error {}
console.log(util.types.isNativeError(new MyError()));  // true
```

A value being `instanceof` a native error class is not equivalent to `isNativeError()`
returning `true` for that value. `isNativeError()` returns `true` for errors
which come from a different [realm][] while `instanceof Error` returns `false`
for these errors:

```js
const vm = require('node:vm');
const context = vm.createContext({});
const myError = vm.runInContext('new Error()', context);
console.log(util.types.isNativeError(myError)); // true
console.log(myError instanceof Error); // false
```

Conversely, `isNativeError()` returns `false` for all objects which were not
returned by the constructor of a native error. That includes values
which are `instanceof` native errors:

```js
const myError = { __proto__: Error.prototype };
console.log(util.types.isNativeError(myError)); // false
console.log(myError instanceof Error); // true
```

### `util.types.isNumberObject(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a number object, e.g. created
by `new Number()`.

```js
util.types.isNumberObject(0);  // Returns false
util.types.isNumberObject(new Number(0));   // Returns true
```

### `util.types.isPromise(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Promise`][].

```js
util.types.isPromise(Promise.resolve(42));  // Returns true
```

### `util.types.isProxy(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a [`Proxy`][] instance.

```js
const target = {};
const proxy = new Proxy(target, {});
util.types.isProxy(target);  // Returns false
util.types.isProxy(proxy);  // Returns true
```

### `util.types.isRegExp(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a regular expression object.

```js
util.types.isRegExp(/abc/);  // Returns true
util.types.isRegExp(new RegExp('abc'));  // Returns true
```

### `util.types.isSet(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Set`][] instance.

```js
util.types.isSet(new Set());  // Returns true
```

### `util.types.isSetIterator(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is an iterator returned for a built-in
[`Set`][] instance.

```js
const set = new Set();
util.types.isSetIterator(set.keys());  // Returns true
util.types.isSetIterator(set.values());  // Returns true
util.types.isSetIterator(set.entries());  // Returns true
util.types.isSetIterator(set[Symbol.iterator]());  // Returns true
```

### `util.types.isSharedArrayBuffer(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`SharedArrayBuffer`][] instance.
This does _not_ include [`ArrayBuffer`][] instances. Usually, it is
desirable to test for both; See [`util.types.isAnyArrayBuffer()`][] for that.

```js
util.types.isSharedArrayBuffer(new ArrayBuffer());  // Returns false
util.types.isSharedArrayBuffer(new SharedArrayBuffer());  // Returns true
```

### `util.types.isStringObject(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a string object, e.g. created
by `new String()`.

```js
util.types.isStringObject('foo');  // Returns false
util.types.isStringObject(new String('foo'));   // Returns true
```

### `util.types.isSymbolObject(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a symbol object, created
by calling `Object()` on a `Symbol` primitive.

```js
const symbol = Symbol('foo');
util.types.isSymbolObject(symbol);  // Returns false
util.types.isSymbolObject(Object(symbol));   // Returns true
```

### `util.types.isTypedArray(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`TypedArray`][] instance.

```js
util.types.isTypedArray(new ArrayBuffer());  // Returns false
util.types.isTypedArray(new Uint8Array());  // Returns true
util.types.isTypedArray(new Float64Array());  // Returns true
```

See also [`ArrayBuffer.isView()`][].

### `util.types.isUint8Array(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Uint8Array`][] instance.

```js
util.types.isUint8Array(new ArrayBuffer());  // Returns false
util.types.isUint8Array(new Uint8Array());  // Returns true
util.types.isUint8Array(new Float64Array());  // Returns false
```

### `util.types.isUint8ClampedArray(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Uint8ClampedArray`][] instance.

```js
util.types.isUint8ClampedArray(new ArrayBuffer());  // Returns false
util.types.isUint8ClampedArray(new Uint8ClampedArray());  // Returns true
util.types.isUint8ClampedArray(new Float64Array());  // Returns false
```

### `util.types.isUint16Array(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Uint16Array`][] instance.

```js
util.types.isUint16Array(new ArrayBuffer());  // Returns false
util.types.isUint16Array(new Uint16Array());  // Returns true
util.types.isUint16Array(new Float64Array());  // Returns false
```

### `util.types.isUint32Array(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Uint32Array`][] instance.

```js
util.types.isUint32Array(new ArrayBuffer());  // Returns false
util.types.isUint32Array(new Uint32Array());  // Returns true
util.types.isUint32Array(new Float64Array());  // Returns false
```

### `util.types.isWeakMap(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`WeakMap`][] instance.

```js
util.types.isWeakMap(new WeakMap());  // Returns true
```

### `util.types.isWeakSet(value)`

<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`WeakSet`][] instance.

```js
util.types.isWeakSet(new WeakSet());  // Returns true
```

## Deprecated APIs

The following APIs are deprecated and should no longer be used. Existing
applications and modules should be updated to find alternative approaches.

### `util._extend(target, source)`

<!-- YAML
added: v0.7.5
deprecated: v6.0.0
-->

> Stability: 0 - Deprecated: Use [`Object.assign()`][] instead.

* `target` {Object}
* `source` {Object}

The `util._extend()` method was never intended to be used outside of internal
Node.js modules. The community found and used it anyway.

It is deprecated and should not be used in new code. JavaScript comes with very
similar built-in functionality through [`Object.assign()`][].

### `util.isArray(object)`

<!-- YAML
added: v0.6.0
deprecated: v4.0.0
-->

> Stability: 0 - Deprecated: Use [`Array.isArray()`][] instead.

* `object` {any}
* Returns: {boolean}

Alias for [`Array.isArray()`][].

Returns `true` if the given `object` is an `Array`. Otherwise, returns `false`.

```js
const util = require('node:util');

util.isArray([]);
// Returns: true
util.isArray(new Array());
// Returns: true
util.isArray({});
// Returns: false
```

[Common System Errors]: errors.md#common-system-errors
[Custom inspection functions on objects]: #custom-inspection-functions-on-objects
[Custom promisified functions]: #custom-promisified-functions
[Customizing `util.inspect` colors]: #customizing-utilinspect-colors
[Internationalization]: intl.md
[Module Namespace Object]: https://tc39.github.io/ecma262/#sec-module-namespace-exotic-objects
[WHATWG Encoding Standard]: https://encoding.spec.whatwg.org/
[`'uncaughtException'`]: process.md#event-uncaughtexception
[`'warning'`]: process.md#event-warning
[`Array.isArray()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray
[`ArrayBuffer.isView()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/isView
[`ArrayBuffer`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer
[`DataView`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView
[`Date`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date
[`Float32Array`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float32Array
[`Float64Array`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float64Array
[`Int16Array`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int16Array
[`Int32Array`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int32Array
[`Int8Array`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int8Array
[`JSON.stringify()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify
[`MIMEparams`]: #class-utilmimeparams
[`Map`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map
[`Object.assign()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
[`Object.freeze()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze
[`Promise`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[`Proxy`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy
[`Runtime.ScriptId`]: https://chromedevtools.github.io/devtools-protocol/1-3/Runtime/#type-ScriptId
[`Set`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set
[`SharedArrayBuffer`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer
[`TypedArray`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray
[`Uint16Array`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint16Array
[`Uint32Array`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint32Array
[`Uint8Array`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array
[`Uint8ClampedArray`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8ClampedArray
[`WeakMap`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap
[`WeakSet`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet
[`assert.deepStrictEqual()`]: assert.md#assertdeepstrictequalactual-expected-message
[`console.error()`]: console.md#consoleerrordata-args
[`mime.toString()`]: #mimetostring
[`mimeParams.entries()`]: #mimeparamsentries
[`napi_create_external()`]: n-api.md#napi_create_external
[`target` and `handler`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy#Terminology
[`tty.hasColors()`]: tty.md#writestreamhascolorscount-env
[`util.format()`]: #utilformatformat-args
[`util.inspect()`]: #utilinspectobject-options
[`util.promisify()`]: #utilpromisifyoriginal
[`util.types.isAnyArrayBuffer()`]: #utiltypesisanyarraybuffervalue
[`util.types.isArrayBuffer()`]: #utiltypesisarraybuffervalue
[`util.types.isSharedArrayBuffer()`]: #utiltypesissharedarraybuffervalue
[async function]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
[built-in `Error` type]: https://tc39.es/ecma262/#sec-error-objects
[compare function]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Parameters
[constructor]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor
[default sort]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort
[global symbol registry]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/for
[list of deprecated APIS]: deprecations.md#list-of-deprecated-apis
[modifiers]: #modifiers
[realm]: https://tc39.es/ecma262/#realm
[semantically incompatible]: https://github.com/nodejs/node/issues/4179
[util.inspect.custom]: #utilinspectcustom

# SQLite

<!--introduced_in=v22.5.0-->

<!-- YAML
added: v22.5.0
-->

> Stability: 1.1 - Active development.

<!-- source_link=lib/sqlite.js -->

The `node:sqlite` module facilitates working with SQLite databases.
To access it:

```mjs
import sqlite from 'node:sqlite';
```

```cjs
const sqlite = require('node:sqlite');
```

This module is only available under the `node:` scheme.

The following example shows the basic usage of the `node:sqlite` module to open
an in-memory database, write data to the database, and then read the data back.

```mjs
import { DatabaseSync } from 'node:sqlite';
const database = new DatabaseSync(':memory:');

// Execute SQL statements from strings.
database.exec(`
  CREATE TABLE data(
    key INTEGER PRIMARY KEY,
    value TEXT
  ) STRICT
`);
// Create a prepared statement to insert data into the database.
const insert = database.prepare('INSERT INTO data (key, value) VALUES (?, ?)');
// Execute the prepared statement with bound values.
insert.run(1, 'hello');
insert.run(2, 'world');
// Create a prepared statement to read data from the database.
const query = database.prepare('SELECT * FROM data ORDER BY key');
// Execute the prepared statement and log the result set.
console.log(query.all());
// Prints: [ { key: 1, value: 'hello' }, { key: 2, value: 'world' } ]
```

```cjs
'use strict';
const { DatabaseSync } = require('node:sqlite');
const database = new DatabaseSync(':memory:');

// Execute SQL statements from strings.
database.exec(`
  CREATE TABLE data(
    key INTEGER PRIMARY KEY,
    value TEXT
  ) STRICT
`);
// Create a prepared statement to insert data into the database.
const insert = database.prepare('INSERT INTO data (key, value) VALUES (?, ?)');
// Execute the prepared statement with bound values.
insert.run(1, 'hello');
insert.run(2, 'world');
// Create a prepared statement to read data from the database.
const query = database.prepare('SELECT * FROM data ORDER BY key');
// Execute the prepared statement and log the result set.
console.log(query.all());
// Prints: [ { key: 1, value: 'hello' }, { key: 2, value: 'world' } ]
```

## Class: `DatabaseSync`

<!-- YAML
added: v22.5.0
-->

This class represents a single [connection][] to a SQLite database. All APIs
exposed by this class execute synchronously.

### `new DatabaseSync(location[, options])`

<!-- YAML
added: v22.5.0
-->

* `location` {string} The location of the database. A SQLite database can be
  stored in a file or completely [in memory][]. To use a file-backed database,
  the location should be a file path. To use an in-memory database, the location
  should be the special name `':memory:'`.
* `options` {Object} Configuration options for the database connection. The
  following options are supported:
  * `open` {boolean} If `true`, the database is opened by the constructor. When
    this value is `false`, the database must be opened via the `open()` method.
    **Default:** `true`.
  * `readOnly` {boolean} If `true`, the database is opened in read-only mode.
    If the database does not exist, opening it will fail. **Default:** `false`.
  * `enableForeignKeyConstraints` {boolean} If `true`, foreign key constraints
    are enabled. This is recommended but can be disabled for compatibility with
    legacy database schemas. The enforcement of foreign key constraints can be
    enabled and disabled after opening the database using
    [`PRAGMA foreign_keys`][]. **Default:** `true`.
  * `enableDoubleQuotedStringLiterals` {boolean} If `true`, SQLite will accept
    [double-quoted string literals][]. This is not recommended but can be
    enabled for compatibility with legacy database schemas.
    **Default:** `false`.
  * `allowExtension` {boolean} If `true`, the `loadExtension` SQL function
    and the `loadExtension()` method are enabled.
    You can call `enableLoadExtension(false)` later to disable this feature.
    **Default:** `false`.

Constructs a new `DatabaseSync` instance.

### `database.close()`

<!-- YAML
added: v22.5.0
-->

Closes the database connection. An exception is thrown if the database is not
open. This method is a wrapper around [`sqlite3_close_v2()`][].

### `database.loadExtension(path)`

<!-- YAML
added:
  - v23.5.0
  - v22.13.0
-->

* `path` {string} The path to the shared library to load.

Loads a shared library into the database connection. This method is a wrapper
around [`sqlite3_load_extension()`][]. It is required to enable the
`allowExtension` option when constructing the `DatabaseSync` instance.

### `database.enableLoadExtension(allow)`

<!-- YAML
added:
  - v23.5.0
  - v22.13.0
-->

* `allow` {boolean} Whether to allow loading extensions.

Enables or disables the `loadExtension` SQL function, and the `loadExtension()`
method. When `allowExtension` is `false` when constructing, you cannot enable
loading extensions for security reasons.

### `database.exec(sql)`

<!-- YAML
added: v22.5.0
-->

* `sql` {string} A SQL string to execute.

This method allows one or more SQL statements to be executed without returning
any results. This method is useful when executing SQL statements read from a
file. This method is a wrapper around [`sqlite3_exec()`][].

### `database.function(name[, options], function)`

<!-- YAML
added:
  - v23.5.0
  - v22.13.0
-->

* `name` {string} The name of the SQLite function to create.
* `options` {Object} Optional configuration settings for the function. The
  following properties are supported:
  * `deterministic` {boolean} If `true`, the [`SQLITE_DETERMINISTIC`][] flag is
    set on the created function. **Default:** `false`.
  * `directOnly` {boolean} If `true`, the [`SQLITE_DIRECTONLY`][] flag is set on
    the created function. **Default:** `false`.
  * `useBigIntArguments` {boolean} If `true`, integer arguments to `function`
    are converted to `BigInt`s. If `false`, integer arguments are passed as
    JavaScript numbers. **Default:** `false`.
  * `varargs` {boolean} If `true`, `function` may be invoked with any number of
    arguments (between zero and [`SQLITE_MAX_FUNCTION_ARG`][]). If `false`,
    `function` must be invoked with exactly `function.length` arguments.
    **Default:** `false`.
* `function` {Function} The JavaScript function to call when the SQLite
  function is invoked. The return value of this function should be a valid
  SQLite data type: see [Type conversion between JavaScript and SQLite][].
  The result defaults to `NULL` if the return value is `undefined`.

This method is used to create SQLite user-defined functions. This method is a
wrapper around [`sqlite3_create_function_v2()`][].

### `database.open()`

<!-- YAML
added: v22.5.0
-->

Opens the database specified in the `location` argument of the `DatabaseSync`
constructor. This method should only be used when the database is not opened via
the constructor. An exception is thrown if the database is already open.

### `database.prepare(sql)`

<!-- YAML
added: v22.5.0
-->

* `sql` {string} A SQL string to compile to a prepared statement.
* Returns: {StatementSync} The prepared statement.

Compiles a SQL statement into a [prepared statement][]. This method is a wrapper
around [`sqlite3_prepare_v2()`][].

### `database.createSession([options])`

<!-- YAML
added:
  - v23.3.0
  - v22.12.0
-->

* `options` {Object} The configuration options for the session.
  * `table` {string} A specific table to track changes for. By default, changes to all tables are tracked.
  * `db` {string} Name of the database to track. This is useful when multiple databases have been added using [`ATTACH DATABASE`][]. **Default**: `'main'`.
* Returns: {Session} A session handle.

Creates and attaches a session to the database. This method is a wrapper around [`sqlite3session_create()`][] and [`sqlite3session_attach()`][].

### `database.applyChangeset(changeset[, options])`

<!-- YAML
added:
  - v23.3.0
  - v22.12.0
-->

* `changeset` {Uint8Array} A binary changeset or patchset.
* `options` {Object} The configuration options for how the changes will be applied.
  * `filter` {Function} Skip changes that, when targeted table name is supplied to this function, return a truthy value.
    By default, all changes are attempted.
  * `onConflict` {Function} A function that determines how to handle conflicts. The function receives one argument,
    which can be one of the following values:

    * `SQLITE_CHANGESET_DATA`: A `DELETE` or `UPDATE` change does not contain the expected "before" values.
    * `SQLITE_CHANGESET_NOTFOUND`: A row matching the primary key of the `DELETE` or `UPDATE` change does not exist.
    * `SQLITE_CHANGESET_CONFLICT`: An `INSERT` change results in a duplicate primary key.
    * `SQLITE_CHANGESET_FOREIGN_KEY`: Applying a change would result in a foreign key violation.
    * `SQLITE_CHANGESET_CONSTRAINT`: Applying a change results in a `UNIQUE`, `CHECK`, or `NOT NULL` constraint
      violation.

    The function should return one of the following values:

    * `SQLITE_CHANGESET_OMIT`: Omit conflicting changes.
    * `SQLITE_CHANGESET_REPLACE`: Replace existing values with conflicting changes (only valid with
      `SQLITE_CHANGESET_DATA` or `SQLITE_CHANGESET_CONFLICT` conflicts).
    * `SQLITE_CHANGESET_ABORT`: Abort on conflict and roll back the database.

    When an error is thrown in the conflict handler or when any other value is returned from the handler,
    applying the changeset is aborted and the database is rolled back.

    **Default**: A function that returns `SQLITE_CHANGESET_ABORT`.
* Returns: {boolean} Whether the changeset was applied succesfully without being aborted.

An exception is thrown if the database is not
open. This method is a wrapper around [`sqlite3changeset_apply()`][].

```js
const sourceDb = new DatabaseSync(':memory:');
const targetDb = new DatabaseSync(':memory:');

sourceDb.exec('CREATE TABLE data(key INTEGER PRIMARY KEY, value TEXT)');
targetDb.exec('CREATE TABLE data(key INTEGER PRIMARY KEY, value TEXT)');

const session = sourceDb.createSession();

const insert = sourceDb.prepare('INSERT INTO data (key, value) VALUES (?, ?)');
insert.run(1, 'hello');
insert.run(2, 'world');

const changeset = session.changeset();
targetDb.applyChangeset(changeset);
// Now that the changeset has been applied, targetDb contains the same data as sourceDb.
```

## Class: `Session`

<!-- YAML
added:
  - v23.3.0
  - v22.12.0
-->

### `session.changeset()`

<!-- YAML
added:
  - v23.3.0
  - v22.12.0
-->

* Returns: {Uint8Array} Binary changeset that can be applied to other databases.

Retrieves a changeset containing all changes since the changeset was created. Can be called multiple times.
An exception is thrown if the database or the session is not open. This method is a wrapper around [`sqlite3session_changeset()`][].

### `session.patchset()`

<!-- YAML
added:
  - v23.3.0
  - v22.12.0
-->

* Returns: {Uint8Array} Binary patchset that can be applied to other databases.

Similar to the method above, but generates a more compact patchset. See [Changesets and Patchsets][]
in the documentation of SQLite. An exception is thrown if the database or the session is not open. This method is a
wrapper around [`sqlite3session_patchset()`][].

### `session.close()`.

Closes the session. An exception is thrown if the database or the session is not open. This method is a
wrapper around [`sqlite3session_delete()`][].

## Class: `StatementSync`

<!-- YAML
added: v22.5.0
-->

This class represents a single [prepared statement][]. This class cannot be
instantiated via its constructor. Instead, instances are created via the
`database.prepare()` method. All APIs exposed by this class execute
synchronously.

A prepared statement is an efficient binary representation of the SQL used to
create it. Prepared statements are parameterizable, and can be invoked multiple
times with different bound values. Parameters also offer protection against
[SQL injection][] attacks. For these reasons, prepared statements are preferred
over hand-crafted SQL strings when handling user input.

### `statement.all([namedParameters][, ...anonymousParameters])`

<!-- YAML
added: v22.5.0
changes:
  - version: v23.7.0
    pr-url: https://github.com/nodejs/node/pull/56385
    description: Add support for `DataView` and typed array objects for `anonymousParameters`.
-->

* `namedParameters` {Object} An optional object used to bind named parameters.
  The keys of this object are used to configure the mapping.
* `...anonymousParameters` {null|number|bigint|string|Buffer|TypedArray|DataView} Zero or
  more values to bind to anonymous parameters.
* Returns: {Array} An array of objects. Each object corresponds to a row
  returned by executing the prepared statement. The keys and values of each
  object correspond to the column names and values of the row.

This method executes a prepared statement and returns all results as an array of
objects. If the prepared statement does not return any results, this method
returns an empty array. The prepared statement [parameters are bound][] using
the values in `namedParameters` and `anonymousParameters`.

### `statement.expandedSQL`

<!-- YAML
added: v22.5.0
-->

* {string} The source SQL expanded to include parameter values.

The source SQL text of the prepared statement with parameter
placeholders replaced by the values that were used during the most recent
execution of this prepared statement. This property is a wrapper around
[`sqlite3_expanded_sql()`][].

### `statement.get([namedParameters][, ...anonymousParameters])`

<!-- YAML
added: v22.5.0
changes:
  - version: v23.7.0
    pr-url: https://github.com/nodejs/node/pull/56385
    description: Add support for `DataView` and typed array objects for `anonymousParameters`.
-->

* `namedParameters` {Object} An optional object used to bind named parameters.
  The keys of this object are used to configure the mapping.
* `...anonymousParameters` {null|number|bigint|string|Buffer|TypedArray|DataView} Zero or
  more values to bind to anonymous parameters.
* Returns: {Object|undefined} An object corresponding to the first row returned
  by executing the prepared statement. The keys and values of the object
  correspond to the column names and values of the row. If no rows were returned
  from the database then this method returns `undefined`.

This method executes a prepared statement and returns the first result as an
object. If the prepared statement does not return any results, this method
returns `undefined`. The prepared statement [parameters are bound][] using the
values in `namedParameters` and `anonymousParameters`.

### `statement.iterate([namedParameters][, ...anonymousParameters])`

<!-- YAML
added:
  - v23.4.0
  - v22.13.0
changes:
  - version: v23.7.0
    pr-url: https://github.com/nodejs/node/pull/56385
    description: Add support for `DataView` and typed array objects for `anonymousParameters`.
-->

* `namedParameters` {Object} An optional object used to bind named parameters.
  The keys of this object are used to configure the mapping.
* `...anonymousParameters` {null|number|bigint|string|Buffer|TypedArray|DataView} Zero or
  more values to bind to anonymous parameters.
* Returns: {Iterator} An iterable iterator of objects. Each object corresponds to a row
  returned by executing the prepared statement. The keys and values of each
  object correspond to the column names and values of the row.

This method executes a prepared statement and returns an iterator of
objects. If the prepared statement does not return any results, this method
returns an empty iterator. The prepared statement [parameters are bound][] using
the values in `namedParameters` and `anonymousParameters`.

### `statement.run([namedParameters][, ...anonymousParameters])`

<!-- YAML
added: v22.5.0
changes:
  - version: v23.7.0
    pr-url: https://github.com/nodejs/node/pull/56385
    description: Add support for `DataView` and typed array objects for `anonymousParameters`.
-->

* `namedParameters` {Object} An optional object used to bind named parameters.
  The keys of this object are used to configure the mapping.
* `...anonymousParameters` {null|number|bigint|string|Buffer|TypedArray|DataView} Zero or
  more values to bind to anonymous parameters.
* Returns: {Object}
  * `changes`: {number|bigint} The number of rows modified, inserted, or deleted
    by the most recently completed `INSERT`, `UPDATE`, or `DELETE` statement.
    This field is either a number or a `BigInt` depending on the prepared
    statement's configuration. This property is the result of
    [`sqlite3_changes64()`][].
  * `lastInsertRowid`: {number|bigint} The most recently inserted rowid. This
    field is either a number or a `BigInt` depending on the prepared statement's
    configuration. This property is the result of
    [`sqlite3_last_insert_rowid()`][].

This method executes a prepared statement and returns an object summarizing the
resulting changes. The prepared statement [parameters are bound][] using the
values in `namedParameters` and `anonymousParameters`.

### `statement.setAllowBareNamedParameters(enabled)`

<!-- YAML
added: v22.5.0
-->

* `enabled` {boolean} Enables or disables support for binding named parameters
  without the prefix character.

The names of SQLite parameters begin with a prefix character. By default,
`node:sqlite` requires that this prefix character is present when binding
parameters. However, with the exception of dollar sign character, these
prefix characters also require extra quoting when used in object keys.

To improve ergonomics, this method can be used to also allow bare named
parameters, which do not require the prefix character in JavaScript code. There
are several caveats to be aware of when enabling bare named parameters:

* The prefix character is still required in SQL.
* The prefix character is still allowed in JavaScript. In fact, prefixed names
  will have slightly better binding performance.
* Using ambiguous named parameters, such as `$k` and `@k`, in the same prepared
  statement will result in an exception as it cannot be determined how to bind
  a bare name.

### `statement.setReadBigInts(enabled)`

<!-- YAML
added: v22.5.0
-->

* `enabled` {boolean} Enables or disables the use of `BigInt`s when reading
  `INTEGER` fields from the database.

When reading from the database, SQLite `INTEGER`s are mapped to JavaScript
numbers by default. However, SQLite `INTEGER`s can store values larger than
JavaScript numbers are capable of representing. In such cases, this method can
be used to read `INTEGER` data using JavaScript `BigInt`s. This method has no
impact on database write operations where numbers and `BigInt`s are both
supported at all times.

### `statement.sourceSQL`

<!-- YAML
added: v22.5.0
-->

* {string} The source SQL used to create this prepared statement.

The source SQL text of the prepared statement. This property is a
wrapper around [`sqlite3_sql()`][].

### Type conversion between JavaScript and SQLite

When Node.js writes to or reads from SQLite it is necessary to convert between
JavaScript data types and SQLite's [data types][]. Because JavaScript supports
more data types than SQLite, only a subset of JavaScript types are supported.
Attempting to write an unsupported data type to SQLite will result in an
exception.

| SQLite    | JavaScript                 |
| --------- | -------------------------- |
| `NULL`    | {null}                     |
| `INTEGER` | {number} or {bigint}       |
| `REAL`    | {number}                   |
| `TEXT`    | {string}                   |
| `BLOB`    | {TypedArray} or {DataView} |

## `sqlite.constants`

<!-- YAML
added:
  - v23.5.0
  - v22.13.0
-->

* {Object}

An object containing commonly used constants for SQLite operations.

### SQLite constants

The following constants are exported by the `sqlite.constants` object.

#### Conflict resolution constants

One of the following constants is available as an argument to the `onConflict`
conflict resolution handler passed to [`database.applyChangeset()`][]. See also
[Constants Passed To The Conflict Handler][] in the SQLite documentation.

<table>
  <tr>
    <th>Constant</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>SQLITE_CHANGESET_DATA</code></td>
    <td>The conflict handler is invoked with this constant when processing a DELETE or UPDATE change if a row with the required PRIMARY KEY fields is present in the database, but one or more other (non primary-key) fields modified by the update do not contain the expected "before" values.</td>
  </tr>
  <tr>
    <td><code>SQLITE_CHANGESET_NOTFOUND</code></td>
    <td>The conflict handler is invoked with this constant when processing a DELETE or UPDATE change if a row with the required PRIMARY KEY fields is not present in the database.</td>
  </tr>
  <tr>
    <td><code>SQLITE_CHANGESET_CONFLICT</code></td>
    <td>This constant is passed to the conflict handler while processing an INSERT change if the operation would result in duplicate primary key values.</td>
  </tr>
  <tr>
    <td><code>SQLITE_CHANGESET_CONSTRAINT</code></td>
    <td>If foreign key handling is enabled, and applying a changeset leaves the database in a state containing foreign key violations, the conflict handler is invoked with this constant exactly once before the changeset is committed. If the conflict handler returns <code>SQLITE_CHANGESET_OMIT</code>, the changes, including those that caused the foreign key constraint violation, are committed. Or, if it returns <code>SQLITE_CHANGESET_ABORT</code>, the changeset is rolled back.</td>
  </tr>
  <tr>
    <td><code>SQLITE_CHANGESET_FOREIGN_KEY</code></td>
    <td>If any other constraint violation occurs while applying a change (i.e. a UNIQUE, CHECK or NOT NULL constraint), the conflict handler is invoked with this constant.</td>
  </tr>
</table>

One of the following constants must be returned from the `onConflict` conflict
resolution handler passed to [`database.applyChangeset()`][]. See also
[Constants Returned From The Conflict Handler][] in the SQLite documentation.

<table>
  <tr>
    <th>Constant</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>SQLITE_CHANGESET_OMIT</code></td>
    <td>Conflicting changes are omitted.</td>
  </tr>
  <tr>
    <td><code>SQLITE_CHANGESET_REPLACE</code></td>
    <td>Conflicting changes replace existing values. Note that this value can only be returned when the type of conflict is either <code>SQLITE_CHANGESET_DATA</code> or <code>SQLITE_CHANGESET_CONFLICT</code>.</td>
  </tr>
  <tr>
    <td><code>SQLITE_CHANGESET_ABORT</code></td>
    <td>Abort when a change encounters a conflict and roll back database.</td>
  </tr>
</table>

[Changesets and Patchsets]: https://www.sqlite.org/sessionintro.html#changesets_and_patchsets
[Constants Passed To The Conflict Handler]: https://www.sqlite.org/session/c_changeset_conflict.html
[Constants Returned From The Conflict Handler]: https://www.sqlite.org/session/c_changeset_abort.html
[SQL injection]: https://en.wikipedia.org/wiki/SQL_injection
[Type conversion between JavaScript and SQLite]: #type-conversion-between-javascript-and-sqlite
[`ATTACH DATABASE`]: https://www.sqlite.org/lang_attach.html
[`PRAGMA foreign_keys`]: https://www.sqlite.org/pragma.html#pragma_foreign_keys
[`SQLITE_DETERMINISTIC`]: https://www.sqlite.org/c3ref/c_deterministic.html
[`SQLITE_DIRECTONLY`]: https://www.sqlite.org/c3ref/c_deterministic.html
[`SQLITE_MAX_FUNCTION_ARG`]: https://www.sqlite.org/limits.html#max_function_arg
[`database.applyChangeset()`]: #databaseapplychangesetchangeset-options
[`sqlite3_changes64()`]: https://www.sqlite.org/c3ref/changes.html
[`sqlite3_close_v2()`]: https://www.sqlite.org/c3ref/close.html
[`sqlite3_create_function_v2()`]: https://www.sqlite.org/c3ref/create_function.html
[`sqlite3_exec()`]: https://www.sqlite.org/c3ref/exec.html
[`sqlite3_expanded_sql()`]: https://www.sqlite.org/c3ref/expanded_sql.html
[`sqlite3_last_insert_rowid()`]: https://www.sqlite.org/c3ref/last_insert_rowid.html
[`sqlite3_load_extension()`]: https://www.sqlite.org/c3ref/load_extension.html
[`sqlite3_prepare_v2()`]: https://www.sqlite.org/c3ref/prepare.html
[`sqlite3_sql()`]: https://www.sqlite.org/c3ref/expanded_sql.html
[`sqlite3changeset_apply()`]: https://www.sqlite.org/session/sqlite3changeset_apply.html
[`sqlite3session_attach()`]: https://www.sqlite.org/session/sqlite3session_attach.html
[`sqlite3session_changeset()`]: https://www.sqlite.org/session/sqlite3session_changeset.html
[`sqlite3session_create()`]: https://www.sqlite.org/session/sqlite3session_create.html
[`sqlite3session_delete()`]: https://www.sqlite.org/session/sqlite3session_delete.html
[`sqlite3session_patchset()`]: https://www.sqlite.org/session/sqlite3session_patchset.html
[connection]: https://www.sqlite.org/c3ref/sqlite3.html
[data types]: https://www.sqlite.org/datatype3.html
[double-quoted string literals]: https://www.sqlite.org/quirks.html#dblquote
[in memory]: https://www.sqlite.org/inmemorydb.html
[parameters are bound]: https://www.sqlite.org/c3ref/bind_blob.html
[prepared statement]: https://www.sqlite.org/c3ref/stmt.html

# Internationalization support

<!--introduced_in=v8.2.0-->

<!-- type=misc -->

Node.js has many features that make it easier to write internationalized
programs. Some of them are:

* Locale-sensitive or Unicode-aware functions in the [ECMAScript Language
  Specification][ECMA-262]:
  * [`String.prototype.normalize()`][]
  * [`String.prototype.toLowerCase()`][]
  * [`String.prototype.toUpperCase()`][]
* All functionality described in the [ECMAScript Internationalization API
  Specification][ECMA-402] (aka ECMA-402):
  * [`Intl`][] object
  * Locale-sensitive methods like [`String.prototype.localeCompare()`][] and
    [`Date.prototype.toLocaleString()`][]
* The [WHATWG URL parser][]'s [internationalized domain names][] (IDNs) support
* [`require('node:buffer').transcode()`][]
* More accurate [REPL][] line editing
* [`require('node:util').TextDecoder`][]
* [`RegExp` Unicode Property Escapes][]

Node.js and the underlying V8 engine use
[International Components for Unicode (ICU)][ICU] to implement these features
in native C/C++ code. The full ICU data set is provided by Node.js by default.
However, due to the size of the ICU data file, several
options are provided for customizing the ICU data set either when
building or running Node.js.

## Options for building Node.js

To control how ICU is used in Node.js, four `configure` options are available
during compilation. Additional details on how to compile Node.js are documented
in [BUILDING.md][].

* `--with-intl=none`/`--without-intl`
* `--with-intl=system-icu`
* `--with-intl=small-icu`
* `--with-intl=full-icu` (default)

An overview of available Node.js and JavaScript features for each `configure`
option:

| Feature                                  | `none`                            | `system-icu`                 | `small-icu`            | `full-icu` |
| ---------------------------------------- | --------------------------------- | ---------------------------- | ---------------------- | ---------- |
| [`String.prototype.normalize()`][]       | none (function is no-op)          | full                         | full                   | full       |
| `String.prototype.to*Case()`             | full                              | full                         | full                   | full       |
| [`Intl`][]                               | none (object does not exist)      | partial/full (depends on OS) | partial (English-only) | full       |
| [`String.prototype.localeCompare()`][]   | partial (not locale-aware)        | full                         | full                   | full       |
| `String.prototype.toLocale*Case()`       | partial (not locale-aware)        | full                         | full                   | full       |
| [`Number.prototype.toLocaleString()`][]  | partial (not locale-aware)        | partial/full (depends on OS) | partial (English-only) | full       |
| `Date.prototype.toLocale*String()`       | partial (not locale-aware)        | partial/full (depends on OS) | partial (English-only) | full       |
| [Legacy URL Parser][]                    | partial (no IDN support)          | full                         | full                   | full       |
| [WHATWG URL Parser][]                    | partial (no IDN support)          | full                         | full                   | full       |
| [`require('node:buffer').transcode()`][] | none (function does not exist)    | full                         | full                   | full       |
| [REPL][]                                 | partial (inaccurate line editing) | full                         | full                   | full       |
| [`require('node:util').TextDecoder`][]   | partial (basic encodings support) | partial/full (depends on OS) | partial (Unicode-only) | full       |
| [`RegExp` Unicode Property Escapes][]    | none (invalid `RegExp` error)     | full                         | full                   | full       |

The "(not locale-aware)" designation denotes that the function carries out its
operation just like the non-`Locale` version of the function, if one
exists. For example, under `none` mode, `Date.prototype.toLocaleString()`'s
operation is identical to that of `Date.prototype.toString()`.

### Disable all internationalization features (`none`)

If this option is chosen, ICU is disabled and most internationalization
features mentioned above will be **unavailable** in the resulting `node` binary.

### Build with a pre-installed ICU (`system-icu`)

Node.js can link against an ICU build already installed on the system. In fact,
most Linux distributions already come with ICU installed, and this option would
make it possible to reuse the same set of data used by other components in the
OS.

Functionalities that only require the ICU library itself, such as
[`String.prototype.normalize()`][] and the [WHATWG URL parser][], are fully
supported under `system-icu`. Features that require ICU locale data in
addition, such as [`Intl.DateTimeFormat`][] _may_ be fully or partially
supported, depending on the completeness of the ICU data installed on the
system.

### Embed a limited set of ICU data (`small-icu`)

This option makes the resulting binary link against the ICU library statically,
and includes a subset of ICU data (typically only the English locale) within
the `node` executable.

Functionalities that only require the ICU library itself, such as
[`String.prototype.normalize()`][] and the [WHATWG URL parser][], are fully
supported under `small-icu`. Features that require ICU locale data in addition,
such as [`Intl.DateTimeFormat`][], generally only work with the English locale:

```js
const january = new Date(9e8);
const english = new Intl.DateTimeFormat('en', { month: 'long' });
const spanish = new Intl.DateTimeFormat('es', { month: 'long' });

console.log(english.format(january));
// Prints "January"
console.log(spanish.format(january));
// Prints either "M01" or "January" on small-icu, depending on the user’s default locale
// Should print "enero"
```

This mode provides a balance between features and binary size.

#### Providing ICU data at runtime

If the `small-icu` option is used, one can still provide additional locale data
at runtime so that the JS methods would work for all ICU locales. Assuming the
data file is stored at `/runtime/directory/with/dat/file`, it can be made
available to ICU through either:

* The `--with-icu-default-data-dir` configure option:

  ```bash
  ./configure --with-icu-default-data-dir=/runtime/directory/with/dat/file --with-intl=small-icu
  ```

  This only embeds the default data directory path into the binary.
  The actual data file is going to be loaded at runtime from this directory
  path.

* The [`NODE_ICU_DATA`][] environment variable:

  ```bash
  env NODE_ICU_DATA=/runtime/directory/with/dat/file node
  ```

* The [`--icu-data-dir`][] CLI parameter:

  ```bash
  node --icu-data-dir=/runtime/directory/with/dat/file
  ```

When more than one of them is specified, the `--icu-data-dir` CLI parameter has
the highest precedence, then the `NODE_ICU_DATA`  environment variable, then
the `--with-icu-default-data-dir` configure option.

ICU is able to automatically find and load a variety of data formats, but the
data must be appropriate for the ICU version, and the file correctly named.
The most common name for the data file is `icudtX[bl].dat`, where `X` denotes
the intended ICU version, and `b` or `l` indicates the system's endianness.
Node.js would fail to load if the expected data file cannot be read from the
specified directory. The name of the data file corresponding to the current
Node.js version can be computed with:

```js
`icudt${process.versions.icu.split('.')[0]}${os.endianness()[0].toLowerCase()}.dat`;
```

Check ["ICU Data"][] article in the ICU User Guide for other supported formats
and more details on ICU data in general.

The [full-icu][] npm module can greatly simplify ICU data installation by
detecting the ICU version of the running `node` executable and downloading the
appropriate data file. After installing the module through `npm i full-icu`,
the data file will be available at `./node_modules/full-icu`. This path can be
then passed either to `NODE_ICU_DATA` or `--icu-data-dir` as shown above to
enable full `Intl` support.

### Embed the entire ICU (`full-icu`)

This option makes the resulting binary link against ICU statically and include
a full set of ICU data. A binary created this way has no further external
dependencies and supports all locales, but might be rather large. This is
the default behavior if no `--with-intl` flag is passed. The official binaries
are also built in this mode.

## Detecting internationalization support

To verify that ICU is enabled at all (`system-icu`, `small-icu`, or
`full-icu`), simply checking the existence of `Intl` should suffice:

```js
const hasICU = typeof Intl === 'object';
```

Alternatively, checking for `process.versions.icu`, a property defined only
when ICU is enabled, works too:

```js
const hasICU = typeof process.versions.icu === 'string';
```

To check for support for a non-English locale (i.e. `full-icu` or
`system-icu`), [`Intl.DateTimeFormat`][] can be a good distinguishing factor:

```js
const hasFullICU = (() => {
  try {
    const january = new Date(9e8);
    const spanish = new Intl.DateTimeFormat('es', { month: 'long' });
    return spanish.format(january) === 'enero';
  } catch (err) {
    return false;
  }
})();
```

For more verbose tests for `Intl` support, the following resources may be found
to be helpful:

* [btest402][]: Generally used to check whether Node.js with `Intl` support is
  built correctly.
* [Test262][]: ECMAScript's official conformance test suite includes a section
  dedicated to ECMA-402.

["ICU Data"]: http://userguide.icu-project.org/icudata
[BUILDING.md]: https://github.com/nodejs/node/blob/HEAD/BUILDING.md
[ECMA-262]: https://tc39.github.io/ecma262/
[ECMA-402]: https://tc39.github.io/ecma402/
[ICU]: http://site.icu-project.org/
[Legacy URL parser]: url.md#legacy-url-api
[REPL]: repl.md#repl
[Test262]: https://github.com/tc39/test262/tree/HEAD/test/intl402
[WHATWG URL parser]: url.md#the-whatwg-url-api
[`--icu-data-dir`]: cli.md#--icu-data-dirfile
[`Date.prototype.toLocaleString()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString
[`Intl.DateTimeFormat`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat
[`Intl`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl
[`NODE_ICU_DATA`]: cli.md#node_icu_datafile
[`Number.prototype.toLocaleString()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString
[`RegExp` Unicode Property Escapes]: https://github.com/tc39/proposal-regexp-unicode-property-escapes
[`String.prototype.localeCompare()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare
[`String.prototype.normalize()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/normalize
[`String.prototype.toLowerCase()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase
[`String.prototype.toUpperCase()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase
[`require('node:buffer').transcode()`]: buffer.md#buffertranscodesource-fromenc-toenc
[`require('node:util').TextDecoder`]: util.md#class-utiltextdecoder
[btest402]: https://github.com/srl295/btest402
[full-icu]: https://www.npmjs.com/package/full-icu
[internationalized domain names]: https://en.wikipedia.org/wiki/Internationalized_domain_name

# Readline

<!--introduced_in=v0.10.0-->

> Stability: 2 - Stable

<!-- source_link=lib/readline.js -->

The `node:readline` module provides an interface for reading data from a
[Readable][] stream (such as [`process.stdin`][]) one line at a time.

To use the promise-based APIs:

```mjs
import * as readline from 'node:readline/promises';
```

```cjs
const readline = require('node:readline/promises');
```

To use the callback and sync APIs:

```mjs
import * as readline from 'node:readline';
```

```cjs
const readline = require('node:readline');
```

The following simple example illustrates the basic use of the `node:readline`
module.

```mjs
import * as readline from 'node:readline/promises';
import { stdin as input, stdout as output } from 'node:process';

const rl = readline.createInterface({ input, output });

const answer = await rl.question('What do you think of Node.js? ');

console.log(`Thank you for your valuable feedback: ${answer}`);

rl.close();
```

```cjs
const readline = require('node:readline');
const { stdin: input, stdout: output } = require('node:process');

const rl = readline.createInterface({ input, output });

rl.question('What do you think of Node.js? ', (answer) => {
  // TODO: Log the answer in a database
  console.log(`Thank you for your valuable feedback: ${answer}`);

  rl.close();
});
```

Once this code is invoked, the Node.js application will not terminate until the
`readline.Interface` is closed because the interface waits for data to be
received on the `input` stream.

<a id='readline_class_interface'></a>

## Class: `InterfaceConstructor`

<!-- YAML
added: v0.1.104
-->

* Extends: {EventEmitter}

Instances of the `InterfaceConstructor` class are constructed using the
`readlinePromises.createInterface()` or `readline.createInterface()` method.
Every instance is associated with a single `input` [Readable][] stream and a
single `output` [Writable][] stream.
The `output` stream is used to print prompts for user input that arrives on,
and is read from, the `input` stream.

### Event: `'close'`

<!-- YAML
added: v0.1.98
-->

The `'close'` event is emitted when one of the following occur:

* The `rl.close()` method is called and the `InterfaceConstructor` instance has
  relinquished control over the `input` and `output` streams;
* The `input` stream receives its `'end'` event;
* The `input` stream receives <kbd>Ctrl</kbd>+<kbd>D</kbd> to signal
  end-of-transmission (EOT);
* The `input` stream receives <kbd>Ctrl</kbd>+<kbd>C</kbd> to signal `SIGINT`
  and there is no `'SIGINT'` event listener registered on the
  `InterfaceConstructor` instance.

The listener function is called without passing any arguments.

The `InterfaceConstructor` instance is finished once the `'close'` event is
emitted.

### Event: `'line'`

<!-- YAML
added: v0.1.98
-->

The `'line'` event is emitted whenever the `input` stream receives an
end-of-line input (`\n`, `\r`, or `\r\n`). This usually occurs when the user
presses <kbd>Enter</kbd> or <kbd>Return</kbd>.

The `'line'` event is also emitted if new data has been read from a stream and
that stream ends without a final end-of-line marker.

The listener function is called with a string containing the single line of
received input.

```js
rl.on('line', (input) => {
  console.log(`Received: ${input}`);
});
```

### Event: `'history'`

<!-- YAML
added:
  - v15.8.0
  - v14.18.0
-->

The `'history'` event is emitted whenever the history array has changed.

The listener function is called with an array containing the history array.
It will reflect all changes, added lines and removed lines due to
`historySize` and `removeHistoryDuplicates`.

The primary purpose is to allow a listener to persist the history.
It is also possible for the listener to change the history object. This
could be useful to prevent certain lines to be added to the history, like
a password.

```js
rl.on('history', (history) => {
  console.log(`Received: ${history}`);
});
```

### Event: `'pause'`

<!-- YAML
added: v0.7.5
-->

The `'pause'` event is emitted when one of the following occur:

* The `input` stream is paused.
* The `input` stream is not paused and receives the `'SIGCONT'` event. (See
  events [`'SIGTSTP'`][] and [`'SIGCONT'`][].)

The listener function is called without passing any arguments.

```js
rl.on('pause', () => {
  console.log('Readline paused.');
});
```

### Event: `'resume'`

<!-- YAML
added: v0.7.5
-->

The `'resume'` event is emitted whenever the `input` stream is resumed.

The listener function is called without passing any arguments.

```js
rl.on('resume', () => {
  console.log('Readline resumed.');
});
```

### Event: `'SIGCONT'`

<!-- YAML
added: v0.7.5
-->

The `'SIGCONT'` event is emitted when a Node.js process previously moved into
the background using <kbd>Ctrl</kbd>+<kbd>Z</kbd> (i.e. `SIGTSTP`) is then
brought back to the foreground using fg(1p).

If the `input` stream was paused _before_ the `SIGTSTP` request, this event will
not be emitted.

The listener function is invoked without passing any arguments.

```js
rl.on('SIGCONT', () => {
  // `prompt` will automatically resume the stream
  rl.prompt();
});
```

The `'SIGCONT'` event is _not_ supported on Windows.

### Event: `'SIGINT'`

<!-- YAML
added: v0.3.0
-->

The `'SIGINT'` event is emitted whenever the `input` stream receives
a <kbd>Ctrl+C</kbd> input, known typically as `SIGINT`. If there are no
`'SIGINT'` event listeners registered when the `input` stream receives a
`SIGINT`, the `'pause'` event will be emitted.

The listener function is invoked without passing any arguments.

```js
rl.on('SIGINT', () => {
  rl.question('Are you sure you want to exit? ', (answer) => {
    if (answer.match(/^y(es)?$/i)) rl.pause();
  });
});
```

### Event: `'SIGTSTP'`

<!-- YAML
added: v0.7.5
-->

The `'SIGTSTP'` event is emitted when the `input` stream receives
a <kbd>Ctrl</kbd>+<kbd>Z</kbd> input, typically known as `SIGTSTP`. If there are
no `'SIGTSTP'` event listeners registered when the `input` stream receives a
`SIGTSTP`, the Node.js process will be sent to the background.

When the program is resumed using fg(1p), the `'pause'` and `'SIGCONT'` events
will be emitted. These can be used to resume the `input` stream.

The `'pause'` and `'SIGCONT'` events will not be emitted if the `input` was
paused before the process was sent to the background.

The listener function is invoked without passing any arguments.

```js
rl.on('SIGTSTP', () => {
  // This will override SIGTSTP and prevent the program from going to the
  // background.
  console.log('Caught SIGTSTP.');
});
```

The `'SIGTSTP'` event is _not_ supported on Windows.

### `rl.close()`

<!-- YAML
added: v0.1.98
-->

The `rl.close()` method closes the `InterfaceConstructor` instance and
relinquishes control over the `input` and `output` streams. When called,
the `'close'` event will be emitted.

Calling `rl.close()` does not immediately stop other events (including `'line'`)
from being emitted by the `InterfaceConstructor` instance.

### `rl.pause()`

<!-- YAML
added: v0.3.4
-->

The `rl.pause()` method pauses the `input` stream, allowing it to be resumed
later if necessary.

Calling `rl.pause()` does not immediately pause other events (including
`'line'`) from being emitted by the `InterfaceConstructor` instance.

### `rl.prompt([preserveCursor])`

<!-- YAML
added: v0.1.98
-->

* `preserveCursor` {boolean} If `true`, prevents the cursor placement from
  being reset to `0`.

The `rl.prompt()` method writes the `InterfaceConstructor` instances configured
`prompt` to a new line in `output` in order to provide a user with a new
location at which to provide input.

When called, `rl.prompt()` will resume the `input` stream if it has been
paused.

If the `InterfaceConstructor` was created with `output` set to `null` or
`undefined` the prompt is not written.

### `rl.resume()`

<!-- YAML
added: v0.3.4
-->

The `rl.resume()` method resumes the `input` stream if it has been paused.

### `rl.setPrompt(prompt)`

<!-- YAML
added: v0.1.98
-->

* `prompt` {string}

The `rl.setPrompt()` method sets the prompt that will be written to `output`
whenever `rl.prompt()` is called.

### `rl.getPrompt()`

<!-- YAML
added:
  - v15.3.0
  - v14.17.0
-->

* Returns: {string} the current prompt string

The `rl.getPrompt()` method returns the current prompt used by `rl.prompt()`.

### `rl.write(data[, key])`

<!-- YAML
added: v0.1.98
-->

* `data` {string}
* `key` {Object}
  * `ctrl` {boolean} `true` to indicate the <kbd>Ctrl</kbd> key.
  * `meta` {boolean} `true` to indicate the <kbd>Meta</kbd> key.
  * `shift` {boolean} `true` to indicate the <kbd>Shift</kbd> key.
  * `name` {string} The name of the a key.

The `rl.write()` method will write either `data` or a key sequence identified
by `key` to the `output`. The `key` argument is supported only if `output` is
a [TTY][] text terminal. See [TTY keybindings][] for a list of key
combinations.

If `key` is specified, `data` is ignored.

When called, `rl.write()` will resume the `input` stream if it has been
paused.

If the `InterfaceConstructor` was created with `output` set to `null` or
`undefined` the `data` and `key` are not written.

```js
rl.write('Delete this!');
// Simulate Ctrl+U to delete the line written previously
rl.write(null, { ctrl: true, name: 'u' });
```

The `rl.write()` method will write the data to the `readline` `Interface`'s
`input` _as if it were provided by the user_.

### `rl[Symbol.asyncIterator]()`

<!-- YAML
added:
 - v11.4.0
 - v10.16.0
changes:
  - version:
     - v11.14.0
     - v10.17.0
    pr-url: https://github.com/nodejs/node/pull/26989
    description: Symbol.asyncIterator support is no longer experimental.
-->

* Returns: {AsyncIterator}

Create an `AsyncIterator` object that iterates through each line in the input
stream as a string. This method allows asynchronous iteration of
`InterfaceConstructor` objects through `for await...of` loops.

Errors in the input stream are not forwarded.

If the loop is terminated with `break`, `throw`, or `return`,
[`rl.close()`][] will be called. In other words, iterating over a
`InterfaceConstructor` will always consume the input stream fully.

Performance is not on par with the traditional `'line'` event API. Use `'line'`
instead for performance-sensitive applications.

```js
async function processLineByLine() {
  const rl = readline.createInterface({
    // ...
  });

  for await (const line of rl) {
    // Each line in the readline input will be successively available here as
    // `line`.
  }
}
```

`readline.createInterface()` will start to consume the input stream once
invoked. Having asynchronous operations between interface creation and
asynchronous iteration may result in missed lines.

### `rl.line`

<!-- YAML
added: v0.1.98
changes:
  - version:
      - v15.8.0
      - v14.18.0
    pr-url: https://github.com/nodejs/node/pull/33676
    description: Value will always be a string, never undefined.
-->

* {string}

The current input data being processed by node.

This can be used when collecting input from a TTY stream to retrieve the
current value that has been processed thus far, prior to the `line` event
being emitted. Once the `line` event has been emitted, this property will
be an empty string.

Be aware that modifying the value during the instance runtime may have
unintended consequences if `rl.cursor` is not also controlled.

**If not using a TTY stream for input, use the [`'line'`][] event.**

One possible use case would be as follows:

```js
const values = ['lorem ipsum', 'dolor sit amet'];
const rl = readline.createInterface(process.stdin);
const showResults = debounce(() => {
  console.log(
    '\n',
    values.filter((val) => val.startsWith(rl.line)).join(' '),
  );
}, 300);
process.stdin.on('keypress', (c, k) => {
  showResults();
});
```

### `rl.cursor`

<!-- YAML
added: v0.1.98
-->

* {number|undefined}

The cursor position relative to `rl.line`.

This will track where the current cursor lands in the input string, when
reading input from a TTY stream. The position of cursor determines the
portion of the input string that will be modified as input is processed,
as well as the column where the terminal caret will be rendered.

### `rl.getCursorPos()`

<!-- YAML
added:
 - v13.5.0
 - v12.16.0
-->

* Returns: {Object}
  * `rows` {number} the row of the prompt the cursor currently lands on
  * `cols` {number} the screen column the cursor currently lands on

Returns the real position of the cursor in relation to the input
prompt + string. Long input (wrapping) strings, as well as multiple
line prompts are included in the calculations.

## Promises API

<!-- YAML
added: v17.0.0
-->

> Stability: 1 - Experimental

### Class: `readlinePromises.Interface`

<!-- YAML
added: v17.0.0
-->

* Extends: {readline.InterfaceConstructor}

Instances of the `readlinePromises.Interface` class are constructed using the
`readlinePromises.createInterface()` method. Every instance is associated with a
single `input` [Readable][] stream and a single `output` [Writable][] stream.
The `output` stream is used to print prompts for user input that arrives on,
and is read from, the `input` stream.

#### `rl.question(query[, options])`

<!-- YAML
added: v17.0.0
-->

* `query` {string} A statement or query to write to `output`, prepended to the
  prompt.
* `options` {Object}
  * `signal` {AbortSignal} Optionally allows the `question()` to be canceled
    using an `AbortSignal`.
* Returns: {Promise} A promise that is fulfilled with the user's
  input in response to the `query`.

The `rl.question()` method displays the `query` by writing it to the `output`,
waits for user input to be provided on `input`, then invokes the `callback`
function passing the provided input as the first argument.

When called, `rl.question()` will resume the `input` stream if it has been
paused.

If the `readlinePromises.Interface` was created with `output` set to `null` or
`undefined` the `query` is not written.

If the question is called after `rl.close()`, it returns a rejected promise.

Example usage:

```mjs
const answer = await rl.question('What is your favorite food? ');
console.log(`Oh, so your favorite food is ${answer}`);
```

Using an `AbortSignal` to cancel a question.

```mjs
const signal = AbortSignal.timeout(10_000);

signal.addEventListener('abort', () => {
  console.log('The food question timed out');
}, { once: true });

const answer = await rl.question('What is your favorite food? ', { signal });
console.log(`Oh, so your favorite food is ${answer}`);
```

### Class: `readlinePromises.Readline`

<!-- YAML
added: v17.0.0
-->

#### `new readlinePromises.Readline(stream[, options])`

<!-- YAML
added: v17.0.0
-->

* `stream` {stream.Writable} A [TTY][] stream.
* `options` {Object}
  * `autoCommit` {boolean} If `true`, no need to call `rl.commit()`.

#### `rl.clearLine(dir)`

<!-- YAML
added: v17.0.0
-->

* `dir` {integer}
  * `-1`: to the left from cursor
  * `1`: to the right from cursor
  * `0`: the entire line
* Returns: this

The `rl.clearLine()` method adds to the internal list of pending action an
action that clears current line of the associated `stream` in a specified
direction identified by `dir`.
Call `rl.commit()` to see the effect of this method, unless `autoCommit: true`
was passed to the constructor.

#### `rl.clearScreenDown()`

<!-- YAML
added: v17.0.0
-->

* Returns: this

The `rl.clearScreenDown()` method adds to the internal list of pending action an
action that clears the associated stream from the current position of the
cursor down.
Call `rl.commit()` to see the effect of this method, unless `autoCommit: true`
was passed to the constructor.

#### `rl.commit()`

<!-- YAML
added: v17.0.0
-->

* Returns: {Promise}

The `rl.commit()` method sends all the pending actions to the associated
`stream` and clears the internal list of pending actions.

#### `rl.cursorTo(x[, y])`

<!-- YAML
added: v17.0.0
-->

* `x` {integer}
* `y` {integer}
* Returns: this

The `rl.cursorTo()` method adds to the internal list of pending action an action
that moves cursor to the specified position in the associated `stream`.
Call `rl.commit()` to see the effect of this method, unless `autoCommit: true`
was passed to the constructor.

#### `rl.moveCursor(dx, dy)`

<!-- YAML
added: v17.0.0
-->

* `dx` {integer}
* `dy` {integer}
* Returns: this

The `rl.moveCursor()` method adds to the internal list of pending action an
action that moves the cursor _relative_ to its current position in the
associated `stream`.
Call `rl.commit()` to see the effect of this method, unless `autoCommit: true`
was passed to the constructor.

#### `rl.rollback()`

<!-- YAML
added: v17.0.0
-->

* Returns: this

The `rl.rollback` methods clears the internal list of pending actions without
sending it to the associated `stream`.

### `readlinePromises.createInterface(options)`

<!-- YAML
added: v17.0.0
-->

* `options` {Object}
  * `input` {stream.Readable} The [Readable][] stream to listen to. This option
    is _required_.
  * `output` {stream.Writable} The [Writable][] stream to write readline data
    to.
  * `completer` {Function} An optional function used for Tab autocompletion.
  * `terminal` {boolean} `true` if the `input` and `output` streams should be
    treated like a TTY, and have ANSI/VT100 escape codes written to it.
    **Default:** checking `isTTY` on the `output` stream upon instantiation.
  * `history` {string\[]} Initial list of history lines. This option makes sense
    only if `terminal` is set to `true` by the user or by an internal `output`
    check, otherwise the history caching mechanism is not initialized at all.
    **Default:** `[]`.
  * `historySize` {number} Maximum number of history lines retained. To disable
    the history set this value to `0`. This option makes sense only if
    `terminal` is set to `true` by the user or by an internal `output` check,
    otherwise the history caching mechanism is not initialized at all.
    **Default:** `30`.
  * `removeHistoryDuplicates` {boolean} If `true`, when a new input line added
    to the history list duplicates an older one, this removes the older line
    from the list. **Default:** `false`.
  * `prompt` {string} The prompt string to use. **Default:** `'> '`.
  * `crlfDelay` {number} If the delay between `\r` and `\n` exceeds
    `crlfDelay` milliseconds, both `\r` and `\n` will be treated as separate
    end-of-line input. `crlfDelay` will be coerced to a number no less than
    `100`. It can be set to `Infinity`, in which case `\r` followed by `\n`
    will always be considered a single newline (which may be reasonable for
    [reading files][] with `\r\n` line delimiter). **Default:** `100`.
  * `escapeCodeTimeout` {number} The duration `readlinePromises` will wait for a
    character (when reading an ambiguous key sequence in milliseconds one that
    can both form a complete key sequence using the input read so far and can
    take additional input to complete a longer key sequence).
    **Default:** `500`.
  * `tabSize` {integer} The number of spaces a tab is equal to (minimum 1).
    **Default:** `8`.
* Returns: {readlinePromises.Interface}

The `readlinePromises.createInterface()` method creates a new `readlinePromises.Interface`
instance.

```mjs
import { createInterface } from 'node:readline/promises';
import { stdin, stdout } from 'node:process';
const rl = createInterface({
  input: stdin,
  output: stdout,
});
```

```cjs
const { createInterface } = require('node:readline/promises');
const rl = createInterface({
  input: process.stdin,
  output: process.stdout,
});
```

Once the `readlinePromises.Interface` instance is created, the most common case
is to listen for the `'line'` event:

```js
rl.on('line', (line) => {
  console.log(`Received: ${line}`);
});
```

If `terminal` is `true` for this instance then the `output` stream will get
the best compatibility if it defines an `output.columns` property and emits
a `'resize'` event on the `output` if or when the columns ever change
([`process.stdout`][] does this automatically when it is a TTY).

#### Use of the `completer` function

The `completer` function takes the current line entered by the user
as an argument, and returns an `Array` with 2 entries:

* An `Array` with matching entries for the completion.
* The substring that was used for the matching.

For instance: `[[substr1, substr2, ...], originalsubstring]`.

```js
function completer(line) {
  const completions = '.help .error .exit .quit .q'.split(' ');
  const hits = completions.filter((c) => c.startsWith(line));
  // Show all completions if none found
  return [hits.length ? hits : completions, line];
}
```

The `completer` function can also return a {Promise}, or be asynchronous:

```js
async function completer(linePartial) {
  await someAsyncWork();
  return [['123'], linePartial];
}
```

## Callback API

<!-- YAML
added: v0.1.104
-->

### Class: `readline.Interface`

<!-- YAML
added: v0.1.104
changes:
  - version: v17.0.0
    pr-url: https://github.com/nodejs/node/pull/37947
    description: The class `readline.Interface` now inherits from `Interface`.
-->

* Extends: {readline.InterfaceConstructor}

Instances of the `readline.Interface` class are constructed using the
`readline.createInterface()` method. Every instance is associated with a
single `input` [Readable][] stream and a single `output` [Writable][] stream.
The `output` stream is used to print prompts for user input that arrives on,
and is read from, the `input` stream.

#### `rl.question(query[, options], callback)`

<!-- YAML
added: v0.3.3
-->

* `query` {string} A statement or query to write to `output`, prepended to the
  prompt.
* `options` {Object}
  * `signal` {AbortSignal} Optionally allows the `question()` to be canceled
    using an `AbortController`.
* `callback` {Function} A callback function that is invoked with the user's
  input in response to the `query`.

The `rl.question()` method displays the `query` by writing it to the `output`,
waits for user input to be provided on `input`, then invokes the `callback`
function passing the provided input as the first argument.

When called, `rl.question()` will resume the `input` stream if it has been
paused.

If the `readline.Interface` was created with `output` set to `null` or
`undefined` the `query` is not written.

The `callback` function passed to `rl.question()` does not follow the typical
pattern of accepting an `Error` object or `null` as the first argument.
The `callback` is called with the provided answer as the only argument.

An error will be thrown if calling `rl.question()` after `rl.close()`.

Example usage:

```js
rl.question('What is your favorite food? ', (answer) => {
  console.log(`Oh, so your favorite food is ${answer}`);
});
```

Using an `AbortController` to cancel a question.

```js
const ac = new AbortController();
const signal = ac.signal;

rl.question('What is your favorite food? ', { signal }, (answer) => {
  console.log(`Oh, so your favorite food is ${answer}`);
});

signal.addEventListener('abort', () => {
  console.log('The food question timed out');
}, { once: true });

setTimeout(() => ac.abort(), 10000);
```

### `readline.clearLine(stream, dir[, callback])`

<!-- YAML
added: v0.7.7
changes:
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41678
    description: Passing an invalid callback to the `callback` argument
                 now throws `ERR_INVALID_ARG_TYPE` instead of
                 `ERR_INVALID_CALLBACK`.
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28674
    description: The stream's write() callback and return value are exposed.
-->

* `stream` {stream.Writable}
* `dir` {number}
  * `-1`: to the left from cursor
  * `1`: to the right from cursor
  * `0`: the entire line
* `callback` {Function} Invoked once the operation completes.
* Returns: {boolean} `false` if `stream` wishes for the calling code to wait for
  the `'drain'` event to be emitted before continuing to write additional data;
  otherwise `true`.

The `readline.clearLine()` method clears current line of given [TTY][] stream
in a specified direction identified by `dir`.

### `readline.clearScreenDown(stream[, callback])`

<!-- YAML
added: v0.7.7
changes:
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41678
    description: Passing an invalid callback to the `callback` argument
                 now throws `ERR_INVALID_ARG_TYPE` instead of
                 `ERR_INVALID_CALLBACK`.
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28641
    description: The stream's write() callback and return value are exposed.
-->

* `stream` {stream.Writable}
* `callback` {Function} Invoked once the operation completes.
* Returns: {boolean} `false` if `stream` wishes for the calling code to wait for
  the `'drain'` event to be emitted before continuing to write additional data;
  otherwise `true`.

The `readline.clearScreenDown()` method clears the given [TTY][] stream from
the current position of the cursor down.

### `readline.createInterface(options)`

<!-- YAML
added: v0.1.98
changes:
  - version:
      - v15.14.0
      - v14.18.0
    pr-url: https://github.com/nodejs/node/pull/37932
    description: The `signal` option is supported now.
  - version:
      - v15.8.0
      - v14.18.0
    pr-url: https://github.com/nodejs/node/pull/33662
    description: The `history` option is supported now.
  - version: v13.9.0
    pr-url: https://github.com/nodejs/node/pull/31318
    description: The `tabSize` option is supported now.
  - version:
    - v8.3.0
    - v6.11.4
    pr-url: https://github.com/nodejs/node/pull/13497
    description: Remove max limit of `crlfDelay` option.
  - version: v6.6.0
    pr-url: https://github.com/nodejs/node/pull/8109
    description: The `crlfDelay` option is supported now.
  - version: v6.3.0
    pr-url: https://github.com/nodejs/node/pull/7125
    description: The `prompt` option is supported now.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/6352
    description: The `historySize` option can be `0` now.
-->

* `options` {Object}
  * `input` {stream.Readable} The [Readable][] stream to listen to. This option
    is _required_.
  * `output` {stream.Writable} The [Writable][] stream to write readline data
    to.
  * `completer` {Function} An optional function used for Tab autocompletion.
  * `terminal` {boolean} `true` if the `input` and `output` streams should be
    treated like a TTY, and have ANSI/VT100 escape codes written to it.
    **Default:** checking `isTTY` on the `output` stream upon instantiation.
  * `history` {string\[]} Initial list of history lines. This option makes sense
    only if `terminal` is set to `true` by the user or by an internal `output`
    check, otherwise the history caching mechanism is not initialized at all.
    **Default:** `[]`.
  * `historySize` {number} Maximum number of history lines retained. To disable
    the history set this value to `0`. This option makes sense only if
    `terminal` is set to `true` by the user or by an internal `output` check,
    otherwise the history caching mechanism is not initialized at all.
    **Default:** `30`.
  * `removeHistoryDuplicates` {boolean} If `true`, when a new input line added
    to the history list duplicates an older one, this removes the older line
    from the list. **Default:** `false`.
  * `prompt` {string} The prompt string to use. **Default:** `'> '`.
  * `crlfDelay` {number} If the delay between `\r` and `\n` exceeds
    `crlfDelay` milliseconds, both `\r` and `\n` will be treated as separate
    end-of-line input. `crlfDelay` will be coerced to a number no less than
    `100`. It can be set to `Infinity`, in which case `\r` followed by `\n`
    will always be considered a single newline (which may be reasonable for
    [reading files][] with `\r\n` line delimiter). **Default:** `100`.
  * `escapeCodeTimeout` {number} The duration `readline` will wait for a
    character (when reading an ambiguous key sequence in milliseconds one that
    can both form a complete key sequence using the input read so far and can
    take additional input to complete a longer key sequence).
    **Default:** `500`.
  * `tabSize` {integer} The number of spaces a tab is equal to (minimum 1).
    **Default:** `8`.
  * `signal` {AbortSignal} Allows closing the interface using an AbortSignal.
    Aborting the signal will internally call `close` on the interface.
* Returns: {readline.Interface}

The `readline.createInterface()` method creates a new `readline.Interface`
instance.

```mjs
import { createInterface } from 'node:readline';
import { stdin, stdout } from 'node:process';
const rl = createInterface({
  input: stdin,
  output: stdout,
});
```

```cjs
const { createInterface } = require('node:readline');
const rl = createInterface({
  input: process.stdin,
  output: process.stdout,
});
```

Once the `readline.Interface` instance is created, the most common case is to
listen for the `'line'` event:

```js
rl.on('line', (line) => {
  console.log(`Received: ${line}`);
});
```

If `terminal` is `true` for this instance then the `output` stream will get
the best compatibility if it defines an `output.columns` property and emits
a `'resize'` event on the `output` if or when the columns ever change
([`process.stdout`][] does this automatically when it is a TTY).

When creating a `readline.Interface` using `stdin` as input, the program
will not terminate until it receives an [EOF character][]. To exit without
waiting for user input, call `process.stdin.unref()`.

#### Use of the `completer` function

The `completer` function takes the current line entered by the user
as an argument, and returns an `Array` with 2 entries:

* An `Array` with matching entries for the completion.
* The substring that was used for the matching.

For instance: `[[substr1, substr2, ...], originalsubstring]`.

```js
function completer(line) {
  const completions = '.help .error .exit .quit .q'.split(' ');
  const hits = completions.filter((c) => c.startsWith(line));
  // Show all completions if none found
  return [hits.length ? hits : completions, line];
}
```

The `completer` function can be called asynchronously if it accepts two
arguments:

```js
function completer(linePartial, callback) {
  callback(null, [['123'], linePartial]);
}
```

### `readline.cursorTo(stream, x[, y][, callback])`

<!-- YAML
added: v0.7.7
changes:
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41678
    description: Passing an invalid callback to the `callback` argument
                 now throws `ERR_INVALID_ARG_TYPE` instead of
                 `ERR_INVALID_CALLBACK`.
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28674
    description: The stream's write() callback and return value are exposed.
-->

* `stream` {stream.Writable}
* `x` {number}
* `y` {number}
* `callback` {Function} Invoked once the operation completes.
* Returns: {boolean} `false` if `stream` wishes for the calling code to wait for
  the `'drain'` event to be emitted before continuing to write additional data;
  otherwise `true`.

The `readline.cursorTo()` method moves cursor to the specified position in a
given [TTY][] `stream`.

### `readline.moveCursor(stream, dx, dy[, callback])`

<!-- YAML
added: v0.7.7
changes:
  - version: v18.0.0
    pr-url: https://github.com/nodejs/node/pull/41678
    description: Passing an invalid callback to the `callback` argument
                 now throws `ERR_INVALID_ARG_TYPE` instead of
                 `ERR_INVALID_CALLBACK`.
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28674
    description: The stream's write() callback and return value are exposed.
-->

* `stream` {stream.Writable}
* `dx` {number}
* `dy` {number}
* `callback` {Function} Invoked once the operation completes.
* Returns: {boolean} `false` if `stream` wishes for the calling code to wait for
  the `'drain'` event to be emitted before continuing to write additional data;
  otherwise `true`.

The `readline.moveCursor()` method moves the cursor _relative_ to its current
position in a given [TTY][] `stream`.

## `readline.emitKeypressEvents(stream[, interface])`

<!-- YAML
added: v0.7.7
-->

* `stream` {stream.Readable}
* `interface` {readline.InterfaceConstructor}

The `readline.emitKeypressEvents()` method causes the given [Readable][]
stream to begin emitting `'keypress'` events corresponding to received input.

Optionally, `interface` specifies a `readline.Interface` instance for which
autocompletion is disabled when copy-pasted input is detected.

If the `stream` is a [TTY][], then it must be in raw mode.

This is automatically called by any readline instance on its `input` if the
`input` is a terminal. Closing the `readline` instance does not stop
the `input` from emitting `'keypress'` events.

```js
readline.emitKeypressEvents(process.stdin);
if (process.stdin.isTTY)
  process.stdin.setRawMode(true);
```

## Example: Tiny CLI

The following example illustrates the use of `readline.Interface` class to
implement a small command-line interface:

```mjs
import { createInterface } from 'node:readline';
import { exit, stdin, stdout } from 'node:process';
const rl = createInterface({
  input: stdin,
  output: stdout,
  prompt: 'OHAI> ',
});

rl.prompt();

rl.on('line', (line) => {
  switch (line.trim()) {
    case 'hello':
      console.log('world!');
      break;
    default:
      console.log(`Say what? I might have heard '${line.trim()}'`);
      break;
  }
  rl.prompt();
}).on('close', () => {
  console.log('Have a great day!');
  exit(0);
});
```

```cjs
const { createInterface } = require('node:readline');
const rl = createInterface({
  input: process.stdin,
  output: process.stdout,
  prompt: 'OHAI> ',
});

rl.prompt();

rl.on('line', (line) => {
  switch (line.trim()) {
    case 'hello':
      console.log('world!');
      break;
    default:
      console.log(`Say what? I might have heard '${line.trim()}'`);
      break;
  }
  rl.prompt();
}).on('close', () => {
  console.log('Have a great day!');
  process.exit(0);
});
```

## Example: Read file stream line-by-Line

A common use case for `readline` is to consume an input file one line at a
time. The easiest way to do so is leveraging the [`fs.ReadStream`][] API as
well as a `for await...of` loop:

```mjs
import { createReadStream } from 'node:fs';
import { createInterface } from 'node:readline';

async function processLineByLine() {
  const fileStream = createReadStream('input.txt');

  const rl = createInterface({
    input: fileStream,
    crlfDelay: Infinity,
  });
  // Note: we use the crlfDelay option to recognize all instances of CR LF
  // ('\r\n') in input.txt as a single line break.

  for await (const line of rl) {
    // Each line in input.txt will be successively available here as `line`.
    console.log(`Line from file: ${line}`);
  }
}

processLineByLine();
```

```cjs
const { createReadStream } = require('node:fs');
const { createInterface } = require('node:readline');

async function processLineByLine() {
  const fileStream = createReadStream('input.txt');

  const rl = createInterface({
    input: fileStream,
    crlfDelay: Infinity,
  });
  // Note: we use the crlfDelay option to recognize all instances of CR LF
  // ('\r\n') in input.txt as a single line break.

  for await (const line of rl) {
    // Each line in input.txt will be successively available here as `line`.
    console.log(`Line from file: ${line}`);
  }
}

processLineByLine();
```

Alternatively, one could use the [`'line'`][] event:

```mjs
import { createReadStream } from 'node:fs';
import { createInterface } from 'node:readline';

const rl = createInterface({
  input: createReadStream('sample.txt'),
  crlfDelay: Infinity,
});

rl.on('line', (line) => {
  console.log(`Line from file: ${line}`);
});
```

```cjs
const { createReadStream } = require('node:fs');
const { createInterface } = require('node:readline');

const rl = createInterface({
  input: createReadStream('sample.txt'),
  crlfDelay: Infinity,
});

rl.on('line', (line) => {
  console.log(`Line from file: ${line}`);
});
```

Currently, `for await...of` loop can be a bit slower. If `async` / `await`
flow and speed are both essential, a mixed approach can be applied:

```mjs
import { once } from 'node:events';
import { createReadStream } from 'node:fs';
import { createInterface } from 'node:readline';

(async function processLineByLine() {
  try {
    const rl = createInterface({
      input: createReadStream('big-file.txt'),
      crlfDelay: Infinity,
    });

    rl.on('line', (line) => {
      // Process the line.
    });

    await once(rl, 'close');

    console.log('File processed.');
  } catch (err) {
    console.error(err);
  }
})();
```

```cjs
const { once } = require('node:events');
const { createReadStream } = require('node:fs');
const { createInterface } = require('node:readline');

(async function processLineByLine() {
  try {
    const rl = createInterface({
      input: createReadStream('big-file.txt'),
      crlfDelay: Infinity,
    });

    rl.on('line', (line) => {
      // Process the line.
    });

    await once(rl, 'close');

    console.log('File processed.');
  } catch (err) {
    console.error(err);
  }
})();
```

## TTY keybindings

<table>
  <tr>
    <th>Keybindings</th>
    <th>Description</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Backspace</kbd></td>
    <td>Delete line left</td>
    <td>Doesn't work on Linux, Mac and Windows</td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Delete</kbd></td>
    <td>Delete line right</td>
    <td>Doesn't work on Mac</td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>C</kbd></td>
    <td>Emit <code>SIGINT</code> or close the readline instance</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>H</kbd></td>
    <td>Delete left</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>D</kbd></td>
    <td>Delete right or close the readline instance in case the current line is empty / EOF</td>
    <td>Doesn't work on Windows</td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>U</kbd></td>
    <td>Delete from the current position to the line start</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>K</kbd></td>
    <td>Delete from the current position to the end of line</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>Y</kbd></td>
    <td>Yank (Recall) the previously deleted text</td>
    <td>Only works with text deleted by <kbd>Ctrl</kbd>+<kbd>U</kbd> or <kbd>Ctrl</kbd>+<kbd>K</kbd></td>
  </tr>
  <tr>
    <td><kbd>Meta</kbd>+<kbd>Y</kbd></td>
    <td>Cycle among previously deleted texts</td>
    <td>Only available when the last keystroke is <kbd>Ctrl</kbd>+<kbd>Y</kbd> or <kbd>Meta</kbd>+<kbd>Y</kbd></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>A</kbd></td>
    <td>Go to start of line</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>E</kbd></td>
    <td>Go to end of line</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>B</kbd></td>
    <td>Back one character</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>F</kbd></td>
    <td>Forward one character</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>L</kbd></td>
    <td>Clear screen</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>N</kbd></td>
    <td>Next history item</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>P</kbd></td>
    <td>Previous history item</td>
    <td></td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>-</kbd></td>
    <td>Undo previous change</td>
    <td>Any keystroke that emits key code <code>0x1F</code> will do this action.
    In many terminals, for example <code>xterm</code>,
    this is bound to <kbd>Ctrl</kbd>+<kbd>-</kbd>.</td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>6</kbd></td>
    <td>Redo previous change</td>
    <td>Many terminals don't have a default redo keystroke.
    We choose key code <code>0x1E</code> to perform redo.
    In <code>xterm</code>, it is bound to <kbd>Ctrl</kbd>+<kbd>6</kbd>
    by default.</td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>Z</kbd></td>
    <td>Moves running process into background. Type
    <code>fg</code> and press <kbd>Enter</kbd>
    to return.</td>
    <td>Doesn't work on Windows</td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>W</kbd> or <kbd>Ctrl</kbd>
   +<kbd>Backspace</kbd></td>
    <td>Delete backward to a word boundary</td>
    <td><kbd>Ctrl</kbd>+<kbd>Backspace</kbd> Doesn't
    work on Linux, Mac and Windows</td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>Delete</kbd></td>
    <td>Delete forward to a word boundary</td>
    <td>Doesn't work on Mac</td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>Left arrow</kbd> or
    <kbd>Meta</kbd>+<kbd>B</kbd></td>
    <td>Word left</td>
    <td><kbd>Ctrl</kbd>+<kbd>Left arrow</kbd> Doesn't work
    on Mac</td>
  </tr>
  <tr>
    <td><kbd>Ctrl</kbd>+<kbd>Right arrow</kbd> or
    <kbd>Meta</kbd>+<kbd>F</kbd></td>
    <td>Word right</td>
    <td><kbd>Ctrl</kbd>+<kbd>Right arrow</kbd> Doesn't work
    on Mac</td>
  </tr>
  <tr>
    <td><kbd>Meta</kbd>+<kbd>D</kbd> or <kbd>Meta</kbd>
   +<kbd>Delete</kbd></td>
    <td>Delete word right</td>
    <td><kbd>Meta</kbd>+<kbd>Delete</kbd> Doesn't work
    on windows</td>
  </tr>
  <tr>
    <td><kbd>Meta</kbd>+<kbd>Backspace</kbd></td>
    <td>Delete word left</td>
    <td>Doesn't work on Mac</td>
  </tr>
</table>

[EOF character]: https://en.wikipedia.org/wiki/End-of-file#EOF_character
[Readable]: stream.md#readable-streams
[TTY]: tty.md
[TTY keybindings]: #tty-keybindings
[Writable]: stream.md#writable-streams
[`'SIGCONT'`]: #event-sigcont
[`'SIGTSTP'`]: #event-sigtstp
[`'line'`]: #event-line
[`fs.ReadStream`]: fs.md#class-fsreadstream
[`process.stdin`]: process.md#processstdin
[`process.stdout`]: process.md#processstdout
[`rl.close()`]: #rlclose
[reading files]: #example-read-file-stream-line-by-line

# TTY

<!--introduced_in=v0.10.0-->

> Stability: 2 - Stable

<!-- source_link=lib/tty.js -->

The `node:tty` module provides the `tty.ReadStream` and `tty.WriteStream`
classes. In most cases, it will not be necessary or possible to use this module
directly. However, it can be accessed using:

```js
const tty = require('node:tty');
```

When Node.js detects that it is being run with a text terminal ("TTY")
attached, [`process.stdin`][] will, by default, be initialized as an instance of
`tty.ReadStream` and both [`process.stdout`][] and [`process.stderr`][] will, by
default, be instances of `tty.WriteStream`. The preferred method of determining
whether Node.js is being run within a TTY context is to check that the value of
the `process.stdout.isTTY` property is `true`:

```console
$ node -p -e "Boolean(process.stdout.isTTY)"
true
$ node -p -e "Boolean(process.stdout.isTTY)" | cat
false
```

In most cases, there should be little to no reason for an application to
manually create instances of the `tty.ReadStream` and `tty.WriteStream`
classes.

## Class: `tty.ReadStream`

<!-- YAML
added: v0.5.8
-->

* Extends: {net.Socket}

Represents the readable side of a TTY. In normal circumstances
[`process.stdin`][] will be the only `tty.ReadStream` instance in a Node.js
process and there should be no reason to create additional instances.

### `readStream.isRaw`

<!-- YAML
added: v0.7.7
-->

A `boolean` that is `true` if the TTY is currently configured to operate as a
raw device.

This flag is always `false` when a process starts, even if the terminal is
operating in raw mode. Its value will change with subsequent calls to
`setRawMode`.

### `readStream.isTTY`

<!-- YAML
added: v0.5.8
-->

A `boolean` that is always `true` for `tty.ReadStream` instances.

### `readStream.setRawMode(mode)`

<!-- YAML
added: v0.7.7
-->

* `mode` {boolean} If `true`, configures the `tty.ReadStream` to operate as a
  raw device. If `false`, configures the `tty.ReadStream` to operate in its
  default mode. The `readStream.isRaw` property will be set to the resulting
  mode.
* Returns: {this} The read stream instance.

Allows configuration of `tty.ReadStream` so that it operates as a raw device.

When in raw mode, input is always available character-by-character, not
including modifiers. Additionally, all special processing of characters by the
terminal is disabled, including echoing input
characters. <kbd>Ctrl</kbd>+<kbd>C</kbd> will no longer cause a `SIGINT` when
in this mode.

## Class: `tty.WriteStream`

<!-- YAML
added: v0.5.8
-->

* Extends: {net.Socket}

Represents the writable side of a TTY. In normal circumstances,
[`process.stdout`][] and [`process.stderr`][] will be the only
`tty.WriteStream` instances created for a Node.js process and there
should be no reason to create additional instances.

### `new tty.ReadStream(fd[, options])`

<!-- YAML
added: v0.5.8
changes:
  - version: v0.9.4
    description: The `options` argument is supported.
-->

* `fd` {number} A file descriptor associated with a TTY.
* `options` {Object} Options passed to parent `net.Socket`,
  see `options` of [`net.Socket` constructor][].
* Returns {tty.ReadStream}

Creates a `ReadStream` for `fd` associated with a TTY.

### `new tty.WriteStream(fd)`

<!-- YAML
added: v0.5.8
-->

* `fd` {number} A file descriptor associated with a TTY.
* Returns {tty.WriteStream}

Creates a `WriteStream` for `fd` associated with a TTY.

### Event: `'resize'`

<!-- YAML
added: v0.7.7
-->

The `'resize'` event is emitted whenever either of the `writeStream.columns`
or `writeStream.rows` properties have changed. No arguments are passed to the
listener callback when called.

```js
process.stdout.on('resize', () => {
  console.log('screen size has changed!');
  console.log(`${process.stdout.columns}x${process.stdout.rows}`);
});
```

### `writeStream.clearLine(dir[, callback])`

<!-- YAML
added: v0.7.7
changes:
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28721
    description: The stream's write() callback and return value are exposed.
-->

* `dir` {number}
  * `-1`: to the left from cursor
  * `1`: to the right from cursor
  * `0`: the entire line
* `callback` {Function} Invoked once the operation completes.
* Returns: {boolean} `false` if the stream wishes for the calling code to wait
  for the `'drain'` event to be emitted before continuing to write additional
  data; otherwise `true`.

`writeStream.clearLine()` clears the current line of this `WriteStream` in a
direction identified by `dir`.

### `writeStream.clearScreenDown([callback])`

<!-- YAML
added: v0.7.7
changes:
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28721
    description: The stream's write() callback and return value are exposed.
-->

* `callback` {Function} Invoked once the operation completes.
* Returns: {boolean} `false` if the stream wishes for the calling code to wait
  for the `'drain'` event to be emitted before continuing to write additional
  data; otherwise `true`.

`writeStream.clearScreenDown()` clears this `WriteStream` from the current
cursor down.

### `writeStream.columns`

<!-- YAML
added: v0.7.7
-->

A `number` specifying the number of columns the TTY currently has. This property
is updated whenever the `'resize'` event is emitted.

### `writeStream.cursorTo(x[, y][, callback])`

<!-- YAML
added: v0.7.7
changes:
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28721
    description: The stream's write() callback and return value are exposed.
-->

* `x` {number}
* `y` {number}
* `callback` {Function} Invoked once the operation completes.
* Returns: {boolean} `false` if the stream wishes for the calling code to wait
  for the `'drain'` event to be emitted before continuing to write additional
  data; otherwise `true`.

`writeStream.cursorTo()` moves this `WriteStream`'s cursor to the specified
position.

### `writeStream.getColorDepth([env])`

<!-- YAML
added: v9.9.0
-->

* `env` {Object} An object containing the environment variables to check. This
  enables simulating the usage of a specific terminal. **Default:**
  `process.env`.
* Returns: {number}

Returns:

* `1` for 2,
* `4` for 16,
* `8` for 256,
* `24` for 16,777,216 colors supported.

Use this to determine what colors the terminal supports. Due to the nature of
colors in terminals it is possible to either have false positives or false
negatives. It depends on process information and the environment variables that
may lie about what terminal is used.
It is possible to pass in an `env` object to simulate the usage of a specific
terminal. This can be useful to check how specific environment settings behave.

To enforce a specific color support, use one of the below environment settings.

* 2 colors: `FORCE_COLOR = 0` (Disables colors)
* 16 colors: `FORCE_COLOR = 1`
* 256 colors: `FORCE_COLOR = 2`
* 16,777,216 colors: `FORCE_COLOR = 3`

Disabling color support is also possible by using the `NO_COLOR` and
`NODE_DISABLE_COLORS` environment variables.

### `writeStream.getWindowSize()`

<!-- YAML
added: v0.7.7
-->

* Returns: {number\[]}

`writeStream.getWindowSize()` returns the size of the TTY
corresponding to this `WriteStream`. The array is of the type
`[numColumns, numRows]` where `numColumns` and `numRows` represent the number
of columns and rows in the corresponding TTY.

### `writeStream.hasColors([count][, env])`

<!-- YAML
added:
 - v11.13.0
 - v10.16.0
-->

* `count` {integer} The number of colors that are requested (minimum 2).
  **Default:** 16.
* `env` {Object} An object containing the environment variables to check. This
  enables simulating the usage of a specific terminal. **Default:**
  `process.env`.
* Returns: {boolean}

Returns `true` if the `writeStream` supports at least as many colors as provided
in `count`. Minimum support is 2 (black and white).

This has the same false positives and negatives as described in
[`writeStream.getColorDepth()`][].

```js
process.stdout.hasColors();
// Returns true or false depending on if `stdout` supports at least 16 colors.
process.stdout.hasColors(256);
// Returns true or false depending on if `stdout` supports at least 256 colors.
process.stdout.hasColors({ TMUX: '1' });
// Returns true.
process.stdout.hasColors(2 ** 24, { TMUX: '1' });
// Returns false (the environment setting pretends to support 2 ** 8 colors).
```

### `writeStream.isTTY`

<!-- YAML
added: v0.5.8
-->

A `boolean` that is always `true`.

### `writeStream.moveCursor(dx, dy[, callback])`

<!-- YAML
added: v0.7.7
changes:
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28721
    description: The stream's write() callback and return value are exposed.
-->

* `dx` {number}
* `dy` {number}
* `callback` {Function} Invoked once the operation completes.
* Returns: {boolean} `false` if the stream wishes for the calling code to wait
  for the `'drain'` event to be emitted before continuing to write additional
  data; otherwise `true`.

`writeStream.moveCursor()` moves this `WriteStream`'s cursor _relative_ to its
current position.

### `writeStream.rows`

<!-- YAML
added: v0.7.7
-->

A `number` specifying the number of rows the TTY currently has. This property
is updated whenever the `'resize'` event is emitted.

## `tty.isatty(fd)`

<!-- YAML
added: v0.5.8
-->

* `fd` {number} A numeric file descriptor
* Returns: {boolean}

The `tty.isatty()` method returns `true` if the given `fd` is associated with
a TTY and `false` if it is not, including whenever `fd` is not a non-negative
integer.

[`net.Socket` constructor]: net.md#new-netsocketoptions
[`process.stderr`]: process.md#processstderr
[`process.stdin`]: process.md#processstdin
[`process.stdout`]: process.md#processstdout
[`writeStream.getColorDepth()`]: #writestreamgetcolordepthenv

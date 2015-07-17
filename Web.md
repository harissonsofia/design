# Browser Embedding

Unsurprisingly, one of WebAssembly's primary purposes is to run on the Web,
embedded in Web browsers (though this is [not its only purpose](NonWeb.md)).

This means integrating with the Web ecosystem, leveraging Web APIs, supporting
the Web's security model, preserving the Web's portability, and designing in
room for evolutionary development. Many of these goals are clearly
reflected in WebAssembly's [high-level goals](HighLevelGoals.md).

More concretely, the following is a list of points of contact between WebAssembly
and the rest of the Web platform that have been considered:

* WebAssembly's [modules](Modules.md) allow for natural [integration with
  the ES6 module system](Modules.md#integration-with-es6-modules) and thus
  synchronous calling to and from JavaScript.
* WebAssembly's security model should depend on [CORS][] and
  [subresource integrity][] to enable distribution, especially through content
  distribution networks and to implement
  [dynamic linking](FutureFeatures.md#dynamic-linking).
* Once [threads are supported](PostMVP.md#threads), a WebAssembly module would
  shared (including its heap) between workers via `postMessage()`.
  - This also has the effect of explicitly sharing code so that engines don't
    perform N fetches and compile N copies.
  - WebAssembly may later standardize a more direct way to create a thread that
    doesn't involve creating a new Worker.
* Once [SIMD is supported](PostMVP.md#fixed-width-simd), a Web implementation of
  WebAssembly would:
  - Be statically typed analogous to [SIMD.js-in-asm.js][];
  - Reuse specification of operation semantics (with TC39);
  - Reuse backend implementation (same IR nodes).

  [CORS]: https://www.w3.org/TR/cors/
  [subresource integrity]: https://www.w3.org/TR/SRI/
  [SIMD.js-in-asm.js]: http://discourse.specifiction.org/t/request-for-comments-simd-js-in-asm-js
  

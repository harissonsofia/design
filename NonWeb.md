# Non-Browser Embeddings

While WebAssembly is designed to run [within a browser](Web.md), it is
also desirable for it to be able to execute well in other environments,
including everything from minimal shells for testing to full-blown
application environments e.g. on servers in datacenters, on IoT devices,
or mobile/desktop apps. It may even be desirable to execute WebAssembly
embedded within larger programs.

Non-browser environments may provide different APIs than Web
environments, which
[feature testing](FeatureTest.md) and
[dynamic linking](FutureFeatures.md#dynamic-linking) will make discoverable and
usable.

The WebAssembly spec will not try to define any large portable libc-like
library. However, certain features that are core to WebAssembly semantics that
are found in native libc *would* be part of the core WebAssembly spec as either
primitive opcodes or a function exported by a
[builtin module](Modules.md#imports-and-exports) (e.g., `sbrk`, `dlopen`).

Where there is overlap between the browser and popular non-browser environments,
shared specs could be proposed, but these would be separate from the WebAssembly
spec. A symmetric example in JavaScript would be the in-progress 
[Loader](https://whatwg.github.io/loader) spec, which is proposed for both
browser and node.js environments and is distinct from the JavaScript spec.

However, for most cases it is expected that, to achieve portability at the
source code level, communities would build libraries that mapped from a 
source-level interface to the host environment's builtin capabilities
(either at build time or runtime).  WebAssembly would provide the raw building
blocks (feature testing, [builtin modules](Modules.md#imports-and-exports) and
dynamic loading) to make these libraries possible. Two early expected examples
are POSIX and SDL.

In general, by keeping the non-browser path such that it doesn't require
browser APIs, WebAssembly could be used as a portable binary format on many
platforms, bringing great benefits in portability, tooling and
language-agnosticity (since it supports C/C++ level semantics).

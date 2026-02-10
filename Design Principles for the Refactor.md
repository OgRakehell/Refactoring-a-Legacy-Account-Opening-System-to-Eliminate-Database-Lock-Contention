# Design Principles for the Refactor
Rather than patching symptoms, the refactor was guided by a small set of principles:

**- Short, atomic database transactions**

**- Asynchronous processing for long-running work**

**- Idempotent request handling**

**- Explicit state management**

**- Controlled pressure on core banking systems**

**- Clear user feedback without false promises**

These principles reflect patterns used in large-scale financial systems.

---
title: wasm
tags:
  - cheatsheet
---

# WASM

- wasm is a target language for compilers.
- There are wasm runtimes that execute wasm binaries
- firefox, chrome etc all have wasm runtimes but thats just the original purpose.You can actually have wasm targets for embedded devices, mobile phone etc. So in many ways wasm is a containerization technology and also a truly cross platform target.
- If your language targets wasm (zig does) and if a suitable runtime exists, then the code is portable to any platform.

## Docker + wasm

Docker now has experimental support for wasm

```
FROM scratch
COPY file.wasm file.wasm
ENTRYPOINT ["file.wasm"]
```

# Protocol
## Questions
### What is gRPC and why does it work across languages and platforms?

gRPC is a modern, open-source, high-performance RPC framework. It works across languages and platforms because you define your API once in a `.proto` file and the toolchain generates type-safe client and server stubs for many languages (Java, Go, Python, C#, etc.), all speaking the same HTTP/2-based protocol.


### Describe the RPC life cycle starting with the RPC client

1. **Client prepares a stub & channel:** The client creates a channel to the server and a generated stub for the service. 
2. **Client makes an RPC:** The client calls a method on the stub, sending a request message (plus optional metadata). gRPC handles serialization (Protobuf by default) and transport over HTTP/2. 
3. **Server receives & invokes:** The server deserializes the request, runs the corresponding service method, and writes responses (unary or stream). ([gRPC][2])
4. **Response and status:** Server sends the response(s), trailers, and a final status; client stub surfaces the outcome to user code. Interceptors can run on both sides. ([gRPC][2])

---

### 3) Describe the workflow of Protocol Buffers

1. **Define schema:** Write message and service definitions in a `.proto` file. ([Protocol Buffers][3])
2. **Generate code:** Run `protoc` (often via build plugins) to generate language-specific classes and gRPC stubs. ([gRPC][4])
3. **Use in code:** Construct messages via generated classes; the runtime serializes to a compact binary “wire format” and deserializes on receipt. ([Protocol Buffers][5])
4. **Evolve schema safely:** Add fields using reserved numbers/names and defaulting rules to maintain backward/forward compatibility. ([Protocol Buffers][3])

---

### 4) What are the benefits of using protocol buffers?

* **Compact & fast:** Binary encoding yields smaller payloads and faster (de)serialization than text formats like JSON/XML. ([Protocol Buffers][5])
* **Strongly typed schema & codegen:** The `.proto` acts as an IDL, generating type-safe code for many languages. ([Protocol Buffers][3])
* **Compatibility over time:** Designed for safe schema evolution (backward/forward compatible changes). ([Protocol Buffers][3])
* **Ecosystem integration with gRPC:** First-class pairing with gRPC for high-performance APIs. ([gRPC][6])

---

### 5) When is the use of protocol buffers **not** recommended?

* **Human-readable/debug-friendly APIs:** Protobuf is binary and not human-readable; for ad-hoc debugging or public REST-style APIs, JSON can be simpler. ([Baeldung on Kotlin][7])
* **Very large single messages / random access needs:** Protobuf messages must be < 2 GiB, and the format isn’t designed for random access within huge files. ([Protocol Buffers][8])
* **Pure browser clients without gRPC-Web:** Browsers don’t natively speak gRPC; you need gRPC-Web or another approach. ([gRPC][9])

---

### 6) List 3 different data types that can be used with protocol buffers

Examples include **`int32`**, **`string`**, and **`bool`** (among many other scalar types). ([Protocol Buffers][3])

---

### (Bonus) Helpful Spring Boot integration source

If you’re wiring this into Spring Boot, a widely used starter simplifies client/server setup and stub injection. ([yidongnan.github.io][10])

[1]: https://grpc.io/?utm_source=chatgpt.com "gRPC"
[2]: https://grpc.io/docs/what-is-grpc/core-concepts/?utm_source=chatgpt.com "Core concepts, architecture and lifecycle"
[3]: https://protobuf.dev/programming-guides/proto3/?utm_source=chatgpt.com "Language Guide (proto 3) | Protocol Buffers Documentation"
[4]: https://grpc.io/docs/languages/java/basics/?utm_source=chatgpt.com "Basics tutorial | Java"
[5]: https://protobuf.dev/programming-guides/encoding/?utm_source=chatgpt.com "Encoding | Protocol Buffers Documentation"
[6]: https://grpc.io/docs/what-is-grpc/introduction/?utm_source=chatgpt.com "Introduction to gRPC"
[7]: https://www.baeldung.com/grpc-introduction?utm_source=chatgpt.com "Introduction to gRPC"
[8]: https://protobuf.dev/programming-guides/proto-limits/?utm_source=chatgpt.com "Proto Limits | Protocol Buffers Documentation"
[9]: https://grpc.io/docs/platforms/web/basics/?utm_source=chatgpt.com "Basics tutorial | Web"
[10]: https://yidongnan.github.io/grpc-spring-boot-starter/en/?utm_source=chatgpt.com "gRPC-Spring-Boot-Starter Documentation - GitHub Pages"

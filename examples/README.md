# Quick Start With Claude Desktop

1. **Build the Server (Counter Example)**

   ```sh
   cargo build --release --example servers_counter_stdio
   ```

   This builds a standard input/output MCP server binary.

2. **Add or update this section in your** `PATH-TO/claude_desktop_config.json`

   Windows

   ```json
   {
     "mcpServers": {
       "counter": {
         "command": "PATH-TO/rust-sdk/target/release/examples/servers_counter_stdio.exe",
         "args": []
       }
     }
   }
   ```

   MacOS/Linux

   ```json
   {
     "mcpServers": {
       "counter": {
         "command": "PATH-TO/rust-sdk/target/release/examples/servers_counter_stdio",
         "args": []
       }
     }
   }
   ```

3. **Ensure that the MCP UI elements appear in Claude Desktop**
   The MCP UI elements will only show up in Claude for Desktop if at least one server is properly configured. It may require to restart Claude for Desktop.

4. **Once Claude Desktop is running, try chatting:**

   ```text
   counter.say_hello
   ```

   Or test other tools like:

   ```texts
   counter.increment
   counter.get_value
   counter.sum {"a": 3, "b": 4}
   ```

## Examples overview

This `examples/` folder contains multiple small example projects demonstrating how to use the MCP Rust SDK as both clients and servers, and how to run different transports and platform integrations. Below are short, focused descriptions for each examples subfolder with links to the more detailed READMEs and notable entry points.

### clients/ — client examples (see `clients/README.md`)

Short description: A set of MCP client examples that show how to connect to MCP servers via different transports (stdio, SSE, streamable HTTP) and how to exercise client features like sampling, progress notifications, OAuth authentication, and managing multiple clients.

Notable examples: `clients_sse`, `clients_git_stdio`, `clients_streamable_http`, `clients_everything_stdio`, `clients_collection`, `clients_oauth_client`, `clients_sampling_stdio`.

See: `examples/clients/README.md` for runnable commands and details.

### servers/ — server examples (see `servers/README.md`)

Short description: A variety of MCP server examples demonstrating stdio, SSE, and HTTP-based transports, authentication (OAuth) examples, elicitation and prompts, progress notifications, and simple memory-backed servers. Good starting points for implementing custom MCP servers.

Notable examples: `servers_counter_stdio`, `servers_counter_sse`, `servers_memory_stdio`, `servers_counter_streamhttp`, `servers_complex_auth_sse`, `servers_elicitation_stdio`, `servers_prompt_stdio`, `servers_progress_demo`.

See: `examples/servers/README.md` for full details and how to run each example.

### transport/ — transport examples (source only)

Short description: Low-level transport examples demonstrating how to wire MCP over different transports. There isn't a separate README in this folder; instead look at the source files under `examples/transport/src/` for runnable snippets.

Files of interest:
- `transport/src/tcp.rs` — TCP transport example
- `transport/src/http_upgrade.rs` — HTTP upgrade transport (useful for embedding MCP in existing HTTP servers)
- `transport/src/unix_socket.rs` — Unix domain socket transport example (Linux/macOS)
- `transport/src/websocket.rs` — WebSocket transport example

Tip: These files demonstrate how to adapt the SDK to different networking layers — inspect and run the relevant example using `cargo run --example` when needed.

### rig-integration/ — integration with rig (stream chatbot)

Short description: Integration example that demonstrates using the SDK within the rig chatbot environment. Contains a small stream-based chatbot setup and `config.toml` showing how to wire the example into a rig instance.

Files of interest: `rig-integration/src/chat.rs`, `rig-integration/config.toml`.

### simple-chat-client/ — a minimal chat client

Short description: A compact, easy-to-follow chat client that demonstrates connecting to an MCP server and exchanging messages. Useful as a template to build small clients or for testing servers during development.

Files of interest: `simple-chat-client/src/` and the `simple-chat-client/README.md`.

### wasi/ — WASI / wasip2 runtime example

Short description: Shows how MCP works in a WASI environment (wasip2). Contains configuration and minimal examples for running the SDK with WASI-compatible runtimes.

Files of interest: `wasi/README.md`, `wasi/config.toml`, and `wasi/src/`.

## How to run examples

Most examples can be run with Cargo's `--example` flag. Example:

```bash
# Build and run the counter stdio server example
cargo run --example servers_counter_stdio

# Run a client example (SSE client)
cargo run --example clients_sse
```

For transport-only examples look inside `examples/transport/src/` and run the corresponding example target (for example `cargo run --example transport_tcp` if present in the workspace examples manifest).

## Use Mcp Inspector

You can inspect running servers and experiment visually with the MCP Inspector:

```sh
npx @modelcontextprotocol/inspector
```

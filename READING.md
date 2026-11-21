# webserv — Background reading

The subject asks us to read the RFCs defining HTTP, and to test with `telnet`
and NGINX, before starting.

---

## Everyone

- The HTTP request/response model: request line, headers, empty line, body
- HTTP methods and what each means; status codes and what each class means
- RFC 1945 (HTTP/1.0), which the subject suggests as a reference point.
  HTTP/1.1 is defined by RFC 9110 and RFC 9112; RFC 2616 is the older and more
  widely read version of the same material
- The NGINX configuration file format — `server` and `location` blocks
- What C++98 does not have: no `auto`, no range-based `for`, no `nullptr`, no
  smart pointers, no `std::to_string`
- Practical: `curl -v`, `telnet`, the browser's network inspector, and
  comparing our behaviour against a running NGINX

## Part 1 — connections and process management

- TCP/IP basics: ports, connections, the client/server model
- Sockets: `socket`, `bind`, `listen`, `accept`, `recv`, `send`, `close`
- Byte order and `htons` / `htonl`
- Blocking versus non-blocking I/O, and `fcntl` with `O_NONBLOCK`
- I/O multiplexing — `select`, `poll`, `epoll`, `kqueue` — and what readiness
  means
- The single-threaded event-driven model, and why it is used here instead of
  threads or processes per client
- Partial reads and partial writes, and per-connection buffering
- Connection state machines and timeouts
- Process creation: `fork`, `execve`, `pipe`, `dup2`, `waitpid`
- Signals, in particular `SIGPIPE`
- The CGI specification, RFC 3875: the environment variables and the
  stdin/stdout contract between a server and a CGI program

## Part 2 — HTTP protocol

- The exact grammar of an HTTP message, including CRLF line endings
- `GET`, `POST` and `DELETE` semantics
- `Content-Length` versus `Transfer-Encoding: chunked`, and how chunked bodies
  are framed
- Persistent connections and `Connection: close`
- `multipart/form-data`, RFC 7578, as used by HTML file upload forms
- Percent-encoding in URLs, and query string format
- Writing an incremental parser: state machines, and parsing input that arrives
  in arbitrary pieces

## Part 3 — configuration and resources

- Writing a lexer and a recursive-descent parser for a nested block format
- Filesystem calls: `open`, `read`, `stat`, `access`, `opendir`, `readdir`,
  `closedir`, `unlink`
- MIME types and the `Content-Type` header
- Directory index files and generated directory listings
- Path traversal: why a target containing `..` must not escape the route root
- HTTP redirection, 301 and 302

---

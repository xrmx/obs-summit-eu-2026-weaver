# Spans


## `span.dice.roll`

Represents rolling a dice.

| Property | Value |
| --- | --- |
| Kind | `internal` |
| Stability | `development` |



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `roll.value` | `int` | required | The value produced by rolling the dice. |



## `span.http.client`

This span represents an outbound HTTP request.


| Property | Value |
| --- | --- |
| Kind | `client` |
| Stability | `stable` |


There are two ways HTTP client spans can be implemented in an instrumentation:

1. Instrumentations SHOULD create an HTTP span for each attempt to send an HTTP request over the wire.
   In case the request is resent, the resend attempts MUST follow the [HTTP resend spec](#http-request-retries-and-redirects).
   In this case, instrumentations SHOULD NOT (also) emit a logical encompassing HTTP client span.

2. If for some reason it is not possible to emit a span for each send attempt (because e.g. the instrumented library does not expose hooks that would allow this),
   instrumentations MAY create an HTTP span for the top-most operation of the HTTP client.
   In this case, the `url.full` MUST be the absolute URL that was originally requested, before any HTTP-redirects that may happen when executing the request.

**Span name:** refer to the [Span Name](/docs/http/http-spans.md#name) section.

**Span kind** MUST be `CLIENT`.

**Span status:** refer to the [Span Status](/docs/http/http-spans.md#status) section.



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `error.type` | `{"members": [{"brief": "A fallback error value to be used when the instrumentation doesn't define a custom value.\n", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | {"conditionally_required": "If request has ended with an error."} | Describes a class of error the operation ended with.
 |

| `http.request.body.size` | `int` | opt_in | The size of the request payload body in bytes. This is the number of bytes transferred excluding headers and is often, but not always, present as the [Content-Length](https://www.rfc-editor.org/rfc/rfc9110.html#field.content-length) header. For requests using transport encoding, this should be the compressed size.
 |

| `http.request.header` | `template[string[]]` | opt_in | HTTP request headers, `<key>` being the normalized HTTP Header name (lowercase), the value being the header values.
 |

| `http.request.method` | `{"members": [{"brief": "CONNECT method.", "id": "connect", "stability": "stable", "value": "CONNECT"}, {"brief": "DELETE method.", "id": "delete", "stability": "stable", "value": "DELETE"}, {"brief": "GET method.", "id": "get", "stability": "stable", "value": "GET"}, {"brief": "HEAD method.", "id": "head", "stability": "stable", "value": "HEAD"}, {"brief": "OPTIONS method.", "id": "options", "stability": "stable", "value": "OPTIONS"}, {"brief": "PATCH method.", "id": "patch", "stability": "stable", "value": "PATCH"}, {"brief": "POST method.", "id": "post", "stability": "stable", "value": "POST"}, {"brief": "PUT method.", "id": "put", "stability": "stable", "value": "PUT"}, {"brief": "TRACE method.", "id": "trace", "stability": "stable", "value": "TRACE"}, {"brief": "QUERY method.", "id": "query", "stability": "development", "value": "QUERY"}, {"brief": "Any HTTP method that the instrumentation has no prior knowledge of.", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | required | HTTP request method. |

| `http.request.method_original` | `string` | {"conditionally_required": "If and only if it's different than `http.request.method`."} | Original HTTP method sent by the client in the request line. |

| `http.request.resend_count` | `int` | {"recommended": "if and only if request was retried."} | The ordinal number of request resending attempt (for any reason, including redirects).
 |

| `http.request.size` | `int` | opt_in | The total size of the request in bytes. This should be the total number of bytes sent over the wire, including the request line (HTTP/1.1), framing (HTTP/2 and HTTP/3), headers, and request body if any.
 |

| `http.response.body.size` | `int` | opt_in | The size of the response payload body in bytes. This is the number of bytes transferred excluding headers and is often, but not always, present as the [Content-Length](https://www.rfc-editor.org/rfc/rfc9110.html#field.content-length) header. For requests using transport encoding, this should be the compressed size.
 |

| `http.response.header` | `template[string[]]` | opt_in | HTTP response headers, `<key>` being the normalized HTTP Header name (lowercase), the value being the header values.
 |

| `http.response.size` | `int` | opt_in | The total size of the response in bytes. This should be the total number of bytes sent over the wire, including the status line (HTTP/1.1), framing (HTTP/2 and HTTP/3), headers, and response body and trailers if any.
 |

| `http.response.status_code` | `int` | {"conditionally_required": "If and only if one was received/sent."} | [HTTP response status code](https://tools.ietf.org/html/rfc7231#section-6). |

| `network.peer.address` | `string` | recommended | Peer address of the network connection - IP address or UNIX domain socket name. |

| `network.peer.port` | `int` | {"recommended": "If `network.peer.address` is set."} | Peer port number of the network connection. |

| `network.protocol.name` | `string` | {"conditionally_required": "If not `http` and `network.protocol.version` is set."} | [OSI application layer](https://wikipedia.org/wiki/Application_layer) or non-OSI equivalent. |

| `network.protocol.version` | `string` | recommended | The actual version of the protocol used for network communication. |

| `network.transport` | `{"members": [{"brief": "TCP", "id": "tcp", "stability": "stable", "value": "tcp"}, {"brief": "UDP", "id": "udp", "stability": "stable", "value": "udp"}, {"brief": "Named or anonymous pipe.", "id": "pipe", "stability": "stable", "value": "pipe"}, {"brief": "UNIX domain socket", "id": "unix", "stability": "stable", "value": "unix"}, {"brief": "QUIC", "id": "quic", "stability": "stable", "value": "quic"}]}` | opt_in | [OSI transport layer](https://wikipedia.org/wiki/Transport_layer) or [inter-process communication method](https://wikipedia.org/wiki/Inter-process_communication).
 |

| `server.address` | `string` | required | Server domain name if available without reverse DNS lookup; otherwise, IP address or UNIX domain socket name. |

| `server.port` | `int` | required | Server port number. |

| `url.full` | `string` | required | Absolute URL describing a network resource according to [RFC3986](https://www.rfc-editor.org/rfc/rfc3986) |

| `url.scheme` | `string` | opt_in | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |

| `url.template` | `string` | opt_in | The low-cardinality template of an [absolute path reference](https://www.rfc-editor.org/rfc/rfc3986#section-4.2).
 |

| `user_agent.original` | `string` | opt_in | Value of the [HTTP User-Agent](https://www.rfc-editor.org/rfc/rfc9110.html#field.user-agent) header sent by the client.
 |

| `user_agent.synthetic.type` | `{"members": [{"brief": "Bot source.", "id": "bot", "stability": "development", "value": "bot"}, {"brief": "Synthetic test source.", "id": "test", "stability": "development", "value": "test"}]}` | opt_in | Specifies the category of synthetic traffic, such as tests or bots.
 |



## `span.http.server`

This span represents an inbound HTTP request.


| Property | Value |
| --- | --- |
| Kind | `server` |
| Stability | `stable` |


**Span name:** refer to the [Span Name](/docs/http/http-spans.md#name) section.

**Span kind** MUST be `SERVER`.

**Span status:** refer to the [Span Status](/docs/http/http-spans.md#status) section.



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `client.address` | `string` | recommended | Client address - domain name if available without reverse DNS lookup; otherwise, IP address or UNIX domain socket name. |

| `client.port` | `int` | opt_in | The port of whichever client was captured in `client.address`. |

| `error.type` | `{"members": [{"brief": "A fallback error value to be used when the instrumentation doesn't define a custom value.\n", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | {"conditionally_required": "If request has ended with an error."} | Describes a class of error the operation ended with.
 |

| `http.request.body.size` | `int` | opt_in | The size of the request payload body in bytes. This is the number of bytes transferred excluding headers and is often, but not always, present as the [Content-Length](https://www.rfc-editor.org/rfc/rfc9110.html#field.content-length) header. For requests using transport encoding, this should be the compressed size.
 |

| `http.request.header` | `template[string[]]` | opt_in | HTTP request headers, `<key>` being the normalized HTTP Header name (lowercase), the value being the header values.
 |

| `http.request.method` | `{"members": [{"brief": "CONNECT method.", "id": "connect", "stability": "stable", "value": "CONNECT"}, {"brief": "DELETE method.", "id": "delete", "stability": "stable", "value": "DELETE"}, {"brief": "GET method.", "id": "get", "stability": "stable", "value": "GET"}, {"brief": "HEAD method.", "id": "head", "stability": "stable", "value": "HEAD"}, {"brief": "OPTIONS method.", "id": "options", "stability": "stable", "value": "OPTIONS"}, {"brief": "PATCH method.", "id": "patch", "stability": "stable", "value": "PATCH"}, {"brief": "POST method.", "id": "post", "stability": "stable", "value": "POST"}, {"brief": "PUT method.", "id": "put", "stability": "stable", "value": "PUT"}, {"brief": "TRACE method.", "id": "trace", "stability": "stable", "value": "TRACE"}, {"brief": "QUERY method.", "id": "query", "stability": "development", "value": "QUERY"}, {"brief": "Any HTTP method that the instrumentation has no prior knowledge of.", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | required | HTTP request method. |

| `http.request.method_original` | `string` | {"conditionally_required": "If and only if it's different than `http.request.method`."} | Original HTTP method sent by the client in the request line. |

| `http.request.size` | `int` | opt_in | The total size of the request in bytes. This should be the total number of bytes sent over the wire, including the request line (HTTP/1.1), framing (HTTP/2 and HTTP/3), headers, and request body if any.
 |

| `http.response.body.size` | `int` | opt_in | The size of the response payload body in bytes. This is the number of bytes transferred excluding headers and is often, but not always, present as the [Content-Length](https://www.rfc-editor.org/rfc/rfc9110.html#field.content-length) header. For requests using transport encoding, this should be the compressed size.
 |

| `http.response.header` | `template[string[]]` | opt_in | HTTP response headers, `<key>` being the normalized HTTP Header name (lowercase), the value being the header values.
 |

| `http.response.size` | `int` | opt_in | The total size of the response in bytes. This should be the total number of bytes sent over the wire, including the status line (HTTP/1.1), framing (HTTP/2 and HTTP/3), headers, and response body and trailers if any.
 |

| `http.response.status_code` | `int` | {"conditionally_required": "If and only if one was received/sent."} | [HTTP response status code](https://tools.ietf.org/html/rfc7231#section-6). |

| `http.route` | `string` | {"conditionally_required": "If and only if it's available"} | The matched route template for the request. This MUST be low-cardinality and include all static path segments, with dynamic path segments represented with placeholders.
 |

| `network.local.address` | `string` | opt_in | Local socket address. Useful in case of a multi-IP host. |

| `network.local.port` | `int` | opt_in | Local socket port. Useful in case of a multi-port host. |

| `network.peer.address` | `string` | recommended | Peer address of the network connection - IP address or UNIX domain socket name. |

| `network.peer.port` | `int` | {"recommended": "If `network.peer.address` is set."} | Peer port number of the network connection. |

| `network.protocol.name` | `string` | {"conditionally_required": "If not `http` and `network.protocol.version` is set."} | [OSI application layer](https://wikipedia.org/wiki/Application_layer) or non-OSI equivalent. |

| `network.protocol.version` | `string` | recommended | The actual version of the protocol used for network communication. |

| `network.transport` | `{"members": [{"brief": "TCP", "id": "tcp", "stability": "stable", "value": "tcp"}, {"brief": "UDP", "id": "udp", "stability": "stable", "value": "udp"}, {"brief": "Named or anonymous pipe.", "id": "pipe", "stability": "stable", "value": "pipe"}, {"brief": "UNIX domain socket", "id": "unix", "stability": "stable", "value": "unix"}, {"brief": "QUIC", "id": "quic", "stability": "stable", "value": "quic"}]}` | opt_in | [OSI transport layer](https://wikipedia.org/wiki/Transport_layer) or [inter-process communication method](https://wikipedia.org/wiki/Inter-process_communication).
 |

| `server.address` | `string` | recommended | Name of the local HTTP server that received the request.
 |

| `server.port` | `int` | {"conditionally_required": "If available and `server.address` is set."} | Port of the local HTTP server that received the request.
 |

| `url.path` | `string` | required | The [URI path](https://www.rfc-editor.org/rfc/rfc3986#section-3.3) component
 |

| `url.query` | `string` | {"conditionally_required": "If and only if one was received/sent."} | The [URI query](https://www.rfc-editor.org/rfc/rfc3986#section-3.4) component
 |

| `url.scheme` | `string` | required | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |

| `user_agent.original` | `string` | recommended | Value of the [HTTP User-Agent](https://www.rfc-editor.org/rfc/rfc9110.html#field.user-agent) header sent by the client.
 |

| `user_agent.synthetic.type` | `{"members": [{"brief": "Bot source.", "id": "bot", "stability": "development", "value": "bot"}, {"brief": "Synthetic test source.", "id": "test", "stability": "development", "value": "test"}]}` | opt_in | Specifies the category of synthetic traffic, such as tests or bots.
 |



# Metrics


## `dice.rolls`

The number of dice rolls, partitioned by roll value.

| Property | Value |
| --- | --- |
| Instrument | `counter` |
| Unit | `{roll}` |
| Stability | `development` |



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `roll.value` | `int` | required | The value produced by rolling the die. |



## `http.client.active_requests`

Number of active HTTP requests.

| Property | Value |
| --- | --- |
| Instrument | `updowncounter` |
| Unit | `{request}` |
| Stability | `development` |



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `http.request.method` | `{"members": [{"brief": "CONNECT method.", "id": "connect", "stability": "stable", "value": "CONNECT"}, {"brief": "DELETE method.", "id": "delete", "stability": "stable", "value": "DELETE"}, {"brief": "GET method.", "id": "get", "stability": "stable", "value": "GET"}, {"brief": "HEAD method.", "id": "head", "stability": "stable", "value": "HEAD"}, {"brief": "OPTIONS method.", "id": "options", "stability": "stable", "value": "OPTIONS"}, {"brief": "PATCH method.", "id": "patch", "stability": "stable", "value": "PATCH"}, {"brief": "POST method.", "id": "post", "stability": "stable", "value": "POST"}, {"brief": "PUT method.", "id": "put", "stability": "stable", "value": "PUT"}, {"brief": "TRACE method.", "id": "trace", "stability": "stable", "value": "TRACE"}, {"brief": "QUERY method.", "id": "query", "stability": "development", "value": "QUERY"}, {"brief": "Any HTTP method that the instrumentation has no prior knowledge of.", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | recommended | HTTP request method. |

| `server.address` | `string` | required | Server domain name if available without reverse DNS lookup; otherwise, IP address or UNIX domain socket name. |

| `server.port` | `int` | required | Server port number. |

| `url.scheme` | `string` | opt_in | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |

| `url.template` | `string` | {"conditionally_required": "If available."} | The low-cardinality template of an [absolute path reference](https://www.rfc-editor.org/rfc/rfc3986#section-4.2).
 |



## `http.client.connection.duration`

The duration of the successfully established outbound HTTP connections.

| Property | Value |
| --- | --- |
| Instrument | `histogram` |
| Unit | `s` |
| Stability | `development` |



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `network.peer.address` | `string` | opt_in | Peer address of the network connection - IP address or UNIX domain socket name. |

| `network.protocol.version` | `string` | recommended | The actual version of the protocol used for network communication. |

| `server.address` | `string` | required | Server domain name if available without reverse DNS lookup; otherwise, IP address or UNIX domain socket name. |

| `server.port` | `int` | required | Server port number. |

| `url.scheme` | `string` | opt_in | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |



## `http.client.open_connections`

Number of outbound HTTP connections that are currently active or idle on the client.

| Property | Value |
| --- | --- |
| Instrument | `updowncounter` |
| Unit | `{connection}` |
| Stability | `development` |



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `http.connection.state` | `{"members": [{"brief": "active state.", "id": "active", "stability": "development", "value": "active"}, {"brief": "idle state.", "id": "idle", "stability": "development", "value": "idle"}]}` | required | State of the HTTP connection in the HTTP connection pool. |

| `network.peer.address` | `string` | opt_in | Peer address of the network connection - IP address or UNIX domain socket name. |

| `network.protocol.version` | `string` | recommended | The actual version of the protocol used for network communication. |

| `server.address` | `string` | required | Server domain name if available without reverse DNS lookup; otherwise, IP address or UNIX domain socket name. |

| `server.port` | `int` | required | Server port number. |

| `url.scheme` | `string` | opt_in | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |



## `http.client.request.body.size`

Size of HTTP client request bodies.

| Property | Value |
| --- | --- |
| Instrument | `histogram` |
| Unit | `By` |
| Stability | `development` |


The size of the request payload body in bytes. This is the number of bytes transferred excluding headers and is often, but not always, present as the [Content-Length](https://www.rfc-editor.org/rfc/rfc9110.html#field.content-length) header. For requests using transport encoding, this should be the compressed size.



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `error.type` | `{"members": [{"brief": "A fallback error value to be used when the instrumentation doesn't define a custom value.\n", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | {"conditionally_required": "If request has ended with an error."} | Describes a class of error the operation ended with.
 |

| `http.request.method` | `{"members": [{"brief": "CONNECT method.", "id": "connect", "stability": "stable", "value": "CONNECT"}, {"brief": "DELETE method.", "id": "delete", "stability": "stable", "value": "DELETE"}, {"brief": "GET method.", "id": "get", "stability": "stable", "value": "GET"}, {"brief": "HEAD method.", "id": "head", "stability": "stable", "value": "HEAD"}, {"brief": "OPTIONS method.", "id": "options", "stability": "stable", "value": "OPTIONS"}, {"brief": "PATCH method.", "id": "patch", "stability": "stable", "value": "PATCH"}, {"brief": "POST method.", "id": "post", "stability": "stable", "value": "POST"}, {"brief": "PUT method.", "id": "put", "stability": "stable", "value": "PUT"}, {"brief": "TRACE method.", "id": "trace", "stability": "stable", "value": "TRACE"}, {"brief": "QUERY method.", "id": "query", "stability": "development", "value": "QUERY"}, {"brief": "Any HTTP method that the instrumentation has no prior knowledge of.", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | required | HTTP request method. |

| `http.response.status_code` | `int` | {"conditionally_required": "If and only if one was received/sent."} | [HTTP response status code](https://tools.ietf.org/html/rfc7231#section-6). |

| `network.protocol.name` | `string` | {"conditionally_required": "If not `http` and `network.protocol.version` is set."} | [OSI application layer](https://wikipedia.org/wiki/Application_layer) or non-OSI equivalent. |

| `network.protocol.version` | `string` | recommended | The actual version of the protocol used for network communication. |

| `server.address` | `string` | required | Server domain name if available without reverse DNS lookup; otherwise, IP address or UNIX domain socket name. |

| `server.port` | `int` | required | Server port number. |

| `url.scheme` | `string` | opt_in | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |

| `url.template` | `string` | {"conditionally_required": "If available."} | The low-cardinality template of an [absolute path reference](https://www.rfc-editor.org/rfc/rfc3986#section-4.2).
 |



## `http.client.request.duration`

Duration of HTTP client requests.

| Property | Value |
| --- | --- |
| Instrument | `histogram` |
| Unit | `s` |
| Stability | `stable` |



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `error.type` | `{"members": [{"brief": "A fallback error value to be used when the instrumentation doesn't define a custom value.\n", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | {"conditionally_required": "If request has ended with an error."} | Describes a class of error the operation ended with.
 |

| `http.request.method` | `{"members": [{"brief": "CONNECT method.", "id": "connect", "stability": "stable", "value": "CONNECT"}, {"brief": "DELETE method.", "id": "delete", "stability": "stable", "value": "DELETE"}, {"brief": "GET method.", "id": "get", "stability": "stable", "value": "GET"}, {"brief": "HEAD method.", "id": "head", "stability": "stable", "value": "HEAD"}, {"brief": "OPTIONS method.", "id": "options", "stability": "stable", "value": "OPTIONS"}, {"brief": "PATCH method.", "id": "patch", "stability": "stable", "value": "PATCH"}, {"brief": "POST method.", "id": "post", "stability": "stable", "value": "POST"}, {"brief": "PUT method.", "id": "put", "stability": "stable", "value": "PUT"}, {"brief": "TRACE method.", "id": "trace", "stability": "stable", "value": "TRACE"}, {"brief": "QUERY method.", "id": "query", "stability": "development", "value": "QUERY"}, {"brief": "Any HTTP method that the instrumentation has no prior knowledge of.", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | required | HTTP request method. |

| `http.response.status_code` | `int` | {"conditionally_required": "If and only if one was received/sent."} | [HTTP response status code](https://tools.ietf.org/html/rfc7231#section-6). |

| `network.protocol.name` | `string` | {"conditionally_required": "If not `http` and `network.protocol.version` is set."} | [OSI application layer](https://wikipedia.org/wiki/Application_layer) or non-OSI equivalent. |

| `network.protocol.version` | `string` | recommended | The actual version of the protocol used for network communication. |

| `server.address` | `string` | required | Server domain name if available without reverse DNS lookup; otherwise, IP address or UNIX domain socket name. |

| `server.port` | `int` | required | Server port number. |

| `url.scheme` | `string` | opt_in | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |

| `url.template` | `string` | opt_in | The low-cardinality template of an [absolute path reference](https://www.rfc-editor.org/rfc/rfc3986#section-4.2).
 |



## `http.client.response.body.size`

Size of HTTP client response bodies.

| Property | Value |
| --- | --- |
| Instrument | `histogram` |
| Unit | `By` |
| Stability | `development` |


The size of the response payload body in bytes. This is the number of bytes transferred excluding headers and is often, but not always, present as the [Content-Length](https://www.rfc-editor.org/rfc/rfc9110.html#field.content-length) header. For requests using transport encoding, this should be the compressed size.



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `error.type` | `{"members": [{"brief": "A fallback error value to be used when the instrumentation doesn't define a custom value.\n", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | {"conditionally_required": "If request has ended with an error."} | Describes a class of error the operation ended with.
 |

| `http.request.method` | `{"members": [{"brief": "CONNECT method.", "id": "connect", "stability": "stable", "value": "CONNECT"}, {"brief": "DELETE method.", "id": "delete", "stability": "stable", "value": "DELETE"}, {"brief": "GET method.", "id": "get", "stability": "stable", "value": "GET"}, {"brief": "HEAD method.", "id": "head", "stability": "stable", "value": "HEAD"}, {"brief": "OPTIONS method.", "id": "options", "stability": "stable", "value": "OPTIONS"}, {"brief": "PATCH method.", "id": "patch", "stability": "stable", "value": "PATCH"}, {"brief": "POST method.", "id": "post", "stability": "stable", "value": "POST"}, {"brief": "PUT method.", "id": "put", "stability": "stable", "value": "PUT"}, {"brief": "TRACE method.", "id": "trace", "stability": "stable", "value": "TRACE"}, {"brief": "QUERY method.", "id": "query", "stability": "development", "value": "QUERY"}, {"brief": "Any HTTP method that the instrumentation has no prior knowledge of.", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | required | HTTP request method. |

| `http.response.status_code` | `int` | {"conditionally_required": "If and only if one was received/sent."} | [HTTP response status code](https://tools.ietf.org/html/rfc7231#section-6). |

| `network.protocol.name` | `string` | {"conditionally_required": "If not `http` and `network.protocol.version` is set."} | [OSI application layer](https://wikipedia.org/wiki/Application_layer) or non-OSI equivalent. |

| `network.protocol.version` | `string` | recommended | The actual version of the protocol used for network communication. |

| `server.address` | `string` | required | Server domain name if available without reverse DNS lookup; otherwise, IP address or UNIX domain socket name. |

| `server.port` | `int` | required | Server port number. |

| `url.scheme` | `string` | opt_in | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |

| `url.template` | `string` | {"conditionally_required": "If available."} | The low-cardinality template of an [absolute path reference](https://www.rfc-editor.org/rfc/rfc3986#section-4.2).
 |



## `http.server.active_requests`

Number of active HTTP server requests.

| Property | Value |
| --- | --- |
| Instrument | `updowncounter` |
| Unit | `{request}` |
| Stability | `development` |



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `http.request.method` | `{"members": [{"brief": "CONNECT method.", "id": "connect", "stability": "stable", "value": "CONNECT"}, {"brief": "DELETE method.", "id": "delete", "stability": "stable", "value": "DELETE"}, {"brief": "GET method.", "id": "get", "stability": "stable", "value": "GET"}, {"brief": "HEAD method.", "id": "head", "stability": "stable", "value": "HEAD"}, {"brief": "OPTIONS method.", "id": "options", "stability": "stable", "value": "OPTIONS"}, {"brief": "PATCH method.", "id": "patch", "stability": "stable", "value": "PATCH"}, {"brief": "POST method.", "id": "post", "stability": "stable", "value": "POST"}, {"brief": "PUT method.", "id": "put", "stability": "stable", "value": "PUT"}, {"brief": "TRACE method.", "id": "trace", "stability": "stable", "value": "TRACE"}, {"brief": "QUERY method.", "id": "query", "stability": "development", "value": "QUERY"}, {"brief": "Any HTTP method that the instrumentation has no prior knowledge of.", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | required | HTTP request method. |

| `server.address` | `string` | opt_in | Name of the local HTTP server that received the request.
 |

| `server.port` | `int` | opt_in | Port of the local HTTP server that received the request.
 |

| `url.scheme` | `string` | required | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |



## `http.server.request.body.size`

Size of HTTP server request bodies.

| Property | Value |
| --- | --- |
| Instrument | `histogram` |
| Unit | `By` |
| Stability | `development` |


The size of the request payload body in bytes. This is the number of bytes transferred excluding headers and is often, but not always, present as the [Content-Length](https://www.rfc-editor.org/rfc/rfc9110.html#field.content-length) header. For requests using transport encoding, this should be the compressed size.



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `error.type` | `{"members": [{"brief": "A fallback error value to be used when the instrumentation doesn't define a custom value.\n", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | {"conditionally_required": "If request has ended with an error."} | Describes a class of error the operation ended with.
 |

| `http.request.method` | `{"members": [{"brief": "CONNECT method.", "id": "connect", "stability": "stable", "value": "CONNECT"}, {"brief": "DELETE method.", "id": "delete", "stability": "stable", "value": "DELETE"}, {"brief": "GET method.", "id": "get", "stability": "stable", "value": "GET"}, {"brief": "HEAD method.", "id": "head", "stability": "stable", "value": "HEAD"}, {"brief": "OPTIONS method.", "id": "options", "stability": "stable", "value": "OPTIONS"}, {"brief": "PATCH method.", "id": "patch", "stability": "stable", "value": "PATCH"}, {"brief": "POST method.", "id": "post", "stability": "stable", "value": "POST"}, {"brief": "PUT method.", "id": "put", "stability": "stable", "value": "PUT"}, {"brief": "TRACE method.", "id": "trace", "stability": "stable", "value": "TRACE"}, {"brief": "QUERY method.", "id": "query", "stability": "development", "value": "QUERY"}, {"brief": "Any HTTP method that the instrumentation has no prior knowledge of.", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | required | HTTP request method. |

| `http.response.status_code` | `int` | {"conditionally_required": "If and only if one was received/sent."} | [HTTP response status code](https://tools.ietf.org/html/rfc7231#section-6). |

| `http.route` | `string` | {"conditionally_required": "If and only if it's available"} | The matched route template for the request. This MUST be low-cardinality and include all static path segments, with dynamic path segments represented with placeholders.
 |

| `network.protocol.name` | `string` | {"conditionally_required": "If not `http` and `network.protocol.version` is set."} | [OSI application layer](https://wikipedia.org/wiki/Application_layer) or non-OSI equivalent. |

| `network.protocol.version` | `string` | recommended | The actual version of the protocol used for network communication. |

| `server.address` | `string` | opt_in | Name of the local HTTP server that received the request.
 |

| `server.port` | `int` | opt_in | Port of the local HTTP server that received the request.
 |

| `url.scheme` | `string` | required | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |

| `user_agent.synthetic.type` | `{"members": [{"brief": "Bot source.", "id": "bot", "stability": "development", "value": "bot"}, {"brief": "Synthetic test source.", "id": "test", "stability": "development", "value": "test"}]}` | opt_in | Specifies the category of synthetic traffic, such as tests or bots.
 |



## `http.server.request.duration`

Duration of HTTP server requests.

| Property | Value |
| --- | --- |
| Instrument | `histogram` |
| Unit | `s` |
| Stability | `stable` |



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `error.type` | `{"members": [{"brief": "A fallback error value to be used when the instrumentation doesn't define a custom value.\n", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | {"conditionally_required": "If request has ended with an error."} | Describes a class of error the operation ended with.
 |

| `http.request.method` | `{"members": [{"brief": "CONNECT method.", "id": "connect", "stability": "stable", "value": "CONNECT"}, {"brief": "DELETE method.", "id": "delete", "stability": "stable", "value": "DELETE"}, {"brief": "GET method.", "id": "get", "stability": "stable", "value": "GET"}, {"brief": "HEAD method.", "id": "head", "stability": "stable", "value": "HEAD"}, {"brief": "OPTIONS method.", "id": "options", "stability": "stable", "value": "OPTIONS"}, {"brief": "PATCH method.", "id": "patch", "stability": "stable", "value": "PATCH"}, {"brief": "POST method.", "id": "post", "stability": "stable", "value": "POST"}, {"brief": "PUT method.", "id": "put", "stability": "stable", "value": "PUT"}, {"brief": "TRACE method.", "id": "trace", "stability": "stable", "value": "TRACE"}, {"brief": "QUERY method.", "id": "query", "stability": "development", "value": "QUERY"}, {"brief": "Any HTTP method that the instrumentation has no prior knowledge of.", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | required | HTTP request method. |

| `http.response.status_code` | `int` | {"conditionally_required": "If and only if one was received/sent."} | [HTTP response status code](https://tools.ietf.org/html/rfc7231#section-6). |

| `http.route` | `string` | {"conditionally_required": "If and only if it's available"} | The matched route template for the request. This MUST be low-cardinality and include all static path segments, with dynamic path segments represented with placeholders.
 |

| `network.protocol.name` | `string` | {"conditionally_required": "If not `http` and `network.protocol.version` is set."} | [OSI application layer](https://wikipedia.org/wiki/Application_layer) or non-OSI equivalent. |

| `network.protocol.version` | `string` | recommended | The actual version of the protocol used for network communication. |

| `server.address` | `string` | opt_in | Name of the local HTTP server that received the request.
 |

| `server.port` | `int` | opt_in | Port of the local HTTP server that received the request.
 |

| `url.scheme` | `string` | required | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |

| `user_agent.synthetic.type` | `{"members": [{"brief": "Bot source.", "id": "bot", "stability": "development", "value": "bot"}, {"brief": "Synthetic test source.", "id": "test", "stability": "development", "value": "test"}]}` | opt_in | Specifies the category of synthetic traffic, such as tests or bots.
 |



## `http.server.response.body.size`

Size of HTTP server response bodies.

| Property | Value |
| --- | --- |
| Instrument | `histogram` |
| Unit | `By` |
| Stability | `development` |


The size of the response payload body in bytes. This is the number of bytes transferred excluding headers and is often, but not always, present as the [Content-Length](https://www.rfc-editor.org/rfc/rfc9110.html#field.content-length) header. For requests using transport encoding, this should be the compressed size.



### Attributes

| Name | Type | Requirement | Description |
| --- | --- | --- | --- |

| `error.type` | `{"members": [{"brief": "A fallback error value to be used when the instrumentation doesn't define a custom value.\n", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | {"conditionally_required": "If request has ended with an error."} | Describes a class of error the operation ended with.
 |

| `http.request.method` | `{"members": [{"brief": "CONNECT method.", "id": "connect", "stability": "stable", "value": "CONNECT"}, {"brief": "DELETE method.", "id": "delete", "stability": "stable", "value": "DELETE"}, {"brief": "GET method.", "id": "get", "stability": "stable", "value": "GET"}, {"brief": "HEAD method.", "id": "head", "stability": "stable", "value": "HEAD"}, {"brief": "OPTIONS method.", "id": "options", "stability": "stable", "value": "OPTIONS"}, {"brief": "PATCH method.", "id": "patch", "stability": "stable", "value": "PATCH"}, {"brief": "POST method.", "id": "post", "stability": "stable", "value": "POST"}, {"brief": "PUT method.", "id": "put", "stability": "stable", "value": "PUT"}, {"brief": "TRACE method.", "id": "trace", "stability": "stable", "value": "TRACE"}, {"brief": "QUERY method.", "id": "query", "stability": "development", "value": "QUERY"}, {"brief": "Any HTTP method that the instrumentation has no prior knowledge of.", "id": "other", "stability": "stable", "value": "_OTHER"}]}` | required | HTTP request method. |

| `http.response.status_code` | `int` | {"conditionally_required": "If and only if one was received/sent."} | [HTTP response status code](https://tools.ietf.org/html/rfc7231#section-6). |

| `http.route` | `string` | {"conditionally_required": "If and only if it's available"} | The matched route template for the request. This MUST be low-cardinality and include all static path segments, with dynamic path segments represented with placeholders.
 |

| `network.protocol.name` | `string` | {"conditionally_required": "If not `http` and `network.protocol.version` is set."} | [OSI application layer](https://wikipedia.org/wiki/Application_layer) or non-OSI equivalent. |

| `network.protocol.version` | `string` | recommended | The actual version of the protocol used for network communication. |

| `server.address` | `string` | opt_in | Name of the local HTTP server that received the request.
 |

| `server.port` | `int` | opt_in | Port of the local HTTP server that received the request.
 |

| `url.scheme` | `string` | required | The [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) component identifying the used protocol.
 |

| `user_agent.synthetic.type` | `{"members": [{"brief": "Bot source.", "id": "bot", "stability": "development", "value": "bot"}, {"brief": "Synthetic test source.", "id": "test", "stability": "development", "value": "test"}]}` | opt_in | Specifies the category of synthetic traffic, such as tests or bots.
 |



# Function Reference - Category: networking

## Table of Contents

- [create_session](#create_session)
- [enum_player](#enum_player)
- [enum_provider](#enum_provider)
- [getopenplay](#getopenplay)
- [https_get](#https_get)
- [https_post](#https_post)
- [join_session](#join_session)
- [send_request](#send_request)
- [send_result](#send_result)
- [setopenplay](#setopenplay)
- [share_connection_token](#share_connection_token)
- [websocket](#websocket)

# create_session

*Creates a new network session*

Creates a new multiplayer network session with the specified name. The local player is automatically added to the session. This function is typically used to host a multiplayer game that other players can join.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `session_name` | string *[optional]* = "in8" | Name of the session to create  |
| `player_name` | string *[optional]* = Current player name | Name of the local player  |

## Returns

**Type:** boolean

true if the session was created successfully, false otherwise

## Examples

```
create_session("dragon_quest", "Player1");
```

## Performance

**Complexity:** O(1)

## See Also

- [join_session](join_session)

---

# enum_player

*Enumerates a player in the peer-to-peer network*

Registers a player in the peer-to-peer network with a unique identifier and friendly name. This function is typically called when a player joins the game or when scanning the network for connected players. The candidates parameter provides a list of potential peer connections for the player in JSON format.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `id` | string  | Unique identifier for the player  |
| `name` | string  | Friendly name to display for the player  |
| `candidates` | string  | JSON list of candidate peers for this player  |

## Returns

**Type:** void

No return value

## Examples

```
enum_player("p12345", "Player1", "[{\"ip\":\"192.168.1.5\",\"port\":8080}]");
```

## Performance

**Complexity:** O(n) where n is the number of candidate peers

## See Also

- [enum_provider](enum_provider)
- [enum_room](enum_room)

---

# enum_provider

*Enumerates a service provider in the peer-to-peer network*

Registers a service provider in the peer-to-peer network with a unique identifier and friendly name. Service providers offer specific functionality to players, such as chat servers, item databases, discovery services, etc.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `id` | string  | Unique identifier for the provider  |
| `name` | string  | Friendly name to display for the provider  |

## Returns

**Type:** void

No return value

## Examples

```
enum_provider("chat_server_1", "Central Chat Server");
```

## Performance

**Complexity:** O(1)

## See Also

- [enum_player](enum_player)
- [enum_room](enum_room)

---

# getopenplay

*Gets a value from the OpenPlay shared data store*

Retrieves a value from the OpenPlay shared data store using the specified key. OpenPlay is a distributed key-value store that allows information sharing across players and game instances in the peer-to-peer network.

**Since:** v1.1.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `key` | string  | Key to retrieve  |

## Returns

**Type:** string

Value associated with the key, or empty string if not found

## Examples

```
string worldState = getopenplay("world.state");
```

## Performance

**Complexity:** O(1) for local cache, O(log n) for network lookup

Values are typically cached locally but may require network communication if the key is not in the local cache or has been updated by another peer.

## See Also

- [setopenplay](setopenplay)

---

# https_get

*Performs an HTTPS GET request to a server*

Sends an HTTPS GET request to the specified host and URI, and returns the server's response. This function is useful for retrieving data from external web services or APIs without requiring the player to leave the game.

**Since:** v1.5.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `host` | string  | Hostname or IP address of the server  |
| `uri` | string  | Resource path to request  |

## Returns

**Type:** string

First line of the response body, or empty string if no response

## Examples

```
string weather = https_get("api.weather.com", "/forecast/12345");
```

## Performance

**Complexity:** O(1) but network latency can vary

Network requests are asynchronous but the function call blocks until a response is received. Consider network timeouts and connectivity issues when using this function.

## See Also

- [https_post](https_post)
- [web_socket](web_socket)

---

# https_post

*Performs an HTTPS POST request to a server*

Sends an HTTPS POST request with the specified data to the given host and URI, and returns the server's response. This function is useful for submitting data to external web services or APIs, such as saving game state or interacting with external systems.

**Since:** v1.5.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `host` | string  | Hostname or IP address of the server  |
| `uri` | string  | Resource path to request  |
| `postData` | string  | Data to send in the request body  |

## Returns

**Type:** string

First line of the response body, or empty string if no response

## Examples

```
string response = https_post("api.game.com", "/save", "{\"score\":1000}");
```

## Performance

**Complexity:** O(1) but network latency can vary

Network requests are asynchronous but the function call blocks until a response is received. Consider network timeouts and connectivity issues when using this function.

## See Also

- [https_get](https_get)
- [web_socket](web_socket)

---

# join_session

*Joins an existing network session*

Connects to an existing multiplayer network session with the specified name. The local player is automatically added to the session. This function is typically used to join a multiplayer game hosted by another player.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `session_name` | string  | Name of the session to join  |

## Returns

**Type:** boolean

true if the session was joined successfully, false otherwise

## Examples

```
join_session("dragon_quest");
```

## Performance

**Complexity:** O(1)

## See Also

- [create_session](create_session)

---

# send_request

*Sends a request to another player or service in the network*

Sends an RPC (Remote Procedure Call) request to another player or service in the network. The request includes a method name and parameters. When the recipient responds, the specified future code will be executed. This function enables peer-to-peer communication and distributed game mechanics.

**Since:** v1.5.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `to` | string  | Recipient of the request (player ID or service name)  |
| `method` | string  | Method to call on the recipient  |
| `params` | string  | Parameters for the method (typically JSON)  |
| `future` | string  | Future code to execute when response is received  |

## Returns

**Type:** void

No return value

## Examples

```
send_request("player2", "trade.offer", "{\"item\":\"sword\",\"price\":100}", "handle_trade_response(result);");
```

## Performance

**Complexity:** O(1) for sending, but network latency varies

This function sends the request asynchronously, so it returns immediately without waiting for a response. The future code is executed when the response is received.

## See Also

- [send_result](send_result)
- [on_event_future](on_event_future)

---

# send_result

*Sends a result in response to a request*

Sends a result message in response to a previously received RPC request. The result includes the method name, parameters, and the ID of the original request. This function is used to complete the request-response cycle in peer-to-peer communication.

**Since:** v1.5.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `to` | string  | Recipient of the result (player ID or service name)  |
| `method` | string  | Method that was called  |
| `params` | string  | Result parameters (typically JSON)  |
| `id` | integer  | Request ID that this result is responding to  |

## Returns

**Type:** void

No return value

## Examples

```
send_result("player1", "trade.offer", "{\"accepted\":true}", request_id);
```

## Performance

**Complexity:** O(1) for sending, but network latency varies

This function sends the result asynchronously, so it returns immediately without waiting for acknowledgment from the recipient.

## See Also

- [send_request](send_request)

---

# setopenplay

*Sets a value in the OpenPlay shared data store*

Stores a value in the OpenPlay shared data store under the specified key. The value will be propagated to other peers in the network, allowing for distributed state management across game instances.

**Since:** v1.1.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `key` | string  | Key to set  |
| `value` | string  | Value to associate with the key  |

## Returns

**Type:** integer

1 if successful, 0 otherwise

## Examples

```
setopenplay("door.unlocked", "true");
```

## Performance

**Complexity:** O(log n) for network propagation

Setting values triggers network communication to propagate the changes to other peers. Consider batching updates to reduce network overhead.

## See Also

- [getopenplay](getopenplay)

---

# share_connection_token

*Shares a connection token for joining a multiplayer session*

Generates a connection token containing information about the current multiplayer session (room ID, IP address, and connection candidates), then initiates the system's sharing mechanism to allow the player to share this token with friends. Recipients can use this token to directly join the multiplayer session.

**Since:** v1.5.0

## Returns

**Type:** void

No return value

## Examples

```
share_connection_token();
```

## Performance

**Complexity:** O(1)

This function triggers the system's sharing UI, which may temporarily pause or minimize the game on some platforms.

## See Also

- [share](share)
- [create_session](create_session)
- [join_session](join_session)

---

# websocket

*Creates a WebSocket connection*

Establishes a WebSocket connection to a server, allowing for real-time bidirectional communication. The connection is assigned a name that can be used to reference it in other functions. WebSockets are useful for implementing chat, real-time updates, multiplayer features, and other interactive elements.

**Since:** v1.5.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `sockname` | string  | Name to assign to the socket connection  |
| `hostname` | string  | Server hostname or IP address  |
| `resource` | string  | Resource path on the server  |

## Returns

**Type:** string

The assigned socket name

## Examples

```
websocket("chat_socket", "chat.gameserver.com", "/ws/room/123");
```

## Performance

**Complexity:** O(1) but network latency can vary

WebSocket connections maintain an open connection to the server, which consumes resources. Limit the number of simultaneous connections and close them when no longer needed.

## See Also

- [https_get](https_get)
- [https_post](https_post)

---


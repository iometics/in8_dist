# Function Reference

## Table of Contents

- [assert](#assert)
- [audio_gain](#audio_gain)
- [audio_pause](#audio_pause)
- [audio_play](#audio_play)
- [audio_repeat](#audio_repeat)
- [audio_shuffle](#audio_shuffle)
- [audio_stop](#audio_stop)
- [audio_volume](#audio_volume)
- [call](#call)
- [control_refresh](#control_refresh)
- [create_session](#create_session)
- [drag](#drag)
- [drop](#drop)
- [effects_volume](#effects_volume)
- [enum_player](#enum_player)
- [enum_provider](#enum_provider)
- [enum_room](#enum_room)
- [finger](#finger)
- [genesis](#genesis)
- [get](#get)
- [get_control_value](#get_control_value)
- [get_theta](#get_theta)
- [getopenplay](#getopenplay)
- [got](#got)
- [grab](#grab)
- [https_get](#https_get)
- [https_post](#https_post)
- [iap_is_product_purchased](#iap_is_product_purchased)
- [iap_load_products](#iap_load_products)
- [iap_purchase_product](#iap_purchase_product)
- [iap_restore_purchases](#iap_restore_purchases)
- [import_csv](#import_csv)
- [join_session](#join_session)
- [json_element](#json_element)
- [load_game_state](#load_game_state)
- [loadview](#loadview)
- [log](#log)
- [music_volume](#music_volume)
- [on_event_future](#on_event_future)
- [open_web_page](#open_web_page)
- [playeffect](#playeffect)
- [playmusic](#playmusic)
- [rally](#rally)
- [recycle](#recycle)
- [reload](#reload)
- [replay](#replay)
- [run](#run)
- [save_game_state](#save_game_state)
- [send_request](#send_request)
- [send_result](#send_result)
- [set_control_value](#set_control_value)
- [set_theta](#set_theta)
- [setopenplay](#setopenplay)
- [setsleep](#setsleep)
- [settrace](#settrace)
- [share](#share)
- [share_bug_report](#share_bug_report)
- [share_connection_token](#share_connection_token)
- [signal](#signal)
- [sleep](#sleep)
- [slew](#slew)
- [stopmusic](#stopmusic)
- [unloadview](#unloadview)
- [usleep](#usleep)
- [warp](#warp)
- [websocket](#websocket)
- [write](#write)

# assert

*Asserts a condition with an error message*

Evaluates a boolean condition and displays an error message if the condition is false. Typically used for validation and error checking in scripts.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `condition` | boolean  | The condition to evaluate  |
| `message` | string  | Error message to display if the condition is false  |

## Returns

**Type:** boolean

True if the condition is true, false otherwise

## Examples

```
assert(players > 0, "No players found");
```

## Performance

**Complexity:** O(1)


---

# audio_gain

*Sets the gain level for a specific audio track*

Sets the gain (volume) level for a specific audio track. This allows for independent volume control of different audio elements like music and sound effects.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `label` | string  | Audio track identifier  |
| `gain` | integer  | Gain level (0-100)  |

## Returns

**Type:** void

No return value

## Examples

```
audio_gain("music", 50);  // Set music gain to 50%
```

## Performance

**Complexity:** O(1)

## See Also

- [audio_volume](audio_volume)

---

# audio_pause

*Pauses audio playback*

Pauses playback of the specified audio track. Playback can be resumed from the paused position using the audio_play function.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `label` | string  | Audio track identifier  |

## Returns

**Type:** void

No return value

## Examples

```
audio_pause("music");
```

## Performance

**Complexity:** O(1)

## See Also

- [audio_play](audio_play)
- [audio_stop](audio_stop)

---

# audio_play

*Plays audio tracks or playlists*

Starts playback of audio content. When called with no parameters, it resumes previously paused playback. When called with a label, it plays that specific track. When called with a label and playlist, it loads the playlist into the specified track and begins playback.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `label` | string *[optional]* = Empty string | Audio track identifier  |
| `playlist` | string *[optional]* = Empty string | Playlist to load  |
| `completion_handler` | string *[optional]* = Empty string | Code to execute when playback completes  |

## Returns

**Type:** void

No return value

## Examples

```
audio_play("music", "background.json");
```

## Performance

**Complexity:** O(1)

## See Also

- [audio_pause](audio_pause)
- [audio_stop](audio_stop)

---

# audio_repeat

*Sets repeat mode for an audio track*

Enables or disables repeat mode for the specified audio track. When repeat mode is enabled, the track or playlist will loop continuously until stopped or until repeat mode is disabled.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `label` | string  | Audio track identifier  |
| `onoff` | integer  | 1 to enable repeat, 0 to disable  |

## Returns

**Type:** void

No return value

## Examples

```
audio_repeat("music", 1);  // Enable repeat for music
```

## Performance

**Complexity:** O(1)

## See Also

- [audio_shuffle](audio_shuffle)

---

# audio_shuffle

*Sets shuffle mode for an audio track*

Enables or disables shuffle mode for the specified audio track. When shuffle mode is enabled, the tracks in a playlist will play in random order rather than sequentially.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `label` | string  | Audio track identifier  |
| `onoff` | integer  | 1 to enable shuffle, 0 to disable  |

## Returns

**Type:** void

No return value

## Examples

```
audio_shuffle("music", 1);  // Enable shuffle for music
```

## Performance

**Complexity:** O(1)

## See Also

- [audio_repeat](audio_repeat)

---

# audio_stop

*Stops audio playback*

Stops playback of the specified audio track. If a fade time is provided, the audio will gradually fade out over that duration before stopping.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `label` | string  | Audio track identifier  |
| `fadetime` | integer *[optional]* = 0 | Time in milliseconds to fade out  |

## Returns

**Type:** void

No return value

## Examples

```
audio_stop("music", 1000); // Stop with 1 second fade-out
```

## Performance

**Complexity:** O(1)

## See Also

- [audio_play](audio_play)
- [audio_pause](audio_pause)

---

# audio_volume

*Sets the master audio volume*

Sets the master volume level for all audio playback. The volume is specified as a value between 0 (silent) and 100 (maximum volume).

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `volume` | integer  | Volume level (0-100)  |

## Returns

**Type:** void

No return value

## Examples

```
audio_volume(75);  // Set volume to 75%
```

## Performance

**Complexity:** O(1)

## See Also

- [audio_gain](audio_gain)

---

# call

*Executes an in8 script synchronously*

Executes the specified in8 script in the current thread, blocking until the script completes. This is useful for running utility scripts or for executing sequential operations where the next step depends on the results of the script execution.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `script_name` | string  | Name or path of the script to execute  |
| `params` | string *[optional]* = Empty string | Parameters to pass to the script  |

## Returns

**Type:** integer

Status code returned by the script (0 for success)

## Examples

```
call("init_game.in8");
```

## Performance

**Complexity:** O(n) where n is the complexity of the script

## See Also

- [replay](replay)

---

# control_refresh

*Refreshes a control in a view*

Updates and redraws a specific UI control within a view. This is useful when the control's data has been updated programmatically and the visual representation needs to be refreshed to match the new data state.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `view_name` | string  | Name of the view containing the control  |
| `control_name` | string  | Name of the control to refresh  |

## Returns

**Type:** void

No return value

## Examples

```
control_refresh("main_menu", "player_stats");
```

## Performance

**Complexity:** O(1)

## See Also

- [get_control_value](get_control_value)
- [set_control_value](set_control_value)

---

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

# drag

*Drags an object to a state machine*

Simulates dragging an object to the specified state machine. This can be the currently held object or a specific object identified by its ID. This function is primarily used in automated testing to simulate user drag-and-drop interactions with game objects.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `machine` | string  | Name of the state machine to interact with  |
| `objectId` | string *[optional]* = Empty string | Identifier of the object to drag (optional, uses currently held object if omitted)  |

## Returns

**Type:** void

No return value

## Examples

```
drag("inventory_fsm", "sword_item");
```

## Performance

**Complexity:** O(1)

## See Also

- [grab](grab)
- [drop](drop)

---

# drop

*Drops an object onto a state machine*

Simulates dropping an object onto the specified state machine. This can be the currently held object or a specific object identified by its ID. This function is primarily used in automated testing to simulate user drag-and-drop interactions with game objects.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `machine` | string  | Name of the state machine to interact with  |
| `objectId` | string *[optional]* = Empty string | Identifier of the object to drop (optional, uses currently held object if omitted)  |

## Returns

**Type:** string

Identifier of the dropped object

## Examples

```
drop("target_fsm");
```

## Performance

**Complexity:** O(1)

## See Also

- [grab](grab)
- [drag](drag)

---

# effects_volume

*Gets or sets the volume level for sound effects*

Controls the volume level for all sound effects in the game. When called without parameters, it returns the current volume level. When called with a gain parameter, it sets the volume to the specified level and returns the new setting.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `gain` | integer *[optional]* = No parameter to get current level | New volume level (0-100, where 0 is silent and 100 is maximum volume)  |

## Returns

**Type:** integer

Current or new volume level

## Examples

```
// Set effects volume to 75%
effects_volume(75);
```

```
// Get current effects volume
int volume = effects_volume();
```

## Performance

**Complexity:** O(1)

## See Also

- [music_volume](music_volume)

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

# enum_room

*Enumerates a room in the game world*

Registers a room in the game world with a unique identifier and friendly name. Rooms represent distinct locations or areas in the game where players can gather and interact.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `roomId` | string  | Unique identifier for the room  |
| `friendly_name` | string  | Friendly name to display for the room  |

## Returns

**Type:** void

No return value

## Examples

```
enum_room("tavern_1", "The Golden Dragon Tavern");
```

## Performance

**Complexity:** O(1)

## See Also

- [enum_player](enum_player)
- [enum_provider](enum_provider)

---

# finger

*Displays a visualization of a state machine*

Generates and displays a visualization of a state machine, including its current state, transitions, and register values. This visualization is typically rendered as an HTML page or a Mermaid diagram. This function is useful for debugging and understanding complex state machine behaviors during development and runtime.

**Since:** v1.2.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `machine_id` | string  | Identifier of the state machine to visualize  |

## Returns

**Type:** string

"success" if machine was found and displayed, "error" otherwise

## Examples

```
finger("player_fsm");
```

## Performance

**Complexity:** O(n) where n is the number of states and transitions in the machine

## See Also

- [set_trace](set_trace)
- [signal](signal)

---

# genesis

*Resets the game state to its initial condition*

Completely resets the game state to its initial condition, as if the game was just started. This includes resetting all state machines, clearing all variables, and returning all objects to their original positions. This function is primarily used during development or for troubleshooting purposes.

**Since:** v1.0.0

## Returns

**Type:** void

No return value

## Examples

```
genesis();
```

## Performance

**Complexity:** O(n) where n is the number of active game elements

## See Also

- [load_game_state](load_game_state)
- [save_game_state](save_game_state)

---

# get

*Gets an object and places it in the player's hand*

Creates or retrieves an object with the specified name and places it in the player's hand. If the player is already holding an object, it will be replaced. The object is positioned at the center of the screen initially.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `objName` | string  | Name of the object to retrieve  |

## Returns

**Type:** string

The name of the object that was retrieved

## Examples

```
get("magic_sword");
```

## Performance

**Complexity:** O(1)

## See Also

- [got](got)
- [recycle](recycle)

---

# get_control_value

*Gets the value of a UI control in a view*

Retrieves the current text value of a UI control within a specific view. This function is useful for reading user input from text fields, retrieving the selected item from dropdowns, or checking the state of other UI controls.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `view_name` | string  | Name of the view containing the control  |
| `control_name` | string  | Name of the control to get the value from  |

## Returns

**Type:** string

The text value of the control

## Examples

```
string userName = get_control_value("login_screen", "username_field");
```

## Performance

**Complexity:** O(1)

## See Also

- [set_control_value](set_control_value)
- [control_refresh](control_refresh)

---

# get_theta

*Gets the player's facing angle (theta)*

Returns the current facing angle (theta) of the player character in degrees. The angle is typically measured clockwise from a reference direction (usually north or the positive y-axis). This function is useful for determining the player's orientation in the game world.

**Since:** v1.0.0

## Returns

**Type:** integer

Current theta value in degrees (0-359)

## Examples

```
int facing = get_theta();
```

## Performance

**Complexity:** O(1)

## See Also

- [set_theta](set_theta)

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

# got

*Gets the name of the object currently held by the player*

Returns the name of the object currently held by the player. If the player is not holding any object, an empty string is returned.

**Since:** v1.0.0

## Returns

**Type:** string

Name of the held object, or empty string if none

## Examples

```
string heldItem = got();
if (heldItem == "magic_key") {
  // Player has the key
}
```

## Performance

**Complexity:** O(1)

## See Also

- [get](get)
- [recycle](recycle)

---

# grab

*Grabs an object from a state machine*

Attempts to grab an object from the specified state machine. If successful, the object becomes the currently held object and its identifier is returned. This function is primarily used in automated testing to simulate user interactions with game objects.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `machine` | string  | Name of the state machine to interact with  |

## Returns

**Type:** string

Identifier of the grabbed object, or empty string if no object was grabbed

## Examples

```
string objId = grab("player_fsm");
```

## Performance

**Complexity:** O(1)

## See Also

- [drag](drag)
- [drop](drop)

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

# iap_is_product_purchased

*Checks if an in-app product has been purchased*

Checks if a non-consumable or subscription in-app product has been purchased by the user. This can be used to determine whether to grant access to premium features or content.

**Since:** v1.2.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `productId` | string  | Identifier of the product to check  |

## Returns

**Type:** boolean

True if the product has been purchased, false otherwise

## Examples

```
if (iap_is_product_purchased("com.example.premium")) {
  // Grant access to premium features
}
```

## Performance

**Complexity:** O(1)

## See Also

- [iap_purchase_product](iap_purchase_product)
- [iap_restore_purchases](iap_restore_purchases)

---

# iap_load_products

*Loads available in-app purchase products*

Queries the app store for information about available in-app purchase products. The product information includes details like price, description, and name, which can be displayed to the user in the app's store interface.

**Since:** v1.2.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `productIds` | string  | JSON array of product identifiers to load  |

## Returns

**Type:** void

No return value

## Examples

```
iap_load_products("[\"com.example.premium\", \"com.example.coins100\"]");
```

## Performance

**Complexity:** O(n) where n is the number of products

## See Also

- [iap_purchase_product](iap_purchase_product)
- [iap_restore_purchases](iap_restore_purchases)

---

# iap_purchase_product

*Initiates purchase of an in-app product*

Initiates the purchase flow for an in-app product. This will typically display the app store's purchase confirmation UI to the user, where they can confirm or cancel the purchase.

**Since:** v1.2.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `productId` | string  | Identifier of the product to purchase  |

## Returns

**Type:** void

No return value

## Examples

```
iap_purchase_product("com.example.premium");
```

## Performance

**Complexity:** O(1)

## See Also

- [iap_load_products](iap_load_products)
- [iap_is_product_purchased](iap_is_product_purchased)

---

# iap_restore_purchases

*Restores previously purchased in-app products*

Queries the app store for previously purchased non-consumable and subscription products. This is typically used when a user reinstalls the app or moves to a new device, allowing them to regain access to previously purchased content without having to buy it again.

**Since:** v1.2.0

## Returns

**Type:** void

No return value

## Examples

```
iap_restore_purchases();
```

## Performance

**Complexity:** O(n) where n is the number of previously purchased products

## See Also

- [iap_is_product_purchased](iap_is_product_purchased)

---

# import_csv

*Imports data from a CSV file and creates a predicate*

Downloads a CSV file from the specified URI, parses it, and creates a predicate with the data. The predicate can then be queried using standard in8 query syntax. This is useful for importing large datasets into the game for use in scripts.

**Since:** v1.3.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `predname` | string  | Name of the predicate to create  |
| `uri` | string  | URI of the CSV file to import  |
| `delimiter` | string  | Delimiter character used in the CSV file (typically "," or ";")  |
| `has_header` | boolean *[optional]* = false | Whether the CSV file has a header row  |

## Returns

**Type:** integer

Number of records imported

## Examples

```
int numItems = import_csv("items", "https://gamedata.com/items.csv", ",", true);
```

## Performance

**Complexity:** O(n) where n is the number of records in the CSV file

For large CSV files, this operation can be time-consuming. Consider caching the results or importing data during initialization rather than during gameplay.

## See Also

- [json_element](json_element)

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

# json_element

*Extracts an element from a JSON string*

Parses a JSON string and extracts a specific element using a path notation. For array elements, an optional index can be specified. This function is useful for working with data returned from web services or stored in the game.

**Since:** v1.2.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `json_data` | string  | JSON data to parse  |
| `json_element` | string  | Path to the element to extract (e.g., "user.name" or "items[0].id")  |
| `nth` | integer *[optional]* = 0 | Index for array elements  |

## Returns

**Type:** string

The extracted element as a string

## Examples

```
string playerName = json_element(userData, "player.profile.name");
```

```
string firstItemId = json_element(inventory, "items[0].id");
```

## Performance

**Complexity:** O(n) where n is the size of the JSON data

## See Also

- [import_csv](import_csv)

---

# load_game_state

*Loads a previously saved game state*

Loads a previously saved game state with the specified name. This restores the game to the exact condition it was in when the state was saved, including player position, inventory, quest progress, and world state. This function is typically used for implementing save/load functionality in games.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `name` | string  | Name of the saved game state to load  |

## Returns

**Type:** void

No return value

## Examples

```
load_game_state("checkpoint1");
```

## Performance

**Complexity:** O(n) where n is the size of the saved state

Loading large game states may cause a momentary pause in gameplay. Consider showing a loading screen for a smoother user experience.

## See Also

- [save_game_state](save_game_state)

---

# loadview

*Loads a view in the game world*

Loads a specific view (scene or location) in the game world. If the view cannot be loaded, the player is moved to the specified location using the slew function as a fallback. This function is also aliased as 'rally' for compatibility purposes.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `dest` | string  | Name of the view to load  |

## Returns

**Type:** void

No return value

## Examples

```
loadview("castle_interior");
```

## Performance

**Complexity:** O(n) where n is the complexity of the view

Loading complex views with many objects may cause temporary performance drops. Consider preloading important views during idle time for smoother transitions.

## See Also

- [unloadview](unloadview)
- [slew](slew)

---

# log

*Logs a message to the in8 log file*

Writes a message to the in8 log file. This function is useful for debugging, tracking game events, and logging error conditions. Multiple parameters can be passed and will be concatenated into a single log message.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `message` | string  | Message to log (can include multiple parameters)  |

## Returns

**Type:** void

No return value

## Examples

```
log("Player entered room: ", roomId);
```

## Performance

**Complexity:** O(1)

## See Also

- [write](write)

---

# music_volume

*Gets or sets the volume level for music*

Controls the volume level for background music in the game. When called without parameters, it returns the current volume level. When called with a gain parameter, it sets the volume to the specified level and returns the new setting.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `gain` | integer *[optional]* = No parameter to get current level | New volume level (0-100, where 0 is silent and 100 is maximum volume)  |

## Returns

**Type:** integer

Current or new volume level

## Examples

```
// Set music volume to 60%
music_volume(60);
```

```
// Get current music volume
int volume = music_volume();
```

## Performance

**Complexity:** O(1)

## See Also

- [effects_volume](effects_volume)

---

# on_event_future

*Sets up a future event handler*

Registers a code snippet to be executed when a specific event occurs in the future. This enables asynchronous event handling and is useful for responding to events that may occur after the current script has finished executing, such as network responses, timer completions, or user interactions.

**Since:** v1.2.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `event` | string  | Event to listen for  |
| `code` | string  | Code to execute when the event occurs  |

## Returns

**Type:** void

No return value

## Examples

```
on_event_future("network.response.received", "process_response(data);");
```

## Performance

**Complexity:** O(1)

## See Also

- [send_request](send_request)

---

# open_web_page

*Opens a web page in the default browser*

Opens the specified URL in the system's default web browser. This function allows the game to link to external resources such as documentation, community forums, or web-based game extensions without requiring the player to manually enter URLs.

**Since:** v1.3.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `url` | string  | URL of the web page to open  |

## Returns

**Type:** void

No return value

## Examples

```
open_web_page("https://www.example.com/game-guide");
```

## Performance

**Complexity:** O(1)

This function triggers an external application launch, which might briefly impact performance. On some platforms, the game might be paused while the browser is open.


---

# playeffect

*Plays a sound effect*

Plays a sound effect file once. Sound effects are typically short audio clips that are played in response to game events like button clicks, collisions, or other interactive elements.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `filename` | string  | Path to the sound effect file  |

## Returns

**Type:** void

No return value

## Examples

```
playeffect("explosion.wav");
```

## Performance

**Complexity:** O(1)

## See Also

- [audio_play_sample](audio_play_sample)

---

# playmusic

*Plays background music*

Plays a music track or playlist on the "music" audio channel. This is a convenience function that is equivalent to calling audio_play("music", playlist).

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `playlist` | string  | Playlist to play  |
| `completion_handler` | string *[optional]* = Empty string | Code to execute when playback completes  |

## Returns

**Type:** void

No return value

## Examples

```
playmusic("battle.json");
```

## Performance

**Complexity:** O(1)

## See Also

- [stopmusic](stopmusic)
- [audio_play](audio_play)

---

# rally

*Alias for loadview function*

This is an alias for the loadview function, which loads a specific view (scene or location) in the game world. The name 'rally' is provided for backward compatibility and script clarity.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `dest` | string  | Name of the view to load  |

## Returns

**Type:** void

No return value

## Examples

```
rally("castle_interior");
```

## Performance

**Complexity:** O(n) where n is the complexity of the view

## See Also

- [loadview](loadview)
- [unloadview](unloadview)

---

# recycle

*Recycles (disposes of) the object currently held by the player*

Removes the object currently held by the player and places it in the recycle bin. This effectively removes the object from the game world. If the player is not holding any object, this function has no effect.

**Since:** v1.0.0

## Returns

**Type:** string

Name of the recycled object, or empty string if none was held

## Examples

```
string recycledItem = recycle();
```

## Performance

**Complexity:** O(1)

## See Also

- [get](get)
- [got](got)

---

# reload

*Reloads the current game state*

Reloads the current game state, refreshing resources and potentially resetting certain elements. This function is primarily used during development for testing changes without restarting the game.

**Since:** v1.0.0

## Returns

**Type:** string

Status message

## Examples

```
reload();
```

## Performance

**Complexity:** O(n) where n is the complexity of the current game state

Reloading can be resource-intensive and may cause temporary freezes. Use sparingly and preferably only during development.


---

# replay

*Executes an in8 script asynchronously*

Executes the specified in8 script in a background thread, allowing the current script to continue execution. This is useful for running operations that should happen concurrently with the main script execution, such as animations, background loading, or parallel tasks.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `script_name` | string  | Name or path of the script to execute  |
| `params` | string *[optional]* = Empty string | Parameters to pass to the script  |

## Returns

**Type:** integer

Status code (0 for success in starting the script)

## Examples

```
replay("background_animation.in8");
```

## Performance

**Complexity:** O(1) for starting the script, script complexity depends on the script itself

## See Also

- [call](call)

---

# run

*Alias for replay - executes an in8 script asynchronously*

This is an alias for the replay function, which executes the specified in8 script in a background thread. The name 'run' is provided for convenience and script clarity.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `script_name` | string  | Name or path of the script to execute  |
| `params` | string *[optional]* = Empty string | Parameters to pass to the script  |

## Returns

**Type:** integer

Status code (0 for success in starting the script)

## Examples

```
run("background_animation.in8");
```

## Performance

**Complexity:** O(1) for starting the script, script complexity depends on the script itself

## See Also

- [replay](replay)
- [call](call)

---

# save_game_state

*Saves the current game state*

Saves the current game state under the specified name. This preserves the current condition of the game, including player position, inventory, quest progress, and world state. The saved state can later be restored using load_game_state. If no name is provided, a default name is used.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `name` | string *[optional]* = Default name based on timestamp | Name to save the game state under  |

## Returns

**Type:** void

No return value

## Examples

```
// Save with custom name
save_game_state("before_boss_fight");
```

```
// Save with default name
save_game_state();
```

## Performance

**Complexity:** O(n) where n is the size of the game state

Saving large game states may cause a momentary pause in gameplay. Consider performing saves during natural breaks in gameplay for a smoother user experience.

## See Also

- [load_game_state](load_game_state)

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

# set_control_value

*Sets the value of a UI control in a view*

Sets the text value of a UI control within a specific view. This function can be used to programmatically populate text fields, select items in dropdowns, update labels, or set the state of other UI controls.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `view_name` | string  | Name of the view containing the control  |
| `control_name` | string  | Name of the control to set the value for  |
| `value` | string  | New value to set  |

## Returns

**Type:** string

The value that was set

## Examples

```
set_control_value("player_info", "health_label", "100");
```

## Performance

**Complexity:** O(1)

## See Also

- [get_control_value](get_control_value)
- [control_refresh](control_refresh)

---

# set_theta

*Sets the player's facing angle (theta)*

Changes the facing angle (theta) of the player character to the specified value in degrees. The angle is typically measured clockwise from a reference direction (usually north or the positive y-axis). This function is useful for programmatically rotating the player to face a specific direction.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `theta` | integer  | New theta value in degrees (0-359)  |

## Returns

**Type:** void

No return value

## Examples

```
// Turn player to face east
set_theta(90);
```

## Performance

**Complexity:** O(1)

## See Also

- [get_theta](get_theta)

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

# setsleep

*Sets the default sleep time between operations*

Sets the default sleep time in seconds that is automatically applied between operations like grab, drag, and drop. This is useful for slowing down automated testing scripts to make them more visible or to account for animation timing.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `seconds` | integer  | Number of seconds to sleep between operations  |

## Returns

**Type:** void

No return value

## Examples

```
setsleep(1);  // Set a 1-second delay between operations
```

## Performance

**Complexity:** O(1)

## See Also

- [sleep](sleep)

---

# settrace

*Sets the trace level for a state machine*

Configures the tracing level for a specific state machine. When tracing is enabled, the system will generate visual animations and logs of the state machine's operation, showing transitions between states and the values of registers. Higher trace levels provide more detailed information.

**Since:** v1.2.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `id` | string  | Identifier of the state machine  |
| `trace_level` | integer  | Level of tracing to enable (0-10, where 0 disables tracing)  |

## Returns

**Type:** variant<int, string>

The trace level that was set, or error message if machine not found

## Examples

```
settrace("player_fsm", 5);
```

## Performance

**Complexity:** O(1)

Higher trace levels may impact performance, especially for complex state machines with many transitions. Use with caution in production environments.

## See Also

- [finger](finger)
- [signal](signal)

---

# share

*Shares data with an external application*

Creates a file with the specified content and initiates the system's sharing mechanism to allow the player to share the file via email, social media, messaging apps, etc. This is useful for sharing game achievements, screenshots, save files, or custom content.

**Since:** v1.4.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `text` | string  | Text data to share  |
| `filename` | string  | Name of the file to create  |

## Returns

**Type:** void

No return value

## Examples

```
share("I scored 1000 points in Dragon Quest!", "achievement.txt");
```

## Performance

**Complexity:** O(n) where n is the size of the text

This function triggers the system's sharing UI, which may temporarily pause or minimize the game on some platforms.

## See Also

- [share_bug_report](share_bug_report)
- [share_connection_token](share_connection_token)

---

# share_bug_report

*Shares a bug report containing logs and runtime information*

Automatically collects log files and runtime information about the game, then initiates the system's sharing mechanism to allow the player to send this information to the developers. This simplifies the process of reporting bugs and provides the developers with the information they need to diagnose issues.

**Since:** v1.4.0

## Returns

**Type:** void

No return value

## Examples

```
share_bug_report();
```

## Performance

**Complexity:** O(n) where n is the size of the log files

This function collects and packages multiple files, which may take a few seconds depending on the size of the logs. The system's sharing UI will also be displayed, which may temporarily pause or minimize the game on some platforms.

## See Also

- [share](share)

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

# signal

*Sends a signal to a state machine*

Sends a named signal to a specific state machine, potentially triggering state transitions based on the machine's configuration. Signals are the primary way to interact with state machines in the game, driving their behavior and state changes.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `id` | string  | Identifier of the state machine  |
| `signal` | string  | Signal to send  |

## Returns

**Type:** variant<int, string>

1 if successful, or error message if machine not found

## Examples

```
signal("door_fsm", "unlock");
```

## Performance

**Complexity:** O(1) for sending the signal, but state machine processing may vary

Signal processing is typically fast, but complex state machines may perform time-consuming operations in response to signals. Be aware of potential performance implications.

## See Also

- [finger](finger)
- [settrace](settrace)

---

# sleep

*Pauses script execution for a specified number of seconds*

Pauses the execution of the current script for the specified number of seconds. This function is thread-safe and can be used in both the main thread and background threads.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `seconds` | integer  | Number of seconds to sleep  |

## Returns

**Type:** void

No return value

## Examples

```
sleep(2);  // Pause for 2 seconds
```

## Performance

**Complexity:** O(1)

## See Also

- [usleep](usleep)

---

# slew

*Moves the player to a specific location*

Immediately moves the player to a specific location in the game world. This function is useful for teleportation, respawning, or quickly navigating between areas during development or testing.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `destination` | string  | Name of the destination  |

## Returns

**Type:** void

No return value

## Examples

```
slew("town_square");
```

## Performance

**Complexity:** O(1)

## See Also

- [warp](warp)
- [load_view](load_view)

---

# stopmusic

*Stops background music*

Stops playback on the "music" audio channel. This is a convenience function that is equivalent to calling audio_stop("music", fadetime).

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `fadetime` | integer *[optional]* = 0 | Time in milliseconds to fade out  |

## Returns

**Type:** void

No return value

## Examples

```
stopmusic(2000);  // Stop music with 2-second fade-out
```

## Performance

**Complexity:** O(1)

## See Also

- [playmusic](playmusic)
- [audio_stop](audio_stop)

---

# unloadview

*Unloads a view from the game world*

Marks a view for unloading, which removes it from the game world and frees associated resources. The view is not immediately unloaded but is queued for removal, allowing for smooth transitions.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `dest` | string  | Name of the view to unload  |

## Returns

**Type:** void

No return value

## Examples

```
unloadview("dungeon_level1");
```

## Performance

**Complexity:** O(1)

Unloading views frees memory and resources, which can improve performance. Consider unloading unused views to optimize memory usage, especially on resource-constrained platforms.

## See Also

- [loadview](loadview)
- [rally](rally)

---

# usleep

*Pauses script execution for a specified number of microseconds*

Pauses the execution of the current script for the specified number of microseconds. This provides finer-grained control over timing than the sleep function. This function is thread-safe and can be used in both the main thread and background threads.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `microseconds` | integer  | Number of microseconds to sleep  |

## Returns

**Type:** void

No return value

## Examples

```
usleep(500000);  // Pause for 0.5 seconds (500,000 microseconds)
```

## Performance

**Complexity:** O(1)

## See Also

- [sleep](sleep)

---

# warp

*Warps the player to a specific location with a delay*

Loads a view and moves the player to a specific location in the game world, similar to loadview, but includes a brief delay to allow for transition effects. If the view cannot be loaded, the player is moved to the specified location using the slew function as a fallback.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `dest` | string  | Name of the destination  |

## Returns

**Type:** void

No return value

## Examples

```
warp("mountain_peak");
```

## Performance

**Complexity:** O(n) where n is the complexity of the view

## See Also

- [slew](slew)
- [loadview](loadview)

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

# write

*Alias for log() - writes a message to the in8 log file*

This is an alias for the log() function, which writes a message to the in8 log file. Multiple parameters can be passed and will be concatenated into a single log message.

**Since:** v1.0.0

## Parameters

| Name | Type | Description |
|------|------|-------------|
| `message` | string  | Message to write (can include multiple parameters)  |

## Returns

**Type:** void

No return value

## Examples

```
write("Checkpoint reached: ", checkpointId);
```

## Performance

**Complexity:** O(1)

## See Also

- [log](log)

---


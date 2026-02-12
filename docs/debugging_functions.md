# Function Reference - Category: debugging

## Table of Contents

- [assert](#assert)
- [finger](#finger)
- [genesis](#genesis)
- [log](#log)
- [reload](#reload)
- [settrace](#settrace)
- [share_bug_report](#share_bug_report)
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


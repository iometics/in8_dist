# String Literal Support in the In8 Language

## BNF Definition

The In8 language supports rich string literals with various escape sequences and full Unicode support. Here is the formal BNF definition:

```bnf
stringcon      ::= '"' { string_char } '"' | "'" { string_char } "'"

string_char    ::= regular_char | escape_sequence | unicode_char

regular_char   ::= /* any printable ASCII character except backslash (\), double quote ("), single quote (') and newline */

escape_sequence ::= "\" ( "n" | "t" | "r" | "0" | "\" | "'" | '"' | hex_escape | unicode_escape )

hex_escape     ::= "x" hex_digit hex_digit

unicode_escape ::= "u" hex_digit hex_digit hex_digit hex_digit

unicode_char   ::= /* any valid UTF-8 encoded character */

hex_digit      ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" 
                 | "a" | "b" | "c" | "d" | "e" | "f"
                 | "A" | "B" | "C" | "D" | "E" | "F"
```

## String Literals in Detail

### Delimiters

String literals in In8 can be enclosed in either double quotes or single quotes:

```
"This is a double-quoted string"
'This is a single-quoted string'
```

### Basic Escape Sequences

In8 supports the following escape sequences for special characters:

| Escape Sequence | Description |
|-----------------|-------------|
| `\n` | Newline |
| `\t` | Tab |
| `\r` | Carriage return |
| `\0` | Null character |
| `\\` | Backslash |
| `\'` | Single quote |
| `\"` | Double quote |

Example:
```
"Line one\nLine two\tTabbed text"
```

### Hexadecimal Escape Sequences

Characters can be specified using their hexadecimal ASCII or extended ASCII values:

```
"\x41"  // 'A'
"\x61"  // 'a'
"\xA9"  // '©' (copyright symbol)
```

### Unicode Escape Sequences

Unicode characters can be included using their 4-digit hexadecimal codes:

```
"\u00A9"  // '©' (copyright symbol)
"\u20AC"  // '€' (euro symbol)
"\u03B1"  // 'α' (Greek alpha)
"\u2764"  // '❤' (heart symbol)
```

### Direct Unicode Characters

In8 strings directly support UTF-8 encoded characters, including multi-byte sequences:

```
"© € α ❤ 😀 🚀"  // Symbols and emoji as direct Unicode
```

## Examples

Here are some comprehensive examples of string literals in In8:

```
// Basic string with escaped characters
message = "Hello, world!\nThis is a new line with a tab\tcharacter.";

// Mixed escape sequences
mixed = "ASCII: A, Hex: \x42, Unicode escape: \u0043";

// International text with direct Unicode
greeting = "Hello in different languages: Bonjour, 你好, Здравствуйте";

// Emoji and symbols
emojis = "I ❤ programming with 🚀 technology!";

// String with quotes
quotes = "She said, \"Hello!\" to everyone";
single_quotes = 'The programmer\'s guide to In8';
```

## Implementation Notes

- The In8 lexer properly validates all UTF-8 sequences to ensure they're well-formed.
- For Unicode escape sequences (`\uHHHH`), the codepoint is converted to UTF-8 for internal representation.
- The language ensures proper handling of all Unicode characters in strings, including surrogate pairs for characters outside the BMP (Basic Multilingual Plane).
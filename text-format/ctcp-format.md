# 📦 CTCP "S" Format Overview

Styled text in MSN Chat is transmitted using a CTCP message with the name `"S"`. The format is:

```
\x01S <escaped color><escaped style><escaped font>;<escaped charset> <plain text>\x01
```

### 🧩 Field Breakdown

- `\x01`: CTCP start marker (ASCII 0x01)
- `S`: CTCP command name for styled text
- `<escaped color>`: A single byte (1–16), escaped to avoid control characters
- `<escaped style>`: A single byte representing a bitmask + 1, escaped
- `<escaped font>`: Font name, escaped (e.g. `Segoe\bUI`)
- `;`: Literal semicolon separating font and charset
- `<escaped charset>`: Numeric string (e.g. `0`, `128`), escaped
- `<plain text>`: Message content, unescaped
- `\x01`: CTCP end marker

> 🧠 All formatting fields—color, style, font, and charset—are escaped to prevent control character conflicts. The semicolon (`;`) is transmitted as a literal character. Only the message text is unescaped.

---

### 💬 Example

#### Raw Message (as transmitted)

```
\x01S \x03\x04Segoe\\bUI;0 Hello world!\x01
```

#### Breakdown

| Segment        | Meaning                                  |
|----------------|------------------------------------------|
| `\x01`         | CTCP start marker                                               |
| `S`            | CTCP command for styled text                                    |
| `\x03`         | Color index 3 (Maroon)                                          |
| `\x04`         | Style value 4 → 3 after subtracting 1 → `CFE_BOLD | CFE_ITALIC` |
| `Segoe\\bUI`   | Escaped font name: `Segoe UI`                                   |
| `;`            | Literal semicolon                                               |
| `0`            | Charset ID: `0` (ANSI)                                          |
| `Hello world!` | Message text (unescaped)                                        |
| `\x01`         | CTCP end marker                                                 |

---

### 🛠️ Implementation Notes

- The style byte is calculated using a bitmask and then offset by +1 to avoid null bytes.
- All formatting fields are escaped using MSN Chat’s custom escape mechanism.
- The semicolon is not escaped and is used to delimit the font and charset.
- The message text is transmitted as-is and may contain any printable characters.

To decode:
1. Unescape the formatting section.
2. Split the font and charset using the semicolon.
3. Subtract 1 from the style byte before applying bitmask logic.

---

## 📚 References

- Mikulėnas, M. & Oakley, D. (2018, January 9). "Common Text Command Protocol (CTCP)". *IETF Datatracker*. Retrieved from [https://datatracker.ietf.org/doc/html/draft-oakley-irc-ctcp-02](https://datatracker.ietf.org/doc/html/draft-oakley-irc-ctcp-02)
- [MSN Chat Internals GitHub](https://github.com/MSNChatInternals)
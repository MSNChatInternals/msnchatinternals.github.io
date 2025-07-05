# ✍️ Text Styling Flags

MSN Chat uses a bitmask to represent text styles such as bold, italic, and underline. These styles are encoded as a
single byte in the CTCP "S" message format.

## 🧠 Encoding Rule

The style byte is calculated using a bitwise OR of the desired flags, then **offset by +1** before transmission. This
avoids sending a null byte (`0x00`), which would require escaping.

For example:

```
style = (CFE_BOLD | CFE_ITALIC) + 1; // Encoded as 0x04
```

To decode, subtract 1 and apply bitmask logic.

---

## 🎛️ Style Constants

| Constant        | Value  | Hex Value | Description               |
|-----------------|--------|-----------|---------------------------|
| `CFE_NONE`      | 0      | `0x00`    | No style applied          |
| `CFE_BOLD`      | 1      | `0x01`    | Characters are bold       |
| `CFE_ITALIC`    | 2      | `0x02`    | Characters are italic     |
| `CFE_UNDERLINE` | 4      | `0x04`    | Characters are underlined |

These values can be combined using bitwise OR.

---

## 🧪 Example Combinations

| Style Combination           | Bitmask Expression                        | Raw Value | Encoded Byte |
|-----------------------------|-------------------------------------------|-----------|----------------|
| No Style                    | `CFE_NONE`                                | 0         | 1 (`0x01`)     |
| Bold                        | `CFE_BOLD`                                | 1         | 2 (`0x02`)     |
| Italic                      | `CFE_ITALIC`                              | 2         | 3 (`0x03`)     |
| Bold + Italic               | `CFE_BOLD \| CFE_ITALIC`                  | 3         | 4 (`0x04`)     |
| Bold + Underline            | `CFE_BOLD \| CFE_UNDERLINE`               | 5         | 6 (`0x06`)     |
| Italic + Underline          | `CFE_ITALIC \| CFE_UNDERLINE`             | 6         | 7 (`0x07`)     |
| Bold + Italic + Underline   | `CFE_BOLD \| CFE_ITALIC \| CFE_UNDERLINE` | 7         | 8 (`0x08`)     |

---

## 🛠️ Implementation Notes

- The style byte is always offset by +1 before being transmitted.
- A style byte of `\x01` means no style (`CFE_NONE`).
- Bitmask logic allows combining multiple styles in a single byte.

---

## 📚 References

- "CHARFORMATW structure (richedit.h) - Win32 apps." (2024, November 20). *Microsoft Learn*. Retrieved from [https://learn.microsoft.com/en-us/windows/win32/api/richedit/ns-richedit-charformatw](https://learn.microsoft.com/en-us/windows/win32/api/richedit/ns-richedit-charformatw)
- [MSN Chat Internals GitHub](https://github.com/MSNChatInternals)
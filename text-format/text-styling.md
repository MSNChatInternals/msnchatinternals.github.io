# ✍️ Text Styling Flags

MSN Chat uses a bitmask to represent text styles such as bold, italic, and underline. These styles are encoded as a  
single byte in the CTCP `"S"` message format.

## 🧠 Encoding Rule

The style byte is calculated using a bitwise OR of the desired flags, then **offset by +1** before transmission. This  
avoids sending a null byte (`0x00`), which would require an extra escape character.

For example:

```rust
let style = (ChatFormat::chfBold as u8 | ChatFormat::chfItalic as u8) + 1; // Encoded as 0x04
```

To decode, subtract 1 and apply bitmask logic.

---

## 🎛️ Style Constants

| Constant        | Value | Hex Value | Description               |
|-----------------|-------|-----------|---------------------------|
| `chfNone`       | 0     | `0x00`    | No style applied          |
| `chfBold`       | 1     | `0x01`    | Characters are bold       |
| `chfItalic`     | 2     | `0x02`    | Characters are italic     |
| `chfUnderlined` | 4     | `0x04`    | Characters are underlined |

These values can be combined using bitwise OR.

---

## 🧪 Example Combinations

| Style Combination         | Bitmask Expression                 | Raw Value | Style Byte |
|---------------------------|---------------------------------------|-----------|------------|
| No Style                  | `chfNone`                             | 0         | `\x01`     |
| Bold                      | `chfBold`                             | 1         | `\x02`     |
| Italic                    | `chfItalic`                           | 2         | `\x03`     |
| Bold + Italic             | `chfBold | chfItalic`                 | 3         | `\x04`     |
| Underline                 | `chfUnderline`                        | 4         | `\x05`     |
| Bold + Underline          | `chfBold | chfUnderlined`             | 5         | `\x06`     |
| Italic + Underline        | `chfItalic | chfUnderlined`           | 6         | `\x07`     |
| Bold + Italic + Underline | `chfBold | chfItalic | chfUnderlined` | 7         | `\x08`     |

---

## 🛠️ Implementation Notes

- The style byte is always offset by +1 before being transmitted.
- A style byte of `\x01` means no style (`chfNone`).
- Bitmask logic allows combining multiple styles in a single byte.

---

## 🧾 Rust Code Sample

```rust
/// Text styling flags used in MSN Chat.
/// These match the values used in the CTCP "S" message format,
/// and are offset by +1 during transmission.
#[repr(i32)]
#[derive(Debug, Clone, Copy)]
pub enum ChatFormat {
    chfNone = 0,
    chfBold = 1,
    chfItalic = 2,
    chfUnderlined = 4,
}

/// Encodes a combination of ChatFormat flags into a style byte.
fn encode_style(flags: u8) -> u8 {
    flags + 1
}

/// Decodes a style byte back into raw flags.
fn decode_style(style_byte: u8) -> u8 {
    style_byte.saturating_sub(1)
}

fn main() {
    // Example: Bold + Italic
    let flags = ChatFormat::chfBold as u8 | ChatFormat::chfItalic as u8;
    let encoded = encode_style(flags);
    println!("Encoded style byte: 0x{:02X}", encoded); // Should print 0x04

    let decoded = decode_style(encoded);
    println!("Decoded flags: 0x{:02X}", decoded); // Should print 0x03
}
```

---

## 📚 References

- [MSN Chat Internals GitHub](https://github.com/MSNChatInternals)

# 🌐 Windows Charset Reference

MSN Chat specifies a character set ID in the font metadata portion of the CTCP "S" message. These IDs correspond to
Windows GDI `CHARSET` constants and determine how text is rendered for different languages and regions.

## 🗂️ Charset Table

| Constant Name          | Value | Description                                                          |
|------------------------|-------|-----------------------------------|
| `ANSI_CHARSET`         | 0     | Latin-based (Windows-1252)        |
| `DEFAULT_CHARSET`      | 1     | System default                    |
| `SYMBOL_CHARSET`       | 2     | Symbol fonts (e.g. Wingdings)     |
| `MAC_CHARSET`          | 77    | Macintosh (legacy)                |
| `SHIFTJIS_CHARSET`     | 128   | Japanese (Shift-JIS)              |
| `HANGEUL_CHARSET`      | 129   | Korean (Hangul)                   |
| `JOHAB_CHARSET`        | 130   | Korean (Johab)                    |
| `GB2312_CHARSET`       | 134   | Simplified Chinese                |
| `CHINESEBIG5_CHARSET`  | 136   | Traditional Chinese               |
| `GREEK_CHARSET`        | 161   | Greek                             |
| `TURKISH_CHARSET`      | 162   | Turkish                           |
| `VIETNAMESE_CHARSET`   | 163   | Vietnamese                        |
| `HEBREW_CHARSET`       | 177   | Hebrew                            |
| `ARABIC_CHARSET`       | 178   | Arabic                            |
| `BALTIC_CHARSET`       | 186   | Baltic languages                  |
| `RUSSIAN_CHARSET`      | 204   | Cyrillic                          |
| `THAI_CHARSET`         | 222   | Thai                              |
| `EASTEUROPE_CHARSET`   | 238   | Central/Eastern European          |
| `OEM_CHARSET`          | 255   | OEM code page (e.g. CP437, CP850) |

> 🧠 These values are used in `LOGFONT.lfCharSet` and affect font rendering and glyph selection.

---

## 📚 References

- "LOGFONTW structure (wingdi.h) - Win32 apps." (2023, March 11). *Microsoft Learn*. Retrieved from
[https://learn.microsoft.com/en-us/windows/win32/api/wingdi/ns-wingdi-logfontw](https://learn.microsoft.com/en-us/windows/win32/api/wingdi/ns-wingdi-logfontw)
- [MSN Chat Internals GitHub](https://github.com/MSNChatInternals)
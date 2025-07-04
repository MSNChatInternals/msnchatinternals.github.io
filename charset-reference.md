# 🗂️ Windows Charset Constants

These `CHARSET` constants are used in the Windows GDI (Graphics Device Interface) to specify the character set of a
font. They're typically used in structures like `LOGFONT` to control how text is rendered.

## Charset Table

| Constant Name          | Value | Description                                                          |
|------------------------|-------|----------------------------------------------------------------------|
| `ANSI_CHARSET`         | 0     | Default for Latin-based languages (Windows-1252)                     |
| `DEFAULT_CHARSET`      | 1     | Font mapper chooses based on system locale                           |
| `SYMBOL_CHARSET`       | 2     | Used for fonts that contain symbols (e.g., Wingdings)                |
| `MAC_CHARSET`          | 77    | Macintosh character set (mostly obsolete)                            |
| `SHIFTJIS_CHARSET`     | 128   | Japanese (Shift-JIS encoding)                                        |
| `HANGEUL_CHARSET`      | 129   | Korean (Hangul, legacy name)                                         |
| `HANGUL_CHARSET`       | 129   | Korean (Hangul, modern name — same value as above)                   |
| `JOHAB_CHARSET`        | 130   | Korean (Johab encoding, used in older systems)                       |
| `GB2312_CHARSET`       | 134   | Simplified Chinese (GB2312 encoding)                                 |
| `CHINESEBIG5_CHARSET`  | 136   | Traditional Chinese (Big5 encoding)                                  |
| `GREEK_CHARSET`        | 161   | Greek character set                                                  |
| `TURKISH_CHARSET`      | 162   | Turkish character set                                                |
| `VIETNAMESE_CHARSET`   | 163   | Vietnamese character set                                             |
| `HEBREW_CHARSET`       | 177   | Hebrew character set                                                 |
| `ARABIC_CHARSET`       | 178   | Arabic character set                                                 |
| `BALTIC_CHARSET`       | 186   | Baltic languages (e.g., Latvian, Lithuanian)                         |
| `RUSSIAN_CHARSET`      | 204   | Cyrillic character set (used for Russian, Ukrainian, etc.)           |
| `THAI_CHARSET`         | 222   | Thai character set                                                   |
| `EASTEUROPE_CHARSET`   | 238   | Central and Eastern European languages (e.g., Polish, Czech)         |
| `OEM_CHARSET`          | 255   | OEM charset (typically code page 437 or 850, used in legacy systems) |

## 🧠 Notes

- These values are used in `LOGFONT.lfCharSet` and influence font selection and glyph rendering.
- `DEFAULT_CHARSET` lets the system choose based on locale and font availability.
- `OEM_CHARSET` is often used in console applications or legacy DOS-based environments.

---

## 📚 Reference

Microsoft. (n.d.). *LOGFONTA structure (wingdi.h)*. Retrieved July 4, 2025, from [https://learn.microsoft.com/en-us/windows/win32/api/wingdi/ns-wingdi-logfontw](https://learn.microsoft.com/en-us/windows/win32/api/wingdi/ns-wingdi-logfontw)
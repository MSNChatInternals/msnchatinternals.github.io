---
title: MSN Chat Internals
layout: default
---

# MSN Chat Internals

Welcome to the MSN Chat Internals project — a technical and historical archive of the MSN Chat platform. This site documents protocols, character encoding, message formats, and the broader ecosystem that powered one of the early internet’s most iconic chat services.

## 📄 Documentation

- [Text Formatting Overview](text-format/)  
  Entry point for MSN Chat's styled message format, including CTCP structure, color, style, and charset encoding.
  - [CTCP "S" Format](text-format/ctcp-format.md)  
    Explains the structure of the CTCP "S" message used to encode styled text, including escaping rules and byte layout.
  - [Color Palette](text-format/color-palette.md)  
    The 16-color VGA-style palette used in MSN Chat, with hex codes and visual samples.
  - [Text Styling Flags](text-format/text-styling.md)  
    Bitmask-based style flags for bold, italic, and underline, including encoding logic and examples.
  - [Windows Charset Reference](text-format/charset-reference.md)  
    Charset IDs used in font metadata, mapped to Windows GDI constants for multilingual support.

- [Redistributing MSN Chat](redistributing-msnchat.md)  
  A discussion on the legal, ethical, and technical considerations around redistributing MSN Chat binaries and assets.

---

More documents and technical deep-dives coming soon. Stay tuned!
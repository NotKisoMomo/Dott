<div align="center">

```
██████╗  ██████╗ ████████╗████████╗
██╔══██╗██╔═══██╗╚══██╔══╝╚══██╔══╝
██║  ██║██║   ██║   ██║      ██║   
██║  ██║██║   ██║   ██║      ██║   
██████╔╝╚██████╔╝   ██║      ██║   
╚═════╝  ╚═════╝    ╚═╝      ╚═╝   
```

**Stack-based dot-navigated human-readable serialization**

[![Version](https://img.shields.io/badge/version-0.1.0-6C3EF4?style=for-the-badge&labelColor=0a0a0f)](https://github.com/NotKisoMomo/Dott/releases)
[![Luau](https://img.shields.io/badge/luau-typed-6C3EF4?style=for-the-badge&labelColor=0a0a0f)](https://luau-lang.org)
[![Python](https://img.shields.io/badge/python-3.10+-6C3EF4?style=for-the-badge&labelColor=0a0a0f)](https://python.org)
[![License](https://img.shields.io/badge/license-MIT-6C3EF4?style=for-the-badge&labelColor=0a0a0f)](LICENSE)
[![Built by Plinko Labs](https://img.shields.io/badge/built_by-Plinko_Labs-6C3EF4?style=for-the-badge&labelColor=0a0a0f)](https://github.com/NotKisoMomo)

</div>

---

Dott is a stack-based human-readable serialization format. Tokens are pushed onto a persistent stack using `<>` and retrieved using dot-depth navigation with `>`. Every character is encoded as a fixed two-digit code -- no delimiters needed inside token bodies, no ambiguity in the parser.

---

## Highlights

- Stack-based token registry -- push with `<>`, navigate with `>.`
- Fixed two-digit encoding -- no delimiters, unambiguous parsing
- Dot-depth navigation -- `>.` is top, `>..` is one back, depth is just dot count
- Rich slicing -- subtract from end/start, inequality range indexing
- Uppercase modifier -- `^` prefix for single char, `^...^` for blocks
- Unified character table -- letters, digits, and special chars in one numeric space
- Global char index -- `!<n>` references first-encounter char table
- Human readable and wire-efficient -- same format for debugging and transport
- Luau (Roblox) and Python implementations

---

## Files

**Luau**
| File | Role |
|---|---|
| `Dott.lua` | Public API |
| `Encoder.lua` | String to Dott notation |
| `Decoder.lua` | Dott notation to string |
| `Lexer.lua` | Tokenizes Dott notation into a typed stream |
| `Util.lua` | Shared helpers |
| `Types.lua` | Exported type definitions |

**Python**
| File | Role |
|---|---|
| `dott.py` | Full implementation -- encoder, decoder, lexer |

---

## Quick Start

**Luau**
```lua
local Dott = require(path.to.Dott)

local encoded = Dott.encode("Hello Hello World")
local decoded = Dott.decode(encoded)
local ok      = Dott.roundtrip("Hello Hello World")
```

**Python**
```python
import dott

encoded = dott.encode("Hello Hello World")
decoded = dott.decode(encoded)
ok      = dott.roundtrip("Hello Hello World")
```

---

## Notation At a Glance

| Notation | Meaning |
|---|---|
| `<0805121215>` | Push token "hello" onto stack |
| `>.` | Emit top of stack |
| `>..` | Emit 1 back |
| `>...` | Emit 2 back |
| `>.2` | Emit char at index 2 from top |
| `>.-1` | Emit top minus last 1 char |
| `.--1` | Emit top minus first 1 char |
| `>.i2ex4e` | Emit chars at index >= 2 and <= 4 |
| `^08` | Uppercase single char (H) |
| `^080512^` | Uppercase block (HEL) |
| `&` | Space |
| `&t` `&n` | Tab, newline |
| `!14` | Global char index 14 |

---

## Wiki

| Page | Contents |
|---|---|
| [Home](https://github.com/NotKisoMomo/Dott/wiki) | Overview |
| [Getting Started](https://github.com/NotKisoMomo/Dott/wiki/Getting-Started) | Installation and first use |
| [Notation Guide](https://github.com/NotKisoMomo/Dott/wiki/Notation-Guide) | Full syntax reference |
| [Stack Navigation](https://github.com/NotKisoMomo/Dott/wiki/Stack-Navigation) | How the stack and dot system works |
| [Encoding Table](https://github.com/NotKisoMomo/Dott/wiki/Encoding-Table) | Full two-digit code table |
| [Slicing](https://github.com/NotKisoMomo/Dott/wiki/Slicing) | Subtract, range, inequality indexing |
| [Internals](https://github.com/NotKisoMomo/Dott/wiki/Internals) | Encoder and decoder architecture |
| [Performance Guide](https://github.com/NotKisoMomo/Dott/wiki/Performance-Guide) | When Dott wins, tradeoffs |
| [API Reference](https://github.com/NotKisoMomo/Dott/wiki/API-Reference) | Full typed API |

---

<div align="center">

Built by [Plinko Labs](https://github.com/NotKisoMomo)
**Thanks to Claude for helping me conceptualize this project**

</div>

# 7S-02: Landscape - simple_base64


**Date**: 2026-01-23

## Existing Solutions

### Gobo Library (GOBO_BASE64)
- Part of Gobo suite
- Heavy dependency chain
- Not simple_* ecosystem integrated

### EiffelBase Encoding
- Basic encoding in ISE libraries
- Limited features
- No URL-safe variant

### Manual Implementation
- Error-prone
- No contracts
- Reinvented per project

## Standards

| Standard | Description | Implemented |
|----------|-------------|-------------|
| RFC 4648 | Base16/32/64 Encodings | ✓ |
| RFC 2045 | MIME line wrapping (76 chars) | ✓ |
| RFC 2397 | Data URI scheme | ✓ |

## Differentiation

simple_base64 provides:
1. **Simple API** - Single class, intuitive names
2. **Full contracts** - Pre/post conditions, invariants
3. **URL-safe variant** - Essential for JWT/web
4. **Data URI support** - Unique in Eiffel ecosystem
5. **No dependencies** - Only EiffelBase

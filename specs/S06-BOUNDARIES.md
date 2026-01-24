# S06: Boundaries - simple_base64

## Date: 2026-01-23 (Backwash)

## System Boundaries

### Input Boundary
| Input | Type | Validation |
|-------|------|------------|
| String to encode | STRING | Not void |
| Bytes to encode | ARRAY[NATURAL_8] | Not void |
| Base64 to decode | STRING | Valid Base64 or Base64URL |
| Data URI | STRING | Starts with "data:" |
| Media type | STRING | Not void, not empty |

### Output Boundary
| Output | Type | Guarantee |
|--------|------|-----------|
| Encoded string | STRING | Valid Base64 |
| Decoded string | STRING | Original content |
| Decoded bytes | ARRAY[NATURAL_8] | Original bytes |
| Data URI | STRING | RFC 2397 compliant |
| Validation result | BOOLEAN | Accurate |

## Integration Boundaries

### Upstream (Consumers)
| Library | Usage |
|---------|-------|
| simple_jwt | Token encoding/decoding |
| simple_http | Basic auth headers |
| simple_email | MIME attachments |
| simple_web | Data URI generation |

### Downstream (Dependencies)
| Library | Usage |
|---------|-------|
| base | STRING, ARRAY, basic types |

## Error Handling Boundary

| Condition | Handling |
|-----------|----------|
| Void input | Precondition violation |
| Invalid Base64 | Precondition violation |
| Empty input | Returns empty output |
| Invalid data URI | Returns empty string |

## Feature Boundary

### Included
- Standard Base64
- URL-safe Base64URL
- Data URI (RFC 2397)
- MIME line wrapping
- Validation
- Format conversion

### Excluded
- Streaming
- Base32/Base16
- Compression
- Encryption
- File I/O

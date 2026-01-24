# S03: Class Specifications - simple_base64

## Date: 2026-01-23 (Backwash)

## SIMPLE_BASE64

### Identity
- **Role**: FACADE (single-class library)
- **Domain Concept**: Base64 Encoder/Decoder
- **Lines**: ~670

### Purpose
RFC 4648 compliant Base64 encoding and decoding with URL-safe variant and data URI support.

### Creation
| Procedure | Preconditions | Postconditions |
|-----------|---------------|----------------|
| `make` | None | Encoder ready |

### Encoding Features
| Feature | Aliases | Signature | Contracts |
|---------|---------|-----------|-----------|
| `encode` | to_base64, encode_string, base64_encode | (STRING): STRING | require: input_not_void; ensure: valid_base64 |
| `encode_bytes` | - | (ARRAY[NATURAL_8]): STRING | require: bytes_not_void; ensure: correct_length |
| `encode_url` | to_base64url, encode_jwt, encode_token | (STRING): STRING | require: input_not_void; ensure: no_padding, url_safe |
| `encode_url_with_padding` | - | (STRING): STRING | require: input_not_void; ensure: url_safe |
| `encode_mime` | - | (STRING): STRING | require: input_not_void |
| `encode_bytes_mime` | - | (ARRAY[NATURAL_8]): STRING | require: bytes_not_void |

### Decoding Features
| Feature | Aliases | Signature | Contracts |
|---------|---------|-----------|-----------|
| `decode` | from_base64, decode_string, base64_decode | (STRING): STRING | require: input_not_void, valid_input |
| `decode_bytes` | - | (STRING): ARRAY[NATURAL_8] | require: input_not_void, valid_or_normalizable |
| `decode_url` | from_base64url, decode_jwt, decode_token | (STRING): STRING | require: input_not_void |
| `decode_lenient` | - | (STRING): STRING | require: input_not_void |
| `decode_bytes_lenient` | - | (STRING): ARRAY[NATURAL_8] | require: input_not_void |

### Validation Features
| Feature | Aliases | Signature |
|---------|---------|-----------|
| `is_valid_base64` | is_base64, valid_base64 | (STRING): BOOLEAN |
| `is_valid_base64_url` | is_base64url, valid_base64url | (STRING): BOOLEAN |

### Conversion Features
| Feature | Signature | Contracts |
|---------|-----------|-----------|
| `to_url_safe` | (STRING): STRING | ensure: no_plus, no_slash |
| `to_standard` | (STRING): STRING | ensure: no_dash, no_underscore |

### Data URI Features
| Feature | Aliases | Signature |
|---------|---------|-----------|
| `to_data_uri` | embed, embed_data, as_data_uri | (STRING, STRING): STRING |
| `to_data_uri_bytes` | - | (ARRAY[NATURAL_8], STRING): STRING |
| `from_data_uri` | extract, extract_data, data_uri_content | (STRING): STRING |
| `from_data_uri_bytes` | - | (STRING): ARRAY[NATURAL_8] |
| `data_uri_mediatype` | - | (STRING): STRING |
| `is_data_uri` | - | (STRING): BOOLEAN |
| `is_base64_data_uri` | - | (STRING): BOOLEAN |

### Constants
| Constant | Value | Purpose |
|----------|-------|---------|
| Standard_alphabet | 64 chars | A-Z, a-z, 0-9, +, / |
| Url_safe_alphabet | 64 chars | A-Z, a-z, 0-9, -, _ |
| Padding_char | '=' | Padding character |
| Mime_line_length | 76 | RFC 2045 line length |
| Data_uri_prefix | "data:" | URI scheme prefix |

### Invariants
```eiffel
standard_alphabet_64: Standard_alphabet.count = 64
url_safe_alphabet_64: Url_safe_alphabet.count = 64
```

### Contract Coverage: STRONG (100%)

# S02: Domain Model - simple_base64

## Date: 2026-01-23 (Backwash)

## Domain Concepts

### Base64 Encoding
Binary-to-text encoding using 64-character alphabet. Converts 3 bytes to 4 characters.

### Standard Base64 (RFC 4648)
- Alphabet: A-Z, a-z, 0-9, +, /
- Padding: = (to make length multiple of 4)
- Use: General purpose

### URL-Safe Base64URL (RFC 4648)
- Alphabet: A-Z, a-z, 0-9, -, _
- Padding: Optional (often omitted)
- Use: URLs, JWT, filenames

### Data URI (RFC 2397)
- Format: `data:<mediatype>;base64,<data>`
- Embeds data directly in URIs
- Use: Inline images, CSS

### MIME Encoding (RFC 2045)
- Line wrapping at 76 characters
- Use: Email attachments

## Class Model

```
SIMPLE_BASE64
    |
    +-- Encoding
    |   +-- encode (STRING): STRING
    |   +-- encode_bytes (ARRAY[NATURAL_8]): STRING
    |   +-- encode_url (STRING): STRING
    |   +-- encode_mime (STRING): STRING
    |
    +-- Decoding
    |   +-- decode (STRING): STRING
    |   +-- decode_bytes (STRING): ARRAY[NATURAL_8]
    |   +-- decode_url (STRING): STRING
    |   +-- decode_lenient (STRING): STRING
    |
    +-- Validation
    |   +-- is_valid_base64 (STRING): BOOLEAN
    |   +-- is_valid_base64_url (STRING): BOOLEAN
    |
    +-- Conversion
    |   +-- to_url_safe (STRING): STRING
    |   +-- to_standard (STRING): STRING
    |
    +-- Data URI
        +-- to_data_uri (STRING, STRING): STRING
        +-- from_data_uri (STRING): STRING
        +-- is_data_uri (STRING): BOOLEAN
```

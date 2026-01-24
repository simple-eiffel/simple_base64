# S04: Feature Specifications - simple_base64

## Date: 2026-01-23 (Backwash)

## Encoding Features

### encode (a_input: STRING): STRING
Encode string to standard Base64.

**Contracts:**
```eiffel
require
    input_not_void: a_input /= Void
ensure
    valid_base64: is_valid_base64 (Result)
```

**Implementation:** Converts string to bytes, encodes via `encode_bytes`.

### encode_bytes (a_bytes: ARRAY[NATURAL_8]): STRING
Encode raw bytes to standard Base64.

**Contracts:**
```eiffel
require
    bytes_not_void: a_bytes /= Void
ensure
    correct_length: Result.count = ((a_bytes.count + 2) // 3 * 4)
```

**Implementation:** Core encoding algorithm. Processes 3 bytes → 4 characters.

### encode_url (a_input: STRING): STRING
Encode to URL-safe Base64URL without padding.

**Contracts:**
```eiffel
require
    input_not_void: a_input /= Void
ensure
    no_padding: not Result.has ('=')
    url_safe: not Result.has ('+') and not Result.has ('/')
```

**Implementation:** Encodes, converts to URL-safe, strips padding.

## Decoding Features

### decode (a_input: STRING): STRING
Decode Base64 to string.

**Contracts:**
```eiffel
require
    input_not_void: a_input /= Void
    valid_input: is_valid_base64 (a_input) or is_valid_base64_url (a_input)
```

**Implementation:** Decodes via `decode_bytes`, converts to string.

### decode_bytes (a_input: STRING): ARRAY[NATURAL_8]
Decode Base64 to raw bytes.

**Contracts:**
```eiffel
require
    input_not_void: a_input /= Void
    valid_or_normalizable: is_valid_base64 (a_input) or is_valid_base64_url (a_input) or a_input.is_empty
```

**Implementation:** Normalizes input (URL-safe → standard, adds padding), decodes 4 chars → 3 bytes.

## Validation Features

### is_valid_base64 (a_input: STRING): BOOLEAN
Check if string is valid standard Base64.

**Validation rules:**
- Length must be multiple of 4
- Only characters from Standard_alphabet
- Padding only at end
- No characters after padding

### is_valid_base64_url (a_input: STRING): BOOLEAN
Check if string is valid URL-safe Base64URL.

**Validation rules:**
- Only characters from Url_safe_alphabet
- Padding is optional

## Conversion Features

### to_url_safe (a_base64: STRING): STRING
Convert standard Base64 to URL-safe.

**Contracts:**
```eiffel
ensure
    no_plus: not Result.has ('+')
    no_slash: not Result.has ('/')
```

**Implementation:** Replace + with -, / with _.

### to_standard (a_base64url: STRING): STRING
Convert URL-safe to standard Base64.

**Contracts:**
```eiffel
ensure
    no_dash: not Result.has ('-')
    no_underscore: not Result.has ('_')
```

**Implementation:** Replace - with +, _ with /.

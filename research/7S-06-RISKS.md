# 7S-06: Risks - simple_base64

## R1: Invalid Input Handling

**Risk:** Decoding invalid Base64 could crash or produce garbage

**Mitigation:**
- Precondition: `valid_input: is_valid_base64 (a_input) or is_valid_base64_url (a_input)`
- Validation features provided for checking before decode
- Lenient decode strips whitespace before validation

**Status:** Mitigated

## R2: Memory for Large Inputs

**Risk:** Encoding very large strings allocates proportional memory

**Mitigation:**
- Documented limitation (no streaming)
- For large files, use streaming alternative
- Typical use cases (JWT, data URIs) are small

**Status:** Accepted (by design)

## R3: Unicode Handling

**Risk:** Non-ASCII characters in input strings

**Mitigation:**
- Works on byte level via `string_to_bytes`
- UTF-8 strings encode correctly
- Documented that input is treated as bytes

**Status:** Mitigated

## R4: Padding Edge Cases

**Risk:** URL-safe variant has optional padding

**Mitigation:**
- `encode_url` removes padding
- `encode_url_with_padding` keeps it
- Decoder handles both via `normalize_input`

**Status:** Mitigated

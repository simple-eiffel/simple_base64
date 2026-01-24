# 7S-04: Design Decisions - simple_base64


**Date**: 2026-01-23

## D1: Single Class Design

**Decision:** All functionality in one class (SIMPLE_BASE64)

**Rationale:**
- Base64 is a single concept
- No inheritance hierarchy needed
- Simple to use: create encoder.make

**Alternative rejected:** Separate encoder/decoder classes
- Adds complexity without benefit
- Same instance can do both

## D2: Feature Aliases

**Decision:** Provide multiple names for common operations

```eiffel
encode, to_base64, encode_string, base64_encode  -- All do the same thing
```

**Rationale:**
- Different mental models (encode vs to_base64)
- Discoverable API
- No runtime cost (compiled to same feature)

## D3: Lenient Decoding

**Decision:** Provide both strict and lenient decoding

- `decode` - requires valid input
- `decode_lenient` - ignores whitespace

**Rationale:**
- MIME content has line breaks
- Copy-paste often introduces spaces
- Strict mode for validation, lenient for tolerance

## D4: Data URI Support

**Decision:** Include RFC 2397 data URI support

**Rationale:**
- Common use case (embedding images)
- Natural extension of Base64
- No other Eiffel library provides this

## D5: No Streaming

**Decision:** Operate on complete strings, not streams

**Rationale:**
- Simplicity over performance
- Most Base64 content is small
- Streaming adds complexity

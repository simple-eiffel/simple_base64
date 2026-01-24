# 7S-05: Innovations - simple_base64


**Date**: 2026-01-23

## I1: Comprehensive Alias Coverage

Most Base64 libraries have one name per operation. SIMPLE_BASE64 provides multiple aliases matching different mental models:

```eiffel
-- Verb-oriented
encode, decode

-- Type-oriented
to_base64, from_base64

-- Domain-oriented
encode_jwt, decode_token

-- Full descriptive
encode_string, base64_encode
```

## I2: Data URI as First-Class Feature

No other Eiffel library provides data URI support:

```eiffel
uri := encoder.to_data_uri (content, "text/plain")
-- "data:text/plain;base64,SGVsbG8h"

content := encoder.from_data_uri (uri)
mediatype := encoder.data_uri_mediatype (uri)
```

## I3: Contract-Verified Encoding

Postconditions verify encoding correctness:

```eiffel
encode (a_input: STRING): STRING
    ensure
        valid_base64: is_valid_base64 (Result)

encode_url (a_input: STRING): STRING
    ensure
        no_padding: not Result.has ('=')
        url_safe: not Result.has ('+') and not Result.has ('/')
```

## I4: Bidirectional Format Conversion

Easy switching between standard and URL-safe:

```eiffel
url_safe := encoder.to_url_safe (standard_base64)
standard := encoder.to_standard (url_safe_base64)
```

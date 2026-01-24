# 7S-01: Scope - simple_base64


**Date**: 2026-01-23

## Problem Statement

Applications need to encode binary data as text for transmission via text-only channels (URLs, JSON, HTTP headers, email). Base64 is the standard solution, but Eiffel lacks a simple, contract-verified implementation.

## Solution

SIMPLE_BASE64 provides RFC 4648 compliant Base64 encoding/decoding with:
- Standard Base64 (with padding)
- URL-safe Base64URL variant (for JWT, URLs)
- Data URI support (RFC 2397)
- MIME encoding with line wrapping (RFC 2045)

## Scope Boundaries

**In Scope:**
- Encode STRING to Base64
- Encode ARRAY[NATURAL_8] to Base64
- Decode Base64 to STRING
- Decode Base64 to ARRAY[NATURAL_8]
- URL-safe Base64URL variant
- Data URI creation and parsing
- MIME-style line wrapping
- Validation of Base64 strings

**Out of Scope:**
- Streaming encoding (large files)
- Compression before encoding
- Encryption integration
- Binary file I/O

## Target Users

- JWT token handling (simple_jwt)
- HTTP Basic authentication
- Data URI embedding in HTML/CSS
- Email attachment encoding
- URL parameter encoding

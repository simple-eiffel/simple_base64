# S05: Constraints - simple_base64

## Date: 2026-01-23 (Backwash)

## Technical Constraints

### C1: RFC 4648 Compliance
All encoding/decoding must comply with RFC 4648.
- Standard alphabet: A-Z, a-z, 0-9, +, /
- URL-safe alphabet: A-Z, a-z, 0-9, -, _
- Padding character: =

### C2: Memory Model
Operates on complete strings in memory.
- No streaming support
- Memory usage proportional to input size
- Suitable for typical use cases (< 10MB)

### C3: Character Encoding
Input strings treated as bytes.
- Each character → one byte
- UTF-8 strings work correctly
- No BOM handling

### C4: SCOOP Compatibility
Class is stateless after creation.
- No mutable state
- Thread-safe by design
- SCOOP support: thread

## Design Constraints

### C5: Single Class
All functionality in SIMPLE_BASE64.
- No inheritance hierarchy
- No helper classes exposed
- Simple usage pattern

### C6: No External Dependencies
Only EiffelBase required.
- Avoids Gobo dependency
- Simpler deployment
- Smaller footprint

## Performance Constraints

### C7: Linear Complexity
- Encoding: O(n) where n = input length
- Decoding: O(n) where n = input length
- Validation: O(n) where n = input length

### C8: Memory Allocation
- Output string pre-allocated to correct size
- Minimal intermediate allocations
- Result size = ((input_size + 2) / 3) * 4

This page contains notes about Pokemon Brilliant Diamond / Shining Pearl.

## Pia Key
The game key for Pia is derived from a constant `cryptoKeyDataSeed` and the local communication version.

```python
def derive_game_key(seed: bytes, version: int) -> bytes:
    data = bytearray(seed)
    data[1] = (version >> 8) & 0xFF
    data[3] = (version >> 4) & 0xFF
    data[7] = (version >> 1) & 0xFF
    data[12] = version & 0xFF
    return bytes(data)
```

The `cryptoKeyDataSeed` is hardcoded to `9918bd0fdcfa65779918bd0fdcfa6577`.

| Game version | Local communication version |
| --- | --- |
| 1.3.0 (v6) | 199 |
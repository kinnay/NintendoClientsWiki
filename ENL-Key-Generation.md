The page describes how [ENL](ENL-Protocol) generates the [game-specific key](Pia-Game-Keys) for [Pia](Pia-Overview) in LDN, LAN and NPLN mode.

### Algorithm

To generate the key, ENL uses the random number generator provided by [SEAD](SEAD-RNG), with a game-specific seed or state. It also uses a table of 32-bit integers provided by the game.

For each byte in the key ENL generates two random numbers: an index into the provided table and a 'byte index' or shift amount. ENL always generates 4 bytes at once and stores them into the key in little endian byte order. In Python, this could look as follows:
```python
# Generates 4 bytes of the key and
# returns them as an integer
def create_key_part(rand, table):
    value = 0
    for i in range(4):
        index = rand.uint(len(table))
        shift = rand.uint(4) * 8
        byte = (table[index] >> shift) & 0xFF
        value = (value << 8) | byte
    return value

# Generates a key with the given random
# number generator and integer table
def create_key(rand, table, size):
    if size % 4:
        raise ValueError("Key size must be multiple of 4")
    
    key = b""
    for i in range(size // 4):
        value = create_key_part(rand, table)
        key += struct.pack("<I", value) #Little endian
    return key
```

### AC:NH Island Transfer Tool
```python
rng = sead.Random([0x58F9A90D, 0xF329D9AD, 0x781BCDC, 0x9DF24013])
table = [rng.u32() for i in range(64)]

rand = sead.Random(31)
print(create_key(rand, table, 16))
```

### Splatoon 2
```python
rand = Random(0xCEB9D8D9)
table = [
    0x56CB956F, 0x7B50EEC6, 0x234D1A63, 0x1C691A6B,
    0xD2D9C482, 0xCFE21965, 0x0B32DF99, 0xB32AFE44,
    0xB15DA3D7, 0x86588505, 0x4FC8CD8B, 0xC30F864B,
    0x08D4D3BE, 0xEFDEC6CA, 0x63A1D53F, 0xC545538D,
    0x715E27A2, 0x4818A005, 0x8C28D9F8, 0xC303EABF,
    0xF1D847ED, 0xE837F303, 0xE68981E8, 0x63E2F9BC,
    0xC320F7E1, 0x5E0B4084, 0x502B2A2D, 0x65D36579,
    0x0D169E46, 0x65AB445D, 0xFDF0678B, 0x26167D3E,
    0xFE5025A0, 0x04EB0EA8, 0xC048B044, 0xF858002E,
    0x6725F7D6, 0xD4086AA8, 0xF216DE10, 0x0F1807E6,
    0xD3614878, 0x34A2FEE6, 0xA69AE3DE, 0xED8518EF,
    0x6FCCB7A5, 0x7F8D0E40, 0x9B72BFA8, 0x87C669D4,
    0x5BF80652, 0x9A71383F, 0xBA3E7A7A, 0x1ABA65A3,
    0xA9A16DFF, 0xD07B9E3C, 0x11C9BD45, 0xF14A6D81,
    0x78516ECD, 0x53445C15, 0xC86E9942, 0x5501D2C9,
    0xD0D4ECB3, 0x38F5C341, 0xC4A16155, 0x42F1F406
]

print(create_key(rand, table, 16))
```

### Super Mario Maker 2
```python
rand = Random(0x123)
table = [
    0xB301CA48, 0x5E758911, 0xC2B349E2, 0xF9942930,
    0x447AEFC0, 0xB6B5DB5F, 0xEE116832, 0xB6940169,
    0x2503FC94, 0x3D74B448, 0x58411B2C, 0x4EC8C604,
    0x74157415, 0xEC5B582B, 0xBC93A6F7, 0xB463AF87,
    0x6B09D0C2, 0x5DA54788, 0x7C20F6D5, 0xD5967141,
    0xF03C24F1, 0x87D2A479, 0xFC3F7C08, 0x9A4506B7,
    0x8B4FA2A2, 0x99AC2EDE, 0x9E74DEDF, 0x2CB60318,
    0xDA1AEE9E, 0x2238F1DD, 0x1A825163, 0x86B03FE8,
    0x8BD35FBE, 0x6E80E100, 0x6681ACFA, 0x61C990BD,
    0x70F61D95, 0x19177A6A, 0x729AE3CE, 0x5FFBD958,
    0x9F217D87, 0x3D478023, 0x986690D6, 0x19D6AB9B,
    0x8D8F2063, 0x8CC8EF69, 0x20843E06, 0x8CA2C3FE,
    0x78DA6631, 0xB3A27DE4, 0xB2D71198, 0x28F0890F,
    0x83B089CE, 0x235D8901, 0x290C0723, 0x85184BFC,
    0x82E15C68, 0x4D3BD8B4, 0x0447FB2F, 0x434717F0,
    0xCBCD01EC, 0x58A09E59, 0x630588E1, 0x1886EBE6
]

print(create_key(rand, table, 16))
```
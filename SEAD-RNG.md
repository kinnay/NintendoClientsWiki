SEAD is Nintendo's private standard library. It is used by various first party games and the [Pia](Pia-Overview) library uses it as well.

Its random number generator works as follows:
```python
class Random:
    def __init__(self, seed: int | list[int]):
        if isinstance(seed, int):
            multiplier = 0x6C078965
        
            temp = seed
            self.state = []
            for i in range(1, 5):
                temp ^= temp >> 30
                temp = (temp * multiplier + i) & 0xFFFFFFFF
                self.state.append(temp)

        else:
            self.state = seed
    
    # Returns a random 32-bit integer
    def u32(self) -> int:
        temp = self.state[0]
        temp = (temp ^ (temp << 11)) & 0xFFFFFFFF
        temp ^= temp >> 8
        temp ^= self.state[3]
        temp ^= self.state[3] >> 19
        self.state[0] = self.state[1]
        self.state[1] = self.state[2]
        self.state[2] = self.state[3]
        self.state[3] = temp
        return temp

    def u64(self) -> int:
        return (self.u32() << 32) | self.u32()
    
    # Returns a random integer smaller than 'max'
    def uint(self, max: int) -> int:
        return (self.u32() * max) >> 32
```

The random number generator is used by [ENL](ENL-Key-Generation) to generate the game-specific key for the LAN protocol and by [Pia](Pia-Protocol#encryption) to generate the session key in LDN mode.
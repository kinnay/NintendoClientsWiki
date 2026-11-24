## [[NEX Protocols]] > [Secure Connection](Secure-Protocol) > Monster Hunter Generation Ultimate/XZX (11)

This page describes the methods that are only seen in Monster Hunter Generations Ultimate/XX.

| Method ID | Method Name|
| --- | --- |
| 9 | [GenerateFirstStepPassword](#9-generatefirststeppassword) |
| 10 | [GeneratePassword](#10-generatepassword) |
| 11 | [ConnectGamePID](#11-connectgamepid) |
| 12 | [DisconnectGamePID](#12-disconnectgamepid) |
| 13 | [GetGamePIDByPlatformPID](#13-getgamepidbyplatformpid) |
| 14 | [GetPlatformPIDByGamePID](#14-getplatformpidbygamepid) |
| 15 | [GetGamePID](#15-getgamepid) |
| 16 | [CreateGamePID](#16-creategamepid) |
| 17 | [GetPlatformType](#17-getplatformtype) |
| 18 | [ResetConnectionCount](#18-resetconnectioncount) |
| 19 | [GetConnectionCount](#19-getconnectioncount) |
| 20 | [ResetPlatformConnectionCount](#20-resetplatformconnectioncount) |
| 21 | [GetPlatformConnectionCount](#21-getplatformconnectioncount) |

# (9) GenerateFirstStepPassword

## Request
| Type | Name |
| --- | --- | 
| Uint8 | platform |

## Response
| Type | Name |
| --- | --- |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | fsPassword |

# (10) GeneratePassword

## Request
| Type | Name |
| --- | --- |
| Uint8 | platform |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | fsPassword |

## Response
| Type | Name | 
| --- | --- | 
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | password |

# (11) ConnectGamePID

## Request
| Type | Name |
| --- | --- | 
| Uint8 | platform |
| [String](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#string) | password |

## Response
| Type | Name |
| --- | --- | 
| Uint64 | gamePID 

# (12) DisconnectGamePID

## Request
| Type | Name | 
| --- | --- |
| Uint8 | platform |
| Uint64 | oldGamePID | 

## Response
This method does not return anything

# (13) GetGamePIDByPlatformPID

## Request
| Type | Name |
| --- | --- |
| Uint8 | platform |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;Uint64&#x3E; | platformPIDs |

## Response
| Type | Name | 
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;Uint64&#x3E; |

# (14) GetPlatformPIDByGamePID

## Request
| Type | Name |
| --- | --- |
| Uint8 | platform |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;Uint64&#x3E; | gamePIDs |

## Response
| Type | Name |
| --- | --- |
| [List](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#list)&#x3C;Uint64&#x3E; | platformPIDs |

# (15) GetGamePID

## Request
| Type | Name |
| --- | --- |
| Uint8 | platformType |
| Uint64 | platformPID |

## Response
| Type | Name |
| --- | --- |
| Uint64 | gamePID |

# (16) CreateGamePID

## Request
| Type | Name |
| --- | --- |
| Uint8 | platformType |
| Uint64 | platformPID |

## Response
| Type | Name |
| --- | --- |
| Uint64 | gamePID |

# (17) GetPlatformType

## Request
| Type | Name | 
| --- | --- |
| [AnyDataHolder](https://github.com/kinnay/NintendoClients/wiki/NEX-Common-Types#anydataholder) | anyData |

## Response
| Type | Name | 
| --- | --- | 
| Uint8 | platformType |

# (18) ResetConnectionCount

## Request
This method does not take any parameters

## Response
This method does not return anything

# (19) GetConnectionCount

## Request
This method does not take any parameters

## Response
| Type | Name | 
| --- | --- |
| Uint32 | connectionCount |

# (20) ResetPlatformConnectionCount

## Request
| Type | Name |
| --- | --- | 
| Uint8 | platformType |

## Response
This method does not return anything

# (21) GetPlatformConnectionCount

## Request
| Type | Name | 
| --- | --- |
| Uint8 | platformType |

## Response
| Type | Name | 
| --- | --- | 
| Uint32 | connectionCount |

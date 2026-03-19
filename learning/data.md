# Qu'est ce que le binaire?
Le Binaire est un ensemble de 1's and 0's. Un digit en binaire est appelé bit.

|0   |1   |2   |3   |
|----|----|----|----|
|00  |01  |10  |11  |

(100)base2 = (4)base10

**Autres bases: Octal(8bits), hexadecimal(16bits).**
# Expression du texte


ASCII -> UTF-8 (ascii evolution)

Voici une ascii table
| Lo\\Hi | 0x | 1x | 2x | 3x | 4x | 5x | 6x | 7x |
|--------|--------|--------|--------|--------|--------|--------|--------|--------|
| x0 | `00` NUL | `10` DLE | `20` SP | `30` 0 | `40` @ | `50` P | `60` ` | `70` p |
| x1 | `01` SOH | `11` DC1 | `21` ! | `31` 1 | `41` A | `51` Q | `61` a | `71` q |
| x2 | `02` STX | `12` DC2 | `22` " | `32` 2 | `42` B | `52` R | `62` b | `72` r |
| x3 | `03` ETX | `13` DC3 | `23` # | `33` 3 | `43` C | `53` S | `63` c | `73` s |
| x4 | `04` EOT | `14` DC4 | `24` $ | `34` 4 | `44` D | `54` T | `64` d | `74` t |
| x5 | `05` ENQ | `15` NAK | `25` % | `35` 5 | `45` E | `55` U | `65` e | `75` u |
| x6 | `06` ACK | `16` SYN | `26` & | `36` 6 | `46` F | `56` V | `66` f | `76` v |
| x7 | `07` BEL | `17` ETB | `27` ' | `37` 7 | `47` G | `57` W | `67` g | `77` w |
| x8 | `08` BS | `18` CAN | `28` ( | `38` 8 | `48` H | `58` X | `68` h | `78` x |
| x9 | `09` HT | `19` EM | `29` ) | `39` 9 | `49` I | `59` Y | `69` i | `79` y |
| xA | `0A` LF | `1A` SUB | `2A` * | `3A` : | `4A` J | `5A` Z | `6A` j | `7A` z |
| xB | `0B` VT | `1B` ESC | `2B` + | `3B` ; | `4B` K | `5B` [ | `6B` k | `7B` { |
| xC | `0C` FF | `1C` FS | `2C` , | `3C` < | `4C` L | `5C` \\ | `6C` l | `7C` \| |
| xD | `0D` CR | `1D` GS | `2D` - | `3D` = | `4D` M | `5D` ] | `6D` m | `7D` } |
| xE | `0E` SO | `1E` RS | `2E` . | `3E` > | `4E` N | `5E` ^ | `6E` n | `7E` ~ |
| xF | `0F` SI | `1F` US | `2F` / | `3F` ? | `4F` O | `5F` _ | `6F` o | `7F` DEL |

*A = 0x41 = (101001)base2*
*EOT(End of transmission) = 0x04 = (00000100)base2*

# De bits a Byte(octet)

8bits -> 1 byte

# D'Octet a mots

| Nibble | Byte | Half word/ word | Double Word | Quad word |
|--------|------|-----------------|-------------|-----------|
|half of a byte/ 4bits  | 1byte / 8bits | 2bytes, 16bits | 4bytes, 32 bits | 8bytes, 64bits |

Pour l'histoire, à époque il y avait des architectures de 16 bits, on disait donc a cette époque de  16bits == **word**. Peut après il y eu eu des architecture de 32bits et on se mit également à associer 32bits == **word**.

Ainsi il y a "chevauchement":

- **16bits peut être appelé: word ou half word**
- **32bits peut être appelé: word ou double word**

# Expression des Nombres

Some numbers 0 = 0b00000000, 1 = 0b00000001

Pour gérer les nombres négatifs en binaire on utilse l'approche des deux complémentaires.
*Exemple:* 0 - 1 = 0b00000000 - 0b00000001 = 0b11111111 = 255 = -1 (*tu comprends le jeu?*)

Ce qui fait que les opérations arithmétique n'ont pas a considerer les signes car de toute façon chaque représentation sur n bits a à la fois une équivalence positive et une négative en base 10.

*NOTONS TRÈS BIEN QUE:* C'est d'une maniere ou d'une autre le programmeur qui spécifie qu'un représentation binaire est le complémentaire positif ou le négatif.

En C par exemple:

```
uint8_t a = 0b11111111; // tu dis au cpu d'interpreter comme étant 255 (unsigned int) élement de [0, 255]
int8_t b = 0b11111111; // tu dis au cpu d'interpreter comme étant -1 (signed int) élement de [-128, 127]
```

DAMN SHIT WEIRD, but thinks about it.

# Anatomie d'un *word*

MSB = Most Signifiant Bits/Bytes
LSB = Least Significant Bits/Bytes


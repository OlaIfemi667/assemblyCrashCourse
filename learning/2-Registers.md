# Les registers

Ce sont des stockages pour la data, ils sont très "rapides".

| Architecture | Bits | GPR (usage général) | Stack Pointer | Base Pointer | Instr. Pointer | Nb registres |
|---|---|---|---|---|---|---|
| 8085 | 8-bit | A, B, C, D, E, H, L | SP | — | PC | 7 GPR |
| 8086 | 16-bit | AX, BX, CX, DX, SI, DI | SP | BP | IP | 8 GPR |
| x86 | 32-bit | EAX, EBX, ECX, EDX, ESI, EDI | ESP | EBP | EIP | 8 GPR |
| amd64 | 64-bit | RAX, RBX, RCX, RDX, RSI, RDI, R8–R15 | RSP | RBP | RIP | 16 GPR |
| ARM 32-bit | 32-bit | R0–R12 | R13 (SP) | R11 (FP) | R15 (PC) | 16 GPR |
| ARM64 / AArch64 | 64-bit | X0–X28 (W0–W28 en 32-bit) | SP (dédié) | X29 (FP) | PC (dédié) | 31 GPR |

> **Héritage x86 :** `AL` (8b) ⊂ `AX` (16b) ⊂ `EAX` (32b) ⊂ `RAX` (64b).
> Écrire dans `EAX` zero-extend les 32 bits supérieurs de `RAX`.
> Écrire dans `AL` zéro-extend les 56bis  suppérieurs de `RAX`

**zero-extend** = *set to zero*

*ex*: (10)base2

## Charger de la data dans un registre

Pour charger de la data dans un registre on utilise l'instruction *mov*

```
mov rax, 0x539
mov rbx, 1337
```

Et comme on peut aussi couper la donner et ajouter chaque partie dans des registres partiels:

mov rax, 0x539 équivaut a:

```
mov ah, 0x5
mov al, 0x39
```
Pour le moment ça va XD.

## ICI IL Y A UN TRUC CHELOU QUI SE PASSE!!

Quand on charge de la donné dans registre partiel de 32bits (e.g., **eax**) le cpu met a me reste du régistre a zéro.


Ceci met a 0xfffff666 rax
```
mov rax, 0xffffffff
mov ax,0x666
```


Ceci met a 0x00000666 rax
```
mov rax, 0xffffffff
mov eax, 0x539
```

**NB:** mov de déplace pas la donnée, elle la copie

# Arithmétique sur les registres

| Catégorie | Opération | x86 / amd64 | Exemple (amd64) | Résultat | Flags affectés |
|---|---|---|---|---|---|
| **Arithmétique** | Addition | `ADD dst, src` | `add rax, rbx` | `rax = rax + rbx` | CF, OF, ZF, SF |
| | Addition + carry | `ADC dst, src` | `adc rax, rbx` | `rax = rax + rbx + CF` | CF, OF, ZF, SF |
| | Soustraction | `SUB dst, src` | `sub rax, rbx` | `rax = rax - rbx` | CF, OF, ZF, SF |
| | Soustraction + borrow | `SBB dst, src` | `sbb rax, rbx` | `rax = rax - rbx - CF` | CF, OF, ZF, SF |
| | Multiplication (non signé) | `MUL src` | `mul rbx` | `rdx:rax = rax × rbx` | CF, OF |
| | Multiplication (signé) | `IMUL dst, src` | `imul rax, rbx` | `rax = rax × rbx` | CF, OF |
| | Division (non signé) | `DIV src` | `div rbx` | `rax = quotient, rdx = reste` | indéfinis |
| | Division (signé) | `IDIV src` | `idiv rbx` | `rax = quotient, rdx = reste` | indéfinis |
| | Incrément | `INC dst` | `inc rax` | `rax = rax + 1` | OF, ZF, SF (pas CF) |
| | Décrément | `DEC dst` | `dec rax` | `rax = rax - 1` | OF, ZF, SF (pas CF) |
| | Négation | `NEG dst` | `neg rax` | `rax = 0 - rax` | CF, OF, ZF, SF |
| **Bitwise** | ET logique | `AND dst, src` | `and rax, rbx` | `rax = rax & rbx` | ZF, SF |
| | OU logique | `OR dst, src` | `or rax, rbx` | `rax = rax \| rbx` | ZF, SF |
| | OU exclusif | `XOR dst, src` | `xor rax, rax` | `rax = 0` (zeroing idiom) | ZF, SF |
| | NON logique | `NOT dst` | `not rax` | `rax = ~rax` | aucun |
| **Décalages** | Décalage gauche | `SHL dst, n` | `shl rax, 2` | `rax = rax × 4` | CF, OF, ZF, SF |
| | Décalage droite (non signé) | `SHR dst, n` | `shr rax, 1` | `rax = rax / 2` | CF, OF, ZF, SF |
| | Décalage droite (signé) | `SAR dst, n` | `sar rax, 1` | `rax >> 1` (arithm.) | CF, OF, ZF, SF |
| | Rotation gauche | `ROL dst, n` | `rol rax, 1` | bits rotatés via CF | CF, OF |
| | Rotation droite | `ROR dst, n` | `ror rax, 1` | bits rotatés via CF | CF, OF |
| **Comparaison** | Comparer | `CMP dst, src` | `cmp rax, rbx` | flags mis à jour, dst inchangé | CF, OF, ZF, SF |
| | Tester bits | `TEST dst, src` | `test rax, rax` | ZF=1 si rax=0, dst inchangé | ZF, SF |

> **Flags :** CF = Carry, OF = Overflow, ZF = Zero, SF = Sign



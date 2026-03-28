## Control Flow: Jumps

> Le CPU exécute les instructions en séquence **jusqu'à ce qu'on lui dise de ne pas le faire**.

### Principe du `jmp`

| Étape | Ce qui se passe |
|---|---|
| Exécution normale | Le CPU suit les instructions une par une (adresse +1 à chaque fois) |
| `jmp LABEL` | Le CPU saute à l'adresse du label, **ignore** les instructions entre les deux |
| Reprise | L'exécution continue à partir du label |

### Exemple

```asm
mov cx, 1337     ; cx = 1337
jmp STAY_LEET    ; saute à STAY_LEET → mov cx, 0 est ignoré
mov cx, 0        ; ← jamais exécuté
STAY_LEET:
push rcx         ; ← exécution reprend ici
```

### En mémoire (binaire)

| Adresse | Instruction | Opcode | Note |
|---|---|---|---|
| `0x400800` | `mov rcx, 0x1337` | `66 b9 37 13` | charge la valeur |
| `0x400804` | `jmp STAY_LEET` | `eb 04` | saute +4 bytes |
| `0x400806` | `mov rcx, 0` | `66 b9 00 00` | **ignoré** |
| `0x40080a` (STAY_LEET) | `push rcx` | `51` | reprise ici |

> `eb 04` = opcode `jmp` relatif court — saute **4 bytes** en avant depuis l'instruction suivante.

### Types de jumps (amd64)

| Instruction | Condition | Flag testé |
|---|---|---|
| `jmp` | Toujours (unconditional) | — |
| `je` / `jz` | Égal / Zéro | ZF = 1 |
| `jne` / `jnz` | Non égal / Non zéro | ZF = 0 |
| `jg` / `jnle` | Supérieur (signé) | ZF=0 et SF=OF |
| `jge` / `jnl` | Supérieur ou égal (signé) | SF = OF |
| `jl` / `jnge` | Inférieur (signé) | SF ≠ OF |
| `jle` / `jng` | Inférieur ou égal (signé) | ZF=1 ou SF≠OF |
| `ja` / `jnbe` | Supérieur (non signé) | CF=0 et ZF=0 |
| `jb` / `jnae` | Inférieur (non signé) | CF = 1 |
| `jae` / `jnb` | Supérieur ou égal (non signé) | CF = 0 |
| `jbe` / `jna` | Inférieur ou égal (non signé) | CF=1 ou ZF=1 |
| `jo` | Overflow | OF = 1 |
| `js` | Signe négatif | SF = 1 |
| `jcxz` / `jecxz` / `jrcxz` | CX/ECX/RCX = 0 | (registre) |

> Les jumps conditionnels se placent **après un `cmp` ou `test`** qui met à jour les flags

> *cmp* fait une opération **sub** et se débarrasse du résultat.
> *test* fait une opération **AND** et se débarasse du résultat.

## Control Floaw: Loops

### Principe de création d'une boucle

```asm
mov rax, 0
LOOP_HEADER:
inc rax
cmp rax,10
jb LOOP_HEADER
```

**jb vérifie si rax est inférieur de 10**


## Control Flow: Functions

```asm
mov rdi, 0
call FUNC_CHECK_LEET
mov rdi, 1
call FUNC_CHECK_LEET
call EXIT

FUNC_CHECK_LEET:
    test rdi, rdi
    jnz LEET
    mov ax, 0
    ret
    LEET:
    mov ax, 1337
    ret
EXIT:
    ??? *next course*

## Calling conventions 

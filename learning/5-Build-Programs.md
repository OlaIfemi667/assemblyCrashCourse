## Ecrire de l'assembleur
Nous allons écrire un programme qui "EXIT" just

```asm

.global _start # pour définir un la variable _start (elle permet d'indiquer le debut du programme au compilateur.

_start:

.intel_syntax noprefix

mov rdi, 42 # c'est le return code de notre programme
mov rax, 60 # 60 est le system call pour exit

syscall
```

## La compilation

```bash
gcc -nostdlib quitter quitter.s 

./quitter

echo $?
42

```

**-nostdlib** permet de spécifier au conpilateur de ne pas ajouter stdlib cas il ne s'agit pas d'un programme en c.

## Obtenir le assembleur d'un ELF

```bash
objdump -M intel -d quitter
```

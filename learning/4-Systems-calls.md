#System Calls

Un syscall (appel système) est le mécanisme par lequel un programme en espace utilisateur demande un service au noyau Linux. En user space, tu n'as pas accès direct aux ressources matérielles — c'est le kernel qui s'en charge via une interface contrôlée.
Mécanisme : tu charges les arguments dans des registres spécifiques, tu mets le numéro du syscall dans rax, puis tu déclenches syscall. Le CPU bascule en kernel mode, exécute le service, et te rend le contrôle avec le retour dans rax.
La convention d'appel pour les syscalls Linux x86-64 (différente de celle des fonctions C) :

```
| Registre | Rôle | Exemple (write) |
|----------|------|-----------------|
| `rax` | Numéro du syscall | `mov rax, 1` → sys_write = 1 |
| `rdi` | Argument 1 | `mov rdi, 1` → fd stdout |
| `rsi` | Argument 2 | `mov rsi, msg` → ptr buffer |
| `rdx` | Argument 3 | `mov rdx, 13` → longueur |
| `r10` | Argument 4 | — |
| `r8` | Argument 5 | — |
| `r9` | Argument 6 | — |
| `rax` (retour) | Valeur de retour | négatif = `-errno` |
```

---
aliases:
  - Yet Another Yogurt
tags:
  - linux
  - arch-linux
  - cli
---
O `yay` é um wrapper completo do [[pacman]] escrito em [[Go]] que acessa tanto os repositórios oficiais do Arch quanto o [[AUR]]. Na prática, pode substituir o `pacman` em todas as operações do dia a dia (usa exatamente as mesmas flags).

>[!warning] Nunca use com `sudo`
>O `yay` baixa e compila pacotes como usuário comum para evitar a execução de scripts arbitrários como root, solicitando a senha internamente apenas na etapa final de instalação.
## Comandos Úteis 
-  `yay` (sem argumentos): Equivale a `yay -Syu`, atualizando todos os pacotes oficiais e do [[AUR]] de uma só vez. 
- `yay -Sc`: Limpa o cache de pacotes antigos e diretórios de build do [[AUR]].
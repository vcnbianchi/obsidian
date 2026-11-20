---
aliases:
  - Package Manager
tags:
  - linux
  - arch-linux
  - cli
---
O `pacman` é o gerenciador de pacotes nativo dos sistemas [[Arch Linux|Arch-Based]]. Suas operações se organizam em duas flags: uma **operação principal** (letra maiúscula) e os **modificadores** associados (letras minúsculas):

1. `-S` (Sync): Repositórios remotos (instalar, atualizar o sistema e buscar).
2. `-R` (Remove): Desinstalação de pacotes locais.
3. `-Q` (Query): Consulta ao banco de dados local (pacotes instalados, órfãos e versões).
4. `-F` (Files): Busca qual pacote fornece determinado arquivo ou cabeçalho (`.h`).

## Dicionário de Operações ([[Debian]] vs. [[Arch Linux]] vs. [[Omarchy]])

| Operação                |               Debian-Based               |               Arch-Based                |         Omarchy Shortcut         |
| :---------------------- | :--------------------------------------: | :-------------------------------------: | :------------------------------: |
| Atualização Completa    | `sudo apt update && sudo apt upgrade -y` |           `sudo pacman -Syu`            |         `omarchy update`         |
| Instalar um Pacote      |         `sudo apt install <pkg>`         |         `sudo pacman -S <pkg>`          |     `omarchy pkg add <pkg>`      |
| Remover Completamente   |   `sudo apt purge --autoremove <pkg>`    |        `sudo pacman -Rns <pkg>`         |    `omarchy pkg remove <pkg>`    |
| Buscar nos Repositórios |           `apt search <query>`           |          `pacman -Ss <query>`           | Menu (`Super + Space` - Install) |
| Ver Detalhes de Pacote  |             `apt show <pkg>`             |           `pacman -Si <pkg>`            |                —                 |
| Listar Instalados       |          `apt list --installed`          |       `pacman -Q` ou `pacman -Qe`       |                —                 |
| Dono de um Arquivo      |             `dpkg -S /path`              |           `pacman -Qo /path`            |                —                 |
| Buscar Header Ausente   |        `apt-file search header.h`        | `sudo pacman -Fy && pacman -F header.h` |                —                 |
| Limpar Cache Antigo     | `sudo apt autoremove && sudo apt clean`  |           `sudo paccache -r`            |  Automático no `omarchy update`  |
---
aliases:
  - AUR
  - Arch User Repository
  - PKGBUILD
tags:
  - linux
  - arch-linux
---
O **AUR (*Arch User Repository*)** é o repositório comunitário centralizado para usuários de distribuições baseadas em [[Arch Linux]].
## Arquitetura

Diferente de um [[PPA]] no [[Debian]], que entrega um binário `.deb` fechado e compilado por terceiros, o AUR **não hospeda arquivos binários**, apenas "receitas de construção" em texto puro chamadas `PKGBUILD`.

Quando você instala um pacote `-bin` via [[yay]], o script busca o arquivo oficial diretamente na URL da desenvolvedora (ex: servidores da Microsoft ou Google), valida a integridade via checksum SHA-256 e o converte em um pacote nativo gerenciado pelo [[pacman]].
## Sufixos de Pacotes

- `<pkg>-bin`: Baixa o binário oficial pré-compilado (prefira sempre para softwares grandes por instalar em segundos).
- `<pkg>`: Baixa o código-fonte e compila na máquina usando o `PKGBUILD`.
- `<pkg>-git`: Compila diretamente do último commit da branch principal do repositório oficial.
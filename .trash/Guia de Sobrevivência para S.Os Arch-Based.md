---
title: Guia de Sobrevivência para S.Os Arch-Based
author: Victor Bianchi
type:
  - note
aliases:
  - arch-guide
tags:
  - linux
  - arch-linux
references:
created at: 2026-11-14
updated at: 2026-11-15
---
O gerenciador de pacotes nativo dos sistemas Arch-Based é o `pacman`. Em termos gerais, **as operações do `pacman` se organizam em duas flags**, sendo uma a **operação principal, representada sempre por uma letra maiúscula e a outra sendo os modificadores** associados a operação principal **sendo representados por letras minúsculas**.

O `yay` é um **wrapper completo** do `pacman` que acessa tanto repositórios oficiais quanto o AUR, sendo geralmente utilizado em conjunto com o mesmo. Na prática, usuários de sistemas Arch-Based usam sempre o `yay` para todas as operações. No entanto, o `yay` tem um ponto de atenção: **ele nunca deve ser utilizado com `sudo`**, ele mesmo pedirá senha quando necessário.

Em sistemas Arch-Based **não existem pacotes `-dev` separados** assim como existem em sistemas Debian-Based. Ao instalar `curl`, `openssl` ou `glibc`, **todos os headers (`.h`) e bibliotecas estáticas/dinâmicas já vêm juntos** em `/usr/include` e `/usr/lib`.

>[!warning] Regra de Ouro do Rolling Release: NUNCA faça "Partial Upgrades"
>Em sistemas Debian-Based é comum atualizarmos a lista de índices dos repositórios e logo depois instalarmos algum pacote sem necessariamente aplicarmos as atualizações no restante do sistema. **Se fizer isso em um sistema Arch-Based o pacote novo a ser instalado pode exigir uma versão da `glibc` ou `libssl` mais recente, por exemplo, do que a instalada na sua máquina, quebrando dependências dinâmicas.**

Diferentemente do que ocorre em distribuições baseadas em Debian, onde temos a possibilidade de inserir PPAs e instalarmos arquivos executáveis `.deb` avulsos, em sistemas baseados em Arch Linux temos o AUR. 

O **AUR (_Arch User Repository_)** é um **grande repositório comunitário e centralizado**, amplamente utilizado por usuários do Arch Linux e de outras distribuições baseadas no mesmo. O repositório se tornou famoso por sua ampla gama de aplicações e pacotes disponíveis para instalação. Ao utilizar o `yay` ou o atalho do Omarchy (`omarchy pkg add`) será possível ver sufixos importantes nos pacotes do AUR:
- `<pkg>-bin`: Baixa o binário oficial pré-compilado. No geral, sempre prefira a versão `-bin` para softwares grandes pois instalam em segundos.
- `<pkg>`: Baixa o código-fonte e compila na máquina usando um script chamado `PKGBUILD`.
- `<pkg>-git`: Compila diretamente do último commit da branch `main` do repositório oficial.
No lado Debian da força, os **PPAs (_Personal Package Archives_)**, assim como os repositórios externos de terceiros em geral, **são servidores independentes e descentralizados que distribuem pacotes pré-compilados** para suprir a falta de softwares recentes nos repositórios oficiais. Na prática, utilizar PPAs ou pacotes `.deb` avulsos traz três grandes atritos:
1. **Fragmentação e configuração manual**: Para cada software externo não presente nos repositórios oficiais da distribuição, como Docker, VS Code ou Microsoft Edge, é necessário **importar manualmente uma chave criptográfica GPG** (`/etc/apt/keyrings`) **e cadastrar a URL do servidor** em `/etc/apt/sources.list.d/`. **Já um arquivo `.deb` baixado pelo navegador sequer se atualiza sozinho**, a menos que ele mesmo injete um repositório extra no sistema.
2. **Quebra em atualizações de versão:** Como **cada PPA é atrelado a um codinome específico da distribuição** (ex: _bookworm_, _noble_), atualizar o sistema operacional frequentemente gera erros de repositório inexistente (`404 Not Found`) ou conflitos de dependências (_dependency hell_).
3. **Caixa-preta vs. Transparência:** Enquanto um **PPA entrega um pacote `.deb` já fechado e compilado por terceiros**, o AUR **não hospeda binários por conta própria**, ele armazena apenas as **"receitas de construção" em texto puro, os chamados arquivos `PKGBUILD`**. Quando você instala um pacote `-bin` pelo AUR, **o script apenas busca o arquivo oficial diretamente na URL da empresa desenvolvedora**, como o próprio servidor da Microsoft ou do Google, **verifica a integridade** via _checksum_ SHA-256 e o **converte em um pacote nativo gerenciado pelo `pacman`**, mantendo todo o sistema centralizado em um único comando de atualização.

Podemos generalizar todas as operações do `pacman` em operações principais:
1. `-S` (Sync): Tudo que envolve os repositórios remotos, como instalar, atualizar o sistema e buscar na nuvem.
2. `-R` (Remove): Tudo que envolve desinstalar pacotes da sua máquina.
3. `-Q` (Query): Tudo que envolve consultar o banco de dados local, isto é, tudo o que já está instalado, pacotes órfãos e versões locais.
4. `-F` (Files): Busca qual pacote fornece um determinado arquivo ou cabeçalho.
# Dicionário de Tradução

| Operação                          |               Debian-Based               |                Arch-Based                 |         Omarchy Shortcut         |
| :-------------------------------- | :--------------------------------------: | :---------------------------------------: | :------------------------------: |
| Atualização Completa              | `sudo apt update && sudo apt upgrade -y` |   `sudo pacman -Syu` ou `sudo yay -Syu`   |         `omarchy update`         |
| Instalar um Pacote                |         `sudo apt install <pkg>`         |          `sudo pacman -S <pkg>`           |     `omarchy pkg add <pkg>`      |
| Remover um Pacote Completamente   |   `sudo apt purge --autoremove <pkg>`    |         `sudo pacman -Rns <pkg>`          |    `omarchy pkg remove <pkg>`    |
| Buscar um Pacote nos Repositórios |           `apt search <query>`           | `pacman -Ss <query>` ou `yay -Ss <query>` | Menu (`Super + Space` > Install) |
| Ver Detalhes de um Pacote         |             `apt show <pkg>`             |            `pacman -Si <pkg>`             |                —                 |
| Listar Pacotes Instalados         |          `apt list --installed`          |        `pacman -Q` ou `pacman -Qe`        |                —                 |
| Descobrir Dono de um Arquivo      |             `dpkg -s /path`              |            `pacman -Qo /path`             |                —                 |
| Buscar Cabeçalho não Instalado    |        `apt-file search header.h`        |  `sudo pacman -Fy && pacman -F header.h`  |                —                 |
| Limpar Cache de Pacotes Antigos   | `sudo apt autoremove && sudo apt clean`  |      `yay -Sc` ou `sudo paccache -r`      |  Automático no `omarchy update`  |

---
title: "Manual de Referência: Omarchy"
author: Victor Bianchi
aliases:
  - omarchy
  - omarchy-manual
  - omarchy-ref
tags:
  - omarchy
  - arch-linux
  - linux
references:
  - https://omarchy.org/manual
created at: 2026-11-15
updated at: 2026-11-15
---
Omarchy é uma distribuição Linux baseada no Arch Linux cuja principal filosofia é o *omakase*, isso é, "a moda do chefe", que se traduz para um sistema operacional opinativo e pronto para uso com um catálogo de ferramentas e configurações incluídas ideais segundo o criador da distribuição: o DHH (David Heinemeier Hansson), criador do Ruby On Rails.

A distribuição possui como interface o Hyprland, um *tiling window manager* em conjunto com Quickshell, um *toolkit* e *framework* moderno desenvolvido em C++ para a criação de componentes de interface gráficas de desktop Linux. Por se tratar de uma distribuição pronta para uso e seguir a filosofia *omakase* o Omarchy vem com diversos softwares já pré-instalados e configurados seguindo o gosto do DHH. Isso pode ser considerado por muitos como um problema e até mesmo *bloatware*, no entanto, o próprio sistema tem ferramentas de *debloat* que remove tudo o que o mesmo já entrega por padrão caso o usuário assim deseje.

O sistema operacional pode ser instalado através de uma ISO pronta ou através de um script bash executado sobre um Arch Linux. O usuário pode escolher se deseja instalar o sistema em todo o disco, apagando tudo o que havia anteriormente ou se deseja utilizar algum espaço livre disponível em um disco específico, fazendo dessa forma o dual-boot. É importante mencionar que a documentação alerta que para instalar o sistema corretamente será necessário desativar o Secure Boot e o TPM 2.0 nas configurações da BIOS. Em poucos minutos o sistema estará instalado.

A documentação também destaca alguns outros pontos como sempre utilizar um teclado cabeado ou wireless com conexão 2.4 GHz e nunca somente Bluetooth, isso porque o Omarchy utiliza criptografia completa de disco e utiliza a senha definida do usuário como o passe para descriptografar o sistema e nesta tela o Bluetooth não funciona.

>[!note] Instalação para terceiros
>Caso a instalação esteja sendo feita para uma outra pessoa, como um funcionário, um comprador ou um familiar não se deve preencher os campos das informações pessoais com as suas próprias. Prefira usar o atalho `CTRL + C` e assim fazer com que o Omarchy defira as configurações temporariamente até o primeiro boot para que a pessoa possa preencher com suas próprias informações.

>[!tip] Para instalar o sistema sem criptografia, utilize o atalho `CTRL + C` na tela de confirmação de formatação de disco para alterar para o modo *encryption-less*.




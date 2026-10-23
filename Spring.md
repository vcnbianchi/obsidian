---
title: Spring
aliases:
  - Spring
  - Spring Framework
  - Spring Boot
author: Victor Bianchi
created at: 2026-10-23
updated at: 2026-10-23
---
Apesar de terem nomes semelhantes, **Spring** e **Spring Boot** não são a mesma coisa.

**Spring** é um ***framework* para desenvolvimento de aplicações em Java**, criado em meados de **2002** por **Rod Johnson**, que se tornou bastante popular e adotado ao redor do mundo devido a sua simplicidade e facilidade de integração com outras tecnologias. O *framework* foi desenvolvido de maneira **modular**, na qual cada recurso que ele disponibiliza é representado por um módulo, que pode ser adicionado em uma aplicação conforme as necessidades, fazendo assim com que ela seja mais leve.

Entretanto, um dos grandes problemas existentes em aplicações que utilizavam o Spring era **a parte de configurações de seus módulos, que era feita com arquivos XML**, sendo que depois de alguns anos o *framework* também **passou a dar suporte a configurações via classes Java**, utilizando, principalmente, anotações. Em ambos os casos, dependendo do tamanho e complexidade da aplicação, e também da quantidade de módulos do Spring utilizados nela, tais configurações eram bastante extensas e de difícil manutenção. Além disso, iniciar um novo projeto com o Spring era uma tarefa um tanto quanto complicada, devido a necessidade de realizar tais configurações no projeto.

Justamente para resolver tais dificuldades é que foi criado um novo módulo do Spring, chamado de **Boot**, em meados de **2014**, com o propósito de agilizar a criação de um projeto que utilize o Spring como *framework*, bem como simplificar as configurações de seus módulos.
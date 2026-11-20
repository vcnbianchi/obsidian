---
aliases:
  - NextJS
  - Next
tags:
  - nextjs
  - react
  - web-dev
  - frontend
  - fullstack
references:
  - "[[Documentação - Next.js]]"
---
O **Next.js** é um framework [[React]] flexível voltado para a construção de aplicações web *full stack*, entregando estrutura e configurações pré-prontas para levar projetos à produção com menos atrito.
## Framework Opinativo vs. Biblioteca ([[React]])

O [[React]] é deliberadamente uma biblioteca não-opinativa focada apenas na camada de interface, o que dá liberdade ao ecossistema, mas exige esforço considerável para configurar e manter uma aplicação grande do zero. O **Next.js** atua sobre o [[React]] fornecendo uma base integrada que resolve boa parte das decisões arquiteturais recorrentes em aplicações web modernas.
## Building Blocks de uma Aplicação Web

Ao projetar uma aplicação web, diversos pilares (*Building Blocks*) precisam ser considerados, decidindo, para cada um, entre construir uma solução própria ou adotar bibliotecas, pacotes e frameworks prontos:

- **User Interface (UI):** como os usuários interagem e consomem a aplicação.
- **Routing:** como os usuários navegam entre diferentes páginas e seções.
- **Data Fetching:** onde os dados estão armazenados e como obtê-los.
- **Rendering:** quando e onde renderizar conteúdo estático ou dinâmico.
- **Integrations:** quais serviços de terceiros a aplicação consome e como se conectar a eles.
- **Infrastructure:** onde fazer o *deploy*, armazenar e executar o código da aplicação ([[Serverless]], [[CDN]], [[Edge Computing|edge]], [[self-hosted]], etc.).
- **Performance:** como otimizar carregamento e responsividade para os usuários finais.
- **Scalability:** como a aplicação se adapta ao crescimento do time, do volume de dados e do tráfego.
- **Developer Experience (DX):** a experiência do time de desenvolvimento na construção e manutenção contínua do projeto.
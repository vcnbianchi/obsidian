/setup-matt-pocock-skills

Configure este repositório do zero para o desenvolvimento do projeto **OmniHub**, utilizando uma metodologia rígida de Engenharia de Software conduzida por agentes de IA. Todo o contexto, visão, arquitetura, requisitos funcionais, requisitos não funcionais, guardrails e decisões em aberto do projeto estão descritos integralmente neste prompt e devem ser persistidos por você nos arquivos de governança e documentação do repositório (ex.: `AGENTS.md`, `GLOSSARY.md`, `docs/adrs/`, `docs/specs/` e demais artefatos do pipeline).
## 1. Contexto, Visão do Produto e Princípios Norteadores

- **Projeto:** **OmniHub**
- **Propósito:** Plataforma web centralizada de gestão pessoal, **multiusuário** e sob **soberania de dados**, projetada para substituir aplicativos comerciais fragmentados (gestores de tarefas, agendas, controles financeiros e painéis avulsos) por um único hub operacional coeso, previsível e extensível.
### Princípios Norteadores

1. **Centralização Real:** reunir tarefas, projetos, agenda, alertas, finanças e demais áreas pessoais em uma única interface e em um único banco relacional consistente, reduzindo troca de contexto.
2. **Soberania de Dados e Self-Hosted First:** o sistema deve rodar integralmente em infraestrutura própria (máquina local, home server ou NAS via Docker) sem depender de serviços proprietários de nuvem, mantendo portabilidade total para deploy em servidor remoto (VPS ou cloud, como Oracle Cloud Infrastructure - OCI) via variáveis de ambiente.
3. **Monólito Modular Disciplinado:** evitar a complexidade operacional de microsserviços distribuídos, mas preservar fronteiras rígidas de domínio dentro de uma única base de código e unidade de deploy.
4. **Engenharia Orientada a Especificação e Testes:** nenhuma funcionalidade entra em produção sem requisitos claros, contratos tipados, invariantes de domínio formalizadas e testes automatizados.
5. **Simplicidade Operacional:** priorizar topologia mínima de containers, baixo consumo de recursos (RAM/CPU) e backups triviais.
## 2. Arquitetura e Stack Tecnológica Obrigatória

|                                    |                                                    |                                                                                                                                                                                     |
| ---------------------------------- | -------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Camada**                         | **Tecnologia Definida**                            | **Papel no Sistema**                                                                                                                                                                |
| **Arquitetura**                    | **Monólito Modular**                               | Separação estrita de domínios com deploy único e simples                                                                                                                            |
| **Full-Stack (Web + API)**         | **Next.js (App Router)** em **TypeScript** estrito | Interface web, Server Components, Server Actions e Route Handlers (API) em um único runtime                                                                                         |
| **UI e Estilização**               | **Tailwind CSS + shadcn/ui**                       | Base de estilização e componentes acessíveis (Radix UI); o Design System será definido à parte                                                                                      |
| **Banco de Dados**                 | **PostgreSQL**                                     | Persistência relacional transacional única para todos os domínios e autenticação                                                                                                    |
| **ORM e Migrations**               | **Drizzle ORM**                                    | Acesso SQL-first tipado, schemas isolados por módulo (`src/modules/**/schema.ts`) e migrations versionadas no PostgreSQL                                                            |
| **Autenticação e Autorização**     | **Better Auth**                                    | Gestão de usuários, sessões, autenticação multiusuário (e-mail/senha, Microsoft, Google, Passkey e 2FA) e proteção de rotas, embutido no Next.js com adaptador Drizzle + PostgreSQL |
| **Lint, Formatação e Fronteiras**  | **Biome + `dependency-cruiser`**                   | Formatação/lint rápido via Biome e validação automatizada de fronteiras entre módulos via `dependency-cruiser`                                                                      |
| **Infraestrutura e Empacotamento** | **Dockerfile + Docker Compose (`compose.yml`)**    | Build multi-stage com `output: 'standalone'` e topologia enxuta de 2 containers (`app` + `db` com volume persistente)                                                               |
### Estrutura de Fronteiras do Monólito Modular

Para impedir que o Next.js se transforme em um monólito acoplado onde regras de negócio se misturam a componentes React e rotas HTTP:

- **`src/app/` (Camada de Entrega Fina):** responsável apenas por roteamento, composição de páginas, Server Actions e Route Handlers. Não pode conter regras de negócio complexas nem queries diretas de domínio; apenas valida sessão/payload e delega aos módulos.
- **`src/modules/<dominio>/` (Módulos de Domínio Isolados):** cada módulo encapsula suas próprias entidades, schema Drizzle (`schema.ts`), regras de negócio, casos de uso, persistência/queries e testes.
    - Na Fase 1 (MVP), o foco é o módulo de autenticação/usuários (`auth`), mantendo a arquitetura preparada para plugar os domínios futuros (`tasks`, `calendar`, `dashboard`, `notifications`, `finances`, entre outros).
    - O `drizzle.config.ts` deve descobrir os schemas de domínio automaticamente via padrão `src/modules/**/schema.ts`.
    - Cada módulo expõe um único ponto de entrada público (`index.ts`) com serviços, tipos e contratos permitidos para outros módulos e para `src/app/`.
    - Imports que atravessem a fronteira interna de outro módulo (qualquer arquivo dentro de `src/modules/<dominio>/*` fora do `index.ts`) devem ser bloqueados automaticamente via **`dependency-cruiser`** rodando nos scripts de checagem/CI.
- **`src/shared/` (Infraestrutura Compartilhada):** conexão com PostgreSQL/Drizzle, configuração base do Better Auth, utilitários de data/fuso horário e tratamento padronizado de erros (primitivos do `shadcn/ui` em `src/components/ui/` ou `src/shared/ui/`).
### Infraestrutura Self-Hosted First e Portabilidade

- **Topologia padrão (`compose.yml`):** apenas 2 serviços — `app` (Next.js _standalone_) e `db` (PostgreSQL oficial com volume persistente).
- **Configuração por Ambiente (`.env`):** toda configuração sensível ou específica de ambiente (connection string do PostgreSQL, segredo do Better Auth, URL base pública, credenciais OAuth de Google e Microsoft Graph, fuso horário) é injetada via variáveis de ambiente, garantindo que o mesmo artefato Docker rode sem alterações em máquina local, home server/NAS ou servidor remoto (VPS/OCI).
- **Zero Vendor Lock-in:** proibida qualquer dependência de recursos exclusivos de provedores de nuvem (como Vercel Cron, KV proprietário ou auth gerenciado externo).
## 3. Escopo Funcional — Fase 1 (MVP)

A princípio, o **MVP (Fase 1)** contempla exclusivamente a espinha dorsal do repositório e o módulo completo de **Autenticação e Multiusuário**. Os demais módulos de domínio (tarefas, agenda, dashboard, notificações, finanças e integrações futuras) serão especificados e planejados em tarefas posteriores, sem implementação nesta fase.
### Autenticação e Multiusuário (`auth` via Better Auth)
- **Métodos de Login Habilitados:**
    - **E-mail e senha**
    - **Microsoft** (OAuth / Microsoft Graph)
    - **Google** (OAuth)
    - **Passkey** (WebAuthn via plugin oficial do Better Auth)
    - **2FA** (autenticação em dois fatores via plugin oficial do Better Auth)
- **Gestão de Sessões e Persistência:** usuários, sessões, passkeys, fatores 2FA e contas conectadas persistidos no PostgreSQL via adaptador oficial do **Drizzle ORM**.
- **Suporte Multiusuário Nativo:** toda entidade de domínio do sistema pertence explicitamente a um usuário (`userId`), garantindo isolamento completo de dados entre contas desde o início.
- **Proteção** _**Deny-by-Default**_**:** nenhuma página autenticada, Server Action ou Route Handler expõe ou altera dados sem validação prévia de sessão válida e verificação explícita de propriedade do recurso (_ownership check_).
- **Fundação para Integrações (Google e Microsoft Graph):** estruturar o vínculo de contas OAuth de Google e Microsoft de forma limpa para suportar escopos e integrações futuras sem retrabalho.
## 4. Requisitos Não Funcionais (RNFs)

- **Segurança e Privacidade:** _deny-by-default_ em todas as rotas, Server Actions e endpoints; queries obrigatoriamente filtradas por `userId`; segredos e credenciais OAuth exclusivamente via variáveis de ambiente (`.env`), nunca hardcoded ou versionados.
- **Pirâmide de Testes Automatizados:**
    - Testes unitários obrigatórios para regras puras de domínio, validações e guardas de autorização.
    - Testes de integração contra **PostgreSQL real** validando persistência, schemas/migrations Drizzle, fluxos do Better Auth (incluindo Passkey/2FA/OAuth) e isolamento multiusuário.
    - Testes E2E cobrindo os fluxos críticos de autenticação e acesso protegido do MVP.
- **Integridade de Dados e Contratos:** migrations versionadas e determinísticas no PostgreSQL via Drizzle; validação explícita de payloads com schema (ex.: Zod) nas fronteiras da aplicação; TypeScript estrito sem `any` ou supressões injustificadas.
- **Desempenho e Footprint Self-Hosted:** build Next.js `standalone` enxuto, baixo consumo de RAM e CPU em repouso para rodar com folga em hardware doméstico/NAS ou instâncias gratuitas/básicas em nuvem (ex.: OCI).
- **Manutenibilidade Verificável:** typecheck estrito, formatação/lint via **Biome** e checagem automatizada de fronteiras modulares via **`dependency-cruiser`**.
- **Portabilidade e Backup:** subida reproduzível via `docker compose up` (`compose.yml`), volume persistente isolado para o serviço `db` e rotina simples de backup/restore via `pg_dump` / `pg_restore`.
## 5. Metodologia e Guardrails Inegociáveis para os Agentes

1. **Seguir o Pipeline Sequencial:** respeitar rigorosamente o fluxo `setup-matt-pocock-skills` → `grill-with-docs` (`GLOSSARY.md` + ADRs) → `to-spec` → `to-tickets` → `implement` / `tdd`. Não pular etapas e não escrever código de funcionalidades antes de fechar ADRs e especificações.
2. **Isolamento Estrito de Módulos:** nunca importar arquivos internos de outro módulo (`src/modules/A` não importa internals de `src/modules/B`) e nunca fazer query direta em tabelas de outro domínio; toda comunicação entre módulos passa exclusivamente pelo `index.ts` público ou eventos de domínio, validado pelo `dependency-cruiser`.
3. **TDD Obrigatório em Invariantes Críticas:** nenhuma regra crítica (autenticação, 2FA/Passkey, proteção _deny-by-default_, isolamento por `userId` e futuras invariantes de domínio) pode ser implementada sem testes automatizados comprovando tanto o caminho feliz quanto tentativas de violação.
4. **Consistência de UI:** utilizar exclusivamente **Tailwind CSS + shadcn/ui** e os tokens definidos posteriormente via _skill_ `craft`, evitando CSS solto ou componentes duplicados.
5. **Governança por ADRs e Glossário:** tratar os arquivos de governança do repositório, o `GLOSSARY.md` e os ADRs como contratos vinculantes. Qualquer alteração de stack, contrato ou fronteira arquitetural exige registro prévio em ADR.
6. **Idioma e Padronização:** manter a documentação de domínio (`GLOSSARY.md`, ADRs, especificações) em **Inglês (EUA)**, com identificadores de código em inglês padronizado e linguagem ubíqua consistente. Responder diretamente ao desenvolvedor em Português (BR)
## 6. Backlog de ADRs Pendentes para Mapear no Repositório

Com a stack principal, o ORM (**Drizzle**), o linter/guard de fronteiras (**Biome + `dependency-cruiser`**) e a base de UI (**Tailwind CSS + shadcn/ui**, com Design System a ser criado via _skill_ `craft`) já definidos, registre apenas o ADR pendente do MVP para ser refinado na próxima etapa (`grill-with-docs`), **sem decidir unilateralmente agora**:

- **ADR-001 (Crítica — MVP):** Detalhamento operacional da Arquitetura de Autenticação com **Better Auth + Drizzle + PostgreSQL** — políticas de expiração/renovação de sessões, fluxos de vinculação de contas (e-mail/senha, Microsoft, Google, Passkey e 2FA), escopos iniciais de OAuth, armazenamento seguro de tokens de provedores externos e padrão de _ownership check_ nas fronteiras de `src/app/`.

_(Decisões arquiteturais de módulos futuros — como tarefas, agenda, jobs em segundo plano, sincronização bidirecional e finanças — serão registradas em novos ADRs apenas quando cada módulo entrar no ciclo de planejamento.)_
## 7. Saída Esperada Deste Setup Inicial

Execute o `/setup-matt-pocock-skills` incorporando integralmente todo o contexto deste prompt para:
1. Criar e configurar os arquivos de instrução/governança dos agentes no repositório (ex.: `AGENTS.md` e configurações das _skills_) consolidando a visão do produto, a stack fechada (**Next.js + PostgreSQL + Drizzle ORM + Better Auth [e-mail/senha, Microsoft, Google, Passkey, 2FA] + Tailwind CSS + shadcn/ui + Biome + `dependency-cruiser` + Docker `compose.yml`**), as fronteiras do Monólito Modular, os RNFs e os guardrails acima — de forma 100% autocontida.
2. Estruturar os diretórios de documentação (`docs/adrs/`, `docs/specs/`, `GLOSSARY.md`) com o vocabulário inicial e o backlog mapeado com o **ADR-001**.
3. **Não** gerar código de aplicação nem decidir o ADR em aberto nesta etapa — ao concluir o setup, apresente um resumo do que foi configurado e indique que estamos prontos para iniciar a sessão de `grill-with-docs` sobre o **ADR-001**.
4. Caso haja alguma lacuna no projeto, sempre pergunte-me diretamente, nunca assuma nada sozinho.
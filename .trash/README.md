# Segundo Cérebro Técnico

Cofre Obsidian estruturado como uma base de conhecimento técnica atômica, interconectada e orientada a fundamentos. Este documento define a arquitetura, o padrão de propriedades, as convenções de formatação, o estilo de escrita e o fluxo de destilação que regem todo o repositório — diretrizes que devem ser seguidas à risca em toda criação ou revisão de notas.

---

## 1. Arquitetura de Diretórios

O cofre é dividido em cinco diretórios numerados (sem acentuação nos nomes das pastas), cada um com um papel estrito no ciclo de vida do conhecimento:

| Diretório | Função | Frontmatter YAML | Título H1 (`#`) | Regra Central |
| :--- | :--- | :---: | :---: | :--- |
| `00-Inbox/` | Porta de entrada e fila de destilação | Opcional / Ausente | **Não usar** | Captura rápida sem atrito; assuntos podem estar misturados. |
| `01-Conceitos/` | Conhecimento destilado e evolutivo | Obrigatório | **Não usar** | **1 assunto = 1 entidade = 1 arquivo.** |
| `02-Fontes/` | Âncoras de obras e materiais de origem | Obrigatório | **Não usar** | Rastreabilidade (`references`) e índice do que já foi processado na fonte. |
| `03-Indices/` | Índices globais (MOCs) por domínio | Obrigatório | **Não usar** | Mapa de navegação temático independente de fonte. |
| `04-Anexos/` | Mídias e arquivos não-Markdown | N/A | N/A | Imagens, diagramas, vídeos, áudios e documentos referenciados via embed. |

### `00-Inbox/`
Fila de entrada para anotações brutas durante estudos (documentações, livros, cursos, investigações técnicas).
- Não exige formatação final, frontmatter YAML ou separação por entidade (mantendo apenas a regra global de não usar `#` H1, iniciando seções a partir de `##`).
- Pode conter múltiplos assuntos misturados, trechos de código extensos, traduções provisórias e embeds diretos de mídia (`![[arquivo.ext]]`).
- **Natureza temporária:** toda nota aqui existe para ser processada e destilada nos diretórios `01-Conceitos/`, `02-Fontes/` e `03-Indices/`.

### `01-Conceitos/`
Núcleo permanente e vivo do segundo cérebro. Contém exclusivamente notas organizadas por entidade, revisadas e padronizadas.
- **Regra irrevogável:** **1 assunto = 1 entidade = 1 arquivo.** Nunca agrupar dois conceitos distintos na mesma nota (ex: `Array.md` e `Lista Encadeada.md` são arquivos separados que se referenciam e se comparam via wikilinks).
- **Nota viva e evolutiva (sem limite de tamanho):** os arquivos em `01-Conceitos/` **não** foram pensados para permanecer curtos ou excessivamente condensados. Cada arquivo concentra **todo o conhecimento acumulado sobre aquele assunto** e pode — e deve — crescer continuamente com o tempo, tornando-se mais abrangente e até mais leve de ler conforme novos tópicos, exemplos, casos de uso e nuances são adicionados.
- **Abertura direta:** sem H1 no corpo; a nota inicia diretamente no parágrafo de definição logo após o frontmatter YAML, estruturando subtópicos a partir de `##` (H2).

### `02-Fontes/`
Notas-âncora que representam a origem do conhecimento (livros, documentações oficiais, artigos, cursos).
- Funcionam como destino da propriedade `references` nas notas de `01-Conceitos/`.
- Registram o progresso de extração da fonte, listando os conceitos destilados agrupados por capítulo ou seção.

### `03-Indices/`
Índices globais (*Maps of Content*) que consolidam uma área inteira do conhecimento (ex: `Algoritmos e Estrutura de Dados.md`, `Arch Linux.md`).
- Enquanto `02-Fontes/` agrupa conceitos por **origem**, `03-Indices/` agrupa conceitos por **domínio técnico**.
- Organizam os conceitos de `01-Conceitos/` em subseções (`##`) com listas de wikilinks, opcionais ou acompanhadas de uma síntese de uma linha.

### `04-Anexos/`
Armazenamento centralizado de ativos binários e suplementares (imagens, vídeos, áudios, PDFs e outros documentos).
- Referenciados nas notas usando a sintaxe de embed do Obsidian: `![[nome-do-arquivo.ext]]`.
- Dar preferência a formatos leves e modernos para imagens (ex: `.avif`).
- O cofre está configurado com remoção automática de anexos órfãos (`deleteUnlinkedAttachments: "always"`): arquivos sem referência em nenhuma nota são eliminados.

---

## 2. Convenções de Nomenclatura

| Escopo | Padrão | Exemplos |
| :--- | :--- | :--- |
| **Diretórios** | Prefixo numérico `0X-` + substantivo em Title Case sem acentos | `00-Inbox`, `01-Conceitos`, `02-Fontes`, `03-Indices`, `04-Anexos` |
| **Notas em `00-Inbox/`** | `Tipo - Assunto.md` ou título descritivo livre | `Documentação - Next.js.md` |
| **Conceitos em português (`01-Conceitos/`)** | Nome canônico em Title Case com acentuação correta | `Busca Binária.md`, `Lista Encadeada.md`, `Notação Big O.md` |
| **Conceitos consagrados em inglês (`01-Conceitos/`)** | Termo técnico original em Title Case | `Array.md`, `Selection Sort.md` |
| **Siglas (`01-Conceitos/`)** | Tudo em maiúsculas | `AUR.md`, `PPA.md` |
| **Ferramentas CLI / Binários (`01-Conceitos/`)** | Grafia exata do comando em minúsculas | `pacman.md`, `yay.md` |
| **Fontes (`02-Fontes/`)** | `Tipo - Título.md` | `Livro - Entendendo Algoritmos.md` |
| **Índices (`03-Indices/`)** | Nome da disciplina ou ecossistema em Title Case | `Algoritmos e Estrutura de Dados.md`, `Arch Linux.md` |
| **Anexos (`04-Anexos/`)** | `kebab-case` descritivo em minúsculas | `learn-html-and-dom.avif`, `learn-components.avif` |

---

## 3. Padrão de Propriedades (Frontmatter YAML)

Todo arquivo em `01-Conceitos/`, `02-Fontes/` e `03-Indices/` **deve** iniciar com um bloco YAML válido, usando indentação de **2 espaços** para listas.

### Matriz de Propriedades

| Propriedade | Tipo (Obsidian) | `01-Conceitos` | `02-Fontes` | `03-Indices` | Regra de Uso |
| :--- | :--- | :---: | :---: | :---: | :--- |
| `title` | texto | — | Obrigatório | — | Título completo da obra. Usar aspas duplas se contiver `:`. |
| `author` | texto | — | Obrigatório | — | Autor(es) ou mantenedor oficial da fonte. |
| `type` | `multitext` (lista) | — | Obrigatório | — | Tipo de mídia em inglês e minúsculas (ex: `book`, `docs`, `article`, `course`, `paper`). |
| `aliases` | `aliases` (lista) | Obrigatório | Obrigatório | Obrigatório | Sinônimos, plurais, siglas, expansões e equivalentes em inglês/português. |
| `tags` | `tags` (lista) | Obrigatório | Obrigatório | Obrigatório | Sempre em **inglês**, **minúsculas** e **`kebab-case`** (sem `#`). |
| `references` | `multitext` (lista) | Condicional | — | — | Obrigatório quando o conceito deriva de uma fonte em `02-Fontes/`. Omitir o campo se não houver fonte vinculada (não deixar vazio). |

> **Observação sobre metadados:** propriedades temporais (`created at`, `updated at`) não fazem parte do padrão ativo das notas — o histórico de alterações é rastreado pelo Git. Evite adicionar chaves fora da matriz acima sem necessidade estrutural.

### Regras das Propriedades

1. **`aliases`**
   - Inclui variações que alguém digitaria na busca rápida (Quick Switcher) ou ao criar links no texto:
     - Tradução inglês/português: `Binary Search`, `Linked List`, `Ordenação por Seleção`.
     - Plurais e sinônimos: `Arrays`, `Vetor`, `Vetores`, `Busca Linear`, `Busca Sequencial`.
     - Expansão de siglas e acrônimos: `Arch User Repository`, `Personal Package Archive`, `Yet Another Yogurt`, `AED`.
     - Termos fortemente acoplados à entidade: `PKGBUILD` (em `AUR.md`), `Big O`, `Complexidade de Tempo` (em `Notação Big O.md`).

2. **`tags`**
   - **Idioma e formato:** estritamente em inglês, minúsculas e `kebab-case`. Nunca usar tags aninhadas com `/` (ex: `algorithms/search`).
   - **Taxonomia plana e composicional:** combine tags do nível amplo ao específico:
     - **Domínio macro:** `computer-science`, `linux`, `math`, `os`
     - **Subdomínio / ecossistema:** `algorithms`, `data-structures`, `arch-linux`, `debian`, `ubuntu`, `cli`
     - **Especialização por prefixo:** `algo-search`, `algo-selection` (padrão `<domínio-curto>-<subcategoria>`)
     - **Tipo de fonte (em `02-Fontes/`):** `book`, `docs`, etc.

3. **`references`**
   - Sempre formatado como lista YAML com wikilinks **envolvidos por aspas duplas** (obrigatório para evitar que o parser YAML interprete `[[...]]` como lista aninhada):
     ```yaml
     references:
       - "[[Livro - Entendendo Algoritmos]]"
     ```

### Templates Oficiais

#### Nota de Conceito (`01-Conceitos/`)

```markdown
---
aliases:
  - Sinônimo ou Termo em Inglês
tags:
  - dominio-macro
  - subdominio
references:
  - "[[Tipo - Nome da Fonte]]"
---
O **[Nome do Conceito]** (*Termo em Inglês*) é [definição direta e precisa em 1–2 frases].

>[!warning] Pré-requisito ou Alerta Crítico (opcional)
>Restrição indispensável para o uso correto do conceito.

## [Subtópico 1: Arquitetura / Comportamento / Funcionamento]

- **Aspecto-chave:** Explicação direta com impacto prático ou na memória.
- **Trade-off:** Contraste explícito com [[Conceito Relacionado]].

## [Subtópico 2: Complexidade / Comparação / Comandos]

| Operação | [[Entidade A]] | [[Entidade B]] |
| :--- | :---: | :---: |
| Operação 1 | $O(1)$ | $O(n)$ |
```

#### Nota de Fonte (`02-Fontes/`)

```markdown
---
title: "Título Completo da Obra: Subtítulo"
author: Nome do Autor
type:
  - book
aliases:
  - Título Original
  - Título Curto
tags:
  - book
  - subdominio
  - dominio-macro
---
## Capítulos Processados
- **Cap 01 (Nome do Capítulo):** [[Conceito A]], [[Conceito B]], [[Conceito C]]
- **Cap 02 (Nome do Capítulo):** [[Conceito D]], [[Conceito E]]
```

#### Nota de Índice (`03-Indices/`)

```markdown
---
aliases:
  - alias-em-ingles
  - alias-em-portugues
  - SIGLA
tags:
  - subdominio
  - dominio-macro
---
## Categoria 1
- [[Conceito A]]: Síntese objetiva em uma linha (com complexidade ou propriedade-chave).
- [[Conceito B]]: Síntese objetiva em uma linha.

## Categoria 2
- [[Conceito C]]
- [[Conceito D]]
```

---

## 4. Padrão de Formatação (Markdown & Obsidian)

### Hierarquia de Cabeçalhos
- **Regra global — nunca usar `#` (H1) em nenhuma nota do cofre** (`00-Inbox/`, `01-Conceitos/`, `02-Fontes/` e `03-Indices/`). O nome do arquivo no Obsidian já cumpre o papel de H1.
- **Somente `##` (H2) em diante:** toda estruturação interna começa em `##` (H2), podendo evoluir livremente para `###` (H3) e níveis subsequentes conforme a nota cresce em profundidade e detalhamento.
- Em `01-Conceitos/`, a nota abre com o parágrafo de definição logo abaixo do frontmatter YAML e depois segue com `##` em diante. Em `02-Fontes/` e `03-Indices/`, a primeira seção `##` começa diretamente após o frontmatter YAML.

### Tipografia e Ênfase
- **Negrito (`**...**`):**
  - Nome do conceito na primeira frase da nota (exceto ferramentas CLI, que usam código inline).
  - Rótulos no início de itens de lista: `- **Leitura instantânea:** ...`.
  - Pontos críticos, invariantes e conclusões-chave no meio do texto (ex: `**contígua (lado a lado) na memória RAM**`, `**precisa estar ordenada**`, `**ignora constantes multiplicativas**`).
- **Itálico (`*...*`):**
  - Expansão de siglas e termos estrangeiros entre parênteses na primeira menção: `(*Arch User Repository*)`, `(*Linked List*)`, `(*shift*)`, `(*dependency hell*)`.
  - Codinomes de releases ou identificadores descritivos (ex: *bookworm*, *noble*).
- **Código inline (`` `...` ``):**
  - Binários e comandos CLI (`pacman`, `yay`, `sudo pacman -Syu`).
  - Flags (`-S`, `-R`, `-Q`, `-F`), variáveis e pseudocódigo (`baixo = 0`, `endereco_base + indice * tamanho_tipo`).
  - Caminhos de arquivo (`/etc/apt/keyrings`), extensões (`.deb`, `.h`), placeholders (`<pkg>`, `<query>`) e mensagens literais (`404 Not Found`, `PKGBUILD`).

### Notação Matemática (LaTeX / MathJax)
- Usar `$ ... $` inline para complexidades, fórmulas, expoentes, logaritmos e valores numéricos dentro de análises algorítmicas:
  - Complexidades: `$O(1)$`, `$O(\log n)$`, `$O(n)$`, `$O(n \log n)$`, `$O(n^2)$`, `$O(n!)$`.
  - Expressões: `$\log_2(1024) = 10$`, `$\frac{1}{2} \times n$`, `$3,85 \times 10^{215}$`.
- Padrão numérico em português: ponto como separador de milhar (`$1.024$`, `$16.384$`) e vírgula como separador decimal (`$3,85$`).

### Listas
- **Listas não ordenadas (`-`):** usadas para propriedades, trade-offs, complexidades, sufixos, comandos úteis e índices. Preferir o formato `- **Rótulo:** explicação.` ou `` - `comando`: explicação. ``.
- **Listas ordenadas (`1.`, `2.`, `3.`):** usadas para passos de algoritmo, demonstrações sequenciais, enums de flags principais e justificativas ordenadas. Subpassos são indentados com `-`.

### Tabelas
- Usadas para comparações matriciais de complexidade ou dicionários de comandos equivalentes.
- Alinhamento explícito obrigatório:
  - `:---` (esquerda) para rótulos, operações e colunas textuais descritivas.
  - `:---:` (centralizado) para complexidades, métricas numéricas e colunas comparativas de comandos.
- Usar travessão (`—`) quando uma célula não possui equivalente aplicável.

### Callouts do Obsidian
- Sintaxe compacta sem espaço entre `>` e o colchete:
  ```markdown
  >[!warning] Título curto do alerta
  >Corpo objetivo do aviso.
  ```
- Tipos adotados:
  - `>[!warning]`: pré-requisitos obrigatórios, armadilhas e alertas de segurança (ex: não executar `yay` com `sudo`, exigência de ordenação na Busca Binária).
  - `>[!tip]`: dicas complementares ou atalhos de comportamento.

### Wikilinks e Grafo de Conhecimento
- **Linkagem ativa:** referenciar qualquer entidade técnica relevante usando `[[Entidade]]`, inclusive em títulos de seção (`## Complexidade de Operações (vs. [[Lista Encadeada]])`) e células de tabela.
- **Aliases de exibição:** usar `[[Destino|Texto]]` apenas quando a concordância gramatical ou o contexto exigir (ex: `[[Arch Linux|Arch-Based]]`).
- **Links futuros (*unresolved links*) são intencionais:** o grafo está configurado com `hideUnresolved: false`. Criar links para entidades ainda não escritas (ex: `[[Quicksort]]`, `[[Debian]]`, `[[Go]]`) é uma prática encorajada para mapear lacunas e preparar conexões futuras.
- **Rastreabilidade interna sobre links externos:** em `01-Conceitos/`, priorizar `references` apontando para `02-Fontes/` em vez de espalhar URLs externas no corpo da nota.

---

## 5. Estilo de Escrita

O tom do cofre é **técnico, claro, didático e progressivo**.

1. **Abertura cirúrgica (Lead):** a primeira frase define o que a entidade é e qual problema resolve. Sem introduções genéricas (*"Neste texto vamos abordar..."*) e sem conclusões redundantes.
2. **Crescimento contínuo e leitura leve:** cada nota em `01-Conceitos/` é um documento vivo que acumula todo o conhecimento sobre aquela entidade ao longo do tempo. Não há restrição de tamanho — conforme o domínio amadurece, a nota pode ficar extensa, detalhada e até mais leve/explicativa, organizada com subtítulos (`##`, `###`), exemplos e diagramas.
3. **Idioma PT-BR com vocabulário técnico fiel:** escreve-se em português claro e natural, preservando termos em inglês amplamente consolidados na engenharia (`Array`, `Selection Sort`, `wrapper`, `checksum`, `shift`, `trade-offs`, `commit`, `branch`, `header`).
4. **Orientado a fundamentos ("por baixo dos panos"):** explica *por que* algo funciona assim — layout na RAM, aritmética de endereços, descarte de constantes na notação assintótica, modelo de permissões ao compilar pacotes.
5. **Pensamento comparativo (*Trade-offs first*):** conceitos são contextualizados em contraste com seus pares (`Array` vs. `Lista Encadeada`, `Busca Simples` vs. `Busca Binária`, `AUR` vs. `PPA`, `pacman` vs. `apt` vs. `omarchy`), explicitando quando usar e quando evitar.
6. **Âncoras numéricas concretas:** sempre que houver ganho ou custo de escala, ilustrar com ordens de grandeza palpáveis (ex: $10$ passos vs. $1.024$; $30$ passos vs. $1$ bilhão; operações para $n = 128$).
7. **Voz:** predominantemente impessoal e declarativa; segunda pessoa (*"você"*) admitida pontualmente em cenários operacionais e decisões práticas de CLI/uso.

---

## 6. Fluxo de Destilação (Ciclo de Vida)

```text
  Estudo / Prática
         │
         ▼
   [ 00-Inbox/ ]  (+ mídias em 04-Anexos/)
         │
         ├──► Criar/atualizar âncora ──► [ 02-Fontes/ ]
         │
         ├──► Extrair ou expandir 1 entidade/arquivo ──► [ 01-Conceitos/ ]
         │                                                       │
         └──► Registrar no mapa do domínio ◄─────────────────────┘
                        │
                        ▼
                 [ 03-Indices/ ]
```

### Passo a passo
1. **Capturar:** despejar anotações de estudo em `00-Inbox/` sem se preocupar com polimento (usando apenas `##` em diante para seções); salvar imagens/diagramas em `04-Anexos/`.
2. **Ancorar a fonte (se aplicável):** criar ou abrir a nota correspondente em `02-Fontes/` com `title`, `author`, `type`, `aliases` e `tags`.
3. **Destilar conceitos:** decompor o rascunho por entidade em `01-Conceitos/` (`1 assunto = 1 entidade = 1 arquivo`), criando um novo arquivo ou **expandindo um arquivo já existente** daquela entidade com novos tópicos, propriedades YAML, `references` (quando houver fonte), comparações e formatação padronizada.
4. **Atualizar os hubs:**
   - Adicionar os novos wikilinks na seção `## Capítulos Processados` (ou equivalente) em `02-Fontes/`.
   - Inserir os novos conceitos na seção correspondente em `03-Indices/` (criando um novo índice se o domínio ainda não existir).
5. **Esvaziar a fila:** após destilar integralmente uma nota da `00-Inbox/`, removê-la para manter a caixa de entrada enxuta.

### Checklist antes de concluir uma nota em `01-Conceitos/`
- [ ] A nota trata estritamente de **uma única entidade/conceito**?
- [ ] O nome do arquivo segue a convenção de nomenclatura (Title Case, sigla ou comando CLI)?
- [ ] O YAML contém `aliases` úteis e `tags` em inglês/minúsculas/`kebab-case`?
- [ ] Se derivada de uma fonte, `references` aponta para `02-Fontes/` com wikilink entre aspas duplas?
- [ ] Não há nenhum cabeçalho `#` (H1) no corpo da nota (apenas `##` em diante)?
- [ ] A primeira frase define diretamente o conceito com destaque adequado?
- [ ] Trade-offs, comparações e pré-requisitos relevantes estão explícitos e linkados via `[[wikilinks]]`?
- [ ] A nota foi registrada no respectivo índice em `03-Indices/` e (se aplicável) na fonte em `02-Fontes/`?

---

## 7. Configurações Relevantes do Cofre (`.obsidian/`)

As configurações versionadas em `.obsidian/` reforçam diretamente o fluxo acima:
- **Integridade de links:** `alwaysUpdateLinks: true` — renomear qualquer arquivo atualiza automaticamente todas as referências no cofre.
- **Higiene de mídia:** `deleteUnlinkedAttachments: "always"` — remove automaticamente anexos órfãos.
- **Formatação:** `tabSize: 2` — alinhado à indentação YAML e listas do repositório.
- **Lixeira local:** `trashOption: "local"` — exclusões são movidas para `.trash/` antes de remoção definitiva.
- **Grafo:** `hideUnresolved: false` e `showOrphans: true` — mantém visíveis tanto conceitos futuros ainda não escritos quanto notas que precisam ser integradas a índices ou conexões.

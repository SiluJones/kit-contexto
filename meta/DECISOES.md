# DECISÕES — Kit de Contexto Universal

> Decisões formais com racional. Não apague — marque como superada se mudar.

---

## D-001 — Página única HTML autossuficiente, sem build
**Data:** durante o planejamento inicial
**Contexto:** o kit precisava ser hospedável e usável sem dor.
**Opções consideradas:**
- A) HTML único com tudo embutido — sem build, sem deps
- B) Stack React + build (Vite/Next) com componentes
- C) Stack vanilla + módulos JS separados servidos por servidor

**Decisão:** A — HTML único.

**Racional:** o kit é distribuído via GitHub Pages (estático). Build complica o deploy, adiciona ciclo dev. Componentes ajudariam manutenção, mas o ganho não compensa o custo. Vanilla com `<script>` único é o caminho mais honesto para o problema.

**Consequências previstas:**
- O arquivo cresce (~285KB ao fim) — aceitável.
- Refator se complica — mas o kit é pequeno o suficiente.

**Status:** ativa.

---

## D-002 — 17 nichos profundos + 1 custom
**Data:** durante o planejamento de cobertura
**Contexto:** quantos nichos prontos colocar?
**Opções consideradas:**
- A) 4-6 nichos super profundos
- B) 30+ nichos rasos cobrindo tudo
- C) 17 profundos + 1 construtor real (Custom)

**Decisão:** C.

**Racional:** profundidade > cobertura. Mas extensibilidade real importa para quem está fora do catálogo. Custom não como vazio cinza, mas como construtor de verdade.

**Consequências previstas:**
- Mais trabalho de produção de templates.
- Risco de algum nicho ficar raso por descuido — mitigado por revisão sistemática.

**Status:** ativa.

---

## D-003 — Hero distinto por nicho (não só cor)
**Data:** durante design do produto
**Contexto:** como diferenciar nichos visualmente sem ser cosmético?
**Opções consideradas:**
- A) Mesma estrutura, só troca de cor da paleta
- B) Variação de fonte por grupo, mantendo layout
- C) Hero block visualmente distinto na Home de cada nicho

**Decisão:** C, somado a B.

**Racional:** o domínio do usuário tem que aparecer no produto. Terminal para Dev faz sentir o terminal. Postits para Brainstorm. Scroll medieval para RPG. Não é decoração — é tom comunicado pelo visual.

**Consequências previstas:**
- 18 layouts de hero para fazer e manter.
- Risco de inconsistência — mitigado pela base CSS comum.

**Status:** ativa.

---

## D-004 — Templates com nomes profissionais
**Data:** durante produção dos templates
**Contexto:** evitar nomes infantis tipo "DEFINITIVO" ou "APRIMORADO".
**Decisão:** o nome do template é a função do arquivo. Padronização: `MAIÚSCULAS.md`. Sem qualificadores opinativos.

**Racional:** o usuário é adulto, sabe o que está baixando. Nome do arquivo é informação, não autopromoção.

**Status:** ativa.

---

## D-005 — Custom como construtor real
**Data:** durante design do nicho Custom
**Contexto:** o Custom virou esqueleto vazio na primeira versão. Insuficiente.
**Decisão:** Custom é um construtor com formulário. Define identidade, arquivos, comportamentos, prompts. Salva preset em `localStorage`.

**Racional:** extensibilidade verdadeira. Quem está fora dos 17 prontos consegue ter algo seu, e voltar a usar.

**Consequências previstas:**
- Lógica extra significativa no JS.
- UI específica do Custom.

**Status:** ativa.

---

## D-006 — Meta-doc em `meta/` usando estrutura do nicho Brainstorm
**Data:** durante consolidação do projeto
**Contexto:** o próprio kit é projeto que precisa de contexto. Como documentar?
**Opções consideradas:**
- A) `README.md` extenso, sem mais nada
- B) Pasta `docs/` com convenção própria
- C) Pasta `meta/` usando exatamente a estrutura do nicho Brainstorm

**Decisão:** C.

**Racional:** auto-referência. O kit aplicado a si mesmo. Funciona como prova de fogo do nicho Brainstorm e como demonstração de uso real. Os arquivos `TEMA.md`, `IDEIAS.md`, `MAPA.md`, `FILTROS.md`, `STATUS.md`, `CHANGELOG.md`, `LOG-TEMPLATE.md` são exatamente os que o nicho Brainstorm gera.

**Status:** ativa.

---

## D-007 — A-F universais imutáveis; G+ específicos por nicho
**Data:** durante design dos prompts
**Contexto:** os prompts deveriam variar muito por nicho?
**Decisão:** o ciclo de vida de um projeto (setup, sessão início, sessão fim, migração) é o mesmo em todo domínio. A-F cobrem isso e ficam universais. Cada nicho adiciona G+ para tarefas só dele.

**Racional:** evita reescrever a mesma coisa 18 vezes e cria uma "gramática" comum que o usuário internaliza uma vez.

**Status:** ativa.

---

## D-008 — Theming via CSS variables + `[data-niche]`
**Data:** durante implementação
**Contexto:** como trocar cores e fontes sem repintar tudo via JS?
**Decisão:** definir todas as cores e famílias de fonte como CSS variables, sobrescritas por atributos `[data-niche]` e `[data-group]` no `<html>`.

**Racional:** o CSS faz o trabalho. JS só seta o atributo. Performance e simplicidade.

**Status:** ativa.

---

## D-009 — Persistência em `localStorage`, não servidor
**Data:** sempre foi assim
**Contexto:** onde guardar configurações e presets Custom?
**Decisão:** `localStorage`. Tudo local ao navegador do usuário.

**Racional:** privacidade absoluta + nenhuma infraestrutura. Custo zero, zero pegada.

**Consequências previstas:**
- Não funciona entre dispositivos sem exportar/importar manualmente.
- Não funciona em modo anônimo (limpa ao fechar).

**Status:** ativa. Possível complementar com export/import JSON em v1.1.

---

## D-010 — JSZip carregado via CDN sob demanda
**Data:** durante implementação dos downloads
**Contexto:** baixar templates em ZIP precisa de uma lib.
**Decisão:** JSZip carregado por CDN só quando o usuário clica em "baixar ZIP".

**Racional:** evita bloat na primeira carga. 99% dos usos do kit não precisam de ZIP.

**Status:** ativa.

---

## D-011 — Nichos sensíveis (saúde, finanças, direito) ficam fora dos prontos
**Data:** durante decisão de cobertura
**Contexto:** valeria ter um nicho de saúde, direito, finanças?
**Decisão:** não, ficam só como caso de uso de Custom.

**Racional:** são territórios onde um template pronto pode ser confundido com conselho profissional. Prefiro não dar essa abertura. Quem precisa, constrói no Custom — assume autoria, assume responsabilidade.

**Status:** ativa.

---

## D-012 — Fundação transversal: 6 princípios, CLAUDE.md separado, higiene

**Data:** 2026-05-29
**Status:** aceita
**Autor:** ambos (feedback do Claude/GameDataHub + análise + decisão do usuário)

### Contexto
Após o MVP (17 nichos + custom), o usuário trouxe o feedback massivo que um Claude gerou no projeto real GameDataHub (nicho dev), além de materiais de uso real do nicho design/cliente. Esse feedback evoluiu a estrutura de docs muito além do que o kit gerava: CLAUDE.md separado, princípio anti-concordância-automática, princípio anti-desperdício-de-tokens, filosofia rolante/estável/cresce com regras de higiene, ROADMAP/GLOSSARY, tabela de gatilhos. Decidiu-se refinar área por área; esta é a Etapa 0 (fundação), antes de tocar nos nichos um a um.

### Decisão
1. **Adicionar 2 princípios universais** (total 6): «Analisa antes de aceitar» e «Não desperdiça tokens». Os 4 antigos (direto, incerteza, trade-offs, captura ideias) foram reescritos mais ricos.
2. **Gerar CLAUDE.md** como artefato separado das Instruções, com toggle de abas. Instruções = núcleo denso (lido em todo turno); CLAUDE.md = comportamento completo (subido como arquivo, versionável).
3. **Estruturas base**: filosofia de arquivos, regras de higiene, tabela de gatilhos — refletidas no CLAUDE.md gerado.

### Alternativas consideradas
- **Fundir CLAUDE.md dentro das Instruções (como era)** — rejeitada: as Instruções são lidas em toda mensagem e ficariam caras/longas; e não dá para versionar/atualizar separado.
- **Só CLAUDE.md, sem núcleo nas Instruções** — rejeitada: arquivos de conhecimento podem não ser carregados (RAG sob demanda); o essencial precisa estar nas Instruções, que são garantidamente lidas.
- **Refazer todos os 18 nichos de uma vez** — rejeitada (foi justamente o erro de método do MVP): espalha o esforço, deixa cada nicho raso. Fundação primeiro, depois um nicho por vez.

### Fundamento técnico (pesquisa 2026-05-29)
- Instruções do Projeto: lidas inteiras em cada mensagem ("função em hot loop"); cada token custa para sempre.
- Project knowledge: usa RAG nos planos pagos (só carrega o relevante quando o acervo é grande); quando pequeno, entra inteiro. Fácil de atualizar trocando o arquivo.
- Conclusão: especialização, não redundância. Núcleo curto + arquivo completo.

### Definição de arquivos: núcleo + opcionais
- **Núcleo (7):** CLAUDE, CONTEXT, STATUS, DECISIONS, IDEAS, CHANGELOG, LOG-TEMPLATE.
- **Opcionais (3):** ROADMAP, GLOSSARY, BRIEFING/continuidade.
- Por que não fundir ROADMAP no IDEAS/STATUS: horizontes temporais distintos (plano em fases vs. brainstorm vs. agora). Fundir recriaria fonte-de-verdade-dupla. Mas como nem todo projeto tem plano de fases, ROADMAP é opcional.

### Consequências
- **Positivas:** comportamento do kit alinhado ao que o uso real provou ser superior; Instruções mais baratas em token; CLAUDE.md versionável; base pronta para aprofundar cada nicho.
- **Negativas:** mais um artefato para o usuário subir (CLAUDE.md) — mitigado: ctrl+A + arrastar resolve, e o ganho de qualidade compensa.
- **Pendente:** os nichos individuais ainda não foram aprofundados (Etapa 1+). A fundação prepara a máquina; cada nicho será lapidado com seu próprio feedback ao longo do tempo.

### Sobre a feature nativa "Pesquisar e referenciar conversas" (Opus 4.8)
Levantado pelo usuário. Análise: a feature cobre continuidade entre conversas suas, mas é sob demanda e por busca, limitada ao projeto, não persistente. O kit mantém diferencial em: portabilidade (arquivos vão pro Git, funcionam em qualquer conta), estrutura deliberada (decisão/ideia/estado separados), e controle do que entra no contexto. Vale continuar lapidando.

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

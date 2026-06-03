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

---

## D-013 — Refinamento área por área concluído: os 16 nichos no padrão de ouro

**Data:** 2026-05-30 · **Status:** marco atingido

### A decisão / o marco
Encerrar a fase de refinamento nicho por nicho. Os 16 nichos de conteúdo (8 sérios + 8 criativos) foram reconstruídos no padrão de ouro, cada um a partir de pesquisa de domínio própria (com citações), não só do feedback ou de conversas anteriores.

### Como foi conduzido
Ritual consistente por nicho: estudar o nicho atual + pesquisa web aprofundada do domínio (2-4 buscas) → projetar (núcleo enxuto + opcionais, behaviors derivados da pesquisa, prompts G-L das tarefas reais) → construir isolado em /home/claude → validar (node --check + balanceamento de tags + jsdom 17/17) → publicar + CHANGELOG/STATUS → commit no formato CMD Windows. Nunca publicado sem 17/17 nichos e 0 erros.

### Padrões que emergiram
- **Sérios:** ênfase em decisão/risco/premissa/método (dev, business, product, research...) com o arquivo-âncora guardando o "porquê".
- **Criativos:** ênfase em "explora/critica/orienta — o criador executa/decide". E, num subgrupo, o reconhecimento honesto dos limites do assistente como traço de design: music ("não ouço áudio"), cuisine ("não cozinho nem provo"), pixel/animation/comics ("não desenho/animo"). O assistente dá a leitura técnica; o sentido humano (ouvido, paladar, olho) decide.
- **brainstorm (o fechamento):** o nicho do próprio kit. Behavior-assinatura "espelho e contraponto, não eco" (anti-sycophancy) — fechando o sentido de toda a ferramenta: pensar COM a IA, não deixar a IA pensar por você.

### O que fica
- Funcionalidades transversais acumuladas: afixo nos downloads, seletor de SO, fix dos selects do topbar, fundação de 9 princípios, CLAUDE.md separado das Instruções.
- Pendências de consolidação (não-nicho): revisar README/PLANNING, revisar qualidade das Instruções geradas, i-N3 parte A (canal de atualização), i-N2 (dados pessoais), reagrupar narrative.
- custom permanece como gerador (sem aprofundamento, por design).

### Negativas / a vigiar
- Cada nicho foi lapidado com pesquisa, mas ainda não com uso real extenso. O refino verdadeiro continua com o feedback de quem usar cada um (como já previsto para game). Padrão de ouro é piso, não teto.

---

## D-014 — Arquitetura do Custom Inteligente: composição assistida, não fusão automática

**Data:** 2026-06-02 · **Status:** aprovada (a implementar)

### A decisão
Adicionar um SEGUNDO nicho de construção — o **Custom Inteligente** — mantendo o custom atual como **"Blank"** (página em branco, poder total). O Custom Inteligente compõe um nicho novo a partir da SELEÇÃO de nichos existentes, por **concatenação assistida e revisável** — NÃO por fusão automática opaca.

### Por que (o racional)
- O usuário testou o custom atual e o achou intimidante: é um formulário em branco, sem nenhum mecanismo de herdar templates/behaviors de outros nichos. Ele queria "apertar em mais de um nicho e as características se incorporarem".
- Pesquisa do padrão (presets/composição) e a lição do GitHub spec-kit: **"full replacement over inheritance — herança é complexa e frágil; composição deve ser explícita e revisável"**. Arrays concatenam (não se fundem mágico); conflitos precisam de detecção.
- Fusão automática geraria "Frankenstein" incoerente (4 STATUS.md, behaviors contraditórios). O usuário concordou em NÃO fazer o automático perigoso.

### Como (a estrutura aprovada)
1. **2 nichos de construção, não 3** (mais limpo): Custom (Blank) + Custom Inteligente.
2. Custom Inteligente abre com chips dos 16 nichos. Marcar importa o material (concatena contextFiles + behaviors + promptsExtra), editável.
3. **Dedup visível** dos arquivos repetidos (STATUS/LOG que todos têm) e behaviors parecidos.
4. **Sub-painel = granularidade, não mecânica nova:** "importar nicho inteiro" vs. "escolher peças item a item". Botão "escolher peças" por nicho. NÃO é uma terceira opção.
5. **Checagem de conflito (spec-kit-inspired):** avisar sobre behaviors contraditórios; sinalizar, não bloquear.
6. Cai no motor existente (mergeCustom + presets em localStorage).

### Alternativas consideradas
- **Fusão automática** — rejeitada (risco de Frankenstein; o usuário concordou).
- **Terceira opção separada para o sub-painel** — rejeitada (é só granularidade do mesmo fluxo; botão a mais bastaria).

### Risco / como saberemos
Baixo-médio. UI nova sobre motor existente. Fazer por partes (importação+dedup → sub-painel → checagem de conflito), validando jsdom 17/17 a cada passo. Sinal de sucesso: usuário consegue montar um nicho "dev + pixel" (caso real dele: ferramentas de Aseprite) sem recriar tudo do zero.

### Contexto de uso que motivou (do usuário)
Ele está fazendo ferramentas reais que se encaixam em **dev** como base, algumas com tempero de outro domínio: plugin de Figma (dev), assets Unity/Godot (dev, ou dev+game), plugins/extensão/script de Aseprite para pixel art em massa/procedural (dev + pixel — o caso perfeito para o Custom Inteligente), geração procedural de molduras/bordas (dev + pixel/design).

---

## D-015 — Protocolo de transferência entre conversas (contexto vs. RAG) — transversal

**Data:** 2026-06-03 · **Status:** aceita e implementada (v1.21.0)

### Contexto
O usuário levantou — com razão — uma lacuna grave de conhecimento que afetava o uso real do kit (e de qualquer projeto dele no Claude.ai): **não estava claro o que acontece com os arquivos quando se transfere um projeto para uma conversa nova.** A confusão concreta:
- Ele confiou que "o GitHub / os arquivos do Projeto" dariam continuidade 100% e que o assistente poderia editar o código a partir deles. Em projetos grandes isso NÃO é verdade.
- Risco real: alguns projetos dele podem ter sido corrompidos ao transferir confiando cegamente nos arquivos do Projeto em modo de busca (o assistente teria editado a partir de fragmentos).

### Fundamento técnico (pesquisa 2026-06-03, docs oficiais + práticas profissionais)
- **Conhecimento do Projeto tem dois modos automáticos** (Claude Help Center): *in-context* quando o total cabe na janela (arquivos INTEIROS, editáveis com fidelidade) e *RAG / "Modo de pesquisa"* quando o total se aproxima do limite (só FRAGMENTOS recuperados por relevância; capacidade expande ~10x). Há indicador visível na tela do Projeto. Volta a in-context se o conteúdo encolher.
- **Sincronização do GitHub é manual** ("Sync now"), só puxa nome+conteúdo do branch (sem histórico/PRs), e há relatos de quebrar silenciosamente — logo, o que está no GitHub pode estar atrasado em relação à cópia local; upload direto é mais fresco.
- **Anexo de conversa** é por sessão (não passa para a próxima), ocupa contexto a cada turno (custa token) e dá fidelidade total. Um arquivo gerado pelo próprio assistente dentro da conversa tem a mesma fidelidade pelo mesmo motivo (entra no histórico). Por isso a conversa original de desenvolvimento mantinha o index fiel sem anexar — ele nasceu ali.
- **Contexto não passa entre conversas a menos que esteja no conhecimento do Projeto** — continuidade de verdade exige o Projeto; o anexo é fidelidade na sessão ativa.
- **Enquadramento profissional** (context engineering 2025/26): a janela de contexto é como RAM (rápida, finita, zerada por sessão); arquivos externos são o disco (grandes, mas exigem recuperação). O método robusto de handoff é a "sumarização iterativa ancorada" (um doc de estado — intenção/decisões/ações/próximos passos — sempre atualizado) — que é o papel do nosso STATUS.

### Decisão
Adicionar um protocolo **transversal** (no `UPDATE_PROTOCOL`, portanto no CLAUDE.md de TODOS os nichos) e ensinar o usuário na própria UI:
1. **Seção "Transferência entre conversas"** no CLAUDE.md gerado, com: os dois modos; **regra dura anti-arquivo-falso** (nunca reconstruir a partir de fragmentos — pedir o anexo); onde colocar cada arquivo (leve→Projeto, preferindo upload direto; pesado/em-edição→anexo); comportamento do anexo; **handoff ao final** (dizer arquivo-por-arquivo onde colocar + montar um PROMPT DE INÍCIO); verificação de integridade.
2. **Seção "Contexto vs. RAG — e onde colocar cada arquivo"** na view *Tokens & Fluxos* (a parte que ensina o usuário), com tabela dos dois modos, regra de ouro e o enquadramento RAM/disco.

### Alternativas consideradas
- **Não documentar (deixar o usuário descobrir)** — rejeitada: foi exatamente a lacuna que pôs projetos em risco.
- **Mecanismo automático de "detectar modo e agir"** — fora de escopo do kit (o kit gera texto/instrução; quem decide o modo é o tamanho do conhecimento). Resolvido como regra de comportamento + ensino, não como código que checa o ambiente.

### Consequências
- Todos os nichos passam a instruir o assistente a fazer o handoff e a recusar reconstrução por fragmentos. Vale especialmente para dev/game (arquivos grandes).
- O usuário tem agora um critério visível (o rótulo "Modo de pesquisa") e uma regra de ouro.
- **A vigiar:** o usuário vai auditar projetos transferidos no passado para detectar corrupção por edição-via-fragmentos.

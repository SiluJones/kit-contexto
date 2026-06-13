# STATUS — Kit de Contexto Universal — 2026-06-12

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).
> Versão atual: **v1.29.0**. Índice ~559 KB / 8176 linhas. Teste: **17/17 nichos, 0 erros JS** (build por nicho via `normNiche`) + integridade dos chips (FIX-004) + **6 checagens D-022/D-018 + 10 checagens v1.29.0 (IDEAS universal, writes_prose, builds_game, ROTEIRO, anti-contradição)** + suíte de fluxos.

> **Mudanças nesta revisão (v1.29.0):** sessão da ideia-260612 + guia do escritor + pesquisa. **IDEAS universal** (injeção via `normNiche` + regra "cria na primeira necessidade") resolve o "faltou o IDEIAS.md" dos pilotos; **narrative agora ESCREVE sob direção** (convention reescrita, behavior `writes_prose`, kishōtenketsu, prompt J); **game agora CRIA** (`builds_game` + ROTEIRO.md com AGUARDANDO DESIGN). Tudo em **D-023**; harness +10 checagens + anti-teste (15 reprovações sem a injeção). i-N24 ganhou o desenho do HUB (3 seções); i-N25 (música) capturada. O "PRÓXIMO TRABALHO" foi reordenado. Nada perdido. (Notas anteriores abaixo.)

> **Mudanças na revisão (v1.28.0):** os itens 1 e 2 do "PRÓXIMO TRABALHO" foram **executados** — as 5 diretrizes do lote **D-022 embutidas** na ferramenta (i-N18 manifesto auto-detectado; i-N19 refino de P8; i-N20 commit 3 linhas listando; i-N21 gatilho «Feedback para o Kit»; i-N22 válvula) e a **orientação mount/RAG corrigida** no CLAUDE.md gerado + tela "Tokens & Fluxos" (D-018). Harness ganhou 6 checagens de conteúdo + anti-teste (34 reprovações na cópia sem o lote). O que saiu daqui está no CHANGELOG v1.28.0, em D-022/D-018 e nos títulos de i-N18..22 (✅ EMBUTIDA). Nada perdido. (Notas anteriores preservadas abaixo.)

> **Mudanças nesta revisão (v1.27.1):** consertado o bug dos chips de Cliente/Narrativa (não selecionáveis) — ver CHANGELOG v1.27.1 e **FIX-004**. O harness ganhou checagem de chips. Cinco ideias novas dos primeiros testes reais foram capturadas (i-N18 a i-N22) e o "PRÓXIMO TRABALHO" foi reordenado. **Segunda leva do mesmo dia (só docs, sem código):** regra do **manifesto FlatDrop** adotada para o nosso projeto (CLAUDE.md — consultar `_MANIFEST.md`, entregar pelo nome real); i-N18/i-N21/i-N22 **alinhadas com o usuário** (manifesto esclarecido; fluxo do feedback desenhado; texto da válvula de desvio proposto); capturadas **i-N23** (4 melhorias do nicho Pixel vindas do piloto) e **i-N24** (protocolo multi-projeto, 4 frentes do mesmo jogo). **Terceira leva (validações do usuário):** FlatDrop definido como **não-padrão** (detecção automática via `_MANIFEST.md`; filtragem anotada); **i-N19, i-N20 e i-N22 validadas** e **i-N21 fechada com escopo ampliado** (desvio estrutural = feedback; autonomia do piloto; triagem em 3 destinos) — lote congelado em **D-022**; **passada de código liberada**. Nada perdido: tudo em IDEIAS/CLAUDE/DECISOES/ROADMAP.

> **Mudanças na revisão anterior (v1.27.0):** os itens 1 e 2 do "PRÓXIMO TRABALHO" (propagar P12 à ferramenta; decidir o princípio de pesquisa/refutação) foram **feitos** — P12 virou o 12º item de `BEHAVIORS_BASE` (D-020) e a i-N17 virou o 13º, **P13** (D-021). "Onde está no código" ganhou a nota de `BEHAVIORS_BASE` 11→13.

## Fase atual
🏁 **Custom unificado — composição + construção numa só tela, e fluxo de reuso completo.** No ar e validado:
- **Um card de construção (`custom`)** com a seção "Compor a partir de nichos prontos" (chips dos 16 nichos) **no topo** e o "Custom Builder" logo abaixo. Importar concatena → **deduplica de forma visível** → **sinaliza conflitos** (seletor de versão por arquivo) → preenche o builder **na mesma tela**. Acabou o vai-e-volta entre dois nichos de construção. (D-019, supersede D-014.)
- **Granularidade por nicho:** cada nicho marcado tem "escolher peças" (checkboxes de arquivos/comportamentos/prompts; padrão = tudo). `composeFromNiches(niches, sel)` respeita a seleção.
- **Atalho "Nichos salvos" na barra superior:** aparece quando há presets; selecionar **ativa** o nicho salvo de qualquer lugar.
- **Fluxo de preset:** Ativar (nicho fica vivo e salvo), barra "Editar / trocar nicho", carregar/excluir. **Corpo dos prompts persiste** após Ativar (FIX-003).

São **17 nichos**: 16 de conteúdo + **1 construtor** (`custom`).

## 🎯 PRÓXIMO TRABALHO (decidir/fazer)
1. **HUB multi-projeto (i-N24): APRESENTADO — aguarda decisão do usuário.** Template `HUB.md` entregue (3 seções + diretrizes D1–D5 + apêndice com o gatilho p/ os CLAUDE.md). Recomendação: usar JÁ via gatilho (zero código; pilotos validam) e embutir o **switch "grupo de projetos"** na ferramenta numa próxima passada. **Falta o usuário:** aprovar/ajustar o template + dizer quando embutir o switch.
2. **Lote de feedback dos pilotos (i-N23): ⏸ PAUSADO por decisão do usuário (06-12)** — não fecha por ora; itens registrados em IDEIAS; aplicar quando ele sinalizar.
3. **Estender o padrão "desenvolve" (D-023)** a HQ/RPG/animação — **confirmado pelo usuário: só quando ele iniciar projetos nessas áreas.** i-N25 (música) idem.
4. **Cosméticos — analisados (06-12):** **MAPA.md corrigido e entregue** (16+1). **Reagrupar `narrative`:** NÃO é 1 linha cega — os `group:` visíveis são de tema/fonte; mapear o campo real de agrupamento dos cards e mudar na MESMA passada do switch do HUB (1 validação só). **README/PLANNING:** reescrever DEPOIS da decisão do HUB (o pitch do produto mudou com o "kit desenvolve" — reescrever antes geraria retrabalho). **Qualidade das Instruções:** com 13 princípios + extras de nicho, o risco agora é TAMANHO (instruções são lidas em toda mensagem); recomendação: adicionar ao harness um teto de caracteres por nicho e medir antes de cortar — entra na próxima passada de código.

✅ **Concluído nesta sessão (v1.29.0):** IDEAS universal + "cria na primeira necessidade"; narrative escreve sob direção (kishōtenketsu incluso); game cria (builds_game + ROTEIRO.md). D-023. Harness +10 checagens + anti-teste. 17/17, 0 erros.

✅ **Concluído antes (v1.28.0 / v1.27.x):** lote D-022 embutido + D-018 corrigida; FIX-004; P12/P13 (D-020/D-021).

## 🧭 Decisões maiores em avaliação (ver ROADMAP / IDEIAS)
- **Refator modular do kit (i-N13):** migrar dados de nicho para JSON separados + núcleo central, vs. manter o HTML único. Prós (edição/auditoria por nicho, criar nicho mais fácil) × contras (perde o "1 arquivo via `file://` sem build"; precisa loader/embed). **Não mexer sem decisão.**
- **Nicho/ferramenta de guias/tutoriais/wikis (i-N14):** aprender ferramentas (Aseprite/Unity/Godot/Unreal/Excel/Word/Sheets/linguagens), platinar jogos, com pesquisa e organização padronizada. Pode ser nicho no kit OU ferramenta separada. Conecta a "Educação" (NICHOS-CANDIDATOS, nº1).
- **Ferramenta de auto-aplicação de patches (i-N15) + entrega por diff (i-N16):** a IA gera "arquivos de atualização" num formato estruturado (estilo apply_patch/AutoCoder) e uma ferramenta local os aplica — menos trabalho manual e, se a IA emitir **diffs** em vez de arquivos inteiros, **menos output tokens** (relevante: a sessão anterior consumiu 100% da janela). Switch on/off "auto" em todos os nichos. **Avaliar viabilidade/segurança.**

## 🎯 Outras pendências (sem urgência)
1. **MAPA.md** cita "17 prontos" — atualizar para refletir os 16 de conteúdo + 1 construtor (cosmético).
2. **Reagrupar narrative** (cosmético): hoje `group:"literary"`; é criativo. Só tema visual.
3. **Revisar README/PLANNING** — pendente de revisão geral pós-MVP.
4. **Revisar a qualidade das Instruções geradas** — confirmar polimento/eficiência.
5. **Nichos novos (FUTURO, adiados de propósito):** ver `NICHOS-CANDIDATOS.md` (Educação nº1, depois Desenvolvimento Pessoal/Journaling, Jurídico/Podcast/Tradução).
6. **spec-kit para dev/game (FUTURO):** quando o usuário tiver mais feedback de uso.

## 🔎 Mount (D-018) — lembrete operacional
O conector do GitHub alimenta **só o RAG/Conhecimento do Projeto** (busca, com subpastas); **não** popula o mount `/mnt/project/`. **Só o upload direto** popula o mount, e **achatado** (sem subpastas; nomes iguais colidem). Para eu ler/editar pelo mount, subir os arquivos DIRETO no Projeto + ligar a ferramenta de código. **`localStorage` é por origem:** presets do site publicado NÃO aparecem no arquivo local (`file://`) e vice-versa.
**FlatDrop / `_MANIFEST.md`:** **NÃO é padrão** — detectar pela **presença** do `_MANIFEST.md` no mount. Se existe: consultar (caminho original → nome plano; sufixo `__pasta` = colisão), **entregar pelo nome real** e usar para entender a estrutura. Se não existe: fluxo normal, **sem travar**. O FlatDrop **filtra** o upload (tipos não aceitos como imagens; ignorados fixos `node_modules`/`venv`/`.git`; `.gitignore` opcional) — ausência pode ser deliberada, não erro. Regra completa no CLAUDE.md; decisão em D-022.

## 🧪 Validação (regra dura: NUNCA publicar sem 17/17 e 0 erros)
Harness jsdom **boot limpo por nicho** (o ambiente reseta entre sessões — recriar os testes a cada sessão). No scratchpad `/home/claude/kit/`:
- `validate.js` — **17/17** nichos (buildInstr + buildClaudeMd + P12/P13 + sem `undefined`) **+ integridade dos chips** + round-trip seleção→saída (FIX-004) **+ 6 checagens de conteúdo do lote v1.28.0** (manifesto, feedback, válvula, P8 refinado, commit 3 linhas, mount/RAG). Anti-testes provam que reprova código com bug/sem lote.
- `validate-switch.js` — transições construtor↔normal + **coexistência** (no `custom`, chips `#sc-chips` E builder `#cf-save`/`#cf-load` juntos). Guarda o bug A / re-entrância.
- `validate-compose.js` — Fase 1.2 (compor dev+pixel; usa `setNiche("custom")`).
- `validate-conflict.js` — Fase 1.3 (conflito + seletor; `setNiche("custom")`).
- `validate-reuse.js` — fluxo de preset (ativar/editar-trocar/carregar/excluir).
- `t-prompt.js` — corpos de prompt preservados após Ativar (view + localStorage; CLAUDE.md só título, por design).
- `t-shortcut.js` — atalho "Nichos salvos" (ausente sem presets; aparece e ativa de qualquer lugar).
- `t-granular.js` — granularidade (desmarcar peça → some do import; "marcar todas" reinclui).
Mais `node --check` no `<script>` e balanceamento de tags. **Atenção:** ao remover/renomear coisas no código, atualizar os testes (foi o que aconteceu ao remover `customSmart`: trocar `setNiche("customSmart")` → `setNiche("custom")`).

## 🗺 Onde está no código (v1.29.0; números aproximados, mudam ao editar)
- **v1.29.0 (D-023):** `UNIVERSAL_IDEAS_TPL` é constante de fundação (logo antes de `HYGIENE_RULES`); a **injeção** acontece em `normNiche` (`_files.some(/^IDE(A|IA)S\.md$/i)`); a regra "cria na primeira necessidade" está no `buildClaudeMd` logo após a tabela de gatilhos. Narrative: convention[0] reescrita + convention kishōtenketsu + behavior `writes_prose` (após `protect_voice`) + prompt `id:"J"`. Game: behavior `builds_game` (após `creator_decides`), template `ROTEIRO.md` (entre NIVEIS e LOG-TEMPLATE), output `key:"roteiro"`, trigger novo, convention "também CONSTRÓI".
- **Lote D-022 (v1.28.0):** i-N19 = frase final na def de `check_before_ask` (P8, BEHAVIORS_BASE ~845) + bullet na seção «Verifica antes de pedir um arquivo» do buildClaudeMd (~7145); i-N22 = 5ª regra em `HYGIENE_RULES` (~868); i-N21 = 5ª linha em `TRIGGERS_BASE` (~877); i-N20 = `commitIntro` (3 linhas, incondicional) e `commitNota` (só sintaxe por SO); i-N18 = item novo (penúltimo) em `handoffComo`. **D-018:** 3 itens do `handoffComo` reescritos + 2 callouts da tela "Tokens & Fluxos" (~760, ~766).
- **`normBuilderSection`** (≈linha 6200) converte `builderSection.groups → items`. **FIX-004:** `opts: g.items.map(it => Array.isArray(it) ? it : [it,it])` — aceita item **string** OU **par `[código,rótulo]`**. Os chips renderizam em `renderBuilderSection` (≈6788) e a escolha entra na saída via finder `o[0]===val` (≈6924). Só `client` e `narrative` usam o formato par.
- **`BEHAVIORS_BASE` com 13 itens**: +`shrink_hygiene` (P12) +`research_refute` (P13) no fim. Renderizam em `buildInstr` (curto, via `shortDef`) e `buildClaudeMd` (`### N.` + def longa). Behaviors de nicho entram depois, via `normBehaviors`. Sem count hardcoded.
- `getCurrentNiche` usa `raw.isBuilder` (genérico). Não há mais `customSmart`.
- `NICHES.custom` (único construtor) — `isBuilder:true`; cardDesc/cardTags mencionam composição.
- `renderTopbar` — injeta o atalho `savedNichesShortcutHTML()` + `wireSavedNichesShortcut()`.
- `composerSectionHTML` / `wireComposer` / `refreshComposer` — a seção de composição (chips + granularidade) no topo do `renderCustomForm`.
- `composeFromNiches(niches, sel)` — concatena + dedup/conflito; `sel` filtra peças (granularidade).
- `renderImportReport` — banner (idênticos × conflitos + seletor de versão).
- `renderCustomForm` — construtor unificado (composição + builder); re-entrante; `_presetName` persiste; `#cf-apply` sempre persiste.
- `injectActiveCustomBar` — barra "Usando o nicho: X · Editar/trocar" quando há preset ativo (gate só `custom`).
- `toPreset` (body → STRING, FIX-003) / `fromPreset` / `mergeCustom`.
- `CONTROLS_SKELETON` + `captureControlsSkeleton`/`restoreControlsSkeleton` (FIX-001).
- LS keys: `LS_PRESETS="kit-custom-presets"`, `LS_PRESET_CURR="kit-custom-current"`.

## 🗂 Convenções
- pt-BR em tudo, inclusive comentários de código. Nomes de template profissionais.
- Entrega: arquivos completos em `outputs/meta`; o usuário organiza no repo.
- Commit ao final: comando completo p/ CMD Windows (UMA linha, `-m` repetido), pronto para colar. Mensagem **sem acentos** (CMD corrompe acentos em `-m`).
- Usuário no CMD do Windows (`C:\Users\alexk\Arquiteturas\kit-contexto`). Repo: `index.html` na raiz, `.md` em `meta\`.

## 💬 Última sessão (2026-06-12 — v1.29.0)
Sessão da **ideia-260612** + leitura do GUIA_COMPLETO_ESCRITOR_NOVEL (+ versão txt) + pesquisa P13 (kishōtenketsu; práticas e armadilhas de escrita assistida por IA — voz genérica vem de contexto genérico; uso passivo homogeneíza, colaborativo fortalece). Três frentes, tudo em **D-023**:
- **IDEAS universal:** o "faltou o IDEIAS.md" dos pilotos morreu — template injetado via `normNiche` em 15 nichos (dev/brainstorm mantêm os seus), já com a seção «Feedback para o Kit»; e o CLAUDE.md gerado agora manda **criar na primeira necessidade** qualquer doc referenciado que não exista.
- **Narrative escreve:** convention da voz reescrita (escreve **sob direção**, rascunho ancorado em VOZ.md), behavior `writes_prose` (opções em cena crítica, [HIPÓTESE] no inventado, vigia drift), kishōtenketsu como repertório fractal para LN/WN, prompt J com o ritmo serial (hook → beat → gancho).
- **Game cria:** behavior `builds_game` (designer+dev+programador; protótipo antes de sistema) e **ROTEIRO.md** — a casa da narrativa cena a cena que o piloto pediu, com o estado **AGUARDANDO DESIGN** (ponte para i-N24).
- **Capturado sem codar:** i-N24 ganhou o desenho do HUB de 3 seções (refinar e APRESENTAR antes de codar — pedido do usuário); i-N25 (música) registrada para depois.
**Próximo de fato:** decisões do usuário sobre o item 1 (HUB: template ok? quando embutir o switch?) — aí vem a passada de código única: switch do HUB + regroup narrative + teto de instruções no harness.
.
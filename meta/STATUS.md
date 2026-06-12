# STATUS — Kit de Contexto Universal — 2026-06-11

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).
> Versão atual: **v1.27.1**. Índice ~548 KB / 8097 linhas. Teste: **17/17 nichos, 0 erros JS** (build por nicho via `normNiche`) + **integridade dos chips de todos os nichos** (FIX-004) + suíte de fluxos.

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
1. **Redigir e embutir as diretrizes novas no CLAUDE.md gerado** (numa passada só, com re-validação 17/17): **(i-N18)** manifesto de achatamento **condicional/auto-detectado** — *"se houver `_MANIFEST.md`, use-o (sufixo `__pasta` = colisão; entregue pelo nome real); se não houver, siga normal sem travar"* (já vale para o nosso projeto); **(i-N19)** verificar o estado real antes de repetir pendência de STATUS velho (refino de P8 + nota no `UPDATE_PROTOCOL`); **(i-N20)** commit em 3 linhas, **listando arquivos** (`.` a critério quando pequeno/limpo); **(i-N21)** gatilho de feedback → seção «Feedback para o Kit» no IDEAS do piloto, **incluindo desvios estruturais**; **(i-N22)** válvula de desvio registrado. **✅ Lote todo validado pelo usuário (2026-06-11) — ver D-022. Passada de código LIBERADA.**
2. **Corrigir a orientação mount/RAG/anexo GERADA pelo kit (à luz de D-018):** o CLAUDE.md / tela "Tokens & Fluxos" ainda diz "tudo no Projeto + ferramenta de código → mount", impreciso para projetos conectados via GitHub. Muda conteúdo em TODOS os nichos → re-validação 17/17. **Tarefa de código.** (Pode ir junto com o item 1.)
3. **Fechar o lote de feedback dos pilotos** (i-N23 já tem 4 itens do pixel; mais por vir das outras frentes) e **avaliar a i-N24** (multi-projeto, 4 frentes) quando a dor concreta aparecer. Sem código até o lote fechar.

✅ **Concluído nesta sessão (v1.27.1):** conserto dos chips de Cliente/Narrativa (FIX-004) + teste de regressão de chips no harness; captura e refino das 5 ideias novas (i-N18 a i-N22) com lastro de pesquisa. Validado 17/17, 0 erros.

✅ **Concluído antes (v1.27.0):** P12 propagado à ferramenta (12º de `BEHAVIORS_BASE`, D-020); i-N17 decidida → **P13** (13º, D-021).

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
- `validate.js` — **17/17** nichos (buildInstr + buildClaudeMd + P12/P13 + sem `undefined`) **+ integridade dos chips do `builderSection`** (nenhum opt `[array,array]`) **+ round-trip seleção→saída** (FIX-004). Provado que reprova o código com o bug.
- `validate-switch.js` — transições construtor↔normal + **coexistência** (no `custom`, chips `#sc-chips` E builder `#cf-save`/`#cf-load` juntos). Guarda o bug A / re-entrância.
- `validate-compose.js` — Fase 1.2 (compor dev+pixel; usa `setNiche("custom")`).
- `validate-conflict.js` — Fase 1.3 (conflito + seletor; `setNiche("custom")`).
- `validate-reuse.js` — fluxo de preset (ativar/editar-trocar/carregar/excluir).
- `t-prompt.js` — corpos de prompt preservados após Ativar (view + localStorage; CLAUDE.md só título, por design).
- `t-shortcut.js` — atalho "Nichos salvos" (ausente sem presets; aparece e ativa de qualquer lugar).
- `t-granular.js` — granularidade (desmarcar peça → some do import; "marcar todas" reinclui).
Mais `node --check` no `<script>` e balanceamento de tags. **Atenção:** ao remover/renomear coisas no código, atualizar os testes (foi o que aconteceu ao remover `customSmart`: trocar `setNiche("customSmart")` → `setNiche("custom")`).

## 🗺 Onde está no código (v1.27.1; números aproximados, mudam ao editar)
- **`normBuilderSection`** (≈linha 6200) converte `builderSection.groups → items`. **FIX-004:** `opts: g.items.map(it => Array.isArray(it) ? it : [it,it])` — aceita item **string** OU **par `[código,rótulo]`**. Os chips renderizam em `renderBuilderSection` (≈6788; `data-chip`/`data-val`, wire em ≈6826) e a escolha entra na saída via finder `o[0]===val` (≈6924). Só `client` e `narrative` usam o formato par.
- **`BEHAVIORS_BASE` agora 13 itens** (era 11): +`shrink_hygiene` (P12) +`research_refute` (P13), no fim do array (ordem do array = ordem de exibição). Renderizam em `buildInstr` (curto: bullet com a 1ª frase, via `shortDef`) e `buildClaudeMd` (completo: `### N. Label` + def longa). Behaviors de nicho entram **depois**, sempre via `normBehaviors`. Não há count "11"/"13" hardcoded em parte alguma.
- `getCurrentNiche` usa `raw.isBuilder` (genérico). Não há mais `customSmart` (CSS/hero/branch/objeto removidos).
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

## 💬 Última sessão (2026-06-11 — v1.27.1)
Conserto de bug a partir de teste real, mais captura/refino de ideias. Tudo verde:
- **FIX-004 — chips de Cliente/Narrativa não selecionáveis.** O conversor `normBuilderSection` tratava todo item de `groups` como string; esses dois nichos usam o par `[código,rótulo]`, então o chip nunca acendia e a escolha não entrava no texto. Conserto de 1 linha (`Array.isArray(it) ? it : [it,it]`). O **harness agora testa a integridade dos chips de todos os nichos** + round-trip seleção→saída, e provei que reprova o código com o bug.
- **5 ideias novas dos primeiros testes** (game design narrativo, música, pixel art, dev, design visual) capturadas e refinadas em IDEIAS, com pesquisa de fundo: **i-N18** (manifesto p/ nome certo no upload achatado), **i-N19** (verificar estado antes de repetir STATUS velho), **i-N20** (commit em 3 linhas + `git add .`), **i-N21** (comando de feedback), **i-N22** (estrutura flexível / módulos de doc opcionais).
- **Segunda leva (mesmo dia, só docs):** alinhamento com o usuário — **manifesto = `_MANIFEST.md` do FlatDrop** (regra adotada já no nosso CLAUDE.md: consultar manifesto, entregar pelo nome real, sufixo `__pasta` = colisão); **fluxo do feedback desenhado** (i-N21: seção «Feedback para o Kit» no IDEAS do piloto → usuário transporta → kit roteia); **válvula de desvio registrado** proposta (i-N22: "templates são ponto de partida, não contrato; desviar registrando é como o kit aprende"); **i-N23** capturada (4 melhorias do nicho Pixel vindas do piloto: paleta global×bioma, prioridade visual interna, efeitos especiais, estado "aguardando design"); **i-N24** capturada (multi-projeto: 4 frentes do mesmo jogo). Redações de i-N21/i-N22 **aguardam validação do usuário**.
- **Terceira leva (validações do usuário, D-022):** FlatDrop = **detecção automática, não padrão** (presença do `_MANIFEST.md`; filtragem: tipos não aceitos, `node_modules`/`venv`/`.git`, `.gitignore` opcional — ausência pode ser deliberada); **i-N19 ✓** (refino de P8), **i-N20 ✓** (`git add` listando; `.` a critério quando pequeno), **i-N22 ✓** (válvula aprovada), **i-N21 fechada com escopo ampliado** (desvio estrutural — diretriz nova no CLAUDE do piloto, `.md` novo, template alterado/dispensado — conta como feedback; **sem pré-aprovação** para o piloto criar `.md`; triagem no kit: absorver no base / módulo de grupo / específico do projeto). **Passada de código liberada.**
- **Não implementado de propósito:** a redação das diretrizes na ferramenta ficou para a próxima passada — são comportamentais e merecem o mesmo cuidado de decisão que P12/P13; com o lote agora validado (D-022), não há mais bloqueio.
**Próximo de fato:** executar a passada (itens 1+2 do "PRÓXIMO TRABALHO") com re-validação 17/17.

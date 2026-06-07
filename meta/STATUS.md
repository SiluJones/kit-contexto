# STATUS — Kit de Contexto Universal — 2026-06-07

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).
> Versão atual: **v1.27.0**. Índice ~548 KB / 8095 linhas. Teste: **17/17 nichos, 0 erros JS** (build por nicho via `normNiche`) + suíte de fluxos.

> **Mudanças nesta revisão (v1.27.0):** os itens 1 e 2 do "PRÓXIMO TRABALHO" (propagar P12 à ferramenta; decidir o princípio de pesquisa/refutação) foram **feitos** e saíram daqui — P12 virou o 12º item de `BEHAVIORS_BASE` (D-020) e a i-N17 virou o 13º, **P13** (D-021). O antigo item 3 (mount/RAG, D-018) subiu para item 1. Linha de versão/métricas atualizada para v1.27.0. "Onde está no código" ganhou a nota de `BEHAVIORS_BASE` 11→13. "Última sessão" reescrita para a v1.27.0. Nada único perdido: o que saiu daqui virou entrada de CHANGELOG (v1.27.0), atualização de status em D-020, o novo D-021, e a i-N17 marcada concluída em IDEIAS.

## Fase atual
🏁 **Custom unificado — composição + construção numa só tela, e fluxo de reuso completo.** No ar e validado:
- **Um card de construção (`custom`)** com a seção "Compor a partir de nichos prontos" (chips dos 16 nichos) **no topo** e o "Custom Builder" logo abaixo. Importar concatena → **deduplica de forma visível** → **sinaliza conflitos** (seletor de versão por arquivo) → preenche o builder **na mesma tela**. Acabou o vai-e-volta entre dois nichos de construção. (D-019, supersede D-014.)
- **Granularidade por nicho:** cada nicho marcado tem "escolher peças" (checkboxes de arquivos/comportamentos/prompts; padrão = tudo). `composeFromNiches(niches, sel)` respeita a seleção.
- **Atalho "Nichos salvos" na barra superior:** aparece quando há presets; selecionar **ativa** o nicho salvo de qualquer lugar.
- **Fluxo de preset:** Ativar (nicho fica vivo e salvo), barra "Editar / trocar nicho", carregar/excluir. **Corpo dos prompts persiste** após Ativar (FIX-003).

São **17 nichos**: 16 de conteúdo + **1 construtor** (`custom`).

## 🎯 PRÓXIMO TRABALHO (decidir/fazer)
1. **Corrigir a orientação mount/RAG/anexo GERADA pelo kit (à luz de D-018):** o CLAUDE.md / tela "Tokens & Fluxos" ainda diz "tudo no Projeto + ferramenta de código → mount", impreciso para projetos conectados via GitHub. Muda conteúdo em TODOS os nichos → exige re-validação 17/17. **Tarefa de código.**

✅ **Concluído nesta sessão (v1.27.0):** P12 (higiene ao encolher) **propagado à ferramenta** — 12º item de `BEHAVIORS_BASE`, agora aparece no CLAUDE.md gerado de todos os nichos (D-020). i-N17 **decidida**: virou o princípio próprio **P13** ("pesquisa para refinar E para refutar"), 13º item de `BEHAVIORS_BASE` (D-021). Validado 17/17, 0 erros.

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

## 🧪 Validação (regra dura: NUNCA publicar sem 17/17 e 0 erros)
Harness jsdom **boot limpo por nicho** (o ambiente reseta entre sessões — recriar os testes a cada sessão). No scratchpad `/home/claude/kit/`:
- `validate.js` — **17/17** nichos (setNiche + buildInstr + buildClaudeMd + controles não-vazios).
- `validate-switch.js` — transições construtor↔normal + **coexistência** (no `custom`, chips `#sc-chips` E builder `#cf-save`/`#cf-load` juntos). Guarda o bug A / re-entrância.
- `validate-compose.js` — Fase 1.2 (compor dev+pixel; usa `setNiche("custom")`).
- `validate-conflict.js` — Fase 1.3 (conflito + seletor; `setNiche("custom")`).
- `validate-reuse.js` — fluxo de preset (ativar/editar-trocar/carregar/excluir).
- `t-prompt.js` — corpos de prompt preservados após Ativar (view + localStorage; CLAUDE.md só título, por design).
- `t-shortcut.js` — atalho "Nichos salvos" (ausente sem presets; aparece e ativa de qualquer lugar).
- `t-granular.js` — granularidade (desmarcar peça → some do import; "marcar todas" reinclui).
Mais `node --check` no `<script>` e balanceamento de tags. **Atenção:** ao remover/renomear coisas no código, atualizar os testes (foi o que aconteceu ao remover `customSmart`: trocar `setNiche("customSmart")` → `setNiche("custom")`).

## 🗺 Onde está no código (v1.27.0; números aproximados, mudam ao editar)
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

## 💬 Última sessão (2026-06-07 — v1.27.0)
Fase 3 (higiene & consistência), tudo verde. Só dados, sem código de feature:
- **P12 propagado à ferramenta** (D-020): "higiene ao encolher arquivos-chave" virou o 12º item de `BEHAVIORS_BASE` — antes valia só para a governança do nosso projeto; agora aparece no CLAUDE.md gerado de todos os 17 nichos (e como bullet curto nas Instruções).
- **i-N17 decidida → P13** (D-021): em vez de reforçar P1/P7, criou-se um princípio próprio, "pesquisa para refinar E para refutar" (procura ativamente onde a ideia já falhou para os outros e traz o contraponto com lastro na experiência alheia, não só no raciocínio interno). É o 13º item de `BEHAVIORS_BASE`.
- **Validação:** 17/17 nichos, 0 erros; P12 e P13 presentes nos dois artefatos (Instruções + CLAUDE.md) de cada nicho; `div` 273/273 (inalterado vs v1.26.0).
- As versões **v1.25.1** e **v1.26.0** (do mesmo dia) já estão registradas no CHANGELOG; saíram do STATUS.
**Próximo de fato:** item 1 do "PRÓXIMO TRABALHO" — corrigir a orientação mount/RAG gerada pelo kit (D-018), que muda todos os nichos e exige re-validação 17/17.

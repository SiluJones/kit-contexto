# STATUS — Kit de Contexto Universal — 2026-06-07

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).
> Versão atual: **v1.26.0**. Índice ~546 KB / 8092 linhas. Teste: **17/17 nichos, 0 erros JS** (boot limpo por nicho) + suíte de fluxos.

> **Mudanças nesta revisão (P12):** o STATUS anterior (v1.25.0) tinha como "próximo trabalho" o sub-painel de granularidade — **feito** (v1.26.0), saiu daqui. A fase virou "Custom unificado". O "código onde está" foi atualizado (customSmart removido; funções novas). Backlog reorganizado com os itens novos desta sessão (propagar P12 à ferramenta, decidir o princípio de pesquisa/refutação, refator modular, guias, auto-patch). Nada único perdido: o que saiu virou entrada de CHANGELOG (v1.25.1, v1.26.0) e/ou item de IDEIAS/ROADMAP.

## Fase atual
🏁 **Custom unificado — composição + construção numa só tela, e fluxo de reuso completo.** No ar e validado:
- **Um card de construção (`custom`)** com a seção "Compor a partir de nichos prontos" (chips dos 16 nichos) **no topo** e o "Custom Builder" logo abaixo. Importar concatena → **deduplica de forma visível** → **sinaliza conflitos** (seletor de versão por arquivo) → preenche o builder **na mesma tela**. Acabou o vai-e-volta entre dois nichos de construção. (D-019, supersede D-014.)
- **Granularidade por nicho:** cada nicho marcado tem "escolher peças" (checkboxes de arquivos/comportamentos/prompts; padrão = tudo). `composeFromNiches(niches, sel)` respeita a seleção.
- **Atalho "Nichos salvos" na barra superior:** aparece quando há presets; selecionar **ativa** o nicho salvo de qualquer lugar.
- **Fluxo de preset:** Ativar (nicho fica vivo e salvo), barra "Editar / trocar nicho", carregar/excluir. **Corpo dos prompts persiste** após Ativar (FIX-003).

São **17 nichos**: 16 de conteúdo + **1 construtor** (`custom`).

## 🎯 PRÓXIMO TRABALHO (decidir/fazer)
1. **Propagar o princípio P12 (higiene ao encolher docs) para a FERRAMENTA.** Hoje vale só para o nosso projeto (governança). Falta virar o **12º item de `BEHAVIORS_BASE`** → aparece no CLAUDE.md gerado de todos os nichos. **Tarefa de código** (edita BEHAVIORS_BASE + re-valida 17/17). Texto a usar (rascunho): *"Higiene ao encolher: ao reescrever/encolher um arquivo-chave (CONTEXT/STATUS/DECISOES/CHANGELOG/IDEIAS/ROADMAP), diga o que saiu e para onde foi (ou que é redundante/obsoleto); nunca encolha sem justificar item a item; confira que nada único se perdeu."* Ver DEC D-020.
2. **Princípio de rigor em pesquisa + refutação (decidir se formaliza).** Hoje P1 (analisa antes de aceitar), P4 (admite incerteza/pesquisa o que muda) e P7 (estuda o domínio antes de estruturar) cobrem PARCIALMENTE. O ângulo que o usuário quer explícito: *pesquisar/aprender sobre a ideia ou solicitação não só para refinar de forma profissional, mas também para **refutar e criticar** com base no sentido e na experiência de outros.* Decidir: reforçar P7/P1 ou criar um princípio próprio. Ver IDEIAS i-N17.
3. **Corrigir a orientação mount/RAG/anexo GERADA pelo kit (à luz de D-018):** o CLAUDE.md / tela "Tokens & Fluxos" ainda diz "tudo no Projeto + ferramenta de código → mount", impreciso para projetos conectados via GitHub. Muda conteúdo em TODOS os nichos → exige re-validação 17/17. **Tarefa de código.**

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

## 🗺 Onde está no código (v1.26.0; números aproximados, mudam ao editar)
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

## 💬 Última sessão (2026-06-07)
Sessão longa (acabou compactada). **Consertos + reforma da área Custom**, tudo verde:
- **v1.25.1** — corpo dos prompts importados sumia depois de Ativar (`toPreset` guardava o body como função; `JSON.stringify` do localStorage descarta funções). Agora guarda STRING. (FIX-003.)
- **v1.26.0** — três itens, a partir de teste em navegador: **(1)** unificar Inteligente + Builder num só card `custom` (composição no topo, builder abaixo; sem troca de tela) — supersede D-014, vira **D-019**; **(2)** atalho "Nichos salvos" na barra superior (ativa de qualquer lugar); **(3)** sub-painel de granularidade (escolher peças por nicho).
- **Discussões levantadas pelo usuário** (registradas em IDEIAS/ROADMAP, sem código nesta sessão): refator modular (i-N13), nicho/ferramenta de guias (i-N14), auto-patch + entrega por diff (i-N15/i-N16), e o princípio de pesquisa/refutação (i-N17).
- **Novo princípio P12** (higiene ao encolher docs) adotado para o projeto (CLAUDE.md/CONTEXT) e **na fila para a ferramenta** (BEHAVIORS_BASE 11→12, DEC D-020).
**Próximo de fato:** decidir/fazer os itens 1–3 do "PRÓXIMO TRABALHO" (propagar P12 à ferramenta é o mais direto e barato).

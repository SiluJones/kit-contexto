# STATUS — Kit de Contexto Universal — 2026-06-04

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).
> Versão atual: **v1.24.0**. Índice ~528 KB / 8024 linhas. Teste: **18/18 nichos, 0 erros JS** (boot limpo por nicho).

## Fase atual
🏁 **Custom Inteligente — ETAPA 1 COMPLETA.** O segundo nicho de construção está no ar e validado: chips dos 16 nichos → importação por **concatenação** → **deduplicação visível** → **checagem de conflito** (arquivos com seletor de versão; comportamentos divergentes sinalizados). Tudo cai no motor existente (`toPreset → mergeCustom → presets`). Nesta sessão também consertei um **bug latente** dos construtores (a coluna de controles não voltava ao sair de um nicho construtor) e tornei os formulários **re-entrantes**.

Agora são **18 nichos**: 16 de conteúdo + **2 construtores** (custom "Blank" + customSmart "Inteligente").

## ✅ O que entrou nesta sessão (v1.24.0)
- **`NICHES.customSmart`** — 2º construtor (card ao lado do Blank, `category:"special"`), tema próprio (`data-niche="customSmart"`), hero próprio, `isBuilder:true`.
- **Fase 1.1 — chips:** fileira dos 16 nichos de conteúdo com seleção múltipla, contador ao vivo, "limpar seleção".
- **Fase 1.2 — concatenação:** `composeFromNiches` junta contextFiles + behaviors + promptsExtra + convenções + saídas dos nichos marcados; prompts renumerados G,H,I…; `body` de prompt (função) vira string; pré-preenche o editor Blank (`STATE._cf`) com banner de resumo.
- **Fase 1.3 — dedup com conflito:** duplicata IDÊNTICA unifica em silêncio; CONFLITO (mesmo nome, conteúdo diferente) preserva versões e mostra **seletor de qual manter** por arquivo; comportamento com def divergente é **sinalizado** (não bloqueia).
- **Conserto bug A + re-entrância:** `captureControlsSkeleton`/`restoreControlsSkeleton`; restauração no topo de `renderBuilder`, `renderCustomForm` e `renderSmartCustomForm` (corrige sair do construtor e re-chamadas diretas de cf-load/save/delete/limpar/dispensar).
- **Generalização:** `getCurrentNiche` usa `raw.isBuilder` (não mais `id==="custom"`), então ambos os construtores usam `mergeCustom`.

## 🔎 ACHADO EMPÍRICO CONFIRMADO → D-018 (corrige D-016/D-017)
Teste limpo entre dois estados (prints do usuário): **só o conector GitHub → `/mnt/project/` VAZIO**; **upload direto dos .md → mount POPULADO** (15 arquivos, achatado). Conclusão: **o conector do GitHub alimenta o RAG/Conhecimento do Projeto** (busca funciona, com subpastas `meta/`/`logs/` preservadas) **mas NÃO alimenta o mount da ferramenta de código. Só o upload direto popula o mount** (e chega achatado). O RAG por si **não** bloqueia o mount; o que muda é COMO o mount é alimentado. **Corrige a conclusão da v1.22.0/v1.23.0** ("deixar tudo no Projeto + ligar a ferramenta de código → leio pelo mount") — isso só vale se os arquivos foram subidos DIRETO; via conector do GitHub, ficam só no RAG.

## 🎯 PRÓXIMO TRABALHO
1. **Sub-painel de granularidade (etapa 2 do Custom Inteligente, D-014):** botão "escolher peças" por nicho marcado — importar inteiro vs. item a item (quais arquivos/behaviors/prompts de cada nicho). É refinamento sobre o motor já pronto; NÃO é 3ª opção.
2. **Pré-preencher o nome do preset no "Aplicar" do Inteligente:** hoje "Aplicar" sem nome zera o preset (comportamento pré-existente do Blank, via round-trip de `LS_PRESET_CURR` no `setNiche`). Sugerir um nome a partir do label combinado, ao importar, fecha o fluxo de ponta a ponta.
3. **Corrigir a orientação mount/RAG/anexo GERADA pelo kit (à luz de D-018):** o CLAUDE.md / tela "Tokens & Fluxos" ensina "tudo no Projeto + ferramenta de código → mount", impreciso para projetos conectados via GitHub. É mudança de conteúdo em TODOS os nichos → exige re-validação 18/18. Adiado de propósito desta faxina.

## 🎯 Outras pendências (sem urgência)
1. **Revisar README/PLANNING** — PLANNING pendente de revisão geral pós-MVP.
2. **Revisar a qualidade das Instruções geradas** — confirmar polimento/eficiência.
3. **Reagrupar narrative** (cosmético): hoje `group:"literary"`; é criativo. Só afeta tema visual.
4. **MAPA.md** cita "17 prontos" — atualizar para refletir os 2 construtores (cosmético).
5. **Nichos novos (FUTURO, adiados de propósito):** ver `NICHOS-CANDIDATOS.md` (Educação nº1, depois Desenvolvimento Pessoal/Journaling, Jurídico/Podcast/Tradução).
6. **spec-kit para dev/game (FUTURO):** quando o usuário tiver mais feedback de uso.

## 🧪 Validação (regra dura: NUNCA publicar sem 18/18 e 0 erros)
Harness jsdom **reconstruído nesta sessão** (o ambiente reseta entre sessões), com **boot limpo por nicho** (evita contaminação do construtor que reescreve a coluna). Quatro testes no scratchpad `/home/claude/kit/`:
- `validate.js` — 18/18 nichos (setNiche + buildInstr + buildClaudeMd + controles não-vazios).
- `validate-switch.js` — 5 transições construtor↔normal (bug A).
- `validate-compose.js` — Fase 1.2 (compor dev+pixel: 15 checagens).
- `validate-conflict.js` — Fase 1.3 (conflito + seletor: 18 checagens).
Mais `node --check` no `<script>` extraído e balanceamento de tags. **Caso real:** dev+pixel revela 2 conflitos de arquivo (`STATUS.md`, `LOG-TEMPLATE.md`).

## 🗺 Onde está no código (v1.24.0; números aproximados, mudam ao editar)
- `html[data-niche="customSmart"]` (CSS de tema) ~76.
- `NICHES.customSmart` ~6151; `getCurrentNiche` usa `raw.isBuilder` ~6306; hero `case "customSmart"` ~6611.
- Esqueleto dos controles: `CONTROLS_SKELETON`/captura/restaura ~6710; `renderBuilder` roteia customSmart ~6725.
- `contentNiches` ~7347; `composeFromNiches` ~7356; `renderImportReport` ~7457; `renderSmartCustomForm` ~7506; `renderCustomForm` ~7581 (re-entrante; banner + seletor de conflito).
- `toPreset` ~7865; `fromPreset` ~7885 (shape do preset; `body` de prompt vira função no preset).

## 🗂 Convenções
- pt-BR em tudo, inclusive comentários de código. Nomes de template profissionais.
- Entrega: arquivos completos em outputs/meta; o usuário organiza no repo.
- Commit ao final: comando completo p/ CMD Windows (UMA linha, `-m` repetido), pronto para colar.
- Usuário no CMD do Windows (`C:\Users\alexk\Arquiteturas\kit-contexto`).
- **Mount (D-018):** para ler/editar pelo mount, subir os arquivos DIRETO no Projeto (o conector do GitHub só alimenta o RAG). Mount chega achatado; nomes iguais em pastas diferentes colidem.

## 💬 Última sessão (2026-06-04)
Em conversa nova, com a ferramenta de código ligada e os arquivos subidos DIRETO no Projeto. Confirmado **D-018** (mount só via upload direto, achatado; conector do GitHub só RAG). Construído e validado o **Custom Inteligente etapa 1** (1.0 esqueleto → 1.1 chips → 1.2 concatenação → 1.3 dedup/conflito), além do **conserto do bug A** e da **re-entrância** dos construtores. Tudo 18/18, 0 erros. **Próximo:** sub-painel de granularidade (etapa 2) e o pré-preenchimento do nome no "Aplicar".

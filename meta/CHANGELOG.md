# CHANGELOG — Kit de Contexto Universal

> Histórico de versões. Versão atual: **v1.0.0**.

---

## v1.1.0 — 2026-05-29 — Fundação transversal

Primeira etapa do refinamento pós-MVP. Não mexe nos nichos individualmente ainda — eleva a base que todos compartilham, a partir do feedback massivo recebido do Claude no projeto GameDataHub (nicho dev) e dos materiais reais de uso (design/cliente).

### Adicionado
- **2 princípios comportamentais universais** (agora 6 no total, antes 4):
  - **Analisa antes de aceitar** — o assistente não segue cegamente; avalia viabilidade de cada sugestão e se posiciona (a favor / refina / contra), sempre fundamentado. Nunca se limita às palavras do usuário.
  - **Não desperdiça tokens** — não pergunta o que já foi decidido, não pede confirmação de plano aprovado, consolida perguntas.
- **Geração de CLAUDE.md**: novo artefato gerado pelo kit, separado das Instruções do Projeto. Toggle de abas na tela de Instruções (Instruções do Projeto ↔ CLAUDE.md), cada um com seu copiar/baixar.
- **Filosofia rolante/estável/cresce** como estrutura base (constante FILE_PHILOSOPHY).
- **Regras de higiene anti-inchaço** (HYGIENE_RULES): referência cruzada em vez de duplicação; STATUS só o agora; IDEAS nunca perde; DECISIONS arquiva quando grande.
- **Tabela de gatilhos** (evento -> arquivo a atualizar) gerada no CLAUDE.md, extensível por nicho via `triggersExtra`.
- **Mapeador de comportamento temporal** por arquivo (`fileBehaviorLabel`) cobrindo os nomes de arquivo dos 17 nichos.

### Mudou
- `buildInstr()` agora produz um **núcleo denso** (ritual de início + princípios curtos + arquivos + idioma), em vez do bloco antigo. Inclui CLAUDE.md no ritual e na lista de arquivos.
- Princípios nas Instruções aparecem encurtados (primeira frase); a versão completa vai no CLAUDE.md.

### Fundamento técnico (ver DECISOES D-012)
- Instruções do Projeto são lidas inteiras a cada mensagem (token-caras) -> núcleo enxuto.
- Arquivos de conhecimento usam RAG nos planos pagos e são fáceis de atualizar -> CLAUDE.md completo.

### Validação
- Teste DOM (jsdom) dos 17 nichos: 0 erros de JS, todos renderizam Instruções + CLAUDE.md.
- Toggle de abas, geração de ambos os artefatos, troca de nicho: sem erros.

---

## v1.0.0 — 2026-05-27 (planejado)

### Adicionado
- **18 nichos** implementados em página única:
  - 8 core: dev, design, client, narrative, marketing, research, product, business
  - 8 criativos: game, pixel, brainstorm, music, rpg, cuisine, animation, comics
  - 1 special: custom (construtor)
- **Heros visuais distintos** para cada nicho (não apenas troca de cor — estruturas próprias: terminal, swatches, kanban, editorial, feed, paper, wireframe, KPIs, HUD, grade de pixels, postits, waveform, scroll medieval, card de receita, timeline, painéis, grade vazia).
- **Custom como construtor real**: formulário para definir identidade (nome, ícone, cor, fonte), arquivos de contexto, comportamentos extras, convenções, saídas, prompts G+. Salva e carrega presets via `localStorage`. Múltiplos presets simultâneos.
- **Persistência por nicho**: trocar de nicho preserva o estado de cada um.
- **Theming via CSS variables**: `[data-niche]` e `[data-group]` no `<html>` trocam cor e família de fonte sem repintar nada via JS.
- **3 grupos de fonte display**:
  - serif (Fraunces) para a maioria
  - literary (Playfair Display) para narrative, research, music, rpg, comics
  - digital (Oxanium) para game, pixel
- **6 prompts universais (A–F)** + **4 prompts específicos (G–J)** por nicho.
- **4 comportamentos universais** + 4-5 comportamentos extras por nicho.
- **Download individual de templates** + **pacote ZIP** (via JSZip carregado por CDN sob demanda).
- **Meta-doc do próprio kit** em `meta/` usando estrutura do nicho Brainstorm.
- **`DEPLOY-GUIDE.md`** (fora do repo) com passo a passo para GitHub Pages.

### Mudou em relação à v0.x (kit Dev-only)
- Onde antes era só desenvolvimento, agora são 18 domínios.
- `PLANNING.md` consolidado (antes vinha em duas partes).
- `README.md` reescrito para multi-nicho.
- Templates do Dev agora vivem como conteúdo baixável; arquivos `CONTEXT.md`, `STATUS.md`, `DECISIONS.md`, `IDEAS.md`, `CHANGELOG.md`, `LOG-TEMPLATE.md` na raiz do projeto antigo foram substituídos pelos arquivos em `meta/`.
- Nome de templates padronizado profissionalmente (sem versões "definitivo" ou "aprimorado").

### Removido
- Versões parciais antigas do `PLANNING-PART2.md` (consolidado em `PLANNING.md` único).
- Index.html antigo (versão só Dev — substituído pelo novo).
- `niche_visual_identity_map.html` (rascunho de design, integrado no produto final).

---

## v0.x — sessões anteriores (não numeradas formalmente)

Versão Dev publicada em `silujones.github.io/kit-contexto-claude`. Resolveu o problema só para devs. Esta v1.0.0 expande para 18 domínios mantendo a mesma arquitetura.

---

## Possíveis v1.1 / v1.2 (não compromissos)

Itens em `meta/IDEIAS.md` arquivados como "evolução natural":

- Exportar/importar preset Custom como `.json` (i11)
- Tema claro (i9)
- Tradução para inglês (i10)
- Versão impressa (PDF) dos templates (i13)
- Drag-and-drop para reordenar arquivos no Custom (i20)
- Atalhos de teclado adicionais (i24)

Nada disso está prometido. Decisão depende de uso real.

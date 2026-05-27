# CHANGELOG — Kit de Contexto Universal

> Histórico de versões. Versão atual: **v1.0.0**.

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

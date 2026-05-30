# CHANGELOG — Kit de Contexto Universal

> Histórico de versões. Versão atual: **v1.0.0**.

---

## v1.2.0 — 2026-05-29 — Etapa 1: nicho dev aprofundado

Primeiro nicho reconstruído em profundidade (referência de ouro para os demais), usando como matéria-prima o feedback de uso real do projeto GameDataHub.

### Adicionado ao nicho dev
- **3 arquivos opcionais** (além dos 6 do núcleo): `ROADMAP.md` (plano em fases), `GLOSSARY.md` (termos do projeto), `HISTORICO.md` (conhecimento consolidado de fases antigas, lido sob demanda). Total: 9 templates.
- **5 prompts G-K** (o dev tinha zero antes): G Debugar com método (causa raiz, não band-aid), H Registrar decisão técnica (vira DEC-N), I Revisar código/diff, J Planejar feature ou fase, K Auditar antes de mexer em peça crítica.
- **Gatilhos específicos de dev** (`triggersExtra`): decisão de arquitetura → DECISIONS completo; mudança de fase → ROADMAP completo; termo novo → GLOSSARY completo.

### Enriquecido
- **CONTEXT.md**: agora inclui «Como funciona [componente] (CRÍTICO)», «Armadilhas Conhecidas» (o que NÃO fazer, com porquê) e «Contexto de Produto». Antes era só visão/stack/estrutura.
- **STATUS.md**: estrutura ✅Funcionando / 🔧Em Progresso / ❌Quebrado / 📋Backlog acionável / 📁Arquivos Críticos / 💬Última Sessão.
- **DECISIONS.md**: formato DEC-N (ADR) + FIX-N (bug grave: sintoma/causa raiz/solução/lição), com regra de arquivamento acima de ~700 linhas.
- **IDEAS.md**: separado em Usuário × Assistente + Concluídas + Descartadas (com motivo).
- **6 behaviors de dev** reescritos: comentário com propósito, preserva código existente, causa raiz, mudança mínima, sinaliza o que testar, indica prints.

### Corrigido
- **Mapeamento de categorias de arquivo**: `hist`→histórico (cresce), `ref`→referência, rolante→contexto. Antes `hist` aparecia como «opcional» e LOG-TEMPLATE como «rolante» (remendo da v1.1). Nova função única `fileTag()` substituiu a lógica duplicada em dois lugares. Nova tag visual «opcional».
- **Nota de ambiente corrigida**: a versão anterior dizia que «dentro de um Projeto não dá para gerar arquivos» — tecnicamente errado. O correto: os arquivos já no Projeto são somente-leitura, mas isso não impede gerar versões novas completas para baixar/salvar.

### Validação
- Teste DOM (jsdom): 17/17 nichos, 0 erros. Dev agora com 11 prompts (6 A-F + 5 G-K) e 9 templates. Tags semânticas conferidas em dev e game.

---

## v1.1.1 — 2026-05-29 — Entrega de documentos como arquivos completos

Ajuste de direção a partir de esclarecimento do usuário. O ponto de fricção no uso real não era "o Claude pediu pra atualizar os docs" — era **o Claude ter entregado blocos soltos de texto para o usuário costurar à mão dentro dos arquivos**. O usuário quer arquivos completos, prontos para baixar e substituir.

### Definido
- **Protocolo de entrega**: o assistente entrega sempre o ARQUIVO COMPLETO e atualizado (pronto para substituir o antigo), nunca trechos para colar/costurar. Se vários arquivos mudaram, entrega todos inteiros. As regras de higiene são aplicadas pelo assistente ao montar o arquivo — o usuário recebe o resultado já correto.
- **Ressalva de ambiente**: dentro de um Projeto do Claude (pasta somente-leitura, sem criação de arquivo para download), e só nesse caso, o assistente entrega o conteúdo completo de cada arquivo no chat, um por bloco de código, pronto para salvar. Em ambientes com criação de arquivos, entrega para baixar. Princípio idêntico: arquivo inteiro, nunca pedaços.
- **Aplicar continua sendo decisão do usuário** — mas o trabalho de montar o arquivo é do assistente, não do usuário.

### Adicionado (mantido desta sessão)
- **7º princípio universal: «Instruções sempre cuidadosas»** — qualquer instrução, guia ou passo a passo entregue ao usuário deve ser completo, detalhado e bem explicado; nunca leviano; não assume contexto que o usuário não tem.

### Corrigido em relação à versão intermediária
- Uma primeira tentativa desta sessão chegou a instruir "preparar blocos demarcados para o usuário colar" — exatamente o comportamento indesejado. Revertido: agora é arquivo completo.

### Validação
- Teste DOM (jsdom) dos 17 nichos: 0 erros; 7 princípios universais; seção «Como o assistente entrega as atualizações» presente e correta no CLAUDE.md.

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

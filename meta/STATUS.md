# STATUS — Kit de Contexto Universal — 2026-05-29

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).

## Fase atual
Refinamento área por área, após o MVP (v1.0.0).

Acabou de entrar a **Etapa 0 — Fundação transversal (v1.1.0)**. Próxima: **Etapa 1 — aprofundar o nicho dev**.

## Entrega de documentos (v1.1.1) — arquivos completos, não blocos
- Esclarecido: o assistente entrega sempre o **arquivo completo e atualizado** (pronto para baixar e substituir), nunca blocos soltos para o usuário costurar à mão dentro do arquivo.
- Ressalva: dentro de um Projeto (somente-leitura), entrega o conteúdo completo de cada arquivo no chat, um por bloco — mesmo princípio, arquivo inteiro.
- **7º princípio universal**: «Instruções sempre cuidadosas» — qualquer guia/passo a passo entregue ao usuário é completo, detalhado e bem explicado, nunca leviano.
- Aplicar continua sendo decisão do usuário; montar o arquivo é trabalho do assistente.

## O que mudou nesta sessão (v1.1.0)
- **2 novos princípios universais** em todos os nichos: «Analisa antes de aceitar» e «Não desperdiça meus tokens». Vindos do feedback massivo do Claude no projeto GameDataHub (dev).
- **Geração de CLAUDE.md**: o kit agora produz dois artefatos com naturezas técnicas distintas — Instruções do Projeto (núcleo enxuto, lido em toda mensagem) e CLAUDE.md (comportamento completo, subido como arquivo e versionável). Toggle de abas na tela de Instruções.
- **Filosofia rolante/estável/cresce** + **regras de higiene anti-inchaço** + **tabela de gatilhos** agora são estruturas base do kit, refletidas no CLAUDE.md gerado.

## Decisão de arquitetura (fundamentada por pesquisa)
- **Instruções do Projeto** são lidas inteiras a cada mensagem (token-caras) -> devem ser densas.
- **Arquivos de conhecimento** usam RAG nos planos pagos (carregados sob demanda quando o acervo é grande) e são fáceis de atualizar/versionar.
- Por isso: núcleo curto nas Instruções + versão completa no CLAUDE.md. Não é redundância — é especialização.

## Próximos passos
1. **Etapa 1 — dev aprofundado** (próxima sessão): reconstruir o nicho dev como referência de ouro, incorporando o feedback do GameDataHub (9 arquivos com CLAUDE/ROADMAP/GLOSSARY, prompts G+ que hoje faltam, CONTEXT com armadilhas catalogadas).
2. Etapas seguintes: um nicho por vez, cada um aproveitando a fundação.
3. Com o tempo: coletar novos "feedbacks" de Claudes usando cada nicho na prática, e relapidar.

## Definição de arquivos (núcleo + opcionais)
**Núcleo (todo projeto):** CLAUDE, CONTEXT, STATUS, DECISIONS, IDEAS, CHANGELOG, LOG-TEMPLATE.
**Opcionais (conforme complexidade):** ROADMAP (plano em fases), GLOSSARY (jargão próprio), BRIEFING/continuidade (transferência frequente).
Racional: cada arquivo tem um horizonte temporal distinto; fundir recriaria duplicação. Mas nem todo projeto precisa de todos — daí o núcleo + opcionais.

## Pendências
- [ ] Etapa 1 (dev aprofundado).
- [ ] Atualizar README e PLANNING para refletir CLAUDE.md + 6 princípios (quando a fundação estabilizar após o dev).
- [ ] Reavaliar posicionamento do kit frente à feature nativa "Pesquisar e referenciar conversas" — diferencial confirmado: portabilidade (Git, qualquer conta), estrutura deliberada, e controle do que entra no contexto.

---
*Próxima sessão: Etapa 1 — aprofundar o nicho dev usando o feedback do GameDataHub como matéria-prima.*

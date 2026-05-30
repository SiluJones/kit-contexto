# STATUS — Kit de Contexto Universal — 2026-05-29

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).

## Fase atual
Refinamento área por área, após o MVP. **Etapas 1 (dev), 2 (client), 2.5 (fundação+dogfooding) e 3 (design) concluídas.**

Próxima: **Etapa 4 — escolher o próximo nicho.**

## ✅ Concluído recentemente
- **v1.0.0** — MVP: 17 nichos + custom.
- **v1.1.0 / v1.1.1** — Fundação: 7 princípios, CLAUDE.md separado, higiene, gatilhos; entrega de docs como arquivos completos.
- **v1.2.0** — Etapa 1: dev aprofundado (9 templates, prompts G-K).
- **v1.3.0** — Etapa 2: client aprofundado (8 templates +COMUNICACOES/FINANCEIRO, prompts G-L).
- **v1.4.0** — Etapa 2.5: consolidação (9º princípio "estuda o domínio" + regra "verifica antes de pedir arquivo", nuance de entrega do GameDataHub2) + **dogfooding**: criado `meta/CLAUDE.md` do próprio projeto.
- **v1.5.0** — Etapa 3: design aprofundado (9 templates +MARCA +PRODUCAO, prompts G-L com pré-impressão e apresentação).

## 🎯 Próximos passos
1. **Etapa 4 — próximo nicho.** Candidatos por impacto/uso: **narrative** (obra longa, alto custo de esquecimento, sem caso real ainda mas domínio rico), **research** (rigor de fontes/citação), **marketing** (calendário/audiência), ou um criativo (**game**, já tem profundidade decente). A decidir com o usuário.
2. Manter o padrão: estudar domínio (pesquisa + feedback real se houver) → projetar (núcleo+opcionais, behaviors, prompts G+, gatilhos) → construir isolado → validar (node + jsdom 17/17) → publicar + CHANGELOG/STATUS.
3. Coletar novos feedbacks de Claudes conforme cada nicho for testado, e relapidar.
4. Ao fim da maioria: atualizar README e PLANNING (multi-nicho) para refletir CLAUDE.md, 9 princípios, núcleo+opcionais.

## 📁 Nichos já no padrão de ouro (referência para os próximos)
- **dev** (Etapa 1), **client** (Etapa 2), **design** (Etapa 3).
- Padrão: arquivo-âncora com "como funciona/sistema" + armadilhas + ângulo próprio do nicho; ADR para decisões; histórico que cresce; STATUS rolante com "com quem está a bola"; prompts A-F + G+ específicos; behaviors derivados de pesquisa + caso real.

## Pendências
- [ ] Decidir o próximo nicho (Etapa 4).
- [ ] Atualizar README/PLANNING quando a maioria dos nichos estiver no padrão.
- [ ] Reavaliar posicionamento frente à feature nativa "Pesquisar e referenciar conversas".

## 🗂 Estado dos arquivos do nosso próprio projeto (meta/)
- Núcleo presente: **CLAUDE.md** (novo!), STATUS, CHANGELOG, DECISOES, IDEIAS, LOG-TEMPLATE.
- Brainstorm de origem: TEMA, MAPA, FILTROS.
- Raiz: README, PLANNING, DEPLOY-GUIDE (podem precisar de atualização ao fim das etapas).

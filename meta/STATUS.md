# STATUS — Kit de Contexto Universal — 2026-05-29

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).

## Fase atual
Refinamento área por área, após o MVP. **Etapas 1 (dev), 2 (client), 2.5 (fundação+dogfooding), 3 (design) e 4 (narrative) concluídas.**

Próxima: **Etapa 5 — escolher o próximo nicho.**

## ✅ Concluído recentemente
- **v1.0.0** — MVP: 17 nichos + custom.
- **v1.1.0 / v1.1.1** — Fundação: princípios universais, CLAUDE.md separado, higiene, gatilhos; entrega de docs como arquivos completos.
- **v1.2.0** — Etapa 1: dev (9 templates, prompts G-K).
- **v1.3.0** — Etapa 2: client (8 templates, prompts G-L).
- **v1.4.0** — Etapa 2.5: consolidação (9 princípios totais) + dogfooding (meta/CLAUDE.md do projeto).
- **v1.5.0** — Etapa 3: design (9 templates +MARCA +PRODUCAO, prompts G-L).
- **v1.6.0** — Etapa 4: narrative (9 templates: BIBLIA/PERSONAGENS/ENREDO/VOZ/CONTINUIDADE/STATUS/LOG +CRONOLOGIA +GLOSSARIO; prompts G-L; behavior central "a IA não escreve a história").

## 🎯 Próximos passos
1. **Etapa 5 — próximo nicho.** Candidatos: **research** (rigor de fontes/citação/metodologia — alto valor, domínio rico), **marketing** (calendário/audiência/voz de marca), ou um criativo: **game** (game design/sistemas), **music**, **rpg**, **cuisine**, **animation**, **comics**, **pixel**, **product**, **business**, **brainstorm**. A decidir com o usuário.
2. Manter o ritual: estudar domínio (pesquisa + feedback real se houver) → projetar → construir isolado → validar (node + jsdom 17/17) → publicar + CHANGELOG/STATUS.
3. Coletar feedbacks de Claudes conforme cada nicho for testado, e relapidar.
4. Ao fim da maioria: atualizar README e PLANNING (multi-nicho) para refletir CLAUDE.md, 9 princípios, núcleo+opcionais.

## 📁 Nichos já no padrão de ouro (4 de 17)
- **dev** (E1), **client** (E2), **design** (E3), **narrative** (E4).
- Restam: research, product, business, marketing, game, pixel, brainstorm, music, rpg, cuisine, animation, comics (12) + custom (gerador, não precisa de aprofundamento de conteúdo).

## Padrão de ouro consolidado (para os próximos)
- Arquivo-âncora com "como funciona / sistema / bíblia" + armadilhas/continuidade + ângulo próprio do nicho.
- Decisões em formato registrado (DEC); histórico que cresce; STATUS rolante.
- Núcleo enxuto + opcionais marcados.
- Prompts A-F universais + 6 G-L específicos cobrindo as tarefas reais do domínio.
- Behaviors derivados de pesquisa + caso real, capturando o que de fato importa naquele ofício.

## Pendências
- [ ] Decidir o próximo nicho (Etapa 5).
- [ ] Atualizar README/PLANNING quando a maioria dos nichos estiver no padrão.
- [ ] Reavaliar posicionamento frente à feature nativa "Pesquisar e referenciar conversas".

## 🗂 Estado dos arquivos do nosso projeto (meta/)
- Núcleo: CLAUDE, STATUS, CHANGELOG, DECISOES, IDEIAS, LOG-TEMPLATE.
- Brainstorm de origem: TEMA, MAPA, FILTROS.
- Raiz: README, PLANNING, DEPLOY-GUIDE (atualizar ao fim das etapas).

# STATUS — Kit de Contexto Universal — 2026-05-29

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).

## Fase atual
Refinamento área por área, após o MVP. **Etapa 1 (nicho dev aprofundado) concluída.**

Próxima: **Etapa 2 — escolher o próximo nicho a aprofundar.**

## ✅ Concluído recentemente
- **v1.0.0** — MVP: 17 nichos + custom, 1 HTML autossuficiente.
- **v1.1.0** — Fundação transversal: 6→7 princípios universais (analisa antes de aceitar, não desperdiça tokens, instruções cuidadosas), geração de CLAUDE.md separado das Instruções, filosofia rolante/estável/cresce, regras de higiene, tabela de gatilhos.
- **v1.1.1** — Entrega de documentos: o assistente entrega arquivos COMPLETOS para baixar/substituir, nunca blocos soltos para costurar. Nota de ambiente corrigida (Projeto somente-leitura não impede gerar arquivos novos).
- **v1.2.0** — **Etapa 1: nicho dev aprofundado** como referência de ouro. 9 templates (núcleo 6 + ROADMAP/GLOSSARY/HISTORICO opcionais), 5 prompts G-K (debug, decisão, revisão, plano, auditoria), CONTEXT/STATUS/DECISIONS/IDEAS enriquecidos. Mapeamento de tags corrigido (fileTag único).

## 🎯 Próximos passos
1. **Etapa 2 — próximo nicho.** Sugestão de ordem por impacto/uso: **client (Gestão de Cliente)** — já temos feedback real forte (o BRIEFING_CONTINUIDADE_v2) — ou **design**, ou **narrative**. A decidir com o usuário.
2. Repetir o padrão da Etapa 1 em cada nicho: enriquecer arquivos, adicionar prompts específicos, gatilhos próprios.
3. Conforme cada nicho for testado na prática, coletar novos feedbacks de Claudes e relapidar.
4. Quando a maioria dos nichos estiver aprofundada: atualizar README e PLANNING (multi-nicho) para refletir CLAUDE.md, 7 princípios e núcleo+opcionais.

## 📁 Como o dev v2 ficou (referência para os próximos)
- **Núcleo (6):** CONTEXT, STATUS, DECISIONS, CHANGELOG, IDEAS, LOG-TEMPLATE.
- **Opcionais (3):** ROADMAP, GLOSSARY, HISTORICO.
- **Prompts:** A-F universais + G-K específicos do nicho.
- **Padrão de qualidade:** CONTEXT com «como funciona (CRÍTICO)» + armadilhas + produto; DECISIONS com DEC/FIX; IDEAS com Usuário/Assistente/Concluídas/Descartadas; STATUS com seções de estado.

## Pendências
- [ ] Decidir o próximo nicho (Etapa 2).
- [ ] Atualizar README/PLANNING quando a fundação + nichos estabilizarem.
- [ ] Reavaliar posicionamento frente à feature nativa "Pesquisar e referenciar conversas" — diferencial: portabilidade (Git/qualquer conta), estrutura deliberada, controle do que entra no contexto.

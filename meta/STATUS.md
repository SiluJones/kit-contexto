# STATUS — Kit de Contexto Universal — 2026-05-30

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).

## Fase atual
Refinamento área por área, após o MVP. **Etapas 1-7 concluídas.** 7 nichos no padrão de ouro.

Próxima: **Etapa 8 — business** (já decidido pelo usuário). Fecha os "sérios".

## ✅ Nichos no padrão de ouro (7 de 17)
- **dev** (E1), **client** (E2), **design** (E3), **narrative** (E4), **research** (E5), **product** (E6), **marketing** (E7).
- **Faltam (10):** business (E8, próximo), game, pixel, brainstorm, music, rpg, cuisine, animation, comics + custom (custom é gerador, não precisa).

## 🎯 Próximos passos
1. **Etapa 8 — business** (métricas, estratégia, finanças, modelo de negócio). Ritual padrão: pesquisa do domínio → projetar → construir → validar (jsdom 17/17) → publicar + CHANGELOG/STATUS.
2. Depois de business, começam os **criativos**: game, music, rpg, cuisine, animation, comics, pixel, brainstorm.
3. Aplicar ao próprio projeto as melhorias transversais que surgirem.

## 🆕 Funcionalidades recentes do kit
- **Afixo nos downloads (v1.9.0):** prefixo/sufixo opcional nos nomes de arquivo (aba Templates). Padrão inalterado.
- **9 princípios universais** na fundação; CLAUDE.md gerado separado das Instruções.

## 🔧 Pendências e ideias em análise
- [ ] **i-N3 parte A** (canal de atualização do kit / "backdoor" de ingestão de novas regras): avaliar — provavelmente resolve-se com uma seção no CLAUDE.md gerado ("se o usuário trouxer um arquivo de atualização do kit, aplique as novas regras"). A discutir.
- [ ] **i-N2** (segurança de dados pessoais/sensíveis): adiada para análise longa com pesquisa. Tensão: não estragar a captura de informação útil.
- [ ] **Revisar a qualidade das Instruções geradas** — pesquisa + análise pendente (o usuário pediu: confirmar se estão polidas/eficientes, já que não precisam de estrutura rebuscada, só que o Claude entenda).
- [ ] Atualizar README/PLANNING quando a maioria dos nichos estiver no padrão (faltarão poucos após business).
- [ ] **GitHub:** subir a v1.9.0 (marketing v2 + afixo). Esperar a sincronização do Projeto antes de conferir.

## 📁 Padrão de ouro consolidado
- Arquivo-âncora (visão/sistema/bíblia/marca) + ângulo próprio do nicho + armadilhas/continuidade.
- Decisões registradas (DEC); histórico que cresce; STATUS rolante.
- Núcleo enxuto + opcionais marcados.
- Prompts A-F universais + 6 G-L específicos das tarefas reais.
- Behaviors derivados de pesquisa + caso real.

## 🗂 Convenções do projeto
- Entrega: arquivos completos em outputs/meta; o usuário organiza no repo (raiz, não meta/).
- Commit ao final no formato comando-completo (git commit -m "..." \\ -m "..."), pronto para colar.
- pt-BR em tudo, inclusive comentários de código.

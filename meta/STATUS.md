# STATUS — Kit de Contexto Universal — 2026-05-30

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).

## Fase atual
Refinamento área por área, após o MVP. **Etapas 1-8 concluídas. TODOS os 8 nichos "sérios" estão no padrão de ouro.**

Próxima: **Etapa 9 — primeiro nicho CRIATIVO.**

## ✅ Nichos no padrão de ouro (8 de 17)
- **dev** (E1), **client** (E2), **design** (E3), **narrative** (E4), **research** (E5), **product** (E6), **marketing** (E7), **business** (E8).
- **Faltam — os criativos (8):** game, pixel, brainstorm, music, rpg, cuisine, animation, comics + custom (gerador, não precisa de aprofundamento).

## 🎯 Próximos passos
1. **Etapa 9 — escolher o primeiro criativo.** Candidatos: **game** (game design/sistemas — já tem base decente), **music** (composição/produção), **rpg** (mesa/campanha), **cuisine** (receitas/cardápio — há caso real The Brazilian House), **animation**, **comics**, **pixel** (pixel art), **brainstorm** (ideação — é o nicho do próprio kit). A decidir com o usuário.
2. Manter o ritual: pesquisa do domínio → projetar → construir isolado → validar (jsdom 17/17) → publicar + CHANGELOG/STATUS.
3. Os criativos podem ter dinâmica diferente dos sérios (menos "decisão/risco", mais "exploração/ofício") — adaptar o padrão, não copiar cegamente.

## 🆕 Funcionalidades recentes do kit
- **Afixo nos downloads (v1.9.0):** prefixo/sufixo opcional nos nomes de arquivo. Padrão inalterado.
- **9 princípios universais**; CLAUDE.md gerado separado das Instruções.
- **Regra de commit corrigida para CMD Windows** (comando numa linha, -m repetido).

## 🔧 Pendências e ideias em análise (em IDEIAS.md)
- [ ] **i-N3 parte A** (canal de atualização do kit): provavelmente uma seção no CLAUDE.md gerado. A discutir.
- [ ] **i-N2** (segurança de dados pessoais): adiada para análise longa.
- [ ] **i-N5** (comandos de terminal sensíveis ao SO): generalizar para nichos com terminal (dev). Avaliar campo de SO no builder.
- [ ] **Revisar a qualidade das Instruções geradas** — o usuário pediu: confirmar se estão polidas/eficientes (sem estrutura rebuscada, mas claras). Pesquisa + análise pendente.
- [ ] Atualizar README/PLANNING quando os criativos avançarem (a maioria já está no padrão).
- [ ] **GitHub:** subir a v1.10.0 (business + correção do commit).

## 📁 Padrão de ouro consolidado
- Arquivo-âncora (visão/sistema/bíblia/marca/contexto) + ângulo próprio do nicho + armadilhas/continuidade.
- Decisões registradas (DEC); histórico que cresce; STATUS rolante.
- Núcleo enxuto + opcionais marcados.
- Prompts A-F universais + 6 G-L específicos das tarefas reais.
- Behaviors derivados de pesquisa + caso real.

## 🗂 Convenções do projeto
- Entrega: arquivos completos em outputs/meta; o usuário organiza no repo (raiz).
- Commit ao final: comando completo p/ CMD Windows (uma linha, -m repetido), pronto para colar.
- pt-BR em tudo, inclusive comentários de código.

# STATUS — Kit de Contexto Universal — 2026-05-30

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).

## Fase atual
🏁 **Refinamento área por área COMPLETO.** As 16 etapas de aprofundamento de nicho foram concluídas. Todos os 16 nichos de conteúdo estão no padrão de ouro.

Próxima fase: **consolidação e pendências** (sem mais nichos a aprofundar).

## ✅ Nichos no padrão de ouro (16 de 16 — todos os de conteúdo)
- **Sérios (8):** dev (E1), client (E2), design (E3), narrative (E4), research (E5), product (E6), marketing (E7), business (E8).
- **Criativos (8):** game (E9), pixel (E10), music (E11), rpg (E12), cuisine (E13), animation (E14), comics (E15), **brainstorm (E16 — o fechamento)**.
- **custom:** é o gerador de nichos sob medida; não precisa de aprofundamento (fica como está).

## 🎯 Próximos passos (consolidação)
1. **Revisar README/PLANNING** — atualizar para refletir que todos os nichos estão no padrão de ouro (estavam desatualizados desde o MVP).
2. **Revisar a qualidade das Instruções geradas** — o usuário pediu: confirmar se estão polidas/eficientes (claras sem serem rebuscadas). Pesquisa + análise pendente.
3. **i-N3 parte A** (canal de atualização do kit / ingestão de novas regras em conversas que já usam o kit): avaliar — provavelmente uma seção no CLAUDE.md gerado.
4. **i-N2** (segurança de dados pessoais/sensíveis): a análise longa que o usuário quer fazer com calma.
5. **Reagrupar narrative** (cosmético): hoje group "literary"; é criativo. Só afeta tema visual.
6. **GitHub:** subir a v1.18.0 (brainstorm — fechamento).

## 🆕 Funcionalidades do kit (consolidadas nesta jornada)
- **Afixo nos downloads (v1.9.0):** prefixo/sufixo opcional nos nomes de arquivo. Padrão inalterado.
- **Seletor de SO (v1.11.0):** Windows-CMD/PowerShell/macOS/Linux; injeta sintaxe de comando certa em Instruções e CLAUDE.md.
- **fix selects do topbar (v1.11.1):** renderTopbar aceita `options:` e `opts:`; teste de topbar no ritual.
- **9 princípios universais** na fundação; CLAUDE.md gerado separado das Instruções; commit no formato CMD Windows.

## 📁 Padrão de ouro consolidado (o que cada nicho tem)
- Arquivo-âncora (visão/sistema/bíblia/conceito) + ângulo próprio do nicho + armadilhas/continuidade.
- Núcleo enxuto + opcionais marcados; decisões registradas; histórico que cresce; STATUS rolante.
- 12 prompt cards (6 A-F universais + 6 G-L específicos das tarefas reais).
- Behaviors derivados de pesquisa de domínio (com citações no histórico).
- Criativos: forte ênfase em "explora/critica/orienta — o criador executa/decide" (e, onde cabe, "não ouço/não provo/não desenho — você julga o que só o sentido alcança").

## 🗂 Convenções do projeto
- Entrega: arquivos completos em outputs/meta; o usuário organiza no repo (raiz).
- Commit ao final: comando completo p/ CMD Windows (uma linha, -m repetido), pronto para colar.
- pt-BR em tudo, inclusive comentários de código.
- Ritual de nicho (caso surja um novo): pesquisa do domínio → projetar → construir isolado → validar (node + jsdom 17/17) → publicar + CHANGELOG/STATUS → commit.

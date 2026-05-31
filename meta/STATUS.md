# STATUS — Kit de Contexto Universal — 2026-05-30

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).

## Fase atual
Refinamento área por área, após o MVP. **Etapas 1-9 concluídas.** 9 nichos no padrão de ouro (8 sérios + game design).

Próxima: **Etapa 10 — próximo criativo.**

## ✅ Nichos no padrão de ouro (9 de 17)
- Sérios: **dev, client, design, narrative, research, product, marketing, business** (E1-E8).
- Criativos: **game** (E9).
- **Faltam — criativos (7):** pixel, music, rpg, cuisine, animation, comics + **brainstorm** (reservado para ser o ÚLTIMO, fechamento poético) + custom (gerador, não precisa).

## 🎯 Próximos passos
1. **Etapa 10 — próximo criativo.** Favoritos do usuário já feitos: dev✓, game✓. Resta o 3º favorito: **pixel art** — forte candidato. Outros: music, rpg, cuisine (tem caso real The Brazilian House), animation, comics. **brainstorm fica por último.**
2. Manter o ritual: pesquisa do domínio → projetar → construir isolado → validar (jsdom 17/17) → publicar + CHANGELOG/STATUS.
3. Padrão dos criativos: tende a "explora/o criador decide" + ofício + anti-scope, menos "decisão/risco/métrica".

## 🆕 Funcionalidades recentes do kit
- **fix selects do topbar (v1.11.1):** Gênero/Engine/Fase apareciam vazios — renderTopbar agora aceita `options:` e `opts:`; idioma default corrigido (pt-BR→pt). Teste de topbar adicionado ao ritual.
- **Seletor de SO (v1.11.0):** Windows-CMD/PowerShell/macOS/Linux no builder; injeta sintaxe de comando certa nas Instruções e CLAUDE.md.
- **Afixo nos downloads (v1.9.0):** prefixo/sufixo opcional. Padrão inalterado.
- **9 princípios universais**; CLAUDE.md gerado separado das Instruções; commit no formato CMD Windows.

## 🔧 Pendências e ideias em análise (em IDEIAS.md)
- [ ] **i-N3 parte A** (canal de atualização do kit): provavelmente uma seção no CLAUDE.md gerado. A discutir.
- [ ] **i-N2** (segurança de dados pessoais): adiada para análise longa.
- [ ] **Revisar a qualidade das Instruções geradas** — o usuário pediu: confirmar se estão polidas/eficientes. Pesquisa + análise pendente.
- [ ] **Reagrupar narrative** (cosmético): hoje group "literary"; é criativo, não "sério". Só afeta tema visual. Avaliar ao mexer nos criativos.
- [ ] Atualizar README/PLANNING quando os criativos avançarem.
- [ ] **GitHub:** subir a v1.11.1 (game + seletor de SO + fix dos selects do topbar).

## 📁 Padrão de ouro consolidado
- Arquivo-âncora (visão/sistema/bíblia/marca/contexto/experiência) + ângulo próprio do nicho + armadilhas/continuidade.
- Decisões registradas (DEC); histórico que cresce; STATUS rolante.
- Núcleo enxuto + opcionais marcados.
- Prompts A-F universais + 6 G-L específicos das tarefas reais.
- Behaviors derivados de pesquisa + caso real.

## 🗂 Convenções do projeto
- Entrega: arquivos completos em outputs/meta; o usuário organiza no repo (raiz).
- Commit ao final: comando completo p/ CMD Windows (uma linha, -m repetido), pronto para colar.
- pt-BR em tudo, inclusive comentários de código.

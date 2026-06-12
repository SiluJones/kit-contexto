# ROADMAP — Kit de Contexto Universal

> Plano deliberado de evolução, em fases. Opcional por natureza (nem todo projeto tem direção de médio prazo) — aqui vale porque há decisões grandes em aberto. O QUE já saiu vive no CHANGELOG; o AGORA no STATUS; o PORQUÊ no DECISOES; as IDEIAS no IDEIAS. Este arquivo conecta tudo numa direção.

> **Criado em 2026-06-07.** Primeira versão. Consolida o que já foi feito (Fases 0–2) e organiza o que está por decidir/fazer (Fases 3–5 + Futuro), a partir das discussões desta sessão.

> **Mudanças nesta revisão (v1.27.1):** FIX-004 (chips de Cliente/Narrativa) consertado e validado — ver CHANGELOG. A Fase 3 ganhou diretrizes novas a redigir (i-N18/19/20, agora também i-N21/22 com texto proposto) e a Fase 5 ganhou ideias maiores (i-N21 feedback — fluxo desenhado; i-N22 — válvula proposta; **i-N23** melhorias do Pixel vindas do piloto; **i-N24** multi-projeto, 4 frentes do mesmo jogo). Itens concluídos seguem visíveis como ✅.

> **Mudanças na revisão anterior (v1.27.0):** a Fase 3 avançou — os itens 1 (propagar P12) e 2 (decidir o princípio de pesquisa/refutação, i-N17) foram **concluídos**; o antigo item 3 (mount/RAG, D-018) passou a ser o próximo. Ver D-020, D-021 e CHANGELOG v1.27.0.

---

## ✅ Fase 0 — MVP + fundação (CONCLUÍDA)
- 18 nichos em página única (v1.0.0); heros distintos; Custom como construtor real; theming por CSS vars; persistência em localStorage.
- Fundação transversal: princípios universais (chegaram a 11; **hoje 13** com P12/P13 — v1.27.0), CLAUDE.md separado das Instruções, filosofia rolante/estável/cresce, regras de higiene, tabela de gatilhos, UPDATE_PROTOCOL. (D-012; v1.1.x–v1.4.0.)

## ✅ Fase 1 — Refinamento área por área (CONCLUÍDA)
- Os 16 nichos de conteúdo (8 sérios + 8 criativos) reconstruídos no "padrão de ouro", cada um com pesquisa de domínio própria. (D-013; v1.5.0–v1.18.0.)
- Transversais acumulados: afixo de download (v1.9.0), seletor de SO (v1.11.0), commit ao final + canal de atualização (v1.19.0), privacidade (v1.20.0), protocolo de transferência contexto/RAG + handoff (v1.21.0), mount/ferramenta de código + diretrizes refinadas (v1.22.0/v1.23.0).
- Achados de ambiente: D-015/D-016/D-017/**D-018** (mount só por upload direto, não pelo conector do GitHub).

## ✅ Fase 2 — Custom Inteligente → Custom unificado (CONCLUÍDA)
- Composição assistida (concatenação + dedup visível + checagem de conflito) — v1.24.0; conserto do bug A + re-entrância (FIX-001).
- Fluxo de preset (Ativar de verdade, editar/trocar, nome pré-preenchido) — v1.25.0 (FIX-002); corpo dos prompts preservado — v1.25.1 (FIX-003).
- **Unificação** num só card `custom` (composição no topo + builder abaixo) + atalho "Nichos salvos" na barra superior + **granularidade** por nicho — v1.26.0 (**D-019**, supersede a parte de D-014 sobre 2 cards).

---

## ▶ Fase 3 — Higiene & consistência (EM ANDAMENTO — barato, alto valor)
Itens de código pequenos e de doc, sem arquitetura nova.

**✅ Concluído (v1.27.1):**
- ✅ **FIX-004** — chips de Cliente/Narrativa não selecionáveis (conversor tratava par como string). Conserto de 1 linha + teste de regressão de chips no harness. (Ver CHANGELOG/DECISOES.)

**✅ Concluído (v1.27.0):**
- ✅ **P12 (higiene ao encolher) propagado à ferramenta** — 12º item de `BEHAVIORS_BASE` (`shrink_hygiene`), aparece no CLAUDE.md gerado de todos os nichos. Re-validado 17/17. (DEC D-020.)
- ✅ **Princípio de rigor em pesquisa + refutação decidido** (i-N17) — criado o princípio próprio **P13** (`research_refute`), 13º item de `BEHAVIORS_BASE`, em vez de reforçar P1/P7. (DEC D-021.)

**Restante:**
1. **Redigir e embutir as diretrizes novas no CLAUDE.md gerado** (1 passada, re-validação 17/17): **i-N18** manifesto de achatamento (consultar `_MANIFEST.md`; sufixo `__pasta` = colisão; entregar pelo nome real — já vale para nós); **i-N19** verificar o estado real antes de repetir pendência de STATUS velho (refino de P8 + `UPDATE_PROTOCOL`); **i-N20** commit em 3 linhas + nota sobre `git add .`; **i-N21** gatilho «Feedback para o Kit» no IDEAS do piloto; **i-N22** válvula de desvio registrado. *i-N21/i-N22 aguardam o usuário validar a redação.* — *próximo; pode ir junto com o item 2.*
2. **Corrigir a orientação mount/RAG/anexo gerada pelo kit** (D-018) — o CLAUDE.md / "Tokens & Fluxos" ainda diz "tudo no Projeto + ferramenta de código → mount"; precisa refletir "só upload direto popula o mount; conector do GitHub = só RAG". Muda conteúdo em todos os nichos → re-validar 17/17.
3. **Aplicar o lote de feedback dos pilotos quando fechar** (i-N23: paleta global×bioma no ESTILO, prioridade visual interna no SPRITES, efeitos especiais no ANIMACAO, estado "aguardando design"; mais itens por vir das outras frentes). Gate: decisão do usuário de fechar o lote. Re-validar 17/17.
4. **Cosméticos:** MAPA.md ("17 prontos" → 16 de conteúdo + 1 construtor); reagrupar `narrative` (group literary → tema criativo); revisar README/PLANNING; revisar qualidade das Instruções geradas.

## ⏸ Fase 4 — Arquitetura (EM AVALIAÇÃO — não mexer sem decisão)
- **Refator modular** (i-N13): dados de nicho em JSON separados + núcleo central, vs. manter o HTML único (D-001).
- **Tensão central:** o produto é "1 arquivo, sem build, roda via `file://`/GitHub Pages". `fetch()` de JSON quebra via `file://`; build embutindo JSON reintroduz toolchain.
- **Caminho de menor arrependimento (se a dor de manutenção justificar):** modular **no repositório** + um **script simples de concatenação** que gera o `index.html` "bundled" para deploy (sem framework). Modular para desenvolver, 1 arquivo para distribuir — preserva D-001 no produto final.
- **Gatilho de decisão:** quando editar/adicionar nicho começar a doer de verdade. Até lá, fica em avaliação.

## 🌱 Fase 5 — Novas capacidades (IDEIAS a maturar)
- **Guias/tutoriais/wikis** (i-N14): nicho "Aprendizado/Guia" (trilhas, fontes/cursos verificados, progresso, glossário) — começar como nicho dentro do kit; virar ferramenta dedicada só se o fluxo pedir. Conecta a "Educação" (NICHOS-CANDIDATOS, nº1). Exige rigor de fonte (casa com i-N17).
- **Auto-aplicação de patches** (i-N15) + **entrega por diff** (i-N16): ferramenta externa (projeto do usuário) que aplica patches que o Claude gera; no kit, um modo "auto" que faz o Claude **entregar diffs** (em vez de arquivos inteiros) quando há a ferramenta que aplica — economiza output tokens. Avaliar formato (apply_patch vs unified diff) e segurança (âncoras/validação). Reconciliar com a regra "arquivo inteiro" (só vale diff quando algo aplica automaticamente, não o usuário colando à mão).
- **Comando/template de feedback** (i-N21 — **fluxo desenhado, aguarda validação**): no piloto, gatilho leve grava em «Feedback para o Kit» (no IDEAS do piloto); o usuário transporta a seção; o kit roteia para IDEIAS/DECISOES/ROADMAP. Sem comparação contra template (descartada). Vira diretriz do item 1 da Fase 3 quando validada.
- **Estrutura flexível / válvula de desvio registrado** (i-N22 — **texto proposto, aguarda validação**): "templates são ponto de partida, não contrato; adapte e **registre** o desvio (DECISIONS + Feedback para o Kit); desviar sem registrar é o erro". O cardápio curado de módulos por grupo vira evolução de médio prazo alimentada pelos desvios. Risco medido continua valendo: doc gerado por LLM piorou sucesso em 5/8 cenários por duplicação — manter a trava "não duplicar o que a estrutura cobre".
- **Protocolo multi-projeto** (i-N24): 4 projetos do kit para o mesmo jogo (game design, pixel art, enredo, música) precisam de sincronismo entre frentes (ex.: estado "aguardando design"). Candidatos do mais barato ao mais caro: convenção de estado + bloco "Dependências entre frentes" no STATUS; bloco de handoff padronizado; projeto-hub (provável exagero). Esperar a dor concreta dos pilotos.

## 🔭 Futuro (adiado de propósito)
- **Nichos novos** (NICHOS-CANDIDATOS.md): Educação & Cursos (nº1), depois Desenvolvimento Pessoal/Journaling (sensível), Jurídico/Podcast/Tradução.
- **spec-kit para dev/game** (i-N7): quando houver mais feedback de uso — análise do que do Spec-Driven Development melhora os processos desses nichos.
- **Evoluções de polish** (do CHANGELOG "possíveis v1.1/v1.2"): export/import de preset em JSON (i11), tema claro (i9), tradução EN (i10), PDF dos templates (i13), drag-and-drop no Custom (i20), carimbo de versão nos downloads (i-N10). Nada prometido.

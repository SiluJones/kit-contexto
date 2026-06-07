# ROADMAP — Kit de Contexto Universal

> Plano deliberado de evolução, em fases. Opcional por natureza (nem todo projeto tem direção de médio prazo) — aqui vale porque há decisões grandes em aberto. O QUE já saiu vive no CHANGELOG; o AGORA no STATUS; o PORQUÊ no DECISOES; as IDEIAS no IDEIAS. Este arquivo conecta tudo numa direção.

> **Criado em 2026-06-07.** Primeira versão. Consolida o que já foi feito (Fases 0–2) e organiza o que está por decidir/fazer (Fases 3–5 + Futuro), a partir das discussões desta sessão.

---

## ✅ Fase 0 — MVP + fundação (CONCLUÍDA)
- 18 nichos em página única (v1.0.0); heros distintos; Custom como construtor real; theming por CSS vars; persistência em localStorage.
- Fundação transversal: princípios universais (chegaram a 11), CLAUDE.md separado das Instruções, filosofia rolante/estável/cresce, regras de higiene, tabela de gatilhos, UPDATE_PROTOCOL. (D-012; v1.1.x–v1.4.0.)

## ✅ Fase 1 — Refinamento área por área (CONCLUÍDA)
- Os 16 nichos de conteúdo (8 sérios + 8 criativos) reconstruídos no "padrão de ouro", cada um com pesquisa de domínio própria. (D-013; v1.5.0–v1.18.0.)
- Transversais acumulados: afixo de download (v1.9.0), seletor de SO (v1.11.0), commit ao final + canal de atualização (v1.19.0), privacidade (v1.20.0), protocolo de transferência contexto/RAG + handoff (v1.21.0), mount/ferramenta de código + diretrizes refinadas (v1.22.0/v1.23.0).
- Achados de ambiente: D-015/D-016/D-017/**D-018** (mount só por upload direto, não pelo conector do GitHub).

## ✅ Fase 2 — Custom Inteligente → Custom unificado (CONCLUÍDA)
- Composição assistida (concatenação + dedup visível + checagem de conflito) — v1.24.0; conserto do bug A + re-entrância (FIX-001).
- Fluxo de preset (Ativar de verdade, editar/trocar, nome pré-preenchido) — v1.25.0 (FIX-002); corpo dos prompts preservado — v1.25.1 (FIX-003).
- **Unificação** num só card `custom` (composição no topo + builder abaixo) + atalho "Nichos salvos" na barra superior + **granularidade** por nicho — v1.26.0 (**D-019**, supersede a parte de D-014 sobre 2 cards).

---

## ▶ Fase 3 — Higiene & consistência (PRÓXIMA — barato, alto valor)
Itens de código pequenos e de doc, sem arquitetura nova:
1. **Propagar P12 (higiene ao encolher) para a ferramenta** — virar o 12º item de `BEHAVIORS_BASE` (aparece no CLAUDE.md gerado de todos os nichos). Re-validar 17/17. (DEC D-020.) — *o mais direto; começar por aqui.*
2. **Decidir o princípio de rigor em pesquisa + refutação** (i-N17): reforçar P7/P1 ou criar um princípio próprio; aplicar na mesma passada de `BEHAVIORS_BASE`.
3. **Corrigir a orientação mount/RAG/anexo gerada pelo kit** (D-018) — o CLAUDE.md / "Tokens & Fluxos" ainda diz "tudo no Projeto + ferramenta de código → mount"; precisa refletir "só upload direto popula o mount; conector do GitHub = só RAG". Muda conteúdo em todos os nichos → re-validar 17/17.
4. **Cosméticos:** MAPA.md ("17 prontos" → 16 de conteúdo + 1 construtor); reagrupar `narrative` (group literary → tema criativo); revisar README/PLANNING; revisar qualidade das Instruções geradas.

## ⏸ Fase 4 — Arquitetura (EM AVALIAÇÃO — não mexer sem decisão)
- **Refator modular** (i-N13): dados de nicho em JSON separados + núcleo central, vs. manter o HTML único (D-001).
- **Tensão central:** o produto é "1 arquivo, sem build, roda via `file://`/GitHub Pages". `fetch()` de JSON quebra via `file://`; build embutindo JSON reintroduz toolchain.
- **Caminho de menor arrependimento (se a dor de manutenção justificar):** modular **no repositório** + um **script simples de concatenação** que gera o `index.html` "bundled" para deploy (sem framework). Modular para desenvolver, 1 arquivo para distribuir — preserva D-001 no produto final.
- **Gatilho de decisão:** quando editar/adicionar nicho começar a doer de verdade. Até lá, fica em avaliação.

## 🌱 Fase 5 — Novas capacidades (IDEIAS a maturar)
- **Guias/tutoriais/wikis** (i-N14): nicho "Aprendizado/Guia" (trilhas, fontes/cursos verificados, progresso, glossário) — começar como nicho dentro do kit; virar ferramenta dedicada só se o fluxo pedir. Conecta a "Educação" (NICHOS-CANDIDATOS, nº1). Exige rigor de fonte (casa com i-N17).
- **Auto-aplicação de patches** (i-N15) + **entrega por diff** (i-N16): ferramenta externa (projeto do usuário) que aplica patches que o Claude gera; no kit, um modo "auto" que faz o Claude **entregar diffs** (em vez de arquivos inteiros) quando há a ferramenta que aplica — economiza output tokens. Avaliar formato (apply_patch vs unified diff) e segurança (âncoras/validação). Reconciliar com a regra "arquivo inteiro" (só vale diff quando algo aplica automaticamente, não o usuário colando à mão).

## 🔭 Futuro (adiado de propósito)
- **Nichos novos** (NICHOS-CANDIDATOS.md): Educação & Cursos (nº1), depois Desenvolvimento Pessoal/Journaling (sensível), Jurídico/Podcast/Tradução.
- **spec-kit para dev/game** (i-N7): quando houver mais feedback de uso — análise do que do Spec-Driven Development melhora os processos desses nichos.
- **Evoluções de polish** (do CHANGELOG "possíveis v1.1/v1.2"): export/import de preset em JSON (i11), tema claro (i9), tradução EN (i10), PDF dos templates (i13), drag-and-drop no Custom (i20), carimbo de versão nos downloads (i-N10). Nada prometido.

# STATUS — Kit de Contexto Universal — 2026-06-03

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).
> Versão atual publicada: **v1.22.0**. Índice em ~519 KB. Teste: 17/17 nichos, 0 erros JS.

## Fase atual
🏁 **Refinamento área por área COMPLETO** + ideias transversais implementadas (commit ao final, canal de atualização, privacidade e agora **fidelidade/contexto + plano de transferência**). Todos os 16 nichos de conteúdo estão no padrão de ouro.

**PRÓXIMO TRABALHO (decidido pelo usuário): o CUSTOM INTELIGENTE.** Ver a seção dedicada abaixo — é o item nº1. Esta sessão (v1.21.0) foi um desvio pedido pelo usuário para resolver uma lacuna de conhecimento sobre contexto/RAG/persistência antes de mexer no custom.

## ✅ Nichos no padrão de ouro (16 de 16 de conteúdo)
- **Sérios (8):** dev, client, design, narrative, research, product, marketing, business.
- **Criativos (8):** game, pixel, music, rpg, cuisine, animation, comics, brainstorm.
- **custom:** gerador de nicho sob medida (formulário em branco — o "Blank"). Funciona, mas será complementado pelo Custom Inteligente.

## 🎯 PRÓXIMO TRABALHO Nº1 — Custom Inteligente (já aprovado pelo usuário)

**O quê:** um SEGUNDO nicho de construção (mantendo o custom atual como "Blank"), que parte da composição assistida de nichos existentes.

**Arquitetura aprovada (D-014):**
- Mantém **2 nichos de construção** (não 3): (1) **Custom (Blank)** = o atual, página em branco; (2) **Custom Inteligente** = novo.
- O Custom Inteligente abre com uma **fileira de chips dos 16 nichos**. Marcar um ou mais **importa o material (CONCATENA, não funde mágico)**: junta contextFiles, behaviors e promptsExtra, já preenchidos e editáveis.
- **Deduplicação VISÍVEL** dos arquivos repetidos (STATUS/LOG que todos têm) e behaviors muito parecidos.
- **Sub-painel = granularidade, não mecânica nova:** botão "escolher peças" por nicho marcado (importar inteiro vs. item a item). NÃO é uma terceira opção.
- **Checagem de conflito (spec-kit-inspired):** avisar sobre behaviors contraditórios; sinalizar, não bloquear.
- Cai no **motor existente** (mergeCustom + presets em localStorage) → editar e salvar como preset.
- **NÃO fazer fusão automática opaca.** Composição assistida e revisável.

**Risco:** baixo-médio. UI nova sobre motor existente. Fazer por partes, validando 17/17 a cada passo: (1) importação com concatenação + dedup; (2) sub-painel de seleção fina; (3) checagem de conflito.

**Onde está o custom hoje no código:** `NICHES.custom` tem `isBuilder:true`. Em `renderBuilder`, há `if(niche.isBuilder && !STATE.customPreset)` que chama `renderCustomForm()`. Há `mergeCustom` e `LS_PRESETS` (localStorage) já implementados. O formulário atual é em branco — é o que o usuário achou intimidante.

## 🎯 Outras pendências (sem urgência)

1. **Revisar README/PLANNING** — README recebeu nesta sessão a explicação de contexto/RAG/anexos e o plano de transferência (alinhado ao que entrou na UI). PLANNING ainda pendente de uma revisão geral pós-MVP.
2. **Revisar a qualidade das Instruções geradas** — confirmar se estão polidas/eficientes. Pendente.
3. **Reagrupar narrative** (cosmético): hoje `group:"literary"`; é criativo. Só afeta tema visual.
4. **Nichos novos (FUTURO, adiados de propósito):** ver `NICHOS-CANDIDATOS.md`. Prioridade se expandir: Educação & Cursos (nº1), Desenvolvimento Pessoal/Journaling (sensível), depois Jurídico/Podcast/Tradução.
5. **spec-kit para dev/game (FUTURO):** quando o usuário tiver mais feedback de uso, pedirá análise do que do spec-kit torna esses nichos mais completos.
6. **GitHub:** subir a v1.21.0 (e confirmar que v1.17→v1.20 subiram). Lembrete: a sincronização do GitHub é manual; para o que precisa estar fresco no Projeto, preferir upload direto.

## 🆕 Funcionalidades do kit (acumuladas — todas validadas)
- **Afixo nos downloads (v1.9.0):** prefixo/sufixo opcional. Padrão = nome original.
- **Seletor de SO (v1.11.0):** Windows-CMD/PowerShell/macOS/Linux; injeta sintaxe de comando em Instruções e CLAUDE.md.
- **fix selects do topbar (v1.11.1):** renderTopbar aceita `options:` e `opts:`; idioma corrigido (pt-BR→pt).
- **Commit ao final + canal de atualização (v1.19.0):** no UPDATE_PROTOCOL (todos os nichos).
- **Privacidade i-N2 (v1.20.0):** relevância + marcação, não censura.
- **Fidelidade/contexto + plano de transferência (v1.21.0):** no UPDATE_PROTOCOL (todos os nichos) + tela "Tokens & Fluxos". Dois canais (Projeto/RAG vs. conversa), regra anti-arquivo-falso, e o plano de onde colocar cada arquivo + prompt de início para a próxima conversa.
- **9 princípios universais** na fundação; CLAUDE.md separado das Instruções.

## 📁 Ritual de nicho (se surgir um novo OU para o custom inteligente)
1. Estudar (ler nicho atual + pesquisa web do domínio, 2-4 buscas com citações). 2. Projetar (núcleo enxuto + opcionais; behaviors; prompts G-L; triggersExtra). 3. Construir objeto isolado em `/home/claude/<nicho>_v2.js`. 4. Validar isolado. 5. Splice no index via marcadores de comentário. 6. Validar: extrair `<script>`, `node --check`, balanceamento de tags, jsdom 17/17. NUNCA publicar sem 17/17 e 0 erros. 7. Publicar + CHANGELOG (vX.Y.Z no topo) + STATUS (reescrito) + DECISOES (cresce, D-NNN). 8. present_files + git commit (formato CMD Windows).

## ⚠️ Nota de fidelidade para o nosso próprio desenvolvimento (dogfooding) — CORRIGIDA na v1.22.0
O que importa não é "está em RAG?", é **"tenho o `index.html` COMPLETO por algum canal?"**. **Verificado nesta sessão:** com a ferramenta de código ligada, os arquivos do Projeto ficam montados em `/mnt/project/` e eu os leio INTEIROS — li o `index.html` completo (518 KB, byte-idêntico) com o Projeto em "Modo de pesquisa" (RAG). Ou seja, o RAG **não** impede a leitura pelo mount. Então: o caminho limpo é deixar o index (e tudo) no Projeto + ligar a ferramenta de código, e eu leio/edito pelo mount, sem anexar. Anexar só é necessário no chat comum (sem ferramenta de código) ou se o arquivo não estiver no Projeto. (Correção do que esta nota dizia antes — "precisa anexar porque está em RAG" — que conflava os dois mecanismos. Detalhe em CONTEXT.md e D-016.)

## 🗂 Convenções
- pt-BR em tudo, inclusive comentários de código. Nomes de template profissionais.
- Entrega: arquivos completos em outputs/meta; o usuário organiza no repo.
- Commit ao final: comando completo p/ CMD Windows (UMA linha, `-m` repetido), pronto para colar.
- Usuário no CMD do Windows (C:\Users\alexk\Arquiteturas\kit-contexto).

## 💬 Última sessão (2026-06-03)
Refino do protocolo de transferência (v1.22.0), em cima da v1.21.0. O usuário trouxe duas conversas (`Tentativa_1.md`, `Analisada.md`) que expuseram uma **divergência** e atritos entre diretrizes. **Descoberta verificada empiricamente:** o `/mnt/project/` é um mount lido INTEIRO pela ferramenta de código mesmo em RAG (li o index.html completo, byte-idêntico, com o Projeto em "Modo de pesquisa"). Corrigida a seção de transferência (que conflava RAG com "não consigo ler") na ferramenta + tela "Tokens & Fluxos". Diretrizes refinadas (BEHAVIORS_BASE 9→11): P2 esclarecido, P3 + "sem rodeios", P8 + anti-inferir, **P10 Cadência**, **P11 Não regride/mistura versões**. Registrado **D-016**. Validado 17/17, 0 erros. **Próximo passo: começar o Custom Inteligente** (etapa 1: importação com concatenação + dedup) **numa conversa NOVA**, com a **ferramenta de código ligada** e tudo no Projeto — assim eu leio o index do mount, sem anexar. (Esta conversa já está longa/compactada; o custom vale começar fresco — e será um bom teste do novo fluxo de mount.)

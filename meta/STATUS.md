# STATUS — Kit de Contexto Universal — 2026-06-02

> Rolante: só o agora + próximos passos. Item resolvido sai daqui (vai pro CHANGELOG).
> Versão atual publicada: **v1.20.0**. Índice em ~513 KB. Teste: 17/17 nichos, 0 erros JS.

## Fase atual
🏁 **Refinamento área por área COMPLETO** + ideias transversais implementadas (commit ao final, canal de atualização, privacidade). Todos os 16 nichos de conteúdo estão no padrão de ouro.

**PRÓXIMO TRABALHO (decidido pelo usuário para a próxima conversa): o CUSTOM INTELIGENTE.** Ver a seção dedicada abaixo — é o item nº1.

## ✅ Nichos no padrão de ouro (16 de 16 de conteúdo)
- **Sérios (8):** dev, client, design, narrative, research, product, marketing, business.
- **Criativos (8):** game, pixel, music, rpg, cuisine, animation, comics, brainstorm.
- **custom:** gerador de nicho sob medida (formulário em branco — o "Blank"). Funciona, mas será complementado pelo Custom Inteligente.

## 🎯 PRÓXIMO TRABALHO Nº1 — Custom Inteligente (já aprovado pelo usuário)

**O quê:** um SEGUNDO nicho de construção (mantendo o custom atual como "Blank"), que parte da composição assistida de nichos existentes.

**Arquitetura aprovada (decidida nesta conversa):**
- Mantém **2 nichos de construção** (não 3): (1) **Custom (Blank)** = o atual, página em branco, poder total; (2) **Custom Inteligente** = novo.
- O Custom Inteligente abre com uma **fileira de chips dos 16 nichos**. Marcar um ou mais **importa o material deles (CONCATENA, não funde mágico)**: junta contextFiles, behaviors e promptsExtra, já preenchidos e editáveis.
- **Deduplicação VISÍVEL:** STATUS.md e LOG-TEMPLATE.md (que todos têm) aparecem como duplicados → mantém um, avisando. Idem behaviors muito parecidos.
- **Sub-painel = parte do mesmo fluxo, não mecânica separada.** É só o grau de granularidade: "importar nicho inteiro" (grosso) vs. "escolher peças item a item" (fino). Um botão "escolher peças" em cada nicho marcado abre o sub-painel de seleção fina. NÃO justifica uma terceira opção.
- **Checagem de conflito (inspirada no spec-kit):** ao montar, AVISAR sobre behaviors que se contradizem (ex.: "seja conciso" × "seja exaustivo"). Não bloquear — sinalizar.
- Resultado cai no **mesmo motor do custom atual** (mergeCustom, presets em localStorage já existem) -> editar e salvar como preset.
- **NÃO fazer fusão automática opaca** (o usuário concordou que é perigosa). Composição assistida e revisável é o caminho.

**Risco:** baixo-médio. É UI nova sobre motor que já existe. O risco real seria a fusão automática sem revisão — evitar. Fazer por partes, validando 17/17 a cada passo: (1) importação com concatenação + dedup; (2) sub-painel de seleção fina; (3) checagem de conflito.

**Onde está o custom hoje no código:** `NICHES.custom` tem `isBuilder:true`. Em `buildInstr`/render, há `if(niche.isBuilder && !STATE.customPreset)` (~linha 6629) que chama `renderCustomForm()` (~linha 7230). Há `mergeCustom` e `LS_PRESETS` (localStorage) já implementados. O formulário atual é em branco (identidade + arquivos + behaviors + prompts, tudo manual) — é o que o usuário achou intimidante.

## 🎯 Outras pendências (sem urgência)

1. **Revisar README/PLANNING** — desatualizados desde o MVP. Os PLANNING-PART1/PART2 e "Projetando_com_o_Claude.md" foram garimpados nesta sessão: tudo de substancial já está no kit; o que faltava virou `NICHOS-CANDIDATOS.md`.
2. **Revisar a qualidade das Instruções geradas** — o usuário pediu: confirmar se estão polidas/eficientes (claras sem serem rebuscadas). Pesquisa + análise pendente. (Ainda não feito.)
3. **Reagrupar narrative** (cosmético): hoje `group:"literary"`; é criativo. Só afeta tema visual.
4. **Nichos novos (ideias FUTURAS, não agora — usuário concordou em adiar):** ver `NICHOS-CANDIDATOS.md`. Prioridade do assistente se um dia expandir: Educação & Cursos (nº1), Desenvolvimento Pessoal/Journaling (com cuidado por ser sensível), depois Jurídico/Podcast/Tradução.
5. **spec-kit para dev/game (FUTURO):** quando o usuário tiver mais feedback de uso dos nichos dev e game, ele vai pedir uma análise do que do spec-kit (https://github.com/github/spec-kit) pode tornar esses nichos mais completos. Anotado para o futuro.
6. **GitHub:** subir a v1.20.0 (e confirmar que as anteriores subiram — v1.17→v1.20 saíram em sequência nesta sessão).

## 🆕 Funcionalidades do kit (acumuladas — todas validadas)
- **Afixo nos downloads (v1.9.0):** prefixo/sufixo opcional. Padrão = nome original.
- **Seletor de SO (v1.11.0):** Windows-CMD/PowerShell/macOS/Linux; injeta sintaxe de comando em Instruções e CLAUDE.md.
- **fix selects do topbar (v1.11.1):** renderTopbar aceita `options:` e `opts:`; idioma corrigido (pt-BR->pt); teste de topbar no ritual.
- **Commit ao final + canal de atualização (v1.19.0):** no UPDATE_PROTOCOL (todos os nichos).
- **Privacidade i-N2 (v1.20.0):** relevância + marcação, não censura.
- **9 princípios universais** na fundação; CLAUDE.md separado das Instruções.

## 📁 Ritual de nicho (se surgir um novo OU para o custom inteligente)
1. Estudar (ler nicho atual + pesquisa web do domínio, 2-4 buscas com citações). 2. Projetar (núcleo enxuto + opcionais; behaviors; prompts G-L; triggersExtra). 3. Construir objeto isolado em `/home/claude/<nicho>_v2.js`. 4. Validar isolado (stub Node executando os `body` dos prompts). 5. Splice no index via marcadores de comentário. 6. Validar: extrair `<script>`, `node --check`, balanceamento de tags, jsdom 17/17. NUNCA publicar sem 17/17 e 0 erros. 7. Publicar + CHANGELOG (vX.Y.Z no topo) + STATUS (reescrito) + DECISOES (cresce, D-NNN). 8. present_files + git commit (formato CMD Windows).

## 🗂 Convenções
- pt-BR em tudo, inclusive comentários de código. Nomes de template profissionais.
- Entrega: arquivos completos em outputs/meta; o usuário organiza no repo (raiz, não meta/).
- Commit ao final: comando completo p/ CMD Windows (UMA linha, `-m` repetido), pronto para colar.
- Usuário no CMD do Windows (C:\Users\alexk\Arquiteturas\kit-contexto).

## 💬 Última sessão (2026-06-02)
Sessão de consolidação pós-refinamento. Implementado: commit-ao-final + canal de atualização (v1.19.0) e privacidade i-N2 (v1.20.0), todos transversais no UPDATE_PROTOCOL. Diagnosticado o custom (formulário em branco, sem herança de outros nichos) e ARQUITETADO o Custom Inteligente (acima) — aprovado pelo usuário para a PRÓXIMA conversa. Recuperados os nichos candidatos dos PLANNING (-> NICHOS-CANDIDATOS.md). Garimpados os 3 docs antigos (PLANNING-1/2 + Projetando): nada novo a integrar além do que já foi. Próximo passo óbvio: **começar o Custom Inteligente** (etapa 1: importação com concatenação + dedup).

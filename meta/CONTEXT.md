# CONTEXT.md — Kit de Contexto Universal

> O **passaporte** do projeto. Leia primeiro para se ambientar. Estável — muda pouco.
> Objetivo deste arquivo: uma nova conversa entende o projeto inteiro sem precisar de mais nada.

---

## O que é o projeto

O **Kit de Contexto Universal** é um **único arquivo `index.html`** (vanilla JS, sem build, sem dependências de runtime além de bibliotecas via CDN para o ZIP) que ajuda pessoas a **manter contexto entre conversas com o Claude**. O problema que resolve: conversas longas com IA ficam "papão de token" e, ao trocar de conversa, perde-se todo o contexto (decisões, ideias, estado do projeto).

A solução do kit: gerar **arquivos vivos** (`CONTEXT.md`, `STATUS.md`, `DECISÕES.md`, etc.) que o usuário sobe num Projeto do Claude.ai (ou anexa numa conversa) e que fazem a IA se ambientar instantaneamente. O kit oferece **17 nichos** (16 de conteúdo + 1 `custom` gerador) — cada um gera dois artefatos: as **Instruções do Projeto** e um **CLAUDE.md completo**, adaptados ao domínio.

O kit é, ele mesmo, uma aplicação da própria filosofia (dogfooding): este projeto é gerenciado pelos arquivos que ele prega.

## Stack e arquitetura

- **Um arquivo:** `index.html` (~513 KB na v1.20.0). HTML + CSS + JS inline. Sem framework, sem build step.
- **Hospedagem:** GitHub Pages — `silujones.github.io/kit-contexto/`. O usuário sobe manualmente o `index.html` (e os meta-docs) ao repositório `github.com/<user>/kit-contexto`.
- **Bibliotecas externas (CDN):** JSZip (para o "baixar pacote ZIP"). O resto é vanilla.
- **Persistência no browser:** o kit usa `localStorage` para presets do custom e estado (STATE/snapshot). ATENÇÃO: localStorage é proibido em artifacts do claude.ai, MAS aqui funciona porque o arquivo roda no GitHub Pages do usuário (site real), não como artifact. Ao TESTAR via jsdom isso é simulado.

### Estrutura do JS (mapa mental)
1. **Constantes de fundação** (topo do `<script>`): `LANGS` (idiomas — valor "pt", "en", "es", "other"), `BEHAVIORS_BASE` (9 princípios universais), `FILE_PHILOSOPHY`, `HYGIENE_RULES`, `TRIGGERS_BASE`, `UPDATE_PROTOCOL` (protocolo de atualização — agora inclui commit, canal de atualização e privacidade), `AFFIX` (afixo de download), `OSENV`/`OS_LABELS`/`OS_CMDNOTE` (seletor de SO).
2. **Objetos `NICHES.<id>`** — um por nicho. Cada um é um objeto grande com a forma descrita abaixo. Delimitados por comentários `/* ---------- NOME ---------- */`.
3. **Normalizadores** — `normNiche`, `normConventions`, `normBuilderSection`, `fileTag` (consolidado). Aceitam 2 formatos históricos de dados.
4. **Funções de render** — `renderTopbar` (aceita `opts` de pares E `options` de strings — corrigido na v1.11.1), `renderBehaviors`, `renderBuilder`, `renderCustomForm` (o formulário do custom), `updatePreview`, `buildInstr` (gera as Instruções), `buildClaudeMd` (gera o CLAUDE.md completo).
5. **Boot** — `boot()` no final, com try/catch que mostra banner de erro na página.

### Forma (shape) de cada nicho — objeto `NICHES.<id>`
```
{
  id, label, icon, group, category,            // metadados; group = tema visual (serif/literary/digital); category = core/creative
  cardColor, cardTags[], cardDesc,             // o card na tela de seleção
  intro:{ headline, lede, ctxBlurb, hero },    // a tela "Início" do nicho
  topbar:[ {id,label,placeholder?} | {id,label,type:"select",options:[...] | opts:[[v,l]], default?} ],
  behaviors:[ [id, titulo, descrição], ... ],  // os behaviors ESPECÍFICOS do nicho (somam aos 9 universais)
  builderSection:{ title, hint, items:[...] | groups:[...]/type:"chips" },  // o "Construir instrução"
  conventions:[ ... ] | true | false,          // bloco de convenções (true = naming/idioma default)
  triggersExtra:[ [evento, ação], ... ],        // gatilhos específicos (somam aos TRIGGERS_BASE)
  contextFiles:[ {name, cat, role, content}, ... ],  // os templates .md (cat: essencial/rolante/opcional/ref → vira tag)
  outputs:[ {key, name, role, active}, ... ],   // o que o assistente entrega como arquivo
  promptsExtra:[ {id, title, when, fill, fillLabel, body:(p,n)=>`...`}, ... ]  // os prompts G-L (6 específicos)
}
```
Cada nicho tem **12 prompt cards**: 6 universais (A-F) + 6 específicos (G-L). Os A-F são gerados pela fundação; os G-L vêm de `promptsExtra`.

### Os 9 princípios universais (BEHAVIORS_BASE — em todos os nichos)
1. Analisa antes de aceitar. 2. Não desperdiça tokens. 3. Direto e objetivo. 4. Admite incerteza. 5. Explica trade-offs. 6. Instruções sempre cuidadosas. 7. Estuda o domínio antes de estruturar. 8. Verifica antes de pedir arquivo. 9. Captura ideias.

### O UPDATE_PROTOCOL (transversal — aparece no CLAUDE.md de TODOS os nichos)
Contém: o protocolo de atualização de arquivos (assistente faz / usuário faz / nota sobre arquivos read-only), e agora 3 seções adicionadas nesta sessão:
- **commit ao final** (commitTitulo/commitIntro/commitNota) — fecha entregas com commit pronto (Conventional Commits), sensível ao SO.
- **canal de atualização do kit** (channelTitulo/channelIntro/channelComo) — ensina o Claude a reconhecer e aplicar updates do kit trazidos para a conversa.
- **privacidade** (privacidadeTitulo/privacidadeIntro/privacidadeRegras) — relevância + marcação, não censura (i-N2).

## Como as peças críticas funcionam

### `today` nos templates — ARMADILHA CRÍTICA
Nos templates `.md` (strings em `content`), datas usam `${today}` (a CONSTANTE), **NUNCA `${today()}`**. O `content` é uma template literal avaliada na carga do arquivo; `${today()}` (chamada de função) TRAVA O BOOT INTEIRO (tela branca). Sempre `${today}`.

### Dois formatos de dados (normalizadores)
Por razões históricas, os nichos existem em 2 formatos. `renderTopbar` aceita `opts:[[valor,label]]` (pares) E `options:["string"]` (strings) — foi a causa do bug v1.11.1. `normConventions` aceita array, `true` (gera bloco default) ou `false`/null. Sempre rodar o teste jsdom após mexer.

### Geração de dois artefatos
`buildInstr()` gera as **Instruções do Projeto** (texto curto para colar no campo de instruções do Claude.ai). `buildClaudeMd()` gera o **CLAUDE.md completo** (documento maior, com fundação + protocolo + gatilhos + saídas). Toggle de abas na UI: `#tab-instr` / `#tab-claude`, preview em `#preview-instr`.

### Afixo de download (v1.9.0)
`AFFIX = {mode, text, sep}` + `applyAffix(name)`. UI na aba Templates: padrão (nome original) / prefixo / sufixo. Aplicado em downloadFile, downloadAllTemplates, ZIP, CLAUDE.md.

### Seletor de SO (v1.11.0)
`OSENV = {value}` + OS_LABELS + OS_CMDNOTE. Campo no "Construir instrução" (`#g-os`): Windows-CMD / Windows-PowerShell / macOS / Linux / não-especificar. Injeta a sintaxe de comando certa nas Instruções E numa seção "Ambiente" do CLAUDE.md. Persiste em STATE.os.

## Armadilhas conhecidas (o que já deu errado — NÃO repetir)

1. **`${today()}` em template** → tela branca. Use `${today}`. (Documentado acima.)
2. **`renderTopbar` lendo só `f.opts`** → selects de topbar (Gênero/Engine/Fase) vinham VAZIOS nos nichos que usam `options:`. Corrigido na v1.11.1 (aceita os dois formatos). O teste jsdom agora detecta select vazio.
3. **`default:"pt-BR"` no langSel** → não casava com LANGS (que usa valor "pt"), idioma aparecia em branco. Todos corrigidos para `default:"pt"` na v1.11.1.
4. **git commit com `\` (continuação de linha bash)** → QUEBRA no CMD do Windows do usuário (`'\' is outside repository`). O usuário usa **CMD do Windows**. Commits devem ser UMA LINHA, com `-m` repetido (cada `-m` = um parágrafo). Registrado no CLAUDE.md do projeto e no seletor de SO.
5. **Publicar sem validar** → NUNCA publicar sem teste jsdom 17/17 e 0 erros JS. Os 2 "erros" de clipboard/download no jsdom são falsos-positivos conhecidos (jsdom não implementa essas APIs).
6. **Caso The Brazilian House** → é projeto de DESIGN GRÁFICO (cardápio físico), NÃO culinária. Já serviu ao nicho design. NÃO usar para cuisine nem outros nichos de conteúdo.

## Produto / posicionamento

- O kit compete (e complementa) a feature nativa "Pesquisar e referenciar conversas" do Claude. Diferencial: portabilidade (arquivos vão pro Git, funcionam em qualquer conta), estrutura deliberada (decisão/ideia/estado separados), controle do que entra no contexto.
- Filosofia central: **separação contexto vs histórico** (o princípio mais sólido do projeto). Contexto = leve, recarregado sempre. Histórico = no Git, lido sob demanda.
- Inspiração distante: GitHub spec-kit (Spec-Driven Development) — ferramenta da GitHub para dar estrutura/spec ao trabalho com IA. Lição aproveitada: "composição assistida > fusão automática"; e o conceito de "doctor/lint" para detectar conflitos (a usar no custom inteligente).

## Localização dos arquivos (no ambiente de trabalho do Claude)

- **Deliverable principal:** `/mnt/user-data/outputs/index.html`.
- **Meta-docs do projeto:** `/mnt/user-data/outputs/meta/` (CONTEXT/CLAUDE/STATUS/CHANGELOG/DECISOES/IDEIAS/NICHOS-CANDIDATOS + TEMA/MAPA/FILTROS/LOG-TEMPLATE herdados).
- **Projeto no GitHub do usuário (somente-leitura aqui):** `/mnt/project/` — versão sincronizada do repo. O usuário sobe manualmente; sincronização às vezes demora (esperar antes de conferir).
- **Scratchpad:** `/home/claude/` — onde se constrói nicho isolado e roda teste. `ft_local.js` é o teste jsdom dos 17 nichos (rodar de /home/claude, com o index em /tmp/test_target.html).

## Idioma e convenções

- **pt-BR em tudo**, inclusive comentários de código e nomes de template (que são profissionais, ex.: STATUS.md, DECISOES.md).
- Entrega via `present_files`; arquivos completos para baixar/substituir, NUNCA blocos soltos para costurar.
- Commit ao final no formato CMD Windows (uma linha, `-m` repetido), pronto para colar.

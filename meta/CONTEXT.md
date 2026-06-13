# CONTEXT.md — Kit de Contexto Universal

> O **passaporte** do projeto. Leia primeiro para se ambientar. Estável — muda pouco.
> Objetivo deste arquivo: uma nova conversa entende o projeto inteiro sem precisar de mais nada.

> **Mudanças nesta revisão (v1.30.x → v1.31.0):** página **06 · HUB** (construtor de frentes do grupo: nicho + nome + responsável por; preview; `buildHub()` gera o `HUB.md` populado; `STATE.hub`/`LS_HUB`). Responsabilidade no bloco da frente (não 4ª seção). `HUB.md` saiu do download por-nicho (`effectiveFiles` não injeta mais); o switch "Projeto em grupo?" segue adicionando a seção do HUB ao CLAUDE.md. 17/17 com round-trip + smoke test. ~575 KB / 8353 linhas. Nota anterior preservada abaixo.

> **Mudanças na revisão (v1.29.0 → v1.30.0):** HUB de grupo como **switch** (`UNIVERSAL_HUB_TPL` + toggle `groupMode` no topbar + `effectiveFiles`/`groupModeOn`; seção HUB no CLAUDE.md gerado quando ligado) e **Instruções enxutas** (os 13 universais viraram 1 linha de nomes em `buildInstr`; −27%; teto de 6500 no harness). Validação 17/17 com +3 checagens. ~563 KB / 8206 linhas. Nota anterior preservada abaixo.

> **Mudanças na revisão (v1.28.0 → v1.29.0):** D-023 fase 1 — nova constante de fundação **`UNIVERSAL_IDEAS_TPL`** (IDEAS injetado via `normNiche` em todo nicho sem o seu) + regra "cria na primeira necessidade" no buildClaudeMd; narrative passa a ESCREVER sob direção (convention reescrita + `writes_prose` + kishōtenketsu + prompt J); game passa a CRIAR (`builds_game` + template `ROTEIRO.md`). Validação 17/17 com +10 checagens. ~559 KB / 8176 linhas. Nota anterior preservada abaixo.

> **Mudanças na revisão (v1.27.x → v1.28.0):**
> - **Lote D-022 embutido na ferramenta** (sem mudar a contagem de 13 princípios): P8 (`check_before_ask`) ganhou o refino "STATUS é pista, não fato" (i-N19; refletido no item 8 da lista abaixo); `HYGIENE_RULES` ganhou a **válvula de desvio registrado** (i-N22); `TRIGGERS_BASE` ganhou o gatilho **«Feedback para o Kit»** (i-N21, inclui desvios estruturais); `UPDATE_PROTOCOL` ganhou o item do **manifesto de achatamento com detecção automática** (i-N18) e o commit em **3 linhas listando arquivos** (i-N20, no `commitIntro` — incondicional).
> - **D-018 corrigida no conteúdo gerado**: CLAUDE.md gerado (`handoffComo`) e tela "Tokens & Fluxos" agora dizem que **só o upload direto popula o mount** (achatado) e que o **conector do GitHub alimenta só a busca**.
> - Validação: 17/17, 0 erros, com 6 checagens novas de conteúdo + anti-teste. ~551 KB / 8101 linhas. Nada perdido; nota anterior preservada abaixo.
>
> **Mudanças nesta revisão (v1.26.0 → v1.27.0):**
> - **P12 e P13 propagados à ferramenta.** `BEHAVIORS_BASE` foi de **11 → 13** princípios: +P12 (higiene ao encolher, `shrink_hygiene`) +P13 (pesquisa para refinar E para refutar, `research_refute`). Aparecem no CLAUDE.md gerado de todos os nichos (e como bullet curto nas Instruções). Toda menção a "11 princípios" e "P12 a propagar / na fila" foi atualizada abaixo. Ver **D-020**, **D-021** e CHANGELOG v1.27.0.
> - **i-N17 decidida** — virou o P13 (princípio próprio, não reforço de P1/P7). Ver D-021.
> - Versão/tamanho atualizados (~548 KB / 8095 linhas); validado **17/17, 0 erros**.
> - A nota da revisão anterior (v1.26.0) fica preservada logo abaixo (nada perdido).
>
> **Mudanças nesta revisão (pós-v1.25.0 → v1.26.0):**
> - **Contagem de nichos 18 → 17.** Os dois construtores (`custom` "Blank" + `customSmart` "Inteligente") foram **fundidos em um só** card `custom` (composição + construção do zero na mesma tela). Ver **D-019** (supersede D-014). Toda menção a "2 construtores / customSmart" foi atualizada.
> - **Mapa do JS atualizado:** `renderSmartCustomForm` saiu; entraram `composerSectionHTML` / `wireComposer` / `refreshComposer` (composição dentro do `renderCustomForm`) e `savedNichesShortcutHTML` / `wireSavedNichesShortcut` (atalho de nichos salvos na barra superior).
> - **Suíte de validação** ampliada (lista atualizada na seção de validação).
> - **Novo princípio de higiene de docs (P12)** anotado — ver «Idioma e convenções» e DECISOES D-020. (Já valia para nós; **propagado para a ferramenta na v1.27.0** — `BEHAVIORS_BASE` 11→12, depois 13 com o P13.)
> - Acrescentado ponteiro para a **questão de arquitetura em aberto** (refator modular) — detalhe em IDEIAS (i-N13) e ROADMAP.
> - Versão/tamanho atualizados (~546 KB / 8092 linhas).
> - **Nada único foi removido** — só atualização de fatos que mudaram. O conteúdo sobre contexto/RAG/mount, armadilhas e produto permanece integral.

---

## O que é o projeto

O **Kit de Contexto Universal** é um **único arquivo `index.html`** (vanilla JS, sem build, sem dependências de runtime além de bibliotecas via CDN para o ZIP) que ajuda pessoas a **manter contexto entre conversas com o Claude**. O problema que resolve: conversas longas com IA ficam "papão de token" e, ao trocar de conversa, perde-se todo o contexto (decisões, ideias, estado do projeto).

A solução do kit: gerar **arquivos vivos** (`CONTEXT.md`, `STATUS.md`, `DECISÕES.md`, etc.) que o usuário sobe num Projeto do Claude.ai (ou anexa numa conversa) e que fazem a IA se ambientar instantaneamente. O kit oferece **17 nichos** (16 de conteúdo + **1 construtor** `custom`, unificado) — cada um gera dois artefatos: as **Instruções do Projeto** e um **CLAUDE.md completo**, adaptados ao domínio.

O kit é, ele mesmo, uma aplicação da própria filosofia (dogfooding): este projeto é gerenciado pelos arquivos que ele prega.

## Stack e arquitetura

- **Um arquivo:** `index.html` (~546 KB / 8092 linhas na v1.26.0). HTML + CSS + JS inline. Sem framework, sem build step.
- **Hospedagem:** GitHub Pages — `silujones.github.io/kit-contexto/`. O usuário sobe manualmente o `index.html` (e os meta-docs) ao repositório `github.com/SiluJones/kit-contexto`.
- **Bibliotecas externas (CDN):** JSZip (para o "baixar pacote ZIP"). O resto é vanilla.
- **Persistência no browser:** o kit usa `localStorage` para presets do custom e estado (STATE/snapshot). ATENÇÃO: localStorage é proibido em artifacts do claude.ai, MAS aqui funciona porque o arquivo roda no GitHub Pages do usuário (site real), não como artifact. Ao TESTAR via jsdom isso é simulado. **`localStorage` é por origem:** presets criados no site publicado NÃO aparecem no arquivo local (`file://`) e vice-versa.
- **Questão de arquitetura em aberto (não decidida):** se vale migrar de um HTML único "pesado" para uma estrutura **modular** (dados de cada nicho em JSON separado + um núcleo central), para tornar a edição/auditoria por nicho mais fácil. Hoje a escolha é o HTML único (D-001), pelo deploy estático sem build e por rodar via `file://`. Trade-offs e caminho possível em **IDEIAS i-N13** e no **ROADMAP** (Fase 4 — em avaliação). Não mexer sem decisão explícita.

### Estrutura do JS (mapa mental)
1. **Constantes de fundação** (topo do `<script>`): `LANGS` (idiomas — valor "pt", "en", "es", "other"), `BEHAVIORS_BASE` (**13** princípios universais — inclui P12 e P13, ver lista abaixo), `FILE_PHILOSOPHY`, `UNIVERSAL_IDEAS_TPL` (template IDEAS injetado via `normNiche` — v1.29.0), `UNIVERSAL_HUB_TPL` (template do HUB de grupo, injetado via `effectiveFiles` quando "Projeto em grupo?" está ligado — v1.30.0), `HYGIENE_RULES`, `TRIGGERS_BASE`, `UPDATE_PROTOCOL` (protocolo de atualização — inclui commit, canal de atualização, privacidade E o plano de transferência/handoff), `AFFIX` (afixo de download), `OSENV`/`OS_LABELS`/`OS_CMDNOTE` (seletor de SO).
2. **Objetos `NICHES.<id>`** — um por nicho (16 de conteúdo + `custom`). Cada um é um objeto grande com a forma descrita abaixo. Delimitados por comentários `/* ---------- NOME ---------- */`.
3. **Normalizadores** — `normNiche`, `normConventions`, `normBuilderSection`, `fileTag` (consolidado). Aceitam 2 formatos históricos de dados.
4. **Funções de render** — `renderTopbar` (aceita `opts` de pares E `options` de strings — corrigido na v1.11.1; **inclui agora o atalho "Nichos salvos"**), `renderBehaviors`, `renderBuilder` (roteia o `custom` para o construtor unificado), `renderCustomForm` (o construtor: **composição no topo + builder manual abaixo**), `updatePreview`, `buildInstr` (gera as Instruções), `buildClaudeMd` (gera o CLAUDE.md completo).
5. **Construtor unificado (Custom):**
   - `composerSectionHTML()` — devolve a seção "Compor a partir de nichos prontos" (os chips dos 16 nichos + sub-painéis de granularidade por nicho). Renderizada NO TOPO do `renderCustomForm`.
   - `wireComposer()` — liga os handlers dos chips, dos toggles "escolher peças", dos checkboxes de peça, do "marcar todas / limpar", e do "Importar e concatenar".
   - `refreshComposer()` — re-renderiza só a seção `#g-composer` (sem reconstruir o builder inteiro) quando muda seleção/expansão/peças.
   - `composeFromNiches(niches, sel)` — concatena contextFiles + behaviors + promptsExtra + convenções + saídas dos nichos marcados, com **dedup visível** e **checagem de conflito**; o 2º parâmetro `sel` filtra **quais peças** entram (granularidade).
   - `renderImportReport()` — banner do resultado (idênticos unificados × ⚠ conflitos + seletor de versão por arquivo).
   - `toPreset` / `fromPreset` / `mergeCustom` — motor de preset (localStorage). **`toPreset` guarda o `body` do prompt como STRING** (função some no `JSON.stringify` — ver FIX-003).
6. **Atalho de nichos salvos (barra superior):** `savedNichesShortcutHTML()` (dropdown que aparece quando há presets) + `wireSavedNichesShortcut()` (selecionar → `localStorage.setItem(LS_PRESET_CURR, name)` + `setNiche("custom")` → ATIVA o nicho salvo de qualquer lugar). Injetado por `renderTopbar`.
7. **Boot** — `boot()` no final, com try/catch que mostra banner de erro na página.

### Forma (shape) de cada nicho — objeto `NICHES.<id>`
```
{
  id, label, icon, group, category,            // metadados; group = tema visual (serif/literary/digital); category = core/creative/special
  cardColor, cardTags[], cardDesc,             // o card na tela de seleção
  intro:{ headline, lede, ctxBlurb, hero },    // a tela "Início" do nicho
  topbar:[ {id,label,placeholder?} | {id,label,type:"select",options:[...] | opts:[[v,l]], default?} ],
  behaviors:[ [id, titulo, descrição], ... ],  // os behaviors ESPECÍFICOS do nicho (somam aos 13 universais)
  builderSection:{ title, hint, items:[...] | groups:[...]/type:"chips" },  // o "Construir instrução"
  conventions:[ ... ] | true | false,          // bloco de convenções (true = naming/idioma default)
  triggersExtra:[ [evento, ação], ... ],        // gatilhos específicos (somam aos TRIGGERS_BASE)
  contextFiles:[ {name, cat, role, content}, ... ],  // os templates .md (cat: essencial/rolante/opcional/ref → vira tag)
  outputs:[ {key, name, role, active}, ... ],   // o que o assistente entrega como arquivo
  promptsExtra:[ {id, title, when, fill, fillLabel, body:(p,n)=>`...`}, ... ],  // os prompts G-L (6 específicos)
  isBuilder: true                               // SÓ no custom — roteia para o construtor unificado
}
```
Cada nicho tem **12 prompt cards**: 6 universais (A-F) + 6 específicos (G-L). Os A-F são gerados pela fundação; os G-L vêm de `promptsExtra`. **Nota:** o CLAUDE.md gerado lista só **título** dos prompts; os **corpos** vivem na aba Prompts (para copiar). Prompts compostos no custom têm corpo **estático** (template com `[placeholders]`), sem campo `fill` dinâmico.

### Os 13 princípios universais (BEHAVIORS_BASE — em todos os nichos)
1. Analisa antes de aceitar. 2. Não desperdiça tokens (mas pedir arquivo necessário ≠ desperdício; inventar arquivo falso = desperdício maior). 3. Direto e objetivo, sem rodeios. 4. Admite incerteza (pesquisa o que muda antes de afirmar). 5. Explica trade-offs. 6. Instruções sempre cuidadosas. 7. Estuda o domínio antes de estruturar. 8. Verifica antes de pedir arquivo; não inventa o que falta (mas inferência PEDIDA pelo usuário é permitida; e STATUS é pista, não fato — confere o estado real antes de repetir uma pendência registrada, e atualiza o STATUS se já foi resolvida). 9. Captura ideias. 10. Cadência (fases auditáveis; não fragmenta o trivial). 11. Usa a versão mais recente que tem; só pára e pede quando não tem a que a tarefa exige. 12. Higiene ao encolher arquivos-chave (não encolhe em silêncio; abre com «Mudanças nesta revisão»; confere que nada único se perdeu). 13. Pesquisa para refinar E para refutar (busca a experiência de outros, inclusive onde a ideia já falhou; o contraponto vem com lastro na prática alheia, não só na própria análise).

> **P12 — Higiene ao encolher arquivos-chave.** Ao reescrever/encolher qualquer arquivo-chave (CONTEXT, STATUS, DECISOES, CHANGELOG, IDEIAS, ROADMAP), informar explicitamente o que saiu e para onde foi (ou que é redundante/obsoleto); nunca encolher sem justificar item a item, e conferir que nada único se perdeu do conjunto. **Estado:** ativo para o nosso projeto (este arquivo o aplica na nota do topo) **e propagado para a ferramenta na v1.27.0** — é o 12º item de `BEHAVIORS_BASE` (id `shrink_hygiene`), no CLAUDE.md gerado de todos os nichos. Ver DEC D-020.

> **P13 — Pesquisa para refinar E para refutar.** Pesquisa a experiência de outros (casos reais, post-mortems, críticas, convenções) não só para refinar a proposta, mas para REFUTÁ-LA quando a evidência aponta contra; procura ativamente onde a ideia já falhou para os outros e traz o contraponto com lastro na prática alheia, não só na própria análise. **Estado:** decidido na v1.27.0 (resolve a i-N17) e propagado à ferramenta — 13º item de `BEHAVIORS_BASE` (id `research_refute`). Por que princípio próprio e não reforço de P1/P7: ver DEC D-021.

### O UPDATE_PROTOCOL (transversal — aparece no CLAUDE.md de TODOS os nichos)
Contém: o protocolo de atualização de arquivos (assistente faz / usuário faz / nota sobre arquivos read-only), e 4 seções adicionadas ao longo das sessões:
- **commit ao final** (commitTitulo/commitIntro/commitNota) — fecha entregas com commit pronto (Conventional Commits), sensível ao SO.
- **canal de atualização do kit** (channelTitulo/channelIntro/channelComo) — ensina o Claude a reconhecer e aplicar updates do kit trazidos para a conversa.
- **privacidade** (privacidadeTitulo/privacidadeIntro/privacidadeRegras) — relevância + marcação, não censura (i-N2).
- **transferência entre conversas / handoff** (handoffTitulo/handoffIntro/handoffComo) — contexto vs. RAG, regra anti-arquivo-falso, onde colocar cada arquivo, e o plano de handoff ao final (i-N9, v1.21.0). **Pendência:** este texto ainda diz "tudo no Projeto + ferramenta de código → mount", impreciso à luz de D-018 (corrigir num passe dedicado).

## Como as peças críticas funcionam

### `today` nos templates — ARMADILHA CRÍTICA
Nos templates `.md` (strings em `content`), datas usam `${today}` (a CONSTANTE), **NUNCA `${today()}`**. O `content` é uma template literal avaliada na carga do arquivo; `${today()}` (chamada de função) TRAVA O BOOT INTEIRO (tela branca). Sempre `${today}`.

### O Custom unificado (construtor único) — como funciona (v1.26.0, D-019)
Há **um** card de construção (`custom`). A tela do construtor tem, de cima para baixo:
1. **Compor a partir de nichos prontos** (`composerSectionHTML`): chips dos 16 nichos de conteúdo. Marcar um nicho abre, abaixo, um bloco "escolher peças" (granularidade): checkboxes de arquivos / comportamentos / prompts daquele nicho (padrão: tudo marcado; "marcar todas" / "limpar" por nicho). "⬇ Importar e concatenar" roda `composeFromNiches(picked, STATE._sc.pieces)` e preenche o builder **abaixo, na mesma tela** (sem trocar de view). Importar de novo substitui o conteúdo atual.
2. **Custom Builder** (`renderCustomForm`): presets (carregar/Ativar/Salvar/Excluir), identidade, textos da Home, arquivos de contexto, comportamentos, convenções, saídas, prompts G+.
Tudo cai no motor existente (`toPreset → mergeCustom → presets` no localStorage). Estado da composição em `STATE._sc` (`{selected, expanded, pieces}`); rascunho do nicho em `STATE._cf`.

### Contexto vs. RAG, mount, anexo, e fidelidade de arquivo — FUNDAMENTAL (v1.22.0 + D-018)
Entender isto mudou como o próprio kit deve ser desenvolvido e transferido:
- **Conhecimento do Projeto tem 2 modos automáticos, por TAMANHO total:** *in-context* (pequeno → arquivos INTEIROS no contexto → o assistente lê/reescreve com fidelidade) e *RAG / "Modo de pesquisa"* (grande → só FRAGMENTOS recuperados por relevância). Indicador visível na tela do Projeto. Volta a in-context se o conteúdo encolher. Capacidade do RAG expande ~10x.
- **O nosso `index.html` (~546 KB) faz o Projeto cair em RAG**, MAS isso não impede a leitura pelo mount: um arquivo que ESTÁ no mount `/mnt/project/` é lido INTEIRO com a **ferramenta de código** ligada, RAG ou não. **O que importa é COMO o mount é alimentado (D-018, teste limpo):** **o conector do GitHub alimenta só o RAG/Conhecimento do Projeto** (busca, com subpastas preservadas) **e NÃO popula o mount**; **só o upload direto** dos arquivos no Projeto popula o mount — e eles chegam **achatados** (sem subpastas; nomes iguais em pastas diferentes colidem → diferenciar com prefixo ou confiar no mapa que o assistente faz no início). Caminho limpo p/ trabalhar pelo mount: **subir os arquivos DIRETO no Projeto** (não confiar só no conector do GitHub) + ferramenta de código ligada. **Anexar** é o caminho do chat comum (sem ferramenta de código). **Nunca** reconstruir de fragmentos (RAG sem mount/anexo): aí eu peço o arquivo.
- **Anexo de conversa:** vale só naquela conversa (não passa para a próxima), ocupa contexto a cada turno (custa token), e dá fidelidade total. Um arquivo gerado pelo próprio assistente dentro da conversa tem a mesma fidelidade pelo mesmo motivo (entrou no histórico).
- **CUIDADO — janela é finita:** "nasceu na conversa = 100% para sempre" é FALSO. É 100% só enquanto está na janela viva; conversa longa é truncada/compactada (aconteceu nesta própria sessão) e aí a fidelidade do que saiu da janela se perde. Para o index grande, isso reforça: subir direto no Projeto, e em conversa nova reanexar/re-subir.
- **Continuidade entre conversas exige o conhecimento do Projeto** (o anexo é fidelidade só na sessão ativa). Sincronização do GitHub é MANUAL ("Sync now") e às vezes falha silenciosamente → para o que precisa estar fresco no Projeto, preferir UPLOAD DIRETO.
- **Enquadramento profissional** (Anthropic "Effective context engineering" + literatura 2025/26): janela = recurso finito; "context rot" (recall cai à medida que enche); estratégias = offload/retrieve/isolate/compress; Git para estado entre sessões. Tudo valida a arquitetura do kit (Instruções enxutas + STATUS como doc de estado ancorado + separação contexto/histórico).

### Dois formatos de dados (normalizadores)
Por razões históricas, os nichos existem em 2 formatos. `renderTopbar` aceita `opts:[[valor,label]]` (pares) E `options:["string"]` (strings) — foi a causa do bug v1.11.1. `normConventions` aceita array, `true` (gera bloco default) ou `false`/null. Sempre rodar o teste jsdom após mexer.

### Geração de dois artefatos
`buildInstr()` gera as **Instruções do Projeto** (texto curto para colar no campo de instruções do Claude.ai). `buildClaudeMd()` gera o **CLAUDE.md completo** (documento maior, com fundação + protocolo + gatilhos + saídas). Toggle de abas na UI: `#tab-instr` / `#tab-claude`, preview em `#preview-instr`.

### Afixo de download (v1.9.0) e Seletor de SO (v1.11.0)
`AFFIX = {mode, text, sep}` + `applyAffix(name)`: UI na aba Templates (padrão / prefixo / sufixo); aplicado em downloadFile, downloadAllTemplates, ZIP, CLAUDE.md. `OSENV = {value}` + OS_LABELS + OS_CMDNOTE: campo no "Construir instrução" (Windows-CMD / Windows-PowerShell / macOS / Linux / não-especificar); injeta a sintaxe de comando certa nas Instruções e numa seção "Ambiente" do CLAUDE.md; persiste em STATE.os.

## Armadilhas conhecidas (o que já deu errado — NÃO repetir)

1. **`${today()}` em template** → tela branca. Use `${today}`. (Documentado acima.)
2. **`renderTopbar` lendo só `f.opts`** → selects de topbar (Gênero/Engine/Fase) vinham VAZIOS nos nichos que usam `options:`. Corrigido na v1.11.1 (aceita os dois formatos). O teste jsdom agora detecta select vazio.
3. **`default:"pt-BR"` no langSel** → não casava com LANGS (valor "pt"), idioma em branco. Todos corrigidos para `default:"pt"` na v1.11.1.
4. **git commit com `\` (continuação de linha bash)** → QUEBRA no CMD do Windows (`'\' is outside repository`). O usuário usa **CMD do Windows**. Commits = UMA LINHA, `-m` repetido (cada `-m` = um parágrafo), **mensagem sem acentos** (CMD corrompe acentos em `-m`).
5. **Publicar sem validar** → NUNCA publicar sem a suíte jsdom verde (17/17 e 0 erros JS). Os "erros" de clipboard/download no jsdom são falsos-positivos (jsdom não implementa essas APIs). "Boot failed: DOMException" no harness é esperado (o teste chama buildClaudeMd/buildInstr direto).
6. **Caso The Brazilian House** → é projeto de DESIGN GRÁFICO (cardápio físico), NÃO culinária. Já serviu ao nicho design. NÃO usar para cuisine nem outros nichos.
7. **Editar um arquivo a partir de FRAGMENTOS (RAG, sem mount nem anexo)** → arquivo falso/incompleto. O critério não é "está em RAG?", é "tenho o arquivo COMPLETO?". Com a ferramenta de código eu leio inteiro pelo mount QUALQUER arquivo que ESTEJA no mount — mas **o mount só é alimentado por upload direto, não pelo conector do GitHub (D-018)**. Então o certo é **subir o arquivo direto no Projeto** + ligar a ferramenta de código. Só quando NÃO há mount nem anexo e sobra fragmento é que eu peço o arquivo, nunca reconstruo.
8. **`toPreset` guardando `body` de prompt como função** → o `JSON.stringify` do localStorage **descarta funções** → o corpo do prompt sumia depois de Ativar (aparecia vazio na aba Prompts e no CLAUDE.md gerado). Corrigido na v1.25.1 (guardar `body` como STRING). Ver FIX-003. **Lição:** nada que vá para o localStorage pode ser função.
9. **Construtor reescrevendo a coluna de controles sem restaurar o esqueleto** → ao sair de um nicho construtor, os controles ficavam errados (e o próximo construtor falhava em cascata). Corrigido com `captureControlsSkeleton`/`restoreControlsSkeleton` + re-entrância (v1.24.0). Ver FIX-001.

## Produto / posicionamento

- O kit compete (e complementa) a feature nativa "Pesquisar e referenciar conversas" do Claude. Diferencial: portabilidade (arquivos vão pro Git, funcionam em qualquer conta), estrutura deliberada (decisão/ideia/estado separados), controle do que entra no contexto.
- Filosofia central: **separação contexto vs histórico** (o princípio mais sólido do projeto). Contexto = leve, recarregado sempre. Histórico = no Git, lido sob demanda.
- Inspiração distante: GitHub spec-kit (Spec-Driven Development). Lições aproveitadas: "composição assistida > fusão automática" (base do Custom) e "doctor/lint" para detectar conflitos (a checagem de conflito do compose).
- **Ideias de expansão de produto em avaliação** (ver IDEIAS + ROADMAP): nicho/ferramenta de **guias/tutoriais/wikis** (aprender Aseprite/Unity/Godot/Unreal/Excel/linguagens; platinar jogos); **ferramenta de auto-aplicação de patches** (a IA gera arquivos de atualização num formato estruturado e uma ferramenta local os aplica — economiza esforço manual e, se a IA emitir diffs em vez de arquivos inteiros, output tokens); possível **refator modular** do próprio kit.

## Localização dos arquivos (no ambiente de trabalho do Claude)

- **Deliverable principal:** `/mnt/user-data/outputs/index.html`.
- **Meta-docs do projeto:** `/mnt/user-data/outputs/meta/` (CONTEXT/CLAUDE/STATUS/CHANGELOG/DECISOES/IDEIAS/ROADMAP/GLOSSARIO/NICHOS-CANDIDATOS + TEMA/MAPA/FILTROS/LOG-TEMPLATE). Logs em `logs/` (ou onde o usuário mantém os logs; o anterior é `2026-06-02.md`).
- **Mount do Projeto:** `/mnt/project/` (somente-leitura aqui). **Alimentado por upload direto** dos arquivos no Projeto, NÃO pelo conector do GitHub (D-018) — que popula só o RAG. Pode estar VAZIO se só o conector estiver ligado; chega achatado.
- **Index e arquivos grandes:** com a ferramenta de código ligada eu leio o `index.html` inteiro do mount `/mnt/project/`. Caminho confiável = **subir o index direto no Projeto** + ligar a ferramenta de código.
- **Scratchpad:** `/home/claude/kit/` — onde se constrói/edita isolado e roda teste. A suíte jsdom roda de lá com o index em disco.

## Idioma e convenções

- **pt-BR em tudo**, inclusive comentários de código e nomes de template (profissionais, ex.: STATUS.md, DECISOES.md).
- Entrega via `present_files`; arquivos completos para baixar/substituir, NUNCA blocos soltos para costurar.
- Commit ao final no formato CMD Windows (uma linha, `-m` repetido, sem acentos), pronto para colar.
- **Handoff ao final:** dizer ao usuário, arquivo por arquivo, onde colocar cada um na próxima conversa (Projeto vs. anexo) e, quando útil, montar o prompt de início.
- **P12 (higiene ao encolher):** ao reescrever um arquivo-chave, abrir com uma nota do que mudou/saiu/por quê; nunca encolher sem justificar item a item; conferir que nada único se perdeu.
- **P13 (pesquisa para refinar E refutar):** ao avaliar uma ideia/solicitação, buscar a experiência de outros — inclusive onde já falhou — e trazer o contraponto fundamentado na prática alheia, não só no raciocínio interno; não concluir "parece bom" sem confrontar com o que o mundo já tentou.

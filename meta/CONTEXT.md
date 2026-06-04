# CONTEXT.md — Kit de Contexto Universal

> O **passaporte** do projeto. Leia primeiro para se ambientar. Estável — muda pouco.
> Objetivo deste arquivo: uma nova conversa entende o projeto inteiro sem precisar de mais nada.

---

## O que é o projeto

O **Kit de Contexto Universal** é um **único arquivo `index.html`** (vanilla JS, sem build, sem dependências de runtime além de bibliotecas via CDN para o ZIP) que ajuda pessoas a **manter contexto entre conversas com o Claude**. O problema que resolve: conversas longas com IA ficam "papão de token" e, ao trocar de conversa, perde-se todo o contexto (decisões, ideias, estado do projeto).

A solução do kit: gerar **arquivos vivos** (`CONTEXT.md`, `STATUS.md`, `DECISÕES.md`, etc.) que o usuário sobe num Projeto do Claude.ai (ou anexa numa conversa) e que fazem a IA se ambientar instantaneamente. O kit oferece **17 nichos** (16 de conteúdo + 1 `custom` gerador) — cada um gera dois artefatos: as **Instruções do Projeto** e um **CLAUDE.md completo**, adaptados ao domínio.

O kit é, ele mesmo, uma aplicação da própria filosofia (dogfooding): este projeto é gerenciado pelos arquivos que ele prega.

## Stack e arquitetura

- **Um arquivo:** `index.html` (~519 KB na v1.23.0). HTML + CSS + JS inline. Sem framework, sem build step.
- **Hospedagem:** GitHub Pages — `silujones.github.io/kit-contexto/`. O usuário sobe manualmente o `index.html` (e os meta-docs) ao repositório `github.com/<user>/kit-contexto`.
- **Bibliotecas externas (CDN):** JSZip (para o "baixar pacote ZIP"). O resto é vanilla.
- **Persistência no browser:** o kit usa `localStorage` para presets do custom e estado (STATE/snapshot). ATENÇÃO: localStorage é proibido em artifacts do claude.ai, MAS aqui funciona porque o arquivo roda no GitHub Pages do usuário (site real), não como artifact. Ao TESTAR via jsdom isso é simulado.

### Estrutura do JS (mapa mental)
1. **Constantes de fundação** (topo do `<script>`): `LANGS` (idiomas — valor "pt", "en", "es", "other"), `BEHAVIORS_BASE` (11 princípios universais), `FILE_PHILOSOPHY`, `HYGIENE_RULES`, `TRIGGERS_BASE`, `UPDATE_PROTOCOL` (protocolo de atualização — agora inclui commit, canal de atualização, privacidade E o plano de transferência/handoff), `AFFIX` (afixo de download), `OSENV`/`OS_LABELS`/`OS_CMDNOTE` (seletor de SO).
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

### Os 11 princípios universais (BEHAVIORS_BASE — em todos os nichos)
1. Analisa antes de aceitar. 2. Não desperdiça tokens (mas pedir arquivo necessário ≠ desperdício; inventar arquivo falso = desperdício maior). 3. Direto e objetivo, sem rodeios. 4. Admite incerteza. 5. Explica trade-offs. 6. Instruções sempre cuidadosas. 7. Estuda o domínio antes de estruturar. 8. Verifica antes de pedir arquivo; não inventa o que falta (mas inferência PEDIDA pelo usuário é permitida). 9. Captura ideias. 10. Cadência (fases auditáveis; não fragmenta o trivial). 11. Usa a versão mais recente que tem; só pára e pede quando não tem a que a tarefa exige.

### O UPDATE_PROTOCOL (transversal — aparece no CLAUDE.md de TODOS os nichos)
Contém: o protocolo de atualização de arquivos (assistente faz / usuário faz / nota sobre arquivos read-only), e 4 seções adicionadas ao longo das últimas sessões:
- **commit ao final** (commitTitulo/commitIntro/commitNota) — fecha entregas com commit pronto (Conventional Commits), sensível ao SO.
- **canal de atualização do kit** (channelTitulo/channelIntro/channelComo) — ensina o Claude a reconhecer e aplicar updates do kit trazidos para a conversa.
- **privacidade** (privacidadeTitulo/privacidadeIntro/privacidadeRegras) — relevância + marcação, não censura (i-N2).
- **transferência entre conversas / handoff** (handoffTitulo/handoffIntro/handoffComo) — contexto vs. RAG, regra anti-arquivo-falso, onde colocar cada arquivo, e o plano de handoff ao final (i-N9, v1.21.0).

## Como as peças críticas funcionam

### `today` nos templates — ARMADILHA CRÍTICA
Nos templates `.md` (strings em `content`), datas usam `${today}` (a CONSTANTE), **NUNCA `${today()}`**. O `content` é uma template literal avaliada na carga do arquivo; `${today()}` (chamada de função) TRAVA O BOOT INTEIRO (tela branca). Sempre `${today}`.

### Contexto vs. RAG, mount, anexo, e fidelidade de arquivo — FUNDAMENTAL (v1.22.0)
Entender isto mudou como o próprio kit deve ser desenvolvido e transferido:
- **Conhecimento do Projeto tem 2 modos automáticos, por TAMANHO total:** *in-context* (pequeno → arquivos INTEIROS no contexto → o assistente lê/reescreve com fidelidade) e *RAG / "Modo de pesquisa"* (grande → só FRAGMENTOS recuperados por relevância). Indicador visível na tela do Projeto. Volta a in-context se o conteúdo encolher. Capacidade do RAG expande ~10x.
- **O nosso `index.html` (~519 KB) faz o Projeto cair em RAG**, MAS isso não impede a leitura: com a **ferramenta de código** ligada, os arquivos do Projeto ficam montados em `/mnt/project/` e eu os abro INTEIROS, RAG ou não. **Verificado (v1.22.0):** li o `index.html` completo (byte-idêntico) com o Projeto em "Modo de pesquisa". Então o caminho limpo é: tudo no Projeto (inclusive o index) + ferramenta de código ligada → leio/edito pelo mount, sem anexar. **Anexar** é o caminho do chat comum (sem ferramenta de código). **Nunca** reconstruir de fragmentos (RAG sem mount/anexo): aí eu peço o arquivo. **Obs. (v1.23.0):** o mount apareceu ACHATADO (sem subpastas; nomes iguais em pastas diferentes podem colidir) — diferenciar com prefixo de pasta, ou confiar no mapa que o assistente faz no início. Confirmar o comportamento do GitHub-com-subpastas exige teste só-GitHub.
- **Anexo de conversa:** vale só naquela conversa (não passa para a próxima), ocupa contexto a cada turno (custa token), e dá fidelidade total. Um arquivo gerado pelo próprio assistente dentro da conversa tem a mesma fidelidade pelo mesmo motivo (entrou no histórico). Por isso a conversa-mãe de desenvolvimento mantinha o index fiel sem anexar — ele nasceu ali.
- **CUIDADO — janela é finita:** "nasceu na conversa = 100% para sempre" é FALSO. É 100% só enquanto está na janela viva; conversa longa é truncada/compactada (aconteceu nesta própria sessão) e aí a fidelidade do que saiu da janela se perde. Para o index grande, isso reforça: anexar, e em conversa nova reanexar.
- **Continuidade entre conversas exige o conhecimento do Projeto** (o anexo é fidelidade só na sessão ativa). Sincronização do GitHub é MANUAL ("Sync now") e às vezes falha silenciosamente → para o que precisa estar fresco no Projeto, preferir UPLOAD DIRETO.
- **Enquadramento profissional** (Anthropic "Effective context engineering" + literatura 2025/26): janela = recurso finito; "context rot" (recall cai à medida que enche); estratégias = offload/retrieve/isolate/compress; Git para estado entre sessões. Tudo valida a arquitetura do kit (Instruções enxutas + STATUS como doc de estado ancorado + separação contexto/histórico).

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
5. **Publicar sem validar** → NUNCA publicar sem teste jsdom 17/17 e 0 erros JS. Os 2 "erros" de clipboard/download no jsdom são falsos-positivos conhecidos (jsdom não implementa essas APIs). O "Boot failed: DOMException" no harness também é esperado (o boot precisa de elementos reais; o teste chama buildClaudeMd/buildInstr direto).
6. **Caso The Brazilian House** → é projeto de DESIGN GRÁFICO (cardápio físico), NÃO culinária. Já serviu ao nicho design. NÃO usar para cuisine nem outros nichos de conteúdo.
7. **Editar um arquivo a partir de FRAGMENTOS (RAG, sem mount nem anexo)** → geraria um arquivo falso/incompleto. O critério não é "está em RAG?", é "tenho o arquivo COMPLETO?". Com a ferramenta de código ligada eu leio o `index.html` (e qualquer arquivo do Projeto) inteiro pelo mount `/mnt/project/`, mesmo em RAG — então o certo é ligar a ferramenta de código, não anexar. Só quando NÃO há mount nem anexo e sobra fragmento é que eu peço o arquivo, nunca reconstruo. (Ver "Contexto vs. RAG" acima e D-016.)

## Produto / posicionamento

- O kit compete (e complementa) a feature nativa "Pesquisar e referenciar conversas" do Claude. Diferencial: portabilidade (arquivos vão pro Git, funcionam em qualquer conta), estrutura deliberada (decisão/ideia/estado separados), controle do que entra no contexto.
- Filosofia central: **separação contexto vs histórico** (o princípio mais sólido do projeto). Contexto = leve, recarregado sempre. Histórico = no Git, lido sob demanda.
- Inspiração distante: GitHub spec-kit (Spec-Driven Development) — ferramenta da GitHub para dar estrutura/spec ao trabalho com IA. Lição aproveitada: "composição assistida > fusão automática"; e o conceito de "doctor/lint" para detectar conflitos (a usar no custom inteligente).

## Localização dos arquivos (no ambiente de trabalho do Claude)

- **Deliverable principal:** `/mnt/user-data/outputs/index.html`.
- **Meta-docs do projeto:** `/mnt/user-data/outputs/meta/` (CONTEXT/CLAUDE/STATUS/CHANGELOG/DECISOES/IDEIAS/NICHOS-CANDIDATOS + TEMA/MAPA/FILTROS/LOG-TEMPLATE herdados).
- **Projeto no GitHub do usuário (somente-leitura aqui):** `/mnt/project/` — versão sincronizada do repo. Pode estar VAZIO ou ATRASADO (sync manual); na dúvida, o usuário anexa o que for grande/atual na conversa.
- **Index e arquivos grandes:** com a ferramenta de código ligada eu leio o `index.html` inteiro do mount `/mnt/project/` (verificado, mesmo com o Projeto em RAG). Caminho confiável = manter o index no Projeto + ligar a ferramenta de código. Anexar só no chat comum (sem ferramenta) ou se o arquivo não estiver no Projeto.
- **Scratchpad:** `/home/claude/` — onde se constrói nicho isolado e roda teste. `test_niches.js` (ou `ft_local.js`) é o teste jsdom dos 17 nichos (rodar de /home/claude, com o index em disco).

## Idioma e convenções

- **pt-BR em tudo**, inclusive comentários de código e nomes de template (que são profissionais, ex.: STATUS.md, DECISOES.md).
- Entrega via `present_files`; arquivos completos para baixar/substituir, NUNCA blocos soltos para costurar.
- Commit ao final no formato CMD Windows (uma linha, `-m` repetido), pronto para colar.
- **Handoff ao final:** dizer ao usuário, arquivo por arquivo, onde colocar cada um na próxima conversa (Projeto vs. anexo) e, quando útil, montar o prompt de início.

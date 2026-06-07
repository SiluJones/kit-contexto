# GLOSSÁRIO — Kit de Contexto Universal

> Termos próprios do projeto que se repetem entre sessões. Opcional, lido sob demanda. Criado em 2026-06-07.

## Produto e estrutura

- **Kit / a ferramenta** — o `index.html` único que gera os arquivos de contexto. (Não confundir com "o projeto", que inclui o kit + os meta-docs.)
- **Nicho** — um domínio pronto (dev, design, music, game…). 16 de conteúdo + 1 construtor (`custom`). Cada um é um objeto `NICHES.<id>` no JS.
- **Nicho de conteúdo** — os 16 prontos (8 "sérios": dev, design, client, narrative, marketing, research, product, business; 8 criativos: game, pixel, brainstorm, music, rpg, cuisine, animation, comics).
- **Construtor / builder** — o nicho `custom`: não tem conteúdo pronto, monta um nicho sob medida. Desde a v1.26.0 é **um só** (antes eram dois: "Blank" e "Inteligente").
- **Composer / chips** — a seção "Compor a partir de nichos prontos" no topo do Custom: os chips dos 16 nichos; marcar e importar concatena o material deles no builder. (Era o "Custom Inteligente".)
- **Granularidade / "escolher peças"** — sub-painel por nicho marcado no composer: escolher QUAIS arquivos/comportamentos/prompts importar (padrão = tudo).
- **Preset** — um nicho custom salvo no `localStorage` (nome → conteúdo). Vários simultâneos.
- **Ativar (um nicho/preset)** — tornar o nicho custom o nicho corrente (reflete em Início/Instruções/Prompts/Templates). Salva o preset antes (evita o footgun FIX-002).
- **Os dois artefatos** — o que o kit gera por nicho: as **Instruções do Projeto** (texto curto p/ o campo de instruções do Claude.ai, lido a cada mensagem) e o **CLAUDE.md** (documento maior, completo, subido como arquivo de conhecimento).
- **Prompts A–F / G–L** — A–F são os 6 prompts universais (ciclo de vida do projeto), iguais em todo nicho; G–L são os 6 específicos do domínio (`promptsExtra`).
- **BEHAVIORS_BASE** — a constante com os princípios universais (hoje 11; P12 a entrar) que aparecem no CLAUDE.md de todos os nichos.
- **UPDATE_PROTOCOL** — a constante com as seções transversais do CLAUDE.md gerado: protocolo de atualização, commit ao final, canal de atualização, privacidade, transferência/handoff.
- **Afixo** — prefixo/sufixo opcional nos nomes dos arquivos baixados (`applyAffix`).

## Contexto, transferência e ambiente

- **Contexto vs. histórico** — o princípio central do kit. Contexto = leve, recarregado sempre (Instruções, STATUS). Histórico = no Git, lido sob demanda (logs, decisões antigas).
- **Conhecimento do Projeto** — os arquivos que você sobe num Projeto do Claude.ai. Têm 2 modos automáticos por tamanho: in-context e RAG.
- **In-context** — quando o conteúdo do Projeto cabe na janela: arquivos INTEIROS no contexto; o Claude lê/reescreve com fidelidade.
- **RAG / "Modo de pesquisa"** — quando o conteúdo é grande: só FRAGMENTOS recuperados por relevância. Há indicador na tela do Projeto. Capacidade ~10x maior.
- **Mount (`/mnt/project/`)** — o sistema de arquivos que a **ferramenta de código** enxerga. Lê arquivos INTEIROS, RAG ou não. **Alimentado SÓ por upload direto** (D-018), e **achatado** (sem subpastas).
- **Conector do GitHub** — sincroniza o repo para o **RAG/Conhecimento do Projeto** (busca, com subpastas), mas **NÃO popula o mount** (D-018). Ótimo para versão/hospedagem e busca; não substitui o upload direto para edição via mount.
- **Upload direto** — subir os arquivos manualmente no Projeto. É o que popula o mount. Preferir para o que precisa estar fresco/editável.
- **Anexo** — arquivo colado numa conversa: fidelidade total, mas só naquela sessão, e custa token a cada turno. Não passa para a próxima conversa.
- **Handoff** — o fechamento de sessão: dizer arquivo por arquivo onde colocar na próxima conversa + (quando útil) montar o prompt de início.
- **Ferramenta de código** — o toggle do Claude.ai que dá acesso ao mount/execução. Necessária para eu ler/editar o `index.html` pelo mount.

## Composição e validação

- **Concatenar / compor** — juntar arquivos/comportamentos/prompts de vários nichos num custom (`composeFromNiches`). NÃO é fusão automática opaca: é assistida e revisável.
- **Dedup (visível)** — quando dois nichos trazem o mesmo arquivo IDÊNTICO, unifica em silêncio e mostra que unificou.
- **Conflito** — mesmo nome, conteúdo DIFERENTE: preserva as versões e oferece um seletor de qual manter (arquivos); comportamento divergente é sinalizado, não bloqueado (inspirado no spec-kit).
- **jsdom / harness** — o ambiente de teste em Node que simula o DOM. A suíte recria o boot por nicho e confere 17/17 + 0 erros. O ambiente reseta entre sessões — os testes são recriados a cada vez.
- **Boot limpo por nicho** — rodar a inicialização isolada para cada nicho no teste, evitando contaminação de um construtor que reescreve a coluna de controles.

## Pessoas/decisões

- **Dogfooding** — o kit aplicado a si mesmo: este projeto é gerenciado pelos arquivos que o kit prega.
- **D-NNN / FIX-NNN** — decisões formais (DECISOES.md) e bugs graves resolvidos. Ex.: D-019 (custom unificado), FIX-003 (corpo de prompt no localStorage).
- **i-NNN / i-N NN** — ideias no IDEIAS.md (i1.. das origens; i-N1.. das sessões pós-MVP).
- **spec-kit** — ferramenta da GitHub para Spec-Driven Development. Inspiração distante: "composição > herança" e "doctor/lint" para conflitos.
- **Padrão de ouro** — o nível de profundidade alvo de um nicho (arquivo-âncora com o "porquê" + armadilhas + ângulo próprio + prompts das tarefas reais). Piso, não teto.

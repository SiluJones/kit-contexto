# CLAUDE.md — Instruções para o Assistente (Projeto: Kit de Contexto Universal)

> Arquivo **estável**. Define COMO o assistente trabalha neste projeto específico.
> O QUE o projeto é fica no `README.md`/`PLANNING.md`; o estado atual no `meta/STATUS.md`.
> Este arquivo é o primeiro a ler em cada sessão — ele carrega as regras que descobrimos ao longo do desenvolvimento, para que cada conversa nova continue de onde a anterior parou, sem regredir.

---

## O que é este projeto (resumo de 30 segundos)

O **Kit de Contexto Universal** é um único `index.html` autossuficiente (vanilla JS, sem build, sem dependências exceto JSZip via CDN) que ajuda usuários a manter contexto entre conversas com o Claude. Ele tem 17 nichos prontos + 1 custom; cada nicho gera Instruções de Projeto, um CLAUDE.md, e templates `.md` para baixar.

O projeto está em **refinamento área por área** após o MVP: a fundação (regras universais) e os nichos vão sendo aprofundados um a um, cada um com pesquisa do domínio + feedback de uso real.

Detalhes completos: `README.md`, `PLANNING.md`, `meta/STATUS.md`, `meta/CHANGELOG.md`, `meta/DECISOES.md`.

---

## 🟢 Ritual de início de sessão

1. Lê **este CLAUDE.md** — confirma como trabalhar.
2. Lê **`meta/STATUS.md`** — descobre a fase atual e o próximo passo.
3. Lê a última entrada de **`meta/CHANGELOG.md`** — vê o que mudou na sessão anterior.
4. Consulta sob demanda (não por padrão): `meta/DECISOES.md` (por que as coisas são como são), `meta/IDEIAS.md`, `PLANNING.md`, e o `index.html` em si.
5. Antes de executar, confirma em uma frase o que entendeu da tarefa.

---

## Princípios de trabalho (os 9 universais do próprio kit, aplicados a nós)

Estes são exatamente os princípios que o kit prega — e que praticamos aqui (dogfooding).

1. **Analisa antes de aceitar.** Não segue cegamente o que o usuário propõe. Avalia viabilidade e se posiciona — a favor, refinando, ou contra — sempre fundamentado. Concordância automática é falha. (Foi assim que decidimos pausar etapas para consolidar a fundação em vez de seguir em frente cegamente.)
2. **Não desperdiça tokens.** Não pergunta o que já foi decidido; não pede confirmação de plano aprovado; não abre menu para decisões óbvias. Em dúvida entre fazer e perguntar, faz e relata.
3. **Direto e objetivo.** Sem floreio, sem bajulação.
4. **Admite incerteza.** Diz quando não verificou. Para fatos que mudam (features da Anthropic, limites técnicos), pesquisa antes de afirmar.
5. **Explica trade-offs.** Em decisão importante, dá o melhor argumento contrário.
6. **Instruções sempre cuidadosas.** Qualquer guia/passo a passo ao usuário é completo e detalhado; deixa claro o que é decisão dele vs. passo necessário.
7. **Estuda o domínio antes de estruturar.** Ao aprofundar um nicho, pesquisa práticas/convenções/armadilhas da área antes de montar a estrutura — não inventa do zero. (Foi o que fez o client ficar bom; é regra, não acaso.)
8. **Verifica antes de pedir arquivo.** Quando o usuário diz «já subi X», a primeira ação é procurar X nos arquivos do projeto/uploads — não perguntar de novo.
9. **Captura ideias.** Registra no IDEIAS tudo que o usuário mencionar, mesmo solto.

---

## 💻 Padrões de código (o `index.html`)

- **Vanilla JS, sem build, sem dependências** (exceto JSZip via CDN, carregado sob demanda só no download em ZIP). Não introduzir framework, bundler, ou npm.
- **Tudo num único arquivo.** CSS no `<style>`, JS no `<script>` ao final. É assim que o kit é distribuído (GitHub Pages estático).
- **Sem `localStorage`/`sessionStorage` quebrando**: o kit USA localStorage para persistir nicho e presets — isso é intencional e funciona no destino (não é artifact). Manter.
- **Estrutura dos nichos**: cada nicho é um objeto `NICHES.{id}` com shape consistente (id, label, icon, group, category, cardColor, cardTags, cardDesc, intro, topbar, behaviors, builderSection, conventions, contextFiles, outputs, promptsExtra, e opcionalmente triggersExtra/isBuilder). Há um **normalizador** (`normNiche`/`normBehaviors`/`normFiles`/etc.) que aceita dois formatos históricos — ao adicionar/editar nicho, não precisa migrar formato, o normalizador resolve.
- **Theming** por `[data-niche]` e `[data-group]` no `<html>` (CSS variables). Cor de acento = `--amber` (renomeado por nicho).
- **Templates `.md`** vivem como strings no campo `content` de cada arquivo do nicho. Cuidado com `${...}` dentro deles: template literal avalia na carga. Use `${today}` (constante), NUNCA `${today()}` — esse foi um bug que travou o boot inteiro.

---

## 📝 Como manter os documentos deste projeto

Os arquivos do projeto vivem em `meta/` (mais `README.md`, `PLANNING.md`, `DEPLOY-GUIDE.md` na raiz). Cada um tem um papel temporal:

| Arquivo | Comportamento | Papel |
|---|---|---|
| `CLAUDE.md` (este) | Estável | Como o assistente trabalha aqui. |
| `README.md` | Estável | O que o kit é (público). |
| `PLANNING.md` | Estável | Arquitetura e racional consolidado. |
| `meta/STATUS.md` | Rolante | Fase atual, próximos passos. O resolvido sai. |
| `meta/CHANGELOG.md` | Cresce (topo) | Uma entrada por versão (vX.Y.Z). |
| `meta/DECISOES.md` | Cresce devagar | Decisões D-NNN com racional. |
| `meta/IDEIAS.md` | Segundo cérebro | Ideias capturadas; nunca perde. |
| `meta/TEMA/MAPA/FILTROS.md` | Estável | Brainstorm de origem (o kit é nicho Brainstorm). |
| `meta/LOG-TEMPLATE.md` | Referência | Molde de log; nunca substituído. |

### Regras de higiene
- **Referência cruzada, não duplicação**: um dado tem uma fonte de verdade.
- **STATUS é só o agora**: versão concluída sai do STATUS e vira entrada no CHANGELOG.
- **DECISOES cresce devagar**: cada decisão grande vira D-NNN; não reescrever as antigas.
- **CHANGELOG por versão**: cada sessão que entrega algo ganha um vX.Y.Z no topo.

### Como ENTREGAR as atualizações (regra dura)
- As mudanças que decorrem do trabalho do assistente são registradas pelo **próprio assistente** — mexeu em STATUS/CHANGELOG/etc., entrega esses arquivos atualizados sem esperar pedido.
- **"Atualizar um doc" = entregar o arquivo COMPLETO** em `/mnt/user-data/outputs`, pronto para o usuário baixar e substituir. **Nunca** trechos para colar nem um arquivo de "instruções de atualização".
- Entregar o **conjunto consistente** de uma vez. Estado meio-atualizado é pior que não mexer.
- O que o usuário quer acrescentar por conta é decisão dele.
- `/mnt/project` é somente-leitura para o assistente — isso não é desculpa para não entregar: lê de lá, edita uma cópia, entrega o resultado completo pela pasta de saída.

### Verificar antes de pedir upload (regra dura)
- Antes de pedir que o usuário suba um arquivo, verifica se ele já não está em `/mnt/project`, nos uploads, ou colado na conversa. Quando o usuário diz «já subi X», procura X primeiro.

---

## 🔬 Como aprofundar um nicho (processo das Etapas)

Sequência que provou funcionar (dev = Etapa 1, client = Etapa 2):

1. **Estudar**: ler o feedback de uso real se houver (ex.: arquivos `__refinado__DEV`, `__GameDataHub2`, BRIEFING) + pesquisar práticas profissionais do domínio na web (casos, convenções, armadilhas, dicas).
2. **Projetar**: cruzar o feedback + a pesquisa + o padrão de ouro do dev v2. Definir arquivos (núcleo enxuto + opcionais marcados), behaviors específicos, prompts G+, gatilhos próprios.
3. **Construir** o objeto do nicho como arquivo isolado primeiro; validar a sintaxe em Node isoladamente.
4. **Inserir** no `index.html` via splice por marcadores de comentário do nicho.
5. **Validar**: `node --check` no script extraído + teste DOM (jsdom) dos 17 nichos (0 erros) + inspeção visual do nicho (templates, prompts, behaviors, tags).
6. **Publicar** o `index.html` completo + atualizar `meta/CHANGELOG.md` (nova versão) e `meta/STATUS.md`.

### Padrão de qualidade de um nicho aprofundado
- Arquivo "âncora" (CONTEXT/PROJETO/equivalente) com: o que é, como funciona o crítico, **armadilhas**, e o **ângulo próprio do nicho** (produto no dev; relação+escopo no client).
- Arquivo de decisões em formato ADR quando fizer sentido.
- IDEAS/segundo-cérebro separando origem (usuário × assistente) + concluídas + descartadas.
- STATUS com seções de estado claras.
- Prompts: A-F universais (não mexer) + G+ cobrindo as tarefas reais do domínio.

---

## ✅ Validação (sempre antes de publicar)

```bash
# 1. Sintaxe do script
python3 -c "import re; html=open('index.html').read(); m=re.search(r'<script>(.*?)</script>',html,re.S); open('/tmp/c.js','w').write(m.group(1))"
node --check /tmp/c.js

# 2. Balanceamento de tags HTML (div/section/script/style/body/html)
# 3. Teste DOM com jsdom: clicar os 17 nichos, conferir 0 erros de JS,
#    e que cada um renderiza templates + prompts + preview + CLAUDE.md
```
Nunca publicar sem o teste DOM passar em 17/17 com 0 erros.

---

## 🚫 Não faça sem pedir

- Não reescrever os prompts universais A-F (são a "gramática" comum do kit).
- Não introduzir dependências, build, ou framework.
- Não refazer vários nichos de uma vez — é uma área por etapa (foi o erro original do MVP).
- Não apagar conteúdo dos meta-docs; CHANGELOG/DECISOES/IDEIAS só crescem.
- Não tratar feedback de outras conversas (GameDataHub etc.) como verdade absoluta: são referência, o assistente avalia e adapta ao que faz sentido para o kit.

---

## Idioma

Respostas e documentos em **pt-BR**, incluindo comentários no código.

---

*Este arquivo é o kit aplicado a si mesmo (dogfooding). Editável: é nosso.*

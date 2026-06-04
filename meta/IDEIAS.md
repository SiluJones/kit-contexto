# IDEIAS — Banco de ideias do Kit

> Ideias capturadas ao longo das conversas que originaram o kit. Marcação simples: ativa, refinada, descartada (com motivo), arquivada para depois.

---

## i1 — A separação contexto/histórico como princípio
**Status:** ativa, virou pilar arquitetural.
**Nota:** o que mata as conversas longas não é o limite por mensagem (continue), é o histórico cumulativo. A solução não é "comprimir" tudo, é separar o que precisa estar sempre presente do que pode ser consultado sob demanda.

---

## i2 — Múltiplos nichos profundos, não muitos rasos
**Status:** ativa, definidora do escopo.
**Nota:** 17 prontos + 1 custom. Recusa explícita a "nichos parasitas" que sobrepunham (Solo Dev Studio caiu por isso — virou Custom preset).

---

## i3 — Brainstorm como o nicho deste próprio kit
**Status:** ativa, virou meta-doc.
**Nota:** o kit aplicado a si mesmo. Pasta `meta/` é a prova de fogo do nicho Brainstorm.

---

## i4 — Cada nicho com hero visual distinto na Home
**Status:** ativa, implementada para os 18.
**Nota:** não basta trocar cor da paleta. O ambiente visual carrega o tom. Terminal para Dev (você sente o terminal). Postits para Brainstorm. Scroll medieval para RPG. Card de receita para Cozinha.

---

## i5 — Templates com nomes profissionais
**Status:** ativa, regra editorial.
**Nota:** sem "DEFINITIVO", "APRIMORADO", "FINAL". O nome do template é a função do arquivo. Padronização adulta.

---

## i6 — Custom realmente extensível
**Status:** ativa, virou construtor.
**Nota:** define identidade + arquivos + comportamentos + prompts + cor + fonte. Salva preset em localStorage. Múltiplos presets simultâneos.

---

## i7 — Prompts A-F universais, G+ específicos por nicho
**Status:** ativa, definidora da estrutura.
**Nota:** ciclo de vida do projeto (setup, sessão, encerramento, migração) é o mesmo em todo domínio. O que muda são as tarefas específicas.

---

## i8 — STATUS.md sempre rolante (não vira histórico)
**Status:** ativa, regra de uso.
**Nota:** STATUS é "agora", não "tudo que aconteceu". Logs vão pro Git. Decisões importantes vão pra DECISOES.md.

---

## i9 — Tema claro
**Status:** arquivada para depois.
**Nota:** o kit hoje é só escuro. Tem gente que prefere claro. Adicionar isso significaria revisar todas as paletas dos nichos. Não é prioridade.

---

## i10 — Tradução para inglês
**Status:** arquivada para depois.
**Nota:** dobrar texto, manter sincronizado. Vale considerar se o uso crescer.

---

## i11 — Exportar/importar preset Custom como JSON
**Status:** arquivada como evolução natural.
**Nota:** o preset Custom hoje só vive no navegador. Permitir baixar/colar JSON resolve "quero meu preset em outro dispositivo".

---

## i12 — Galeria de presets compartilhados
**Status:** descartada na v1.
**Nota:** exigiria back-end. Tira a simplicidade do kit-página. Pode existir num produto separado, não neste.

---

## i13 — Versão impressa (PDF) dos templates
**Status:** arquivada.
**Nota:** alguns nichos (cozinha, RPG) podem se beneficiar. JSZip já cuida do empacotamento; PDF seria extra.

---

## i14 — "Solo Dev Studio" como nicho
**Status:** descartada, virou caso de Custom.
**Nota:** sobrepunha Game Design quando o foco era game, e Dev + Produto quando era app. Sem ganho real.

---

## i15 — Nicho de Educação / Aprendizado pessoal
**Status:** descartada na v1.
**Nota:** amplo demais. Quem estuda formalmente cabe em Pesquisa. Quem cria material didático cabe em Marketing/Conteúdo. Quem cuida de roteiro de aula cabe em Custom.

---

## i16 — Nicho de Saúde / Bem-estar
**Status:** descartada deliberadamente.
**Nota:** território sensível. Não quero fazer prompts que possam mascarar conselho médico.

---

## i17 — Nicho de Finanças pessoais
**Status:** descartada na v1.
**Nota:** mesmo motivo de saúde — território onde um nicho pronto pode virar conselho financeiro implícito. Cabe muito bem em Custom.

---

## i18 — Nicho jurídico (Direito)
**Status:** descartada na v1.
**Nota:** domínio profissional sério, exigiria precisão sobre citação de leis e jurisprudência por país. Custom dá conta.

---

## i19 — Memória do Claude como toggle no kit
**Status:** descartada.
**Nota:** a memória do Claude é configuração do Claude.ai, não do kit. O fluxo recomendado já cobre conversas novas via Prompt A.

---

## i20 — Drag-and-drop para reordenar arquivos do Custom
**Status:** arquivada como polish.
**Nota:** ordem dos arquivos não afeta funcionamento; é UX. Pode entrar numa v1.1 se eu tocar de novo no Custom.

---

## i21 — Auto-save da configuração além do localStorage
**Status:** ativa, já implementada como persistência por nicho.
**Nota:** cada nicho tem seu próprio state salvo. Trocar de nicho e voltar recupera.

---

## i22 — Validação do JSON de preset importado
**Status:** vinculada à i11.
**Nota:** se eu permitir importar preset, preciso validar. Não é trivial.

---

## i23 — Modo "biblioteca pessoal" de prompts custom
**Status:** descartada na v1, vira parte do Custom.
**Nota:** ao salvar preset, você salva seus prompts G+. Não preciso de uma biblioteca paralela.

---

## i24 — Atalhos de teclado
**Status:** arquivada como polish.
**Nota:** Esc fecha overlay já existe. Mais atalhos (Cmd+1/2/3/4/5 para navegar views) seriam um nice-to-have.

---

## Arquivadas com motivo (resumo)

- i9, i10, i11, i13, i20, i22, i24 — evoluções possíveis, sem prioridade
- i12, i19, i23 — descartadas por mudar a natureza do kit
- i14 — descartada por sobreposição
- i15, i16, i17, i18 — descartadas por escolha editorial (cabem em Custom)

---

## i-N1 — Git commit pronto ao final de toda entrega de código/conteúdo (IMPLEMENTAR JÁ)
**Status:** aprovada — virou princípio (CLAUDE.md do kit + behavior dos nichos onde houver Git).
**Nota:** sempre que algo for para o GitHub, o assistente entrega no final a mensagem de commit pronta na convenção correta (Conventional Commits), fácil de copiar e colar. O usuário pediu explicitamente "fácil para copiar". Aplicar ao próprio projeto também.

---

## i-N2 — Mecanismo de segurança para dados pessoais/sensíveis nos documentos (ADIAR p/ análise longa)
**Status:** arquivada para análise profunda futura — NÃO implementar agora.
**Problema:** durante uma conversa, o usuário pode mencionar algo pessoal/constrangedor de passagem (exemplo dado por ele: comentar que não tem namorada no meio de uma ideia). Isso poderia ser salvo literalmente num documento de contexto. A pergunta: o kit deveria ter um mecanismo que, ao detectar informação realmente pessoal/comprometedora que precise aparecer, pergunte permissão antes de registrar?
**Tensão identificada pelo próprio usuário (importante):** o medo é que um mecanismo desses ESTRAGUE o processo — reduzindo/limitando a captura de informação importante (ideias, funcionamento da ferramenta). Hoje ele não passa nada realmente pessoal além das ideias, e QUER que elas sejam registradas com riqueza.
**Avaliação preliminar (a aprofundar):** distinguir "informação pessoal incidental e irrelevante ao projeto" (não registrar — não tem valor de contexto mesmo) de "informação que o projeto precisa". O primeiro caso já deveria ser filtrado naturalmente por relevância, sem precisar de mecanismo especial nem de perguntar. O risco do mecanismo é gerar fricção e perda. Requer: pesquisa sobre privacy-by-design em ferramentas de nota, análise de onde traçar a linha, e o usuário formular melhor o caso. Por ora: o princípio geral de só registrar o que tem valor de contexto provavelmente já cobre 90%.

---

## i-N3 — "Backdoor" de atualização do kit + prefixo/sufixo configurável nos downloads
**Status:** ativa, a avaliar viabilidade (2 partes).
**Parte A — canal de atualização:** um mecanismo que prepare a conversa (e o Claude) para receber atualizações do kit — novos princípios, cláusulas, templates refinados — de forma que conversas que já usam o kit possam ingerir as novas regras facilmente, só subindo as novas versões de template. Ideia: um arquivo/seção "changelog de regras do kit" que o usuário sobe, e o Claude reconhece e aplica.
**Parte B — prefixo/sufixo nos downloads:** uma opção no kit que ofereça adicionar prefixo ou sufixo aos arquivos baixados (ex.: CLAUDE.md → CLAUDE__v1.8.md ou meuprojeto__CLAUDE.md), com um padrão convencional/identificador. Útil para versionar e para a ingestão de dados.
**Avaliação preliminar:** Parte B é viável e barata (é só manipulação de string no nome do arquivo no download — já temos a função downloadFile). Parte A é mais sutil: "preparar o Claude" não é algo que o kit-HTML faça (o kit gera texto; quem "prepara o Claude" é o conteúdo que entra nas Instruções/CLAUDE.md). Pode ser resolvido com uma seção no CLAUDE.md tipo "se o usuário trouxer um arquivo de atualização do kit, aplique as novas regras aos próximos outputs". A avaliar com calma.

---

## i-N4 — Mecânica "concluir entrega + perguntar permissão no mesmo turno"
**Status:** ativa, a refinar como regra de eficiência.
**Nota:** o usuário sugeriu (e o assistente concordou): quando uma nova ideia exige permissão/decisão dele para prosseguir, em vez de só perguntar e gastar um turno, o assistente avalia se dá para JÁ concluir e entregar uma parte de trabalho útil (ex.: a próxima etapa de nicho) e deixar a pergunta de permissão no final — aproveitando o turno. Eficiência de tokens. A refinar: só vale quando o trabalho a adiantar é independente da decisão pendente (não pode depender da resposta). Candidato a virar nota no CLAUDE.md do kit como prática de trabalho.

---

## i-N5 — Comandos de terminal sensíveis ao SO (Windows/Mac/Linux)
**Status:** ativa, a avaliar. Surgiu de um bug real.
**Problema:** o assistente gerou um `git commit` com continuação de linha `\` (sintaxe bash/Linux) e quebrou no CMD do Windows do usuário (`'\' is outside repository`). Isso vale para QUALQUER comando de terminal que o kit ou o Claude gere.
**Implicação no kit:** as Instruções/CLAUDE.md geradas podem conter comandos (git, instalação, scripts). Se o usuário estiver em Windows (CMD ou PowerShell), Mac ou Linux, a sintaxe muda (continuação de linha, separadores de path, aspas).
**Possível solução:** o kit poderia ter um campo no builder ("Sistema operacional / shell: Windows-CMD / Windows-PowerShell / Mac-Linux") que injeta na instrução a convenção certa de comando. Ou uma regra no CLAUDE.md gerado: "comandos de terminal no formato compatível com o SO do usuário; na dúvida, perguntar". Para o nosso projeto já foi resolvido (CMD Windows, -m repetido numa linha só). A avaliar como generalizar para os nichos que envolvem terminal (dev principalmente).

---

# Atualização de status — 2026-06-02 (sessão de consolidação)

## i-N1 (commit ao final) — ✅ IMPLEMENTADA E GENERALIZADA (v1.19.0)
Antes só no CLAUDE.md do nosso projeto (dogfooding); agora é seção do UPDATE_PROTOCOL → aparece no CLAUDE.md de TODOS os nichos, sensível ao SO.

## i-N2 (privacidade / dados pessoais) — ✅ IMPLEMENTADA (v1.20.0)
No formato relevância + marcação (NÃO censura): incidental irrelevante fica fora por irrelevância; sensível-mas-útil é sinalizado com opção de generalizar/omitir; na dúvida, pergunta. Seção do UPDATE_PROTOCOL.

## i-N3 (backdoor de atualização + afixo) — ✅ AMBAS IMPLEMENTADAS
- Parte B (afixo prefixo/sufixo): v1.9.0.
- Parte A (canal de atualização): v1.19.0 — seção no CLAUDE.md que ensina o Claude a reconhecer/aplicar updates do kit trazidos para a conversa.

## i-N4 (entregar + perguntar no mesmo turno) — ✅ JÁ É PRÁTICA
No CLAUDE.md do projeto. Usada o tempo todo nesta jornada.

## i-N5 (comandos sensíveis ao SO) — ✅ IMPLEMENTADA (v1.11.0)
Seletor de SO no builder; injeta sintaxe em Instruções e CLAUDE.md.

---

## i-N6 — Custom Inteligente (composição assistida de nichos) — APROVADA, A IMPLEMENTAR
A grande próxima feature. Ver D-014 (DECISOES) e a seção dedicada no STATUS. Resumo: 2º nicho de construção que importa/concatena material de nichos existentes, com dedup visível, sub-painel de seleção fina e checagem de conflito (spec-kit-inspired). NÃO fusão automática.

## i-N7 — spec-kit para refinar dev e game (FUTURO, do usuário)
Quando tiver mais feedback de uso dos nichos dev e game, o usuário pedirá uma análise do que do GitHub spec-kit (Spec-Driven Development) pode tornar os PROCESSOS desses nichos mais completos. O usuário não tem certeza se vai conseguir usar o spec-kit em si, mas quer a análise. Anotado.

## i-N8 — Exemplos prontos no Custom (instanciar nichos candidatos) — IDEIA do usuário, condicional
Após o Custom Inteligente, avaliar oferecer "exemplos" prontos para criar instantaneamente os nichos que ficaram de fora (ver NICHOS-CANDIDATOS.md) — ou instruir como criá-los. O usuário disse "se for problemático, esqueça". A reavaliar depois do Custom Inteligente.

---

# Atualização de status — 2026-06-03 (sessão sobre contexto/RAG e transferência)

## i-N9 — Protocolo de transferência entre conversas (contexto vs. RAG + handoff) — ✅ IMPLEMENTADA (v1.21.0)
**Origem:** do usuário (que sofria com a falta de clareza sobre o que o Claude consegue ou não fazer com arquivos do Projeto vs. anexados) + análise/pesquisa do assistente.
**O que é:** uma seção transversal no CLAUDE.md gerado (UPDATE_PROTOCOL → todos os nichos) que ensina o assistente a: reconhecer os dois modos do conhecimento do Projeto (in-context vs. RAG/"Modo de pesquisa"); **nunca reconstruir um arquivo a partir de fragmentos** (regra dura anti-arquivo-falso — pedir o anexo); orientar onde colocar cada arquivo (leve→Projeto por upload direto; pesado/em-edição→anexo); e fazer o **handoff ao final** — dizer arquivo-por-arquivo onde colocar para a próxima conversa e montar um PROMPT DE INÍCIO pronto. Mais uma seção de ensino ("Contexto vs. RAG") na view Tokens & Fluxos para o usuário.
**Por que importava:** o usuário pôs projetos em risco ao transferir confiando cegamente nos arquivos do Projeto em modo de busca. Ver D-015 para o fundamento técnico (docs oficiais + práticas de context engineering: janela = RAM, arquivos = disco; sumarização iterativa ancorada = papel do STATUS).
**A vigiar (do usuário):** auditar projetos transferidos no passado para detectar corrupção por edição-via-fragmentos.

## i-N10 — Afixo de versão automático / "carimbo de versão do kit" nos downloads (SEMENTE, do usuário)
**Status:** semente — surgiu de raspão ("um padrão convencional/identificador" na i-N3-B). Vale considerar: o kit poderia oferecer carimbar automaticamente a versão do kit no nome ou no rodapé dos arquivos gerados, ajudando o "canal de atualização" a saber de qual versão um arquivo veio. Não prometido.

---

## i-N9 (extensão v1.22.0) — Mount/ferramenta de código no protocolo + diretrizes refinadas — ✅ IMPLEMENTADA
Continuação da i-N9. O usuário trouxe duas conversas (`Tentativa_1.md`, `Analisada.md`) que expuseram uma divergência (uma dizia "leio do mount em RAG, não precisa anexar"; a outra dizia "anexe por causa do RAG") e atritos entre diretrizes. **Verifiquei empiricamente** que o `/mnt/project/` é um mount lido inteiro pela ferramenta de código mesmo em RAG (li o index completo, byte-idêntico). Resultado: corrigida a seção de transferência (o critério é "tenho o arquivo COMPLETO?", não "está em RAG?"); adicionado o caminho limpo (tudo no Projeto + ferramenta de código → mount, sem anexar) + ritual de checar o mount; e refinadas as diretrizes universais (BEHAVIORS_BASE 9→11): P2 esclarecido, P3 "sem rodeios", P8 anti-inferir, **P10 Cadência**, **P11 Não regride/mistura versões**. Ver D-016.

## i-N11 — "Ativar a ferramenta de código" como passo padrão do handoff (do usuário) — ✅ IMPLEMENTADA (v1.22.0)
O usuário quis que, para os projetos dele (dev/game), toda transferência já comece com a ferramenta de código ligada e usando o mount — sem ter que pedir a cada vez para verificar se dá para atualizar scripts/metadados, e sem se limitar a "dev lê pelo mount; chat comum anexa". Atendido: o prompt de início gerado lembra de ligar a ferramenta de código; o CLAUDE.md manda o assistente checar o mount no início e pedir para ligar se faltar. (O toggle em si é do usuário — não dá para um prompt ligar sozinho; o kit resolve com lembrete + ritual de verificação.)

---

## Nichos como ideias FUTURAS (adiados de propósito pelo usuário)
Ver NICHOS-CANDIDATOS.md (recuperado dos PLANNING). Não fazer agora. Prioridade do assistente se um dia expandir: Educação & Cursos (nº1); Desenvolvimento Pessoal/Journaling (cuidado: sensível); depois Jurídico/Podcast/Tradução. Tradução & Localização foi sugestão do assistente (não estava no PLANNING).

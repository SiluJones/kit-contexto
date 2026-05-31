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

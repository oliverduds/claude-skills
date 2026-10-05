---
name: refinar
description: Refina uma ideia inicial vaga em um brief completo antes de construir, fazendo rodadas de perguntas de múltipla escolha (sempre com uma opção marcada como recomendada e a saída "Outro" para texto livre) até fechar objetivo, critério de "pronto", formato de entrega, restrições e regras de parada, seguindo o guia "Getting the most out of Opus 5.5". Use quando o usuário invocar /refinar ou pedir explicitamente para refinar, afinar, lapidar, destrinchar ou fechar o escopo de uma ideia antes de começar ("refina isso comigo", "me ajuda a fechar o escopo", "vamos amadurecer essa ideia", "refine this idea with me", "help me scope this before building"). Não use em pedidos comuns que não pedem refinamento, nem para otimizar um prompt já escrito (isso é o prompt-optimizer).
argument-hint: "<ideia inicial, em uma ou duas frases>"
---

# /refinar — da ideia vaga ao brief pronto para construir

O usuário manda o começo de uma ideia ("quero um dashboard de vendas", "preciso de um relatório sobre X"). Seu trabalho é transformar isso num brief que um modelo consiga executar de ponta a ponta sem voltar para perguntar, e depois construir a partir dele. O brief segue o guia *Getting the most out of Opus 5.5* (resumo em [references/guia-opus.md](references/guia-opus.md)): tarefa inteira numa mensagem, linha de chegada explícita, regras de parada claras, sem frases de "pense com cuidado".

A forma de chegar lá é por perguntas de múltipla escolha, nunca por perguntas abertas. O motivo: o usuário quer decidir rápido, comparando alternativas concretas, e ter sempre uma saída recomendada para quando não tiver opinião. Texto livre continua disponível porque a ferramenta de perguntas já adiciona "Outro" em cada pergunta.

## Fluxo

### 0. Ler a ideia e mapear o que falta

Antes de perguntar qualquer coisa, leia a ideia e o contexto disponível (repositório aberto, arquivos citados, conversa anterior). Classifique o tipo de pedido, porque isso muda quais lacunas importam:

| Tipo | Exemplos | Lacunas que mais pesam |
|---|---|---|
| Software | feature, script, app, refatoração, automação em código | onde vive (repo/stack), como se prova que funciona, o que não tocar |
| Documento / texto | relatório, petição, post, apresentação, e-mail | público e uso, tom, formato final, fontes |
| Pesquisa / análise | comparar opções, levantar dados, estudar um tema | pergunta exata, fontes aceitas, forma do resultado, o que fazer com o que não se confirma |
| Processo / automação | rotina, pipeline, integração entre ferramentas | gatilho, entrada e saída, falhas aceitáveis, quem aprova |
| Outro | qualquer coisa fora disso | trate pelo brief genérico abaixo |

Monte mentalmente o brief (template mais abaixo) e marque quais campos a ideia já responde. **Nunca pergunte o que já foi dito ou o que dá para descobrir sozinho** (lendo o código, um arquivo, uma URL). Perguntar o óbvio desperdiça a atenção do usuário e faz o fluxo parecer burocrático.

O banco de perguntas por tipo está em [references/banco-de-perguntas.md](references/banco-de-perguntas.md). Use como repertório, não como checklist: escolha as que fecham as lacunas reais desta ideia.

### 1. Rodadas de perguntas (AskUserQuestion)

Use a ferramenta `AskUserQuestion`. Regras do formato, que são o que o usuário pediu:

- **Até 4 perguntas por rodada.** Agrupe as lacunas mais decisivas primeiro: ordem típica é objetivo/resultado concreto → critério de "pronto" → formato de entrega → restrições e o que não fazer → regras de parada → divisão do trabalho.
- **Divisão do trabalho só vira pergunta quando a tarefa tem partes independentes** (vários serviços, arquivos, fontes ou documentos que não dependem um do outro). Nesse caso, ofereça "Dividir entre subagentes (Recomendado)" com a lista das partes na descrição, contra "Fazer em sequência na sessão". Tarefa pequena ou linear não ganha essa pergunta: você escreve "Na sessão" no brief e segue. Subagente custa tokens e coordenação, só compensa quando há paralelismo real.
- **2 a 4 opções por pergunta**, mutuamente exclusivas (ou `multiSelect: true` quando combinar faz sentido).
- **A opção recomendada vem primeiro, com "(Recomendado)" no rótulo.** Recomende de verdade: a que você escolheria se tivesse que decidir sozinho, pelo que já sabe do contexto.
- **Cada opção = rótulo curto + descrição do que acontece se for escolhida.** O usuário deu este modelo de formato (é exemplo de forma, não são as opções a oferecer):
  - "Me dê opções" → eu apresento as alternativas.
  - "Me faça perguntas antes de começar" → eu uso esse recurso para esclarecer o que você quer.
  - "Não pergunte, escolha a melhor opção" → eu sigo com a opção padrão sem parar para perguntar.

  A descrição diz a consequência, não só repete o rótulo.
- **Sem perguntas abertas.** Se a resposta é um dado (URL, nome, número), ou você descobre sozinho, ou oferece opções plausíveis e deixa "Outro" para o usuário digitar.
- **Rótulo com no máximo 5 palavras, cabeçalho com no máximo 12 caracteres.** A interface corta o resto.

Quando a resposta vier por "Outro" e abrir lacunas novas, uma rodada a mais é normal. Quando o usuário responder algo que torna uma pergunta planejada irrelevante, descarte-a.

**Critério de término:** pare de perguntar quando todos os campos do brief estiverem preenchidos e nenhuma dúvida restante mudaria materialmente o trabalho. Dúvidas menores viram "Premissas" no brief, não perguntas. Normalmente são 2 ou 3 rodadas; se passar de 4, você está perguntando coisas que deveria assumir.

### 2. Apresentar o brief e pedir decisão

Mostre o brief no template abaixo, em português, e feche com uma última `AskUserQuestion`:

- **Construir agora (Recomendado)** → executo o brief inteiro nesta sessão, parando só nos pontos definidos nele.
- **Ajustar algo** → você pergunta, em mais uma múltipla escolha, qual seção ajustar (o usuário descreve a mudança pelo "Outro"), corrige o brief e repete esta decisão.
- **Salvar e parar** → grava o brief em `BRIEF.md` no diretório de trabalho e encerra; o usuário constrói depois.

### 3. Construir

Se aprovado, trate o brief como a tarefa inteira. Isso é o que o guia pede: receber tudo de uma vez e seguir até a linha de chegada. Em particular:

- Siga as **Regras de parada** do brief ao pé da letra. Quando um passo não precisa do usuário, continue; ponha notas de status na mesma mensagem da próxima ação.
- Em trabalhos longos, mantenha a lista de tarefas em `TASKS.md`, ticando o que terminou e adicionando o que descobrir. Isso sobrevive a resumos de contexto.
- Siga a **Divisão do trabalho** do brief. Se ela lista partes para subagentes, dispare todos na mesma vez (não um de cada vez), passe a cada um a parte do brief que lhe cabe mais o critério de "pronto" e as restrições, e confira a evidência de cada um antes de aceitar (leia o arquivo, rode o teste, abra a página). Consolide no formato que o brief pediu. Se o brief diz "Na sessão", não delegue.
- Ao terminar, abra o relatório com **"O que preciso de você"** (decisões, aprovações, dúvidas) antes do resumo. É a primeira coisa que o usuário vai ler.
- Marque o que não conseguiu confirmar e onde procurou.

## Template do brief

```markdown
# Brief: <título curto>

**Objetivo.** O que o usuário quer e para quê, em 1–2 frases.

**Pronto significa.** Lista verificável. Cada item é algo que dá para checar
(um teste passa, um arquivo existe com tal estrutura, uma página abre e mostra X).

**Entrega.** Formato e local do resultado (arquivo, PR, documento, mensagem),
com estrutura quando couber ("uma linha por fornecedor, colunas: custo, fim do contrato, dono").

**Contexto e insumos.** Repositório, arquivos, URLs, dados, decisões já tomadas.

**Restrições.** O que não fazer, o que não tocar, estilos a evitar
(para design: nomeie os padrões a deixar de fora, não diga só "evite o genérico").

**Regras de parada.** Quando continuar sem perguntar e quando parar:
sempre antes de algo destrutivo (apagar dados, force-push, mudar algo fora do repositório)
e nos pontos que o usuário escolheu.

**Divisão do trabalho.** "Na sessão" quando a tarefa é uma sequência só.
Quando há partes independentes (vários serviços, arquivos, fontes, documentos),
liste-as e diga que cada uma vai para um subagente, que a evidência de cada um é conferida
antes de aceitar, e como o resultado é consolidado (uma tabela, um PR, um arquivo).

**Premissas.** Decisões menores que você tomou sem perguntar, para o usuário poder vetar.

**Fora de escopo.** O que fica para depois.
```

Omita uma seção só se ela realmente não se aplica (um texto de 3 parágrafos não precisa de "Regras de parada"). Não escreva "pense com cuidado", "seja minucioso" nem variações: o modelo já pensa antes de responder e essas frases só atrasam.

## Exemplo resumido

**Ideia:** "/refinar quero um dashboard de vendas"

**Rodada 1** (4 perguntas): quem olha o dashboard e com que frequência; fonte dos dados (planilha / banco / API, com a recomendada baseada no que há no repo); formato (página HTML estática / app com filtros / notebook); período e granularidade.

**Rodada 2** (3 perguntas): métricas obrigatórias; o que não pode ter (estilos, bibliotecas pesadas, dados sensíveis); quando parar e perguntar (só se a fonte estiver inconsistente / também antes de publicar).

**Brief:** apresentado no template, com "Pronto significa: abre em navegador sem servidor, mostra receita mensal e top 10 clientes dos últimos 12 meses lidos de vendas.csv, filtra por vendedor, sem dependência externa além do CDN do Chart.js".

**Decisão:** Construir agora → executa até o fim, relatório começa por "O que preciso de você".

## Referências

- [references/guia-opus.md](references/guia-opus.md): princípios do guia resumidos, com as frases-modelo. Leia ao montar o brief se tiver dúvida sobre como formular "pronto", regras de parada ou pedidos de design.
- [references/banco-de-perguntas.md](references/banco-de-perguntas.md): perguntas prontas por tipo de ideia, já no formato rótulo + consequência.

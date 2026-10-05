# Guia "Getting the most out of Opus 5.5" — resumo para montar briefs

Fonte: https://claude.dev/blog/getting-the-most-out-of-opus-5-5/ (lido em 2026-10-04). Este arquivo existe para que a skill não precise buscar a URL em cada uso. Se o guia mudar, atualize aqui.

## Três coisas para fazer primeiro

1. **Entregue a tarefa inteira.** Diga como é "pronto" e quando quer que ele pare e pergunte. Depois deixe trabalhar.
2. **Apague as linhas "pense com cuidado".** O modelo já pensa antes de cada resposta e decide sozinho a profundidade. Tirar essas frases acelerou as respostas sem perda de qualidade.
3. **Quando uma execução longa terminar, leia primeiro o que ele precisa de você.**

## 1. Como pedir

### Diga como é "pronto" e deixe rodar
Dê a tarefa inteira numa mensagem só. Nomeie a linha de chegada. Exemplo do guia:

> "Migre os endpoints de pagamento do cliente antigo para o novo. Pronto significa: todo endpoint usa o cliente novo, o cliente antigo foi apagado e a suíte de testes passa. Pare e me pergunte só se um teste falhar por um motivo que você não consiga explicar."

Isso permite ao modelo reconhecer quando terminou, o que importa muito em trabalhos de vários passos.

**Para o brief:** a seção "Pronto significa" é uma lista verificável. Cada item precisa ser checável (um teste passa, um arquivo existe com tal estrutura, uma página abre e mostra X). "Ficar bom" não é critério.

### Pare de mandar "pensar forte"
Remova "think carefully", "think step by step", "seja minucioso" e variações de prompts e de instruções salvas.

### Acrescente a uma tarefa em andamento
Dá para mandar mensagens enquanto ele trabalha ("Também mantenha os nomes antigos dos endpoints como aliases"). Evita reiniciar tarefas longas.

### Em design, nomeie os estilos que você não quer
Em vez de "evite um visual genérico", liste os padrões a deixar de fora. Exemplo do guia:

> "evite fundos creme ou off-white, palavras em itálico de destaque nos títulos, rótulos de seção numerados, rótulos em monoespaçado ou botões em formato de pílula."

Depois itere sobre o que ele escolheu no lugar.

**Para o brief:** em qualquer pedido visual (página, app, artifact, slide), a seção "Restrições" lista padrões concretos a evitar.

## 2. Conduzindo execuções longas no Claude Code

### Diga quais paradas você quer
Regra sugerida para o CLAUDE.md, que serve igualmente como "Regras de parada" de um brief:

> "Quando um passo não precisar da minha opinião, continue. Ponha notas de status na mesma mensagem da sua próxima ação. Pare e pergunte só quando não conseguir continuar sem mim, ou antes de qualquer coisa destrutiva: apagar dados, force-push ou mudar algo fora deste repositório."

Mantenha os prompts de permissão ligados para comandos destrutivos.

### Divida trabalho grande entre subagentes
Para auditorias ou migrações grandes:

> "Dê cada serviço a um subagente próprio. Quando um subagente reportar, confira a evidência antes de aceitar. Termine com uma tabela só."

### Mantenha a lista de tarefas num arquivo

> "Mantenha um checklist em TASKS.md. Marque cada item quando terminar e acrescente qualquer coisa nova que encontrar."

Sobrevive ao resumo da janela de contexto em execuções longas.

## 3. Conferindo o resultado

### Leia primeiro o que ele precisa de você
Quando uma execução longa termina, procure decisões, aprovações e dúvidas pendentes antes de ler o resumo completo.

**Para o brief e para a construção:** o relatório final começa pela seção "O que preciso de você".

### Peça uma revisão do código antes de você revisar

> "Revise o diff deste branch contra main. Liste só problemas pelos quais você bloquearia o merge. Para cada um, dê arquivo e linha, por que está errado e como mostrar que falha."

### Peça para marcar o que não conseguiu confirmar
Em pesquisa: "marque tudo o que não conseguiu confirmar e diga onde procurou."

## 4. Nos apps do Claude

- **Anexe o gráfico ou a captura de tela** em vez de transcrever. O modelo lê relações espaciais e detalhes visuais com precisão.
- **Peça para checar documentos longos:** "Confira este deck procurando qualquer coisa que se contradiga: números, datas e nomes. Cite cada problema e diga onde está."
- **Peça o arquivo pronto**, com a estrutura: "uma linha por fornecedor, com colunas para custo, fim do contrato e responsável."
- **Em projetos longos, diga quando respostas estão fechadas:** "Quando você já tiver respondido algo, trate como resolvido. Foque no que estou pedindo agora e não revisite uma resposta anterior a menos que eu pergunte." Omita isso em trabalho analítico que precisa de refinamento iterativo.

## 5. Mensagens sinalizadas (flags)

Quando uma mensagem é sinalizada, o Claude costuma trocar para um modelo mais antigo. Volte pelo seletor de modelo (apps) ou `/model` (Claude Code), ou desligue a troca automática nas configurações. Não peça para ele reproduzir o raciocínio interno na resposta: isso dispara sinalizações.

## 6. Velocidade

Modo rápido (fast mode) no Claude Code para trabalho interativo de ida e volta: texto chega antes, custo por token maior.

## Checklist do guia (texto original resumido)

**Pedir**
- A tarefa diz como é "pronto".
- Nenhuma linha de "pense forte" em prompts ou instruções salvas.
- Pedidos de design listam os estilos a deixar de fora.
- Gráficos e capturas vão anexados, não redigitados.

**Execuções longas no Claude Code**
- O CLAUDE.md diz quando parar e quando continuar, e para parar antes de algo destrutivo.
- Prompts de permissão continuam ligados para comandos destrutivos.
- Auditorias e migrações grandes são divididas entre subagentes.
- A lista de tarefas fica num arquivo.

**Conferir**
- A parte "precisa de você" do relatório é lida primeiro.
- Uma passada de revisão roda antes de uma pessoa revisar.
- Respostas de pesquisa marcam o que não pôde ser confirmado.

**Flags**
- Você sabe voltar: seletor de modelo ou /model.
- "Trocar de modelo quando uma mensagem for sinalizada" está do jeito que você quer.

## Como isso vira campos do brief

| Princípio do guia | Campo do brief |
|---|---|
| Tarefa inteira numa mensagem | O brief inteiro é essa mensagem |
| Diga como é "pronto" | **Pronto significa** (lista verificável) |
| Peça o arquivo pronto, com estrutura | **Entrega** |
| Anexe o material em vez de transcrever | **Contexto e insumos** |
| Nomeie os estilos a deixar de fora | **Restrições** |
| Diga quais paradas quer; pare antes do destrutivo | **Regras de parada** |
| Trate respostas dadas como fechadas | **Premissas** (decisões já tomadas) |
| Divida entre subagentes; confira a evidência de cada um | **Divisão do trabalho** (subagentes só quando há partes independentes; "Na sessão" caso contrário) |
| Lista de tarefas em TASKS.md | Instrução de execução em trabalho longo |
| Leia primeiro o que ele precisa de você | Relatório final começa por "O que preciso de você" |
| Marque o que não confirmou | Instrução de execução em pesquisa |

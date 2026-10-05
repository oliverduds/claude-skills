# Banco de perguntas por tipo de ideia

Repertório, não checklist. Escolha só as que fecham lacunas reais da ideia em mãos e descarte o que o contexto já responde. Cada opção está no formato **rótulo → o que acontece se escolhida**. A primeira opção de cada pergunta é uma sugestão de recomendada; troque a recomendação quando o contexto apontar para outra.

Adapte os rótulos ao caso concreto: "Planilha vendas.csv" é melhor que "Planilha" quando você já viu o arquivo.

## Comuns a qualquer tipo

**Resultado concreto**
- Qual é a primeira coisa que você quer ver funcionando?
  - Versão mínima completa → entrego o fluxo inteiro em versão simples e itero depois.
  - Parte mais arriscada primeiro → ataco o trecho mais incerto e paro para mostrar.
  - Tudo de uma vez → só mostro quando o conjunto estiver pronto.

**Critério de pronto**
- Como você vai saber que ficou pronto?
  - Testes/verificação automática passam → defino as checagens e rodo até passarem.
  - Você olha e aprova → paro ao terminar e espero seu ok.
  - Métrica atingida → fixo um número alvo e reporto o alcançado.

**Regras de parada**
- Quando devo parar e te perguntar?
  - Só antes de algo destrutivo → sigo até o fim; paro antes de apagar, publicar ou mudar fora do escopo.
  - Em cada decisão de design relevante → paro para escolhermos juntos nas bifurcações.
  - Em marcos definidos → paro ao fim de cada etapa combinada.

**Divisão do trabalho** (só quando há partes independentes; liste-as na descrição)
- Como executar as partes?
  - Dividir entre subagentes → cada parte (A, B, C) vai para um subagente em paralelo; confiro a evidência de cada um e consolido num resultado só.
  - Em sequência na sessão → faço uma parte de cada vez, mais lento e mais fácil de acompanhar.
  - Só a primeira parte agora → entrego A, você avalia, e as outras ficam para depois.

**Prazo e tamanho**
- Quanto esforço faz sentido agora?
  - Rápido e funcional → simples, sem polimento, pronto hoje.
  - Bem feito → cobre casos de borda e tem testes/revisão.
  - Protótipo descartável → serve para validar a ideia e será jogado fora.

## Software

**Onde vive**
- Em qual repositório/stack isso entra?
  - Neste repositório, stack atual → sigo as convenções que já existem aqui.
  - Projeto novo → crio do zero, e pergunto a stack a seguir.
  - Script avulso → um arquivo só, sem estrutura de projeto.

- Stack para projeto novo (adapte ao que o usuário costuma usar):
  - Python → script/CLI ou FastAPI, com pytest.
  - Node/TypeScript → Node 20+, testes com vitest.
  - HTML estático → abre direto no navegador, sem build.

**Como se prova**
- Que tipo de teste você quer?
  - Testes automatizados novos → escrevo testes que cobrem o comportamento e rodo.
  - Só rodar os que existem → não crio testes, garanto que a suíte atual continua passando.
  - Verificação manual guiada → entrego um roteiro de passos para você conferir.

**Fronteiras**
- O que não devo tocar?
  - Só os arquivos da feature → não refatoro nada ao redor.
  - Posso ajustar o entorno → refatoro o necessário para a feature ficar limpa.
  - Nada fora de uma pasta → fico restrito ao diretório indicado.

**Dados e integrações**
- De onde vêm os dados?
  - Arquivo local existente → leio do caminho que você indicar.
  - Banco/API já configurado → uso a conexão que o projeto já tem.
  - Dados de exemplo → gero fixtures para desenvolver e troco depois.

**Entrega**
- Como você quer receber?
  - Commit em branch nova → deixo pronto para você revisar e abrir PR.
  - PR aberto → abro o PR com descrição e checklist.
  - Só arquivos no working tree → não comito nada.

## Documento / texto

**Público e uso**
- Quem vai ler e para quê?
  - Decisor que vai aprovar algo → curto, conclusão primeiro, opções com recomendação.
  - Equipe que vai executar → detalhado, passos e responsáveis.
  - Público externo → linguagem acessível, sem jargão interno.

**Tom e voz**
- Que tom?
  - Formal e objetivo → frases curtas, sem adjetivos, terceira pessoa.
  - Conversacional → primeira pessoa, direto ao leitor.
  - Voz já definida → sigo um guia de estilo/persona que você indicar.

**Formato final**
- Em que formato?
  - Markdown no chat/arquivo → texto simples, fácil de colar.
  - Documento (Docs/Word/PDF) → arquivo pronto para enviar.
  - Apresentação → slides com uma ideia por slide.

**Tamanho**
- Quanto texto?
  - Uma página → cabe numa tela, até ~500 palavras.
  - Completo → o que o assunto exigir, com seções.
  - Resumo executivo + anexo → curto na frente, detalhe atrás.

**Fontes**
- De onde tiro o conteúdo?
  - Material que você fornece → só uso o que você mandar.
  - Pesquisa na web com fontes citadas → busco, cito e marco o que não confirmei.
  - Conhecimento geral → sem citações, você revisa os fatos.

## Pesquisa / análise

**Pergunta exata**
- O que você precisa decidir com essa pesquisa?
  - Escolher entre opções → comparo e recomendo uma, com critérios.
  - Entender um tema → explico o estado da arte, sem recomendar.
  - Levantar números → tabela com valores, data e fonte de cada um.

**Fontes aceitas**
- Que fontes valem?
  - Oficiais/primárias → documentação, leis, papers, relatórios originais.
  - Qualquer fonte confiável → inclui imprensa e blogs técnicos, com link.
  - Só o material que você der → não busco fora.

**Forma do resultado**
- Como você quer ver?
  - Tabela comparativa → uma linha por opção, colunas pelos critérios.
  - Texto com recomendação → narrativa curta terminando numa escolha.
  - Relatório completo → seções, evidências e lista do que não foi confirmado.

**Incerteza**
- O que faço com o que não consigo confirmar?
  - Marco e sigo → aponto cada item não confirmado e onde procurei.
  - Paro e pergunto → interrompo quando uma lacuna muda a conclusão.
  - Deixo de fora → só entra o que tem fonte.

## Processo / automação

**Gatilho**
- O que dispara a rotina?
  - Horário fixo → agendamento (cron/tarefa agendada).
  - Evento → novo arquivo, e-mail, webhook, commit.
  - Manual → você roda quando quiser.

**Entrada e saída**
- O que entra e o que sai?
  - Arquivo → lê de uma pasta, grava em outra.
  - Serviço → lê de uma API/ferramenta e grava em outra.
  - Notificação → o resultado é uma mensagem para alguém.

**Falhas**
- O que acontece quando algo dá errado?
  - Avisa e para → notifica e aguarda alguém olhar.
  - Tenta de novo e registra → reexecuta N vezes e grava log.
  - Pula o item → continua com os demais e lista os que falharam no fim.

**Aprovação**
- Alguém aprova antes de a ação final acontecer?
  - Sim, sempre → gera rascunho/pendência e espera ok.
  - Só em casos sensíveis → define quais e para só neles.
  - Não → executa de ponta a ponta.

## Design / interface (complemento para qualquer tipo com parte visual)

**Estilos a deixar de fora** (multiSelect)
- O que não pode ter no visual?
  - Fundos creme/off-white → fundo branco ou escuro limpo.
  - Itálico de destaque em títulos → títulos retos.
  - Rótulos de seção numerados → sem "01, 02, 03".
  - Botões em pílula → cantos levemente arredondados.

**Referência**
- Tem referência visual?
  - Sistema de design existente → sigo tokens/componentes do projeto.
  - Captura de tela/link que você vai mandar → espero o material antes de começar.
  - Sem referência → proponho uma direção e você veta o que não gostar.

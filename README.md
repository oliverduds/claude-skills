# claude-skills

Skills pessoais para o Claude Code. Cada pasta em `skills/` é uma skill independente, com `SKILL.md` e, quando precisa, `references/` e `evals/`.

## Instalar

Em qualquer computador com Node 18+:

```bash
npx skills add oliverduds/claude-skills
```

O instalador lista as skills do repositório e pergunta quais instalar e onde (global, em `~/.claude/skills/`, ou só no projeto atual). Para atualizar depois:

```bash
npx skills update
```

Sem npx, basta copiar a pasta da skill para `~/.claude/skills/`:

```bash
git clone https://github.com/oliverduds/claude-skills
cp -r claude-skills/skills/refinar ~/.claude/skills/
```

## Skills

### refinar

Transforma uma ideia inicial vaga num brief completo antes de construir. Faz rodadas de perguntas de múltipla escolha (sempre com uma opção recomendada e a saída "Outro" para texto livre) até fechar objetivo, critério de "pronto", entrega, restrições, regras de parada e divisão do trabalho. Depois apresenta o brief e, se aprovado, constrói. O brief segue o guia [Getting the most out of Opus 5.5](https://claude.dev/blog/getting-the-most-out-of-opus-5-5/).

Uso:

```
/refinar quero um dashboard de vendas
```

Arquivos:

- `SKILL.md`: o fluxo.
- `references/guia-opus.md`: o guia resumido e a correspondência com os campos do brief.
- `references/banco-de-perguntas.md`: perguntas prontas por tipo de ideia.
- `evals/evals.json`: casos de teste usados no desenvolvimento.

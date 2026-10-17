# study-workflow-skills

Skills de estudo com IA. Cada skill funciona sozinha; juntas, formam um ciclo opcional de **estudar → validar → registrar → revisar**.

## Skills

| Skill | O que faz | Status |
| -- | -- | -- |
| `teacher-feedback` | Revisa o seu estudo como um professor: guia com perguntas em vez de dar a resposta e sempre cita a fonte | Disponível |
| `note-standardizer` | Converte um estudo em uma nota markdown padronizada (vault do Obsidian, com `[[links]]`) | Planejada |
| `learn-about` | Faz perguntas socráticas sobre um assunto e atualiza o seu nível por sub-tópico, com revisões espaçadas | Planejada |

As skills são independentes: não dependem umas das outras e cada uma pode ser usada isoladamente.

## Fluxo sugerido

Uma forma de usá-las em sequência (sugestão, nada é obrigatório):

1. Estude um assunto (por exemplo, Docker) e escreva um resumo com as suas palavras.
2. `teacher-feedback`: valida o resumo até estar correto.
3. `note-standardizer`: registra o estudo validado em uma nota padronizada.
4. `learn-about`: testa o que você aprendeu e agenda a próxima revisão. Se aparecer uma lacuna, volte ao passo 1.

## Entradas e saídas

1. **teacher-feedback**
   * Entrada: um resumo (texto colado ou arquivo anexado), opcionalmente com as fontes que você usou para estudar.
   * Saída: afirmações classificadas (corretas, incorretas, imprecisas ou não verificadas), perguntas e pistas para você chegar à resposta, e a fonte de cada verificação. A resposta direta só vem se você pedir.
2. **note-standardizer**
   * Entrada: um estudo.
   * Saída: nota markdown com as seções *O que é*, *Quando usar*, *Por que existe*, *Quando não usar*, *Exemplos*, *Tópicos relacionados*.
3. **learn-about**
   * Entrada: assunto + arquivo de contexto de domínio.
   * Saída: perguntas socráticas, avaliação das respostas, contexto atualizado (nível por sub-tópico) e agenda de revisão espaçada.

## Instalação

**Claude Code**

```bash
claude plugin marketplace add imJpereira/study-workflow-skills
claude plugin install study-workflow-skills@study-workflow
```

**Codex / Copilot CLI**

```bash
codex plugin marketplace add imJpereira/study-workflow-skills
codex plugin add study-workflow-skills@study-workflow
```

**Qualquer outro agente compatível com Agent Skills** (copia os arquivos, sem atualização automática)

```bash
npx skills add imJpereira/study-workflow-skills
```

## Referências

* Skill de referência: `learn-codebase`
* Projeto no Linear: [Learning Workflow](https://linear.app/joao-pedro-santos-pereira/project/learning-workflow-064a1774231f/overview)

## Licença

[MIT](LICENSE)

---
name: note-standardizer-with-obsidian
description: Transforma o resumo ou as anotações do usuário em uma nota markdown organizada para o Obsidian (frontmatter, seções definidas pelo conteúdo, [[wikilinks]] e relações reais com outras notas do vault, nos dois sentidos), mantendo as palavras e o tom do próprio usuário, e grava a nota direto na pasta do vault. Use sempre que o usuário colar ou anexar (docx, pdf, md, txt) um resumo, estudo, impressões de um livro, anotações de aula ou qualquer texto e pedir para padronizar, organizar, formatar, estruturar, "transformar em nota", "colocar no Obsidian" ou "deixar mais articulado" — mesmo sem dizer "Obsidian" ou o nome da skill.
---

# note-standardizer-with-obsidian

Você transforma o texto bruto do usuário em uma nota de Obsidian bem organizada. O valor da nota está em ser **do usuário**: ela deve soar como ele e conter o que ele realmente pensou. Seu trabalho é a estrutura e a clareza, não o conteúdo. Por isso você reorganiza e articula, mas não acrescenta fatos, não corrige conteúdo e não pesquisa.

Escreva na mesma língua do texto do usuário.

Um vault do Obsidian é só uma pasta de arquivos `.md` (com uma subpasta `.obsidian/`). Não existe MCP do Obsidian: você lê e grava os arquivos do vault diretamente.

## Entrada

Texto colado no chat ou arquivo anexado (docx, pdf, md, txt).

## Passo 0 — Ler as preferências

Se existir `~/.config/study-workflow-skills/note-standardizer.md`, leia antes de tudo. É uma lista de regras curtas em texto livre que guarda as escolhas do usuário (ex.: "tags em minúsculas e sem acento", "sem seção de Relações", o vault escolhido, se grava automático). Ordem de prioridade: o que o usuário pedir agora > preferências salvas > padrões desta skill. Ao final, diga em uma linha quais preferências aplicou (ex.: "Apliquei: tags minúsculas, vault X"), para o usuário poder ajustar. Se o arquivo não existe, siga com os padrões.

## Passo 1 — Montar a nota

**Seções saem do conteúdo.** Não há template fixo. Leia o texto, identifique os temas que ele realmente trata e agrupe por eles. Um resumo de Docker pode virar *O que é*, *Para que serve*, *Em que casos usar*; impressões de um livro podem virar *Personagens*, *Resumo da obra*, *Minha análise*, *Relação com filósofos*. Use nomes curtos, no estilo do que o usuário escreveu. Não crie seção vazia para algo que ele não abordou: uma nota com seções inventadas parece completa, mas finge conteúdo que não existe. Se o texto for curto ou de um tema só, faça uma nota enxuta, com uma ou duas seções, em vez de forçar divisões.

**Fidelidade à linguagem do usuário.** Articular significa ordenar, agrupar, ligar frases e corrigir gramática e digitação. Mantenha as palavras, os termos e o tom dele, mesmo informais (não troque "bagunça" por "heterogeneidade"), e a primeira pessoa. Evite floreio, frase de efeito e vocabulário mais "técnico" do que o dele. Quando o texto mistura fatos e opiniões (comum em livros e debates), mantenha as opiniões dele em seção própria e identificáveis como opinião, sem suavizar nem inflar.

**Sem conteúdo novo.** Não acrescente fatos, não corrija erros de conteúdo, não complete lacunas. Se notar uma lacuna ou algo que parece duvidoso, não mexa no texto: registre em **uma linha no fim da resposta** (fora da nota), por exemplo "não cobri X" ou "a afirmação Y parece duvidosa; se quiser validar, o `teacher-feedback` pode checar". A skill fica independente: validar é outra tarefa.

**Tema ambíguo.** Se o texto admite mais de uma leitura (ex.: "Python" como linguagem ou como cobra), escolha a mais provável, gere a nota e avise a suposição em uma linha no fim. Só pergunte antes se não houver jeito razoável de agrupar o conteúdo.

**Formato da nota**

```markdown
---
title: <título da nota>
tags: [<tag1>, <tag2>]
created: <AAAA-MM-DD de hoje>
---

# <título>

## <Seção derivada do conteúdo>
<texto do usuário, reorganizado>

## <Outra seção>
...

## Relações
<ver Passo 3>
```

- `[[wikilinks]]` no corpo só para conceitos que o usuário citou (ex.: `[[Container]]`, `[[Imagem]]`). Nada inventado.
- `## Relações` só existe se houver relações reais (ver Passo 3).
- Tags curtas, derivadas do assunto.

## Passo 2 — Achar o vault

Você precisa do vault para buscar relações e gravar. Resolva assim:

1. **Preferências já têm um vault** e a pasta ainda existe com `.obsidian/` dentro: use-o, sem perguntar.
2. **Caso contrário, descubra os candidatos.** Primeiro leia o registro de vaults do próprio Obsidian (Linux: `~/.config/obsidian/obsidian.json`; macOS: `~/Library/Application Support/obsidian/obsidian.json`; Windows: `%APPDATA%\obsidian\obsidian.json`), que lista os caminhos em `vaults`. Se não existir, procure pastas `.obsidian` (profundidade limitada, ex. 4, a partir de `~`, `~/Documents` e pastas de sincronização comuns; ignore pastas ocultas e `node_modules`). O vault é a pasta pai de `.obsidian`.
3. **Primeira vez: pergunte, nesta ordem, e espere a resposta:**
   - **Vault:** "É este o vault? `<caminho>`" (se houver vários, liste e peça para escolher; se não achar nenhum, diga e peça o caminho, ou siga só com o texto no chat).
   - **Pasta:** "Em qual pasta do vault as notas devem ir? (padrão: raiz)".
   - **Gravação:** "Quer que eu grave sempre direto no vault, ou prefere confirmar a cada nota?"
4. **Salve as respostas** em `~/.config/study-workflow-skills/note-standardizer.md` (crie a pasta e o arquivo se faltar), como linhas curtas, por exemplo:
   - `Vault do Obsidian: /caminho/do/vault`
   - `Pasta padrão das notas: Estudos/`
   - `Gravar direto no vault: sim` (ou `não, confirmar a cada nota`)

   Essas três respostas são pedidas justamente para guardar, então não precisa de um segundo "salvar?"; apenas avise em uma linha que ficaram salvas e que o usuário pode editar o arquivo ou pedir para mudar.

Se o usuário nega o vault sugerido, não insista: pergunte o caminho certo ou siga só com o texto no chat.

## Passo 3 — Relações

O usuário quer que as notas do vault fiquem ligadas, mesmo quando o resumo não menciona a ligação. Mas só entram relações que existem de verdade: nunca sugira tópicos que ainda não existem como nota. Uma lista de "talvez" polui o vault, e uma nota só ganha o link quando a outra existir.

Sem vault resolvido, não há relações: a nota sai sem a seção.

Com vault resolvido, liste as notas `.md` do vault (nomes de arquivo) e, se preciso, leia títulos, tags e cabeçalhos. Duas notas se relacionam quando há ligação **concreta**: o texto de uma cita ou depende do assunto da outra, ou uma é parte da outra (*Volumes* é parte de *Docker*). Ser "do mesmo tema geral" não basta. Na dúvida, não relacione.

- **Nota nova:** ponha em `## Relações`, no fim, um link puro para cada nota existente relacionada (`- [[Docker]]`), sem frase explicativa escrita por você, para não inventar texto. Se não achou nenhuma relação, omita a seção (sem seção vazia).
- **Notas existentes:** para cada nota relacionada, acrescente uma linha com o link para a nova em `## Relações` dela, criando a seção no fim se não existir. Só acrescente essa linha: não altere mais nada na nota antiga e não duplique um link que já está lá.

Exemplo: o usuário cria *Volumes* e já existe *Docker*. *Volumes* ganha `- [[Docker]]` em Relações, e *Docker* ganha `- [[Volumes]]`. Se *Volumes* já tivesse sido criado antes de qualquer outra nota, não haveria Relações nele; quando *Docker* chegar, *Docker* liga em *Volumes* e *Volumes* ganha o link de volta.

Se as preferências do usuário dizem para omitir relações, omita.

## Passo 4 — Entregar e gravar

Mostre sempre a nota completa em markdown no chat, seguida das linhas de aviso (lacunas, suposições, preferências aplicadas).

Depois grave no vault, conforme a preferência:

- **"Gravar direto: sim":** grave em `<vault>/<pasta padrão>/<Título>.md`, aplique as linhas de Relações nas notas existentes (Passo 3) e diga o caminho final. Liste no fim exatamente o que mudou nas notas antigas (nota e linha acrescentada).
- **Confirmar a cada nota:** pergunte "Gravar em `<caminho>`?" mostrando também as edições planejadas nas notas antigas (nota e linha), e só aplique com um sim.
- **Sem vault resolvido:** só devolva o texto e diga que não gravou nada.

Se a nota nova não for gravada, nenhuma nota antiga é alterada.

**Nunca sobrescreva.** Se já existir nota com esse nome, pare e pergunte se prefere outro título ou acrescentar ao conteúdo existente; mesmo com "gravar direto: sim". Crie a pasta de destino se faltar. Nome de arquivo: o título, trocando caracteres inválidos em nomes de arquivo (`/ \ : * ? " < > |`) por espaço ou hífen.

## Passo 5 — Preferências

O usuário pode guardar outras preferências para as próximas notas no mesmo arquivo (`~/.config/study-workflow-skills/note-standardizer.md`, global, markdown simples, uma regra curta por linha, editável à mão). Além das respostas do Passo 2, grave só de duas formas, nunca em silêncio:

- o usuário pede ("lembra que eu prefiro X", "agora quero confirmar a cada nota"): grave;
- o usuário corrige o resultado ("tira essa seção", "tag em inglês"): pergunte "Salvar isso como preferência?" e grave só com um sim.

Acrescente a regra sem apagar as existentes; se uma nova contradiz uma antiga, atualize a antiga.

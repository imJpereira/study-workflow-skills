---
name: note-standardizer-with-obsidian
description: Transforma o resumo ou as anotações do usuário em uma nota markdown organizada para o Obsidian (frontmatter, seções definidas pelo conteúdo, [[wikilinks]] e uma seção de relações com outras notas), mantendo as palavras e o tom do próprio usuário. Use sempre que o usuário colar ou anexar (docx, pdf, md, txt) um resumo, estudo, impressões de um livro, anotações de aula ou qualquer texto e pedir para padronizar, organizar, formatar, estruturar, "transformar em nota", "colocar no Obsidian" ou "deixar mais articulado" — mesmo sem dizer "Obsidian" ou o nome da skill. Se houver um MCP do Obsidian conectado, busca relações no vault e oferece gravar a nota lá.
---

# note-standardizer-with-obsidian

Você transforma o texto bruto do usuário em uma nota de Obsidian bem organizada. O valor da nota está em ser **do usuário**: ela deve soar como ele e conter o que ele realmente pensou. Seu trabalho é a estrutura e a clareza, não o conteúdo. Por isso você reorganiza e articula, mas não acrescenta fatos, não corrige conteúdo e não pesquisa.

Escreva na mesma língua do texto do usuário.

## Entrada

Texto colado no chat ou arquivo anexado (docx, pdf, md, txt).

## Passo 0 — Ler as preferências

Se existir `~/.config/study-workflow-skills/note-standardizer.md`, leia antes de tudo. É uma lista de regras curtas em texto livre que o usuário foi salvando (ex.: "tags em minúsculas e sem acento", "pasta padrão `Estudos/`", "sem seção de Relações"). Ordem de prioridade: o que o usuário pedir agora > preferências salvas > padrões desta skill. Ao final, diga em uma linha quais preferências aplicou (ex.: "Apliquei: tags minúsculas, pasta Estudos/"), para o usuário poder ajustar. Se o arquivo não existe, siga com os padrões e não crie nada.

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
<ver Passo 2>
```

- `[[wikilinks]]` no corpo só para conceitos que o usuário citou (ex.: `[[Container]]`, `[[Imagem]]`). Nada inventado.
- Tags curtas, derivadas do assunto.

## Passo 2 — Relações

O usuário quer que a nota seja ligada a outras, mesmo que o resumo não as mencione. Essas ligações ficam na seção `## Relações`, no fim, identificada como adição da skill, para o corpo continuar sendo só o que o usuário disse.

- **Com MCP do Obsidian disponível:** busque no vault notas relacionadas ao assunto e ligue as que existem com `[[wikilinks]]`. Notas que fariam sentido mas ainda não existem entram numa lista à parte, como sugestão.
- **Sem MCP:** sugira `[[tópicos]]` pela sua própria avaliação e avise que não sabe o que existe no vault dele.

Se as preferências do usuário dizem para omitir a seção, omita.

## Passo 3 — Entregar e perguntar sobre gravar

Mostre sempre a nota completa em markdown no chat, seguida das linhas de aviso (lacunas, suposições, preferências aplicadas).

**Nunca grave sem perguntar.** Procure nas ferramentas disponíveis alguma que leia, escreva ou busque notas de um vault do Obsidian (não presuma nome de MCP). Se encontrar, pergunte: "Quer gravar no Obsidian? Em qual pasta?". Só grave com um sim, em `<Título>.md` na pasta indicada (ou na raiz do vault se ele não indicar). Nunca sobrescreva: se já existir nota com esse título, pare e pergunte se prefere outro título ou acrescentar ao conteúdo existente. Se não houver MCP, só devolva o texto e diga que não gravou nada.

## Passo 4 — Preferências

O usuário pode guardar preferências para as próximas notas, em `~/.config/study-workflow-skills/note-standardizer.md` (arquivo global, markdown simples, uma regra curta por linha, editável à mão). Grave nele só de duas formas, nunca em silêncio:

- o usuário pede ("lembra que eu prefiro X"): grave;
- o usuário corrige o resultado ("tira essa seção", "tag em inglês"): pergunte "Salvar isso como preferência?" e grave só com um sim.

Crie o arquivo (e a pasta) somente depois de um sim. Acrescente a regra sem apagar as existentes; se uma nova contradiz uma antiga, atualize a antiga.

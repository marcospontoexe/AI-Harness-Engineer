---
name: "salvar-contexto"
description: "Use quando o usuário disser 'salvar contexto', 'handoff' ou 'checkpoint', ao concluir uma funcionalidade ou milestone importante, ou quando a conversa ficar longa. Grava o estado da sessão no CONTEXTO.md da raiz do projeto (ou no arquivo de handoff que o projeto definir), seguindo um template de 9 seções, para que outro chat retome exatamente de onde parou."
---

# salvar-contexto

Grava todo o estado da sessão num arquivo de handoff, para que **qualquer outro chat consiga retomar exatamente de onde parou**, com o mesmo contexto. O próximo chat não tem memória nenhuma desta conversa: escreva para um estranho, de forma explícita.

## Onde gravar

- Por padrão, no `CONTEXTO.md` da raiz do projeto: um arquivo por projeto.
- **Exceção: projeto com regra própria de handoff.** Se o `CLAUDE.md` ou o `.claude/rules/` do projeto definir outro lugar para o estado da sessão, siga a regra dele: o lugar, o modelo e o procedimento. Ex.: com vários branches em paralelo, um arquivo por branch (`DOCS/handoff/<branch>.md`) evita que todo merge dê conflito no mesmo `CONTEXTO.md`.

## Procedimento

1. **Termine** a tarefa atual. Nunca pare no meio da edição de um arquivo.
2. **Crie ou atualize** o arquivo de handoff.
   - Se já existir, **atualize** as seções em vez de duplicar: mantenha o histórico relevante e remova o que já foi superado.
   - **Leia o arquivo imediatamente antes de editar** e altere só os trechos que mudaram. Outra sessão pode tê-lo reescrito depois da sua última leitura, e regravar o arquivo inteiro a partir de uma leitura antiga apaga o trabalho dela.
   - Se o arquivo descrever outra tarefa (seção 1) com o status geral "em andamento", outra sessão pode estar trabalhando nela em paralelo: não sobrescreva, pergunte ao usuário.
3. **Atualize o cabeçalho.**
   - Data e hora: pegue com o comando `date`; não estime.
   - Sessão nº: o número anterior + 1 (ou 1, se o arquivo é novo).
   - Status geral: "concluído" quando a tarefa terminou. É ele que avisa a próxima sessão de que pode começar outra tarefa sem perguntar.
4. **Preencha todas as seções** do template abaixo. Não deixe seção vazia: escreva "nenhum" quando não houver conteúdo.
5. **Mantenha o arquivo enxuto.** Cada seção tem só o resumo. Quando um tópico precisar de mais detalhe (uma decisão longa, um passo a passo etc.), escreva-o num arquivo em `DOCS/` na raiz do projeto e deixe no handoff só o link. Se esse tópico for durar além da tarefa, acrescente também uma linha com o link ao índice do `CLAUDE.md` do projeto, que deve continuar sendo só um índice.
6. **Separe o permanente do estado da sessão.** Uma armadilha ou um "sempre faça X" que vale além da tarefa atual vira uma regra curta em `.claude/rules/`: a do projeto, se ele estiver em git; senão, a `~/.claude/rules/`. Use `paths:` no cabeçalho da regra para limitá-la ao pacote ou ao tipo de arquivo a que ela se aplica. A regra aponta para o detalhe; o handoff só aponta para a regra.
7. **Confirme ao usuário** que o contexto foi salvo, com o caminho do arquivo em link. Se o projeto usar git, ofereça commitar o arquivo para que ele persista entre máquinas.

## Template

```markdown
# CONTEXTO DA SESSÃO

- **Última atualização:** AAAA-MM-DD HH:MM
- **Sessão nº:** N
- **Status geral:** (em andamento | bloqueado | pronto para revisão | concluído)

## 1. Objetivo da tarefa
Descrição em 1–3 frases do que estamos tentando alcançar (o "porquê").

## 2. Já feito ✅
- Itens concluídos, com o(s) arquivo(s) afetado(s).
- Ex.: "Implementado endpoint POST /login em [src/auth.py](src/auth.py)"

## 3. Em andamento 🔧
- O que estava sendo feito no momento do checkpoint.
- Em qual arquivo/linha parei e qual era o próximo passo imediato.

## 4. Próximos passos (planejado) 📋
- Lista ordenada do que falta fazer.
- Quanto mais específico, melhor (arquivo, função, comportamento esperado).

## 5. Decisões e raciocínio 🧠
- Escolhas técnicas feitas e o porquê.
- Alternativas descartadas (para evitar refazer a análise).
- Suposições assumidas.

## 6. Estado do projeto / ambiente
- Arquivos-chave e o papel de cada um.
- Branch git atual, alterações não commitadas, migrations pendentes, etc.
- Variáveis de ambiente ou dependências relevantes.

## 7. Bloqueios e pendências ⚠️
- Erros não resolvidos, dúvidas para o usuário, decisões aguardando aprovação.

## 8. Comandos úteis
- Comandos para rodar/testar/buildar o projeto.
- Ex.: `npm run dev`, `pytest tests/`, etc.

## 9. Como retomar
Instrução direta para o próximo chat: "Leia este arquivo e continue a partir
da seção 3 / passo X."
```

## Cuidados

- **Caminhos absolutos ou relativos à raiz**, nunca referências vagas ("aquele arquivo").
- **Não salve segredos** (tokens, senhas, chaves) no `CLAUDE.md` nem no handoff.
- **Arquivo cresceu demais:** mova as versões antigas para `CONTEXTO.arquivo.md`.
- **Não renumere seções que outros arquivos citam** (ex.: "CONTEXTO.md §5"): a citação passa a apontar para o lugar errado, sem aviso.
- **Pasta temporária não é backup:** `/tmp` e a pasta de rascunho da sessão podem ser apagadas sem aviso. O backup durável é o commit.

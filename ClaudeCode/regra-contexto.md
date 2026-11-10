# Regra: Persistência de Contexto (Handoff entre sessões)

> Cole esta regra no `CLAUDE.md` do projeto, ou no `~/.claude/CLAUDE.md` para valer em todos os projetos.

---

## Objetivo

Garantir que nenhum trabalho se perca quando a sessão atual se tornar demasiado longa. O agente deve gravar todo o estado da sessão num arquivo de handoff, de forma que **qualquer outro chat consiga retomar exatamente de onde parou**, com o mesmo contexto.

---

## Gatilho

Execute o procedimento de salvamento abaixo **antes de continuar qualquer tarefa** sempre que uma das seguintes condições for atingida:

1. A conversa prolongar-se por muitas interações (aproximando-se do limite prático da janela de contexto).
2. Uma funcionalidade ou milestone importante for concluída.
3. O usuário disser explicitamente: `salvar contexto`, `handoff` ou `checkpoint`.

> O agente não sabe com precisão quanto da janela de contexto já usou. O gatilho confiável é o comando explícito do item 3; além dele, salve por conta própria ao concluir cada bloco grande de trabalho.

---

## Procedimento de salvamento

1. **Termine** a tarefa atual. Nunca pare no meio da edição de um arquivo.
2. Crie ou atualize o arquivo **`CONTEXTO.md`** na raiz do projeto.
   - Se já existir, **atualize** as seções em vez de duplicar (mantenha o histórico relevante, remova o que já foi superado).
   - **Leia o arquivo imediatamente antes de editar** e altere só os trechos que mudaram. Outra sessão pode tê-lo reescrito depois da sua última leitura, e regravar o arquivo inteiro a partir de uma leitura antiga apaga o trabalho dela.
   - Se o arquivo descrever outra tarefa (seção 1) com o status geral "em andamento", outra sessão pode estar trabalhando nela em paralelo: não sobrescreva, pergunte ao usuário.
   - Sempre atualize o campo de data/hora e o número da sessão. Pegue a data e a hora com o comando `date`; não estime.
   - Quando a tarefa terminar, marque o status geral como "concluído". É o que avisa a próxima sessão de que pode começar outra tarefa sem perguntar.
3. Preencha **todas** as seções do template abaixo. Não deixe seções vazias — escreva "nenhum" quando não houver conteúdo.
4. Confirme ao usuário que o contexto foi salvo e informe o caminho do arquivo usando link.
5. **Gestão do CONTEXTO.md:** mantenha o CONTEXTO.md enxuto. Ele segue o template abaixo, mas cada seção deve ter só o resumo. Quando um tópico precisar de mais detalhe (uma decisão longa, um passo a passo etc.), escreva-o num arquivo em DOCS/ na raiz do projeto e coloque no CONTEXTO.md apenas o link para ele. O objetivo é não sobrecarregar a janela de contexto ao ler o CONTEXTO.md. Se precisar de mais informações sobre um tópico, abra o arquivo específico em DOCS/.
6. **Gestão do CLAUDE.md:** mantenha o CLAUDE.md do projeto enxuto também. Além destas regras, ele leva só um **índice**: uma linha por tópico, com o link para o arquivo detalhado em DOCS/.

---

## Template do `CONTEXTO.md`

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

---

## Como retomar em um novo chat

No início de qualquer nova sessão, o agente deve:

1. Verificar se existe o arquivo de handoff: o `CONTEXTO.md` na raiz do projeto (ou em `.claude/`), ou o que a regra própria do projeto definir.
2. Se existir, **lê-lo por completo antes de qualquer outra ação**.
3. Resumir ao usuário em 2–3 linhas onde o trabalho parou e qual é o próximo passo, e então continuar.

> Comando sugerido para o usuário iniciar um novo chat:
> **"Leia o `CONTEXTO.md` e continue de onde a sessão anterior parou."**

---

## Boas práticas

- **Escreva para um estranho:** o próximo chat não tem memória nenhuma; seja explícito.
- **Caminhos absolutos ou relativos à raiz**, nunca referências vagas ("aquele arquivo").
- **Não salve segredos** (tokens, senhas, chaves) no `CLAUDE.md` e `CONTEXTO.md`.
- **Um arquivo por projeto:** mantenha `CONTEXTO.md` enxuto; arquive versões antigas em `CONTEXTO.arquivo.md` se necessário.
- **Projeto com regra própria de handoff:** se o projeto já definir outro lugar para o estado da sessão, siga a regra dele no lugar do `CONTEXTO.md` da raiz. Ex.: com vários branches em paralelo, um arquivo por branch (`DOCS/handoff/<branch>.md`) evita que todo merge dê conflito no mesmo `CONTEXTO.md`.
- **Regra permanente não é estado de sessão:** uma armadilha ou um "sempre faça X" que vale além da tarefa atual vira uma regra curta em `.claude/rules/` (a do projeto, ou `~/.claude/rules/` para valer em todos os projetos). O `CONTEXTO.md` só aponta para ela.
- **Não renumere seções que outros arquivos citam** (ex.: "CONTEXTO.md §5.9"): a citação passa a apontar para o lugar errado, sem aviso.
- **Commit opcional:** se o usuário usar git, ofereça commitar o `CONTEXTO.md` para que ele persista entre máquinas. Pasta temporária (`/tmp`, a pasta de rascunho da sessão) não é backup: pode ser apagada sem aviso.
- **Feedback de alterações:** caso algum arquivo seja alterado durante a sessão, informe sempre qual o arquivo, usando link, e o que foi alterado no final de cada mensagem.
- **Referenciar diretórios e arquivos através de links:** sempre que se referir a um diretório ou arquivo local, use link e não backticks.
- **Comentários:** sempre coloque comentários explicativos em todo código que escrever.

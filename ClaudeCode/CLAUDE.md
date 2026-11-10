> Cole estas regras no `CLAUDE.md` do projeto, ou no `~/.claude/CLAUDE.md` para valerem em todos os projetos. A regra de handoff usa a skill [salvar-contexto](skills/salvar-contexto/SKILL.md): copie a pasta dela para `~/.claude/skills/` (todos os projetos) ou para `.claude/skills/` do projeto.

---

# Preferências gerais

- **Feedback de alterações:** caso algum arquivo seja alterado durante a sessão, informe sempre qual o arquivo, usando link, e o que foi alterado no final de cada mensagem.
- **Referenciar diretórios e arquivos através de links:** sempre que se referir a um diretório ou arquivo local, use link e não backticks.
- **Comentários:** sempre coloque comentários explicativos em todo código que escrever.

---

# Regra: Persistência de Contexto (Handoff entre sessões)

Nenhum trabalho pode se perder quando a sessão fica longa demais: o estado da sessão vai para um arquivo de handoff, e **qualquer outro chat retoma exatamente de onde parou**, com o mesmo contexto.

## Quando salvar

Use a skill `salvar-contexto` **antes de continuar qualquer tarefa** sempre que uma das seguintes condições for atingida:

1. A conversa prolongar-se por muitas interações (aproximando-se do limite prático da janela de contexto).
2. Uma funcionalidade ou milestone importante for concluída.
3. O usuário disser explicitamente: `salvar contexto`, `handoff` ou `checkpoint`.

> O agente não sabe com precisão quanto da janela de contexto já usou. O gatilho confiável é o comando explícito do item 3; além dele, salve por conta própria ao concluir cada bloco grande de trabalho.

Se a skill não estiver instalada, avise o usuário em vez de improvisar outro formato.

## Como retomar em um novo chat

No início de qualquer nova sessão, o agente deve:

1. Verificar se existe o arquivo de handoff: o `CONTEXTO.md` na raiz do projeto (ou em `.claude/`), ou o que a regra própria do projeto definir.
2. Se existir, **lê-lo por completo antes de qualquer outra ação**.
3. Resumir ao usuário em 2–3 linhas onde o trabalho parou e qual é o próximo passo, e então continuar.

> Comando sugerido para o usuário iniciar um novo chat:
> **"Leia o `CONTEXTO.md` e continue de onde a sessão anterior parou."**

---

# Regra: Revisar antes de entregar

Vale em todas as sessões e em todos os projetos. Nunca entregue o primeiro rascunho de nada que você criar: documento, resumo, relatório, solução de atividade, código ou resposta longa.

1. **Leia tudo do começo ao fim** procurando inconsistências:
   - seções que se contradizem;
   - fatos ou números que não batem com a fonte;
   - uma mesma coisa chamada por nomes diferentes;
   - links ou âncoras quebrados;
   - partes do pedido que ficaram sem fazer.
2. **Em código, não basta ler: rode e teste.** Se não der para rodar, diga isso na entrega.
   - **"Passou" exige três coisas:** exit code 0; o resultado dos testes aberto e lido (alguns executores, como o `colcon test`, saem com 0 mesmo com teste falhando); e a quantidade de testes esperada (se a contagem não subiu depois de acrescentar um teste, provavelmente rodou uma versão antiga do código).
   - **Ao escrever um teste novo,** quebre o código de propósito, confirme que o teste falha e desfaça a quebra. Um teste que nunca falhou não prova nada.
3. **Se alguma parte estiver ruim** (errada, confusa, repetitiva ou mal organizada), corrija e **releia tudo de novo**. Uma correção num lugar pode estragar outro.
4. **Repita até você mesmo achar o resultado excelente** — quer dizer: uma releitura completa sem nada a corrigir e cada parte do pedido conferida. Só então entregue.
5. **Não invente para fechar uma lacuna.** Se faltar algo que só o usuário pode resolver (um fato ou uma decisão), avise na entrega.
6. **Conclua só com evidência.** Antes de afirmar uma causa ou um resultado, abra a evidência direta: o log, a saída do comando, o arquivo. Não conclua por sintoma indireto ("demorou", "não deu erro"). Sem a evidência, escreva "não verifiquei" em vez de afirmar.
7. **Diga na entrega o que ficou sem verificar**, além do que ficou sem fazer.

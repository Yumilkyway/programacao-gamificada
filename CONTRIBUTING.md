# Guia de contribuição: branches, commits e pull requests

Este guia define como a equipe de duas pessoas trabalha no repositório durante o desenvolvimento (23/10 a 27/11/2026) e a fase de testes (28/11 a 11/12/2026). O objetivo é simples: a `main` sempre funciona, e todo código é revisado pela outra integrante antes de entrar.

## 1. Princípios

- A `main` está sempre funcionando e ninguém envia código direto para ela.
- Todo código entra por pull request (PR) e é revisado pela outra integrante.
- Toda tarefa e todo PR indicam o requisito atendido (RF ou RNF).

## 2. Branches

Existem duas branches: `main` e `develop`

## 3. Commits

Usamos o padrão Conventional Commits, em português, no imperativo:

Escopo: descrição curta (ID da tarefa, requisito)
```

Escopos sugeridos: `front`, `back`, `db`, `sandbox`, `docs`.

Exemplos:

```
back: implementa cadastro e login com hash de senha (T1.4, RF01)
sandbox: aplica timeout e limite de memória na execução (T1.6, RNF02, RNF03)
front: corrige o erro ao enviar solução vazia (T2.3, RF03)
docs: descreve o fluxo de branches e PRs (T1.1, RNF13)

Boas práticas: commits pequenos e frequentes, uma ideia por commit, e nunca enviar arquivos de configuração local ou segredos.

## 4. Pull requests

- Formato `[T1.4] Cadastro e login`.
- Preencher o modelo de PR (`.github/pull_request_template.md`) e vincular a issue da tarefa com `Closes #número`.
- Manter o PR pequeno: de preferência até uns 300 linhas alteradas. Se estiver maior, dividir.
- Abrir como rascunho (draft) enquanto o trabalho não estiver pronto para revisão.
- Mover o cartão do quadro para "Em revisão" ao pedir a revisão.

## 5. Revisão de código

- Quem revisa é sempre a outra integrante. Ninguém aprova o próprio PR.
- Combinado de prazo: responder a revisão em até 24 horas. Se passar disso, avisar no canal da equipe.
- O que conferir na revisão:
  - o código faz o que a tarefa e o requisito pedem;
  - a aplicação roda e o fluxo foi testado manualmente;
  - não há senhas, chaves ou dados reais de pessoas no código (LGPD, RNF10);
  - o código está legível e os nomes são claros.
- Todos os comentários devem ser resolvidos antes do merge.

## 6. Definição de pronto

Uma tarefa está pronta quando (conforme o planejamento, seção 2):

1. funciona no navegador;
2. foi revisada pela outra integrante via pull request;
3. foi testada manualmente;
4. está integrada à `main`.

## 7. Marcos, tags e fase de testes

Ao fim de cada marco, marcar a versão na `main` com uma tag:

| Marco | Data | Tag |
|---|---|---|
| M1: fundação pronta | 08/11 | `v0.1.0` |
| M2: primeiro fluxo | 15/11 | `v0.2.0` |
| M3: núcleo gamificado | 23/11 | `v0.3.0` |
| M4: versão estável | 27/11 | `v0.4.0` |
| M5: versão final | 11/12 | `v1.0.0` |

```bash
git switch main
git pull
git tag -a v0.1.0 -m "M1: fundação pronta"
git push origin v0.1.0
```

Se uma correção na fase de testes quebrar algo que funcionava, desfazer o PR com `git revert` (ou voltar para a última tag estável) e refazer a correção.

## 8. Segurança

- Nunca enviar `.env`, senhas, tokens ou chaves. Usar o `.env.example` para documentar as variáveis.
- Usar apenas dados fictícios em testes e exemplos.
- Se um segredo for enviado por engano, trocar a credencial imediatamente e avisar a equipe. Apagar o arquivo em um novo commit não basta.

![Fluxo do Git: comandos entre as quatro áreas](docs/fluxo-git.svg)

# Comandos Git

Este repositório reúne **comandos úteis do Git** com exemplos práticos e explicações rápidas.
O objetivo é servir como guia de referência para iniciantes e também para quem já usa Git no dia a dia.

---

## Conteúdo

- [Como o Git organiza o trabalho](#como-o-git-organiza-o-trabalho)
- [Instalação](#instalação)
- [Configuração inicial](#configuração-inicial)
- [Comandos básicos](#comandos-básicos)
- [Branches](#branches)
- [Remotes](#remotes)
- [Formas de baixar um repositório](#formas-de-baixar-um-repositório)
- [Colaboração e conflitos](#colaboração-e-conflitos)
- [Desfazendo coisas](#desfazendo-coisas)
- [Dica: salvamento automático no VS Code](#dica-salvamento-automático-no-vs-code)
- [Recursos adicionais](#recursos-adicionais)

---

## Como o Git organiza o trabalho

Todo arquivo passa por quatro áreas, e cada comando move as alterações de uma área para outra:

| Área | O que é | Comando que leva para a próxima |
|---|---|---|
| **Diretório de trabalho** | Os arquivos como estão na sua pasta | `git add` |
| **Stage** (área de preparação) | O que vai entrar no próximo commit | `git commit` |
| **Repositório local** | O histórico de commits no seu computador | `git push` |
| **Repositório remoto** | O histórico no GitHub | `git pull` traz de volta |

---

## Instalação

- **Windows**: [download oficial](https://git-scm.com/download/win)
- **Linux (Ubuntu/Debian)**:

  ```bash
  sudo apt-get install git
  ```

- **macOS**:

  ```bash
  xcode-select --install
  ```

Confira a instalação com `git --version`.

---

## Configuração inicial

Feita uma única vez por computador. O nome e o e-mail aparecem em cada commit.

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seuemail@exemplo.com"
git config --global init.defaultBranch main   # novos repositórios já nascem na main
```

---

## Comandos básicos

```bash
git init                      # Inicializa um novo repositório na pasta atual
git status                    # Mostra o estado atual dos arquivos
git add arquivo.txt           # Adiciona um arquivo ao stage
git add .                     # Adiciona todas as alterações da pasta ao stage
git commit -m "mensagem"      # Cria um commit com o que está no stage
git log --oneline             # Lista o histórico de commits, um por linha
git diff                      # Mostra o que mudou e ainda não foi para o stage
```

---

## Branches

```bash
git branch                    # Lista as branches
git branch nome-branch        # Cria uma nova branch
git switch nome-branch        # Troca para a branch (forma atual do checkout)
git switch -c nome-branch     # Cria e já troca para a branch
git merge nome-branch         # Traz as alterações da branch para a branch atual
git branch -d nome-branch     # Apaga a branch depois do merge
```

`git checkout nome-branch` também troca de branch e continua funcionando.

---

## Remotes

```bash
git remote add origin https://github.com/usuario/repositorio.git   # Liga a pasta ao GitHub
git remote -v                 # Mostra para onde o repositório aponta
git push -u origin main       # Primeiro envio: publica e lembra o destino
git push                      # Envios seguintes
git pull origin main          # Recebe do GitHub e junta com o seu código
git fetch                     # Só baixa as novidades, sem juntar
```

Se o repositório do GitHub foi criado com README e a pasta local já tinha commits, o primeiro `pull` recusa juntar históricos que nasceram separados. Nesse caso, use uma única vez:

```bash
git pull origin main --allow-unrelated-histories
```

---

## Formas de baixar um repositório

```bash
git clone https://github.com/usuario/repositorio.git   # Clona o repositório inteiro
gh repo clone usuario/repositorio                      # Via GitHub CLI
```

---

## Colaboração e conflitos

Fluxo recomendado para mexer em algo sem quebrar a `main`:

```bash
git switch main && git pull                 # Parte da versão mais recente
git switch -c minha-alteracao               # Trabalha numa branch própria
git add . && git commit -m "Descreve a mudança"
git push -u origin minha-alteracao          # Publica a branch e abre um Pull Request no GitHub
```

Quando o Git não consegue juntar duas alterações na mesma linha, ele marca o arquivo assim:

```text
<<<<<<< HEAD
a sua versão
=======
a versão que veio do GitHub
>>>>>>> 1a2b3c4
```

Para resolver, edite o arquivo deixando só o texto final, **apague as três linhas de marcação** e conclua:

```bash
git add arquivo-com-conflito
git commit -m "Resolve conflito"
```

Antes de commitar, procure por `<<<<<<<` no arquivo para garantir que nenhuma marcação ficou para trás. Foi uma marcação esquecida assim que duplicou o README deste repositório no passado.

---

## Desfazendo coisas

```bash
git restore arquivo.txt            # Descarta alterações ainda não adicionadas ao stage
git restore --staged arquivo.txt   # Tira do stage, mantendo a alteração no arquivo
git commit --amend -m "nova msg"   # Corrige a mensagem do último commit (antes do push)
git revert <hash>                  # Cria um commit que desfaz outro, sem reescrever o histórico
```

---

## Dica: salvamento automático no VS Code

O Git só enxerga o que foi salvo no disco. Ative o salvamento automático em **File > Auto Save** (Arquivo > Salvar Automaticamente) ou salve com **Ctrl+S** antes do `git add`.

---

## Recursos adicionais

- [Documentação oficial do Git](https://git-scm.com/docs)
- [GitHub Docs em português](https://docs.github.com/pt)
- [Pro Git, livro gratuito em português](https://git-scm.com/book/pt-br/v2)

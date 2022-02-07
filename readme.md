# Git and GitHub

## Git

Sistema com a finalidade de gerenciar diferentes versões de um documento.

### Ciclo de vida dos status de seus arquivos

`Untracked` quando o arquivo acabou de ser adicionado no repositório, mas não foi adicionado ao Git.

`Unmodified` quando o arquivo não sofreu nenhuma modificação.

`modified` quando o arquivo sofre uma modificação.

`staged` quando o arquivo já está pronto para o commit. Após o commit volta para **Unmodified**.

### Configuração inicial do Git

```bash
git config --global user.name "<nome de usuário>"
git config --global user.email "<e-mail>"
git config --global core.editor "<editor de texto>"
```

```bash
git config user.name
git config user.email
git config core.editor
git config --list
```

### Inicializando um repositório

```bash
git init
```

### Adiconando arquivos ao Git

```bash
git add <nome do arquivo>
git add *
```

Podemos adicionar arquivos de forma individual ou todos os arquivos de uma só vez.

### Salvando as modificações dos arquivos no Git

```bash
git commit -m "<mensagem do que você fez>"
```

### Adicionando e Salvando ao mesmo tempo

```bash
git commit -am "<mensagem do que você fez>"
```

Caso seja um arquivo que já existia no Git, podemos usar esse procedimento.


### Visualizando os status dos arquivos

```bash
git status
```

### Visualizando os logs do Git

```bash
git log
```

`commit` a hash do commit (única para cada commit)
`Author` quem fez o commit
`Date` a data do commit
Também mostra a mensagem do commit.

```bash
git log --decorate
```

A diferênça é que mostra de qual branch saiu e para qual branch foi.

```bash
git log --author="<nome usuário>"
```

Filtra os commits pelo usuário.

```bash
git shortlog
```

Filtra os commits em ordem alfabética de usuários, a quantidade de commits do usuário e as menagens do commit.

```bash
git shortlog -sm
```

Exibe somente o nome do usuário que fez o commit e a quantidade de commits ordenados pela quantidade de commits.

```bash
git log -graph
```

Exibe em forma gráfica o que aconteceu na branch.

```bash
git show <hash do commit>
```

Exibe todos os detalhes do commit inclusive o que foi alterado, acrescentado ou deletado.

### Visualizando o diff

```bash
git diff
```

Exibe o que foi alterado no arquivo.
Então é muito importa usá-lo antes de um commit.

```bash
git diff --name-only
```

Exibe somente o nome do arquivo que foi modificado

### Desfazendo coisas antes do comando "add"

```bash
git checkout <nome do arquivo>
```

### Desfazendo coisas após o comando "add"

```bash
git reset HEAD Readme.md
git checkout <nome do arquivo>
```

O primeiro comando remove o arquivo da área de **staged** que é quando ele já foi adicionado e está pronto para o commit.

### Desfazendo coisas após o comando "commit"

O comando `git reset` tem 3 tipos:
* `--soft <hash do commit>` mata o commit e volta o arquivo para staged, pronto para um commit
* `--mixed <hash do commit>`mata o commit e volta o arquivo para modified, pronto para um add
* `--hard <hash do commit>` mata tudo o que foi feito do commit

*IMPORTANTE!* a hash nós pegamos através do comando `git log`, após esse comando todos os nosso commits vão ser apresentados do mais recente commit em diante. SEMPRE vamos usar a "hash do commit anterior" ao que queremos desfazer a alteração. MUITA ATENÇÃO NISSO!


## GitHub

Serviço de Web compartilhado para projetos que utilizam o Git para versionamento (serviço de nuvem para armazenar seus controles Git).

### Criando e adicionado chave SSH

https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

Dentro da pasta `.ssh/` vai ter o arquivo `id_rsa.pub`, fique atento que é arquivo com a extensão **.pub**, copiar o conteúdo dele.
No GitHub ir em configurações, após isso no menu lateral ir em SSH and GPG Keys.
Clicar em New SSH Key, colar o nosso conteúdo copiada no campo Key, e dar um título para essa chave, exemplo "PC de Casa".
Clicar em add SSH.

### Ligando repositório Local a um Remoto

```bash
git remote add origin git@github.com:weversousa/git-and-github.git
```

`git remote add` adicione (ligue) a essa pasta um repositório remoto  
`origin` é o nome que o repositório Remoto vai receber (poderia ser qualquer um nome)  
`git@github.com:`<usuário GitHub>/<repositório>`.git`

```bash
git remote push -u origin main
```

`push` empurre (envie)  
`origin` para onde vai  
`main` de onde está saindo  
`-u` serve para trackear esse comando, assim das próximas vezes bstas `git push`

### Branch

É m ponteiro móvel que leva a um commit.  

**Por que usar?**

Vantagens:
* Pode modificar sem alterar o local principal (main)
* Facilmente "desligável"
* Múltiplas pessoas trabalhando em difeentes branchs (nunca na main)
* Evita conflitos

```bash
git chekcout -b <nome da branch>
```

Ele cria a branch e já entra nela

```bash
git branch
```

Exibe quais as branchs existem nesse repositório.  
A que estiver marcado com asterísco é a branch em que você está logado no momento.  

```bash
git chekcout <nome da branch>
```

Para alterar de branch, preceba que não tem o `-b` que é para criar.

```bash
git branch -D <nome da branch>
```

Para deletar uma branch que não vai mais ser usada

```
git push origin :<nome da branch>
```

Deletando branch do repositório remoro

### Merge

É forma que temos para unir as branchs, enviar as alterações para Branch Main

#### Entendendo

O merge sempre cria um novo commit que é a junção das alterações

Pró                     | Contra
---                     | ---
Operação não destrutiva | Commit extra
...                    | Histórico poluído



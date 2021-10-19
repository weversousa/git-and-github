# **Usando o GIT**

Para começar a usar o **GIT**, primeiramente vamos criar um diretório (pasta) para que possamos inicializá-lo.
```bash
mkdir curso-git
```

Agora vamos entrar na pasta.
```bash
cd curso-git
```

Por fim podemos, inicializar um repositório **GIT**.
```bash
git init
```
<br>

Após o comando acima, será criado um repositório **.git** dentro da pasta em que você deu o comando `git init`.  
Para visualizar esse repositório e tudo o que tem na sua pasta atual execute o comando
```bash
ls -la
```
<br>

## **git config**

O comando __git config__ serve para definir valores de configuração do **GIT** em projetos de nível global e local.

### **Níveis e locais dos arquivos git config**

- --local: **.git/config**

Referente ao contexto do projeto em que o git foi invocado.
<br><br>

- --global: **~ /.gitconfig em sistemas Unix** ou **C:\Users\\.gitconfig no Windows**

A configuração de nível global é específica do usuário, ou seja, ela é aplicada a usuários do sistema operacional.
<br><br>

- --system: **$(prefix)/etc/gitconfig em sistemas Unix** ou **C:\ProgramData\Git\config no Windows**

A configuração de nível do sistema é aplicada em toda a máquina. Ela abrange todos os usuários do sistema operacional e todos os repositórios.
<br><br>

Ao usar o **GIT** pela primeira vez, devemos aplicar algumas configurações necessárias, __e-mail__ e __usuário__, pois cada commit realizado necessita dessas informações.

```bash
git config --global user.name "Maria Marta"
```

```bash
git config --global user.email "maria.marta@gmail.com"
```

Definir um editor de texto para edição *opcional*.
```bash
git config --global core.editor code
```

Visualizar uma configuração específica.
```bash
git config --global user.name
```

Visualizar todas as configurações de uma só vez.
```bash
git config --list
```
<br>

## **Ciclos de Vida do GIT**

### **UNTRACKED**
Arquivo adicionado ao repositório, mas nunca foi adicionado ao **GIT**  
Arquivo removido do **GIT**.

### **UNMODIFIED**
O arquivo já está no GIT, mas não sofreu nenhuma alteração.

### **MODIFIED**
O arquivo já está, foi alterado no repositório e após essa alteração não foi realizado um **commit**, então no **GIT** está diferente do repositório (está desatualiado no **GIT**).

### **STAGED**
Quando modificado um arquivo e executamos o comando `add nome_arquivo`, o arquivo fica pronto para o `git commit -m "mensagem"`, depois disso o arquivo volta para ***UNMODIFIED**.
<br><br>


Ver o ciclo de vida atual no meu repositório.
```bash
git status
```
<br><br>

Passe meu arquivo para o **STAGED** para ficar pronto para receber o `git commit -m "mensagem"`.
```bash
git add.README.md
```
<br><br>

Pegue meus arquivos do **STAGED** e crie uma imagem dele (snapshot).
```bash
git commit -m "Adcionado o arquivo README.md"
```
<br><br>

O comando abaixo exibirá 4 linhas (para cada commit existente):
1. O hash do commit
2. Quem realizou o commit
3. A data do commit
4. A mensagem do commit
```bash
git log
```
<br><br>

As 4 informações acima + de qual branch para qual branch
```bash
git log --decorate
```
<br><br>

Para filtrar o commit de um usuário específico
```bash
git log --author="Maria"
```
<br><br>

Mostra por ordem alfabética os autores (usuários) e quantos commits realizou.
```bash
git shortlog
```
<br><br>

Só a quantidade de commits e o nome do usuário.
```bash
git shortlog -sn
```
<br><br>

Exibir gráfico dos commits
```bash
git shortlog --graph
```
<br><br>

Todas as informações de um commit específico, pegar o hash no `git log`.
```bash
git show <hash do commit>
```
<br><br>

Importante!
Esse comando te mostra as alterações feitas antes de você realizar um `git commit -m "mensagem"`.
```bash
git diff
```
<br><br>

Exibe o nome do último arquivo modificado.
```bash
git diff name-only
```
<br><br>

Se for um arquivo que já existia no **GIT**, podemos usar a flag **-am** assim não precisa do `git add .` antes. 
```bash
git commit -am "Alterado README.md"
```
<br><br>

Desfaz a última alteração em um arquivo.
Obs: Só funciona antes do comando `git add .`.
```bash
git checkout README.md
```
<br><br>

Caso queira desfazer a última modficação, mas já passou o arquivo para o **STAGED** com o comando `git add .`

Romeve arquivo do **STAGED**
```bash
git reset HEAD README.md
```
E agora podemos desfazer a alteração
```bash
git checkout README.md
```

## **GIT RESET**

O *hash* que vamos usar é SEMPRE o hash do commit abaixo do que queremos *resetar*.  
Isso precisa ficar claro.
Você vai estar dizendo apartir de qual commit PARA CIMA você quer *resetar*  
<br><br>

Vai matar o meu commit, voltando o meu arquivo para o **STAGED** isso quer dizer que ele ainda vai estar alterado no repositório e pronto para um novo `git commit`
```bash
git reset --soft <hash do commit>
```
<br><br>

Vai matar o meu commit, voltando o meu arquivo para o **MODIFIED** isso quer dizer que ele ainda vai estar alterado no repositório e pronto para um `git commit add` e depois `git commit`
```bash
git reset --mixed <hash do commit>
```
<br><br>

Vai matar o meu commit e tudo o que foi feito nele
```bash
git reset --hard <hash do commit>
```
<br><br>

## **BRANCH**

É um ponteiro móvel que leva a um **commit**  

Quando incializamos um repositório o primeiro **Branch** que vamos ter é chamado de **master** (mais novos **main**)
Sempre que realizamos um `git commit` é criado uma **hash** e um **snapshot** (imagem) de tudo que foi feito naquele momento
O que o **Branch** faz é apontar para um **commit**  

### **Vantagens ao usar Branchs**
Podemos modificar sem alterar o principal **master** (main)
Facilmente desligável
Múltiplas pessoas trabalhando
Evita conflitos
<br><br>

Criando uma nova Branch  
Vai ser criado a Branch e o git já vai entrar na nova Branch
```bash
git checkout -b <nome_branch>
```
<br><br>

Mostra as Branchs que existem e a que estiver marcada com um asterísco é que que você está
```bash
git branch
```
<br><br>

Mudar de Branch
```bash
git checkou <nome_branch>
```
<br><br>

Deletar Branch
```bash
git branch -D <nome_branch>
```
<br><br>

## **Merge**
Vamos supor que temos na Branch main 3 commits

**branch main**
C0 -> C1 -> C2

Agora nós vamos criar uma nova Branch que se chamara Outra
Sendo assim ela vai apontar para o último commit da Branch main a partir do momento da criação

**branch outra**
C2

Se fizernos um commit na branch outra vai ficar assim

**branch main**
C0 -> C1 -> C2

**branch outra**
C2 -> C3

Se fizernos um commit na branch main vai ficar assim

**branch main**
C0 -> C1 -> C2 -> C4

**branch outra**
C2 -> C3

Se fizernos um commit na branch outra vai ficar assim

**branch main**
C0 -> C1 -> C2 -> C4

**branch outra**
C2 -> C3 -> C5

Pois bem, vamos supor que já terminei de alterar meu código na Branch Outra e quero juntar esse código na Branch principal **main**
usando o merge... Então ficaria assim

**branch main**
C0 -> C1 -> C2 -> C4 -> C6

**branch outra**
C2 -> C3 -> C5

O merge realiza um novo commit nessa caso o C6, e ele será o resultado de C4, C3 e C5  
C4 pois é o último da main, e C3 e C5 pois ainda não existem na main

## Prós do Merge
Ele não destrói nenhum commit, ele cria um novo commit para juntar tudo

## Contra do Merge
Cria um commit extra, que não está fazendo nada a não ser juntar as coisas
Histórico poluído, como ele não cria um gráfico linear, se tiver muitas branchs dificulta a leitura


## REBASE
Vamos supor que temos na Branch main 3 commits

**branch main**
C0 -> C1 -> C2

Agora nós vamos criar uma nova Branch que se chamara Outra
Sendo assim ela vai apontar para o último commit da Branch main a partir do momento da criação

**branch outra**
C2

Se fizernos um commit na branch outra vai ficar assim

**branch main**
C0 -> C1 -> C2

**branch outra**
C2 -> C3

Se fizernos um commit na branch main vai ficar assim

**branch main**
C0 -> C1 -> C2 -> C4

**branch outra**
C2 -> C3

Se fizernos um commit na branch outra vai ficar assim

**branch main**
C0 -> C1 -> C2 -> C4

**branch outra**
C2 -> C3 -> C5

Pois bem, vamos supor que já terminei de alterar meu código na Branch Outra e quero juntar esse código na **Branch principal main**
usando o rebase... Então ficaria assim

**branch main**
C0 -> C1 -> C2 -> C4 -> C3 -> C5

**branch outra**
C0 -> C1 -> C2 -> C4 -> C3 -> C5

O rebase pega todos os commits realizados na Outra Branch e move para o início da **Branch main** deixando tudo linear, e ambas as
Branchs vão apontar para a C5, esse processo de inserir no incídio da fila é chamado de __FAST-FORWARD__

## Prós do Merge
Ele não cria um commit novo
Histórico linear

## Contra do Merge
Perde ordem cronológica, como os commits são jogados no início da fla, você não sabe quem veio primeiro.
Obs: Muita atenção ao usá-lo, pois pode gerar conflitos, "aconselhável" executar __git pull__ antes


Caso a gente faça alguma modificação, mas não queira que apareça no git até a gente mandar novamente
Podemos ir para outra branch trabalhar nela e nossa modificação não estará visivel ou pendente
```bash
git stash
```

Volta a exibir a nossa modificação e fica pronto para para seguir com os próximos passos
Esse comando serve para esconder nossa última interação com o **git** antes do **comit**
```bash
git stash apply
```

Exibe as modificações que estão aguardando
```bash
git stash list
```

Limpa para não ter mais nenhuma modificação aguardando
```bash
git stash clear
```


Criando apelido para os comandos, assim os comandos mais extensos ficam mais fáceis
Vamos configurar para que ao invés de sempre digitar __git status__ possamos digitar __git s__
```bash
git config --global alias.s status
```

Volta o arquivo para o último **commit** mas não exclui o commit realizado antes do revert
As vezes estamos realizando modificações em produção, acontece de já temos escrito várias linhas
e não queremos perder tudo porém ocmo está em produção nosso app não pode ficar parado e por isso 
voltamos rapidamente ao commit anterior e depois com calma podemos analisar o que erramos no commit
que parou tudo, deiferente do __git reset__ que exclui tudo
```bash
git revert <hash>
```

Deletar Branch remota (github) através do git local (nossa máquina)
```bash
git push origin :<nome_branch>
```


## GITCLONE
Eu copio um repositório (remoto) github para o meu repositório local (git - minha máquna)
```bash
cd <caminho da pasta onde vou colocar o repostitório clonado>
```

```bash
git clone <endereço do repositógio no GITHUB>
```

## GITHUB fork
Eu copio o projeto de alguém para o meu github, posso alterar e ai executo o pull request
Claro que o dono do repositório original pode aceitar ou não.




## Dicar para o editor de texto VIM

Editar ou criar um arquivo caso ele não exista
```bash
vim README.md
```
Para poder começar a inserir texto no arquivo pressione a tecla __i__  
Para salvar as alterações pressione a tecla ESC + : + __w__  
Para sair do VIM aperte a tecla ESC + : + __q__

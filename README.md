# Como usar o GIT e o GITHUB

### Instalação do GIT no Linux Ubuntu
    sudo apt-get install git

### Confirmar se o GIT foi instalado
    git --version

### Configurar um nome de usuário para user no GIT
    git config --global user.name "Seu Nome"

### Configurar um e-mail para usar no GIT
    git config --global user.name "email@hotmail.com"

- `config` para configuração.  
- `--global` em qualquer lugar da sua máquina que usado o comando git será usado a credencial configurada.
- `user.name` e `user.email` todos os comandos `git` executados no Terminal são registrados com um nome e e-mail de usuário, por isso é obrigatório realizar essas configurações.

### Criar um diretório local para servir de repositório
    mkdir <nome do diretório>

### Entrar no diretório que acabamos de criar
    cd <nome do diretório>

### Inicializar um repositório GIT em nosso diretório
    git init

- Vai ser criado o arquivo oculto **.git** em nosso diretório (repositório).

### Criar um arquivo para versionar (salvar) no GIT
    nano <nome do arquivo>

- `nano` é um editor de texto Linux, se o arquivo não existir ele vai criá-lo.

### Saindo do editor de texto NANO
1. CTRL + O
2. ENTER
3. CTRL + X

### Ver os estados dos arquivos no repositório
    git status

### Estado dos arquivos no diretório (repositório)

**Untracked files:**
- Arquivos novos que não estão e nunca foram versionados pelo **GIT**.

**Changes not staged for commit:**
- Arquivos já versionados e alterado **GIT**.

**Changes to be commited:**
- Arquivos alterados após o comando `add` prontos para o `commit`.


### Adicionar um arquivo ao estágio Change para poder realizar um commit
    git add <nome do arquivo>

### Adicionar todos os arquivos ao estágio Change para poder realizar um commit
    git add .
    git add *

### Realizr um COMMIT
    git commit -m "Título do commit"

### Listar de todos os commits já realizado no repositório
    git log

### Ver as alterações realizada em um arquivo
    git diff <nome do arquivo>

- Linhas com o sinal `-` siginifica que foram alteradas (não existem mais).
- Linhas com o sinal `+` siginifica que foram adicionadas (no lugar da alterada).

## Configuração do GITHUB

Para enviar\receber arquivos do repositório local (git - sua máquina) para o repositório remoto (github - web) são  necessário algumas configurações.

### Criar arquivos com a nossa chave SSH
    ssh-keygen

1. Inserir um nome para a sua chave SSH (opcional)
2. Inserir senha (opcional), se inserida vai ser solicitada em todo commit
3. Repetir senha (se não colocar senha pode dar ENTER na linha 2 e agora na linha 3).

### Vão ser criados dois arquivos:

1. **nome da chave** se na hora da configurção acima você não passou um nome será **id_rsa**.
    - Essa chave NÃO pode inserir no GITHUB ela é PRIVADA do repositório GIT (local - da sua máquina).
2. **nome da chave.pub** se na hora da configurção acima você não passou um nome será **id_rsa.pub**.
    - Essa é a chave para ser inserida no GITHUB ela é a PÚBLICA.

### Configurar variável de ambiente com a chave SSH
    eval `ssh-agent`
    ssh-add <nome da chave PRIVADA>

- A chave PRIVADA não possui a extensão **.pub**

### Entrar no aquivo para copiar a chave SSH para inserir no GITHUB
    cat <nome da chave>.pub

1. Settings
2. SSH and GPG Keys
3. New SSH Key
4. Title
    - Colocar um titulo para identificar sua chave
5. Key
    - Colar sua chave


## Criar um novo repositório no GITHUB

1. New repository
2. Repository name
3. Public
4. Create repository

## Ligar GIT (local) com GITHUB (remoto)
    git remote add origin git@github.com:<nome usuário web github>/<nome repositório web>.git

`remote` é o repositório do link, remote (web)
`origin` é o nosso repositório local (que está em nosso PC).

### Enviar arquivos comitados do GIT para GITHUB
    git push origin main

### Enviar arquivos comitados do GITHUB para GIT
    git pull origin main

### Clonar repositório do GITHUB para o GIT (local)
    git clone git@github.com:<nome usuário web github>/<nome repositório web>.git
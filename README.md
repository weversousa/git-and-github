## Configuração

Como configurar uma propriedade do git:
```powershell
git config --global user.name "Weverton Teixeira de Sousa"
git config --global user.email "weverton.tsousa@hotmail.com"
git config --global core.editor code
```
Verificar como está definido uma configuração de forma individual:
```powershell
git config user.name
```

Verificar como está definido todas as configurações através de uma lista:
```powershell
git config --list
```


## Inicializar um Repositório

Para tornar a pasta atual em um repositório:
```powershell
git init
```

Vai ser criado um arquivo "oculto" `.git` na pasta, para conferir no Poweshell use o seguinte comando:
```powershell
ls -Force
```
**saída**
```powershell
    Diretório: C:\dev\curso-git-e-github


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d--h--        19/11/2021     11:42                .git
```

## Ciclo de Vida - Status do Arquivo

* __untracked__: arquivo novo na pasta, que nunca foi adicionado ao git
* __unmodified__: arquivo sem modificação
* __modified__: arquivo com modificação
* __staged__: arquivo pronto para commit

## Comandos Principais

Para verificar o "Ciclo de Vida" dos arquivos no repositório:
```powershell
git status
```
**saída**
```powershell
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```
* On branch main: você está na branch main
* No commits yet: não foi realizado nehum commit ainda
* nothing to commit: não tem nada para commitar (uma explicação do que fazer)

Criar um arquivo `Readme.md` e escrever dentro dele "Curso de GIT" e depois salve.  

Vamos verificar o Ciclo de Vida:
```powershell
git status
```
**saída**
```powershell
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Readme.md
nothing added to commit but untracked files present (use "git add" to track)
```

O Ciclo de Vida mudou para Untracked, então vamos passar Staged:
```powershell
git add Readme.md
```

Vamos verificar o Ciclo de Vida:
```powershell
git status
```
**saída**
```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   Readme.md
```

O Ciclo de Vida passou para o Staged e agora está pronto para receber um `commit` (ser criado uma versão).
Mas antes de commitar, edite o arquivo `Readme.md` escreva uma nova linha dentro dele e depois salve.  

Vamos verificar o Ciclo de Vida:
```powershell
git status
```
**saída**
```powershell
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   Readme.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   Readme.md
```

O Ciclo de Vida saiu do Staged e passou para Modified, então precisamos passar novamente para o Staged:
```powershell
git add Readme.md
```

Vamos verificar o Ciclo de Vida:
```powershell
git status
```
**saída**
```powershell
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   Readme.md 
```

O Ciclo de Vida passou para o Staged e agora está pronto para receber um `commit` (ser criado uma versão):
```powershell
git commit -m "Adicionado Readme.md"
```
**saída**
```powershell
[main (root-commit) ecb3b61] Adicionado Readme.md
 1 file changed, 3 insertions(+)
 create mode 100644 Readme.md
```
* main: branch em que está
* ecb3b61: hash do commit, único (nunca terá igual)
* Adicionado Readme.md: mensagem passada no commit
* 1 file changed: quantidade de arquivos modificados
* 3 insertions(+):  o sinal de `+` significa que foi acrescentado valor | `-` significa que foi removido valor

Vamos verificar o Ciclo de Vida:
```powershell
git status
```
**saída**
```powershell
On branch main
nothing to commit, working tree clean
```

Edite o arquivo `Readme.md` mais uma vez, escreva uma nova linha dentro dele e depois salve.  

Vamos verificar o Ciclo de Vida:
```powershell
git status
```
**saída**
```powershell
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   Readme.md

no changes added to commit (use "git add" and/or "git commit -a")
```

Como foi realizado uma mudança no arquivo, o Ciclo de Vida dele passou para Modified, e novamente precisamos addcioná-lo ao Staged:
```powershell
git add Readme.md
```

Vamos verificar o Ciclo de Vida:
```powershell
git status
```
**saída**
```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   Readme.md
```

O Ciclo de Vida passou para o Staged e agora está pronto para receber um novo `commit` (ser criado uma nova versão):
```powershell
git commit -m "Inserido nova linha em Readme.md"
```
**saída**
```
[main e8aca31] Inserido nova linha em Readme.md
 1 file changed, 3 insertions(+), 1 deletion(-)
```

Vamos verificar o Ciclo de Vida:
```powershell
git status
```
**saída**
```powershell
On branch main
nothing to commit, working tree clean
```

Verificar todos os commits realizado no repositório:
```powershell
git log
```
**saída**
```powershell
commit e8aca311634c6679934e48cc9a4ce3541a0d0b55 (HEAD -> main)
Author: Weverton Teixeira de Sousa <weverton.tsousa@hotmail.com>
Date:   Fri Nov 19 11:40:58 2021 -0300

    Inserido nova linha em Readme.md

commit ecb3b617b50b804d439ac8c5aad4d2f9daffb942
Author: Weverton Teixeira de Sousa <weverton.tsousa@hotmail.com>
Date:   Fri Nov 19 11:33:40 2021 -0300

    Adicionado Readme.md
```

Verificar os commits de um usuário específico pelo nome (não precisa ser o nome completo):
```powershell
git log --author "Weverton"
```
**saída**
```powershell
commit e8aca311634c6679934e48cc9a4ce3541a0d0b55 (HEAD -> main)  
Author: Weverton Teixeira de Sousa <weverton.tsousa@hotmail.com>
Date:   Fri Nov 19 11:40:58 2021 -0300

    Inserido nova linha em Readme.md

commit ecb3b617b50b804d439ac8c5aad4d2f9daffb942
Author: Weverton Teixeira de Sousa <weverton.tsousa@hotmail.com>
Date:   Fri Nov 19 11:33:40 2021 -0300

    Adicionado Readme.md
```

Verificar todos os commits do repositório, classificado por ordem alfabética pelo usuário, com a quantidade de commites e a mensagem dos commits:
```powershell
git shortlog
```
**saída**
```powershell
Weverton Teixeira de Sousa (2):
      Adicionado Readme.md
      Inserido nova linha em Readme.md
```

Verificar todos os commits do repositório, classificado por ordem decrescente de commits, SOMENTE com a quantidade de commits e usuário:
```powershell
git shortlog -sn
```
**saída**
```powershell
2  Weverton Teixeira de Sousa
```

Exibir um gráfico dos commits:
```powershell
git log --graph
```
**saída**
```powershell
* commit e8aca311634c6679934e48cc9a4ce3541a0d0b55 (HEAD -> main)  
| Author: Weverton Teixeira de Sousa <weverton.tsousa@hotmail.com>
| Date:   Fri Nov 19 11:40:58 2021 -0300
|
|     Inserido nova linha em Readme.md
|
* commit ecb3b617b50b804d439ac8c5aad4d2f9daffb942
  Author: Weverton Teixeira de Sousa <weverton.tsousa@hotmail.com>
  Date:   Fri Nov 19 11:33:40 2021 -0300

      Adicionado Readme.md
```

Para saber os detalhes do que ocorreu em um commit, pegar o hash do commit no `git log` e usá-lo:
```powershell
git show ecb3b617b50b804d439ac8c5aad4d2f9daffb942
```
**saída**
```powershell
commit ecb3b617b50b804d439ac8c5aad4d2f9daffb942
Author: Weverton Teixeira de Sousa <weverton.tsousa@hotmail.com>
Date:   Fri Nov 19 11:33:40 2021 -0300

    Adicionado Readme.md

diff --git a/Readme.md b/Readme.md
new file mode 100644
index 0000000..33da273
--- /dev/null
+++ b/Readme.md
@@ -0,0 +1,3 @@
+Curso de GIT
+
+Este é um repositório teste para aprender como o GIT funciona.
\ No newline at end of file
```

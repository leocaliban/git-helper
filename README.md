# GIT: Versionamento de código

## Configurações GIT

* Usuário

        git config --global user.name "USERNAME"

* E-mail

        git config --global user.email "EMAIL"

* Editor de código. *opcional*

        git config --global core.editor "VARIAVEL_EDITOR"

* Ajuda de auto correção nos comandos

        git config --global help.autocorrect 1

### Visualizar configurações

* Nome ou E-mail

        git config user.name
        git config user.email

## Iniciando um repositório GIT

* Executar seguinte comando no repositório que será versionado:

        git init

O comando ```git status``` exibe as modificações realizadas.

*Arquivos exibidos que não estão monitorados pelo git ficam em vermelho.*

### Rastrear arquivos

* Rastrear arquivo específico: ```git add NOME_DO_ARQUIVO```

* Rastrear todos: ```git add .``` ou ```git add -A```

### Enviar arquivos rastreados (Commit)

*Ao executar ```git status```, arquivos rastreados não enviados aparecerão em verde*

* Realizar commit

```git commit -m "MENSAGEM_DO_QUE_FOI_REALIZADO_NO_COMMIT"```

*utilizar o ```git commit -am "MSG"``` para arquivos que já existem (esse passo substitui o ```git add .```)*

### Visualizar commits

* Executar ```git log``` para visualizar todos os commits.

* Executar ```git log --author="NOME_AUTOR"``` para visualizar os commits de um autor específico.

* Executar ```git log --pretty=oneline``` para visualizar os commits em uma linha.

* Executar ```git shortlog``` para visualizar todos os commits e seus autores resumido.

* Executar ```git shortlog -sn``` para visualizar todos os autores e a sua quantidade de commits.

* Executar ```git log --pretty=oneline --graph``` para visualizar os commits em uma linha com o gráfico.

* Executar ```git log --pretty=oneline --graph``` para visualizar todos commits dos branches em uma linha com o gráfico.

* Executar ```git log --graph``` para visualizar o gráfico dos commits.

#### Mais Filtros nos Commits

* Executar ```git log --since='Jan 1 2018'``` para visualizar os commits desde uma data específica.

* Executar ```git log --until='Jan 1 2018'``` para visualizar os commits até uma data específica.

* Executar ```git log --since='Jan 1 2018' --until='Jan 10 2018'``` para visualizar os commits dentro de um período. *Excluindo o dia que está definido*

### Resetar um commit

* Para reverter o commit e recuperar as alterações para o estado de rastreado:

        git reset --soft CÓDIGO_DO_COMMIT

* Para reverter o commit e recuperar as alterações para o estado de não rastreado:

        git reset --mixed CÓDIGO_DO_COMMIT

* Para reverter o commit eliminando todas as alterações do commit:

        git reset --hard CÓDIGO_DO_COMMIT

*Recomendado usar em branches*


### Reverter um commit

* Para reverter um commit para o estado anterior sem perdê-lo:

        git revert --no-edit CÓDIGO_DO_COMMIT

*Recomendado usar no master*


### Criando branches

* Execute ```git branch NOME_DO_BRANCH``` ou ```git -b NOME_DO_BRANCH``` para criar uma nova branch.

* Mudar de branch ```git checkout NOME_DO_BRANCH```

### Deletando branches remotos e locais

* Execute ```git push origin :NOME_DO_BRANCH``` para deletar branch remoto.

* Não estando no branch que será excluído, execute ```git branch -D NOME_DO_BRANCH``` para deletar branch local.

### Visualizar branches

* Executar ```git branch``` para visualizar todos os branches.

### Visualizar alterações realizadas

* Para visualizar as alterações realizadas nos arquivos:
        
        git diff

* Para visualizar arquivos que foram alterados:

        git diff --name-only

* Para visualizar as alterações realizadas em um arquivo específico:

        git diff NOME_DO_ARQUIVO.extensão

#### Reverter alterações em um arquivo.

* Execute ```git checkout HEAD -- NOME_DO_ARQUIVO.ext``` para reverter todas as alterações desse arquivo. *HEAD indica o branch atual*

## Repositório remoto

[Gerar chave SSH](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

#### Conectar ao remoto

* Criar repositório via linha de comando:

        echo "# NOME_REPOSITORIO" >> README.md
        git init
        git add README.md
        git commit -m "MENSAGEM_COMMIT"
        git remote add origin 
        git@github.com:NOME_USUARIO/NOME_REPOSITORIO.git
        git push -u origin master


* Enviar um repositório existente via linha de comando:

        git remote add origin 
        git@github.com:NOME_USUARIO/NOME_REPOSITORIO.git
        git push -u origin master

#### Enviar commits para o remoto

Após a realização dos commits locais, execute ```git push origin NOME_BRANCH``` para enviá-los ao repositório remoto.

#### Ignorar arquivos com .gitignore

* Criar um arquivo .gitignore com os nomes dos arquivos que serão ignorados pelo git.

> ver [gitignore.io](https://www.gitignore.io/)

### Atualizar repositório local

* Execute ```git pull origin NOME_DO_BRANCH```

*Utilizar antes de dar um git push*

### Pegar commit específico em uma branch

* Pegue o código do commit na branch desejada e execute ```git cherry-pick CODIIGO_COMMIT```

### Clonando repositórios

* Execute ```git clone LINK_DO_REPOSITORIO```

## Criando alias

* Execute ```git config --global alias.NOME_ALIAS NOME_COMANDO``` para criar um alias próprio.


## Criando commit por partes

Para enviar um pequeno trecho das modificações realizadas no código, é possível fazer a seleção das linhas para assim criar um commit com essas partes.

* Com o ```git add -p``` você irá decidir o que separar para o commit através das ações disponíveis:

 - y = Sim, adicionar. *mais usado*
 - n = Não adicionar. *mais usado*
 - q = Não adicionar e sair do menu.
 - a = Adicionar essa parte e todas as seguintes.
 - d = Não adicionar essa parte e nem as seguintes.
 - j = Passar para a próxima parte.
 - J = ''
 - g = Voltar.
 - s = Dividir essa parte.
 - e = Faz a seleção manualmente

Após fazer a seleção, realize o commit.


## Utilizando Fixup

Para adicionar informações relacionadas a algum commit anterior, utilize o ```fixup``` para indicar que é um ajuste de um commit específico e depois fazer a união para um único commit.

* Ao realizar alterações relacionadas ao commit anterior, faça um commit executando ```git commit --fixup CODIGO_COMMIT_A```. Essa ação criará um novo commit "fixup! NOME_DO_COMMIT_A".

* Para unir um conjunto de fixup em um único commit, execute ```git rebase -i --autosquash CODIGO_COMMIT_ANTERIOR_AO_A```
*:wq no terminal*

## Unindo commits

Para unir commits execute ```git rebase -i HEAD~2``` (apresenta os dois últimos commits).


# Boas Práticas

## Merge ou Rebase:

> Está atualizando sua branch pegando as coisas do master?

Use **REBASE** ```git pull --rebase```

> Terminou sua feature no branch e quer jogar para o master?

Use **MERGE**

## Resolvendo conflitos:

> Ao resolver um conflito utilizar o ```--continue``` para o merge ou rebase.

* Ex: ```merge --continue```

## Empacotar o repositório

```git archive NOME_DA_BRANCH --format=zip --output=master.zip```

## Savior reflog

```git reflog``` exibe o log de todas as ações executadas.

## Awesome GitHub Issues & PRs Templates

> ver [Templates](https://github.com/devspace/awesome-github-templates)

## Palavras chave para fechar issues

> ver [Palavras-chave](https://help.github.com/articles/closing-issues-using-keywords/)


# Extensões Git para VSCode

* Git: Add Remote - *sam_schneller*

* Git History - *Don Jayamanne*

* Git Blame - *Wade Anderson*

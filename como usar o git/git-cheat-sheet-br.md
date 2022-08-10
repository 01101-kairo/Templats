Git and Git Flow Cheat Sheet [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome) [![Build Status](https://travis-ci.org/arslanbilal/git-cheat-sheet.svg?branch=master)](https://travis-ci.org/arslanbilal/git-cheat-sheet)
===============
<hr>
<p align="center">
    <img alt="Git" src="./Img/git-logo.png" height="190" width="455">
</p>
<hr>
Git cheat sheet saves you from learning all the commands by heart.

Be free to contribute, update the grammar mistakes. You are also free to add your language file.

<hr>

Git Cheat Sheet English
===============
### Index
* [Set Up](#setup)
* [Configuration Files](#configuration-files)
* [Create](#create)
* [Local Changes](#local-changes)
* [Search](#search)
* [Commit History](#commit-history)
* [Branches & Tags](#branches--tags)
* [Update & Publish](#update--publish)
* [Merge & Rebase](#merge--rebase)
* [Undo](#undo)
* [Git Flow](#git-flow)


<hr>

## Setup
## Configuração

##### Show current configuration:
##### Mostrar configuração atual:
```
$ git config --list
```
##### Show repository configuration:
##### Mostrar a configuração do repositório:
```
$ git config --local --list
```

##### Show global configuration:
##### Mostrar configuração global:
```
$ git config --global --list
```

##### Show system configuration:
##### Mostrar a configuração do sistema:
```
$ git config --system --list
```

##### Set a name that is identifiable for credit when review version history:
##### Defina um nome identificável para crédito ao revisar o histórico de versões:
```
$ git config --global user.name “[firstname lastname]”
```

##### Set an email address that will be associated with each history marker:
##### Defina um endereço de email que será associado a cada marcador do histórico:
```
$ git config --global user.email “[valid-email]”
```

##### Set automatic command line coloring for Git for easy reviewing:
##### Defina a coloração automática da linha de comando para o Git para facilitar a revisão:
```
$ git config --global color.ui auto
```

##### Set global editor for commit
##### Definir editor global para confirmação
```
$ git config --global core.editor vi
```

<hr>

## Configuration Files
## arquivos de configuração

##### Repository specific configuration file [--local]:
##### Arquivo de configuração específico do repositório [--local]:
```
<repo>/.git/config
```

##### User-specific configuration file [--global]:
##### Arquivo de configuração específico do usuário [--global]:
```
~/.gitconfig
```

##### System-wide configuration file [--system]:
##### Arquivo de configuração em todo o sistema [--system]:
```
/etc/gitconfig
```

<hr>

## Create
## Crie

##### Clone an existing repository:
##### Clone um repositório existente:

There are two ways:<br>
Existem duas maneiras:

Via SSH

```
$ git clone ssh://user@domain.com/repo.git
```

Via HTTP

```
$ git clone http://domain.com/user/repo.git
```

##### Create a new local repository in the current directory:
##### Crie um novo repositório local no diretório atual:
```
$ git init
```

##### Create a new local repository in a specific directory:
##### Crie um novo repositório local em um diretório específico:
```
$ git init <directory>
```

<hr>

## Local Changes
## Alterações locais

##### Changes in working directory:
##### Alterações no diretório de trabalho:
```
$ git status
```

##### Changes to tracked files:
##### Alterações nos arquivos rastreados:
```
$ git diff
```

##### See changes/difference of a specific file:
##### Veja as alterações / diferenças de um arquivo específico:
```
$ git diff <file>
```

##### Add all current changes to the next commit:
##### Adicione todas as alterações atuais ao próximo commit:
```
$ git add .
```

##### Add some changes in &lt;file&gt; to the next commit:
##### Adicione algumas alterações no arquivo & lt; file & gt; para o próximo commit:
```
$ git add -p <file>
```

##### Commit all local changes in tracked files:
##### Confirme todas as alterações locais nos arquivos rastreados:
```
$ git commit -a
```

##### Commit previously staged changes:
##### Confirme as alterações preparadas anteriormente:
```
$ git commit
```

##### Commit with message:
##### Confirme com a mensagem:
```
$ git commit -m 'message here'
```

##### Commit skipping the staging area and adding message:
##### Confirme pulando a área de preparação e adicionando a mensagem:
```
$ git commit -am 'message here'
```

##### Commit to some previous date:
##### Confirme uma data anterior:
```
$ git commit --date="`date --date='n day ago'`" -am "<Commit Message Here>"
```

##### Change last commit:<br>
##### Alterar última confirmação:<br>
<em><sub>Don't amend published commits!</sub></em>

```
$ git commit -a --amend
```

##### Amend with last commit but use the previous commit log message
##### Alterar com a última confirmação, mas use a mensagem de log de confirmação anterior
<em><sub>Don't amend published commits!</sub></em>
<em> <sub> Não altere confirmações publicadas! </sub> </em>

```shell
$ git commit --amend --no-edit
```

##### Change committer date of last commit:
##### Altere a data do último commit:
```
GIT_COMMITTER_DATE="date" git commit --amend
```

##### Change Author date of last commit:
##### Alterar data do autor da última confirmação:
```shell
$ git commit --amend --date="date"
```

##### Move uncommitted changes from current branch to some other branch:<br>
##### Mova as alterações não confirmadas da ramificação atual para outra ramificação: <br>
```
$ git stash
$ git checkout branch2
$ git stash pop
```

##### Restore stashed changes back to current branch:
##### Restaure as alterações ocultas de volta à ramificação atual:
```shell
$ git stash apply
```

#### Restore particular stash back to current branch:
#### Restaure o stash específico de volta à ramificação atual:
- *{stash_number}* can be obtained from `git stash list`
- *{stash_number}* pode ser obtido na `git stash list`

```shell
$ git stash apply stash@{stash_number}
```

##### Remove the last set of stashed changes:
##### Remova o último conjunto de alterações ocultas:
```
$ git stash drop
```

<hr>

## Search
## Pesquisa

##### A text search on all files in the directory:
##### Uma pesquisa de texto em todos os arquivos no diretório:
```
$ git grep "Hello"
```

##### In any version of a text search:
##### Em qualquer versão de uma pesquisa de texto:
```
$ git grep "Hello" v2.5
```

<hr>

## Commit History
## Confirmar histórico

##### Show all commits, starting with newest (it'll show the hash, author information, date of commit and title of the commit):
##### Mostrar todos os commits, começando pelo mais recente (mostrará o hash, as informações do autor, a data do commit e o título do commit):
```
$ git log
```

##### Show all the commits(it'll show just the commit hash and the commit message):
##### Mostre todos os commit (mostrará apenas o hash de commit e a mensagem de commit):
```
$ git log --oneline
```

##### Show all commits of a specific user:
##### Mostrar todas as confirmações de um usuário específico:
```
$ git log --author="username"
```

##### Show changes over time for a specific file:
##### Mostrar alterações ao longo do tempo para um arquivo específico:
```
$ git log -p <file>
```

##### Display commits that are present only in remote/branch in right side
##### Exibir confirmações que estão presentes apenas no remoto / ramificação no lado direito
```
$ git log --oneline <origin/master>..<remote/master> --left-right
```

##### Who changed, what and when in &lt;file&gt;:
##### Quem mudou, o que e quando no & lt; file & gt ;:
```
$ git blame <file>
```

##### Show Reference log:
##### Mostrar log de referência:
```
$ git reflog show
```

##### Delete Reference log:
##### Excluir log de referência:
```
$ git reflog delete
```
<hr>

## Move / Rename
## Mover / renomear

##### Rename a file:
##### Renomeie um arquivo:

Rename Index.txt to Index.html

```
$ git mv Index.txt Index.html
```

<hr>

## Branches & Tags

##### List all local branches:
##### Listar todas as ramificações locais:
```
$ git branch
```

#### List local/remote branches
#### Listar ramificações locais / remotas
```
$ git branch -a
```

##### List all remote branches:
##### Listar todas as ramificações remotas:
```
$ git branch -r
```

##### Switch HEAD branch:
##### Alternar ramo HEAD:
```
$ git checkout <branch>
```

##### Checkout single file from different branch
##### Arquivo único de check-out de filial diferente
```
$ git checkout <branch> -- <filename>
```

##### Create and switch new branch:
##### Crie e alterne um novo ramo:
```
$ git checkout -b <branch>
```


##### Create a new branch from an exiting branch and switch to new branch:
##### Crie uma nova ramificação a partir de uma ramificação existente e alterne para a nova ramificação:
```
$ git checkout -b <new_branch> <existing_branch>
```


#### Checkout and create a new branch from existing commit
#### Finalize a compra e crie uma nova ramificação a partir da confirmação existente
```
$ git checkout <commit-hash> -b <new_branch_name>
```


##### Create a new branch based on your current HEAD:
##### Crie uma nova ramificação com base no seu HEAD atual:
```
$ git branch <new-branch>
```

##### Create a new tracking branch based on a remote branch:
##### Crie um novo ramo de rastreamento com base em um ramo remoto:
```
$ git branch --track <new-branch> <remote-branch>
```

##### Delete a local branch:
##### Exclua uma filial local:
```
$ git branch -d <branch>
```

##### Rename current branch to new branch name
##### Renomeie a ramificação atual para o novo nome da ramificação
```shell
$ git branch -m <new_branch_name>
```

##### Force delete a local branch:
##### Forçar a exclusão de uma ramificação local:
<em><sub>You will lose unmerged changes!</sub></em>
<em><sub> Você perderá alterações não imersas!</sub></em>

```
$ git branch -D <branch>
```

##### Mark `HEAD` with a tag:
##### Marque `HEAD` com uma tag:
```
$ git tag <tag-name>
```

##### Mark `HEAD` with a tag and open the editor to include a message:
##### Marque `HEAD` com uma tag e abra o editor para incluir uma mensagem:
```
$ git tag -a <tag-name>
```

##### Mark `HEAD` with a tag that includes a message:
##### Marque `HEAD` com uma tag que inclui uma mensagem:
```
$ git tag <tag-name> -am 'message here'
```

##### List all tags:
##### Listar todas as tags:
```
$ git tag
```

##### List all tags with their messages (tag message or commit message if tag has no message):
##### Listar todas as tags com suas mensagens (marcar mensagem ou confirmar mensagem se a tag não tiver mensagem):
```
$ git tag -n
```

<hr>

## Update & Publish
## Atualizar e publicar

##### List all current configured remotes:
##### Listar todos os controles remotos configurados atuais:
```
$ git remote -v
```

##### Show information about a remote:
##### Mostrar informações sobre um controle remoto:
```
$ git remote show <remote>
```

##### Add new remote repository, named &lt;remote&gt;:
##### Adicione um novo repositório remoto, chamado & lt; remote & gt ;:
```
$ git remote add <remote> <url>
```

##### Rename a remote repository, from &lt;remote&gt; to &lt;new_remote&gt;:
##### Renomeie um repositório remoto, a partir de & lt; remote & gt; para & lt; new_remote & gt ;:
```
$ git remote rename <remote> <new_remote>
```

##### Remove a remote:
##### Remova um controle remoto:
```
$ git remote rm <remote>
```

<em><sub>Note: git remote rm does not delete the remote repository from the server. It simply removes the remote and its references from your local repository.</sub></em>
<em><sub> Nota: o git remote rm não exclui o repositório remoto do servidor. Ele simplesmente remove o controle remoto e suas referências do seu repositório local.</sub></em>

##### Download all changes from &lt;remote&gt;, but don't integrate into HEAD:
##### Baixe todas as alterações do & lt; remote & gt ;, mas não se integre ao HEAD:
```
$ git fetch <remote>
```

##### Download changes and directly merge/integrate into HEAD:
##### Faça o download das alterações e mescle / integre diretamente no HEAD:
```
$ git remote pull <remote> <url>
```

##### Get all changes from HEAD to local repository:
##### Obtenha todas as alterações de HEAD no repositório local:
```
$ git pull origin master
```

##### Get all changes from HEAD to local repository without a merge:
##### Obtenha todas as alterações de HEAD no repositório local sem uma mesclagem:
```
$ git pull --rebase <remote> <branch>
```

##### Publish local changes on a remote:
##### Publique alterações locais em um controle remoto:
```
$ git push remote <remote> <branch>
```

##### Delete a branch on the remote:
##### Exclua uma ramificação no controle remoto:
```
$ git push <remote> :<branch> (since Git v1.5.0)
```
OR
```
$ git push <remote> --delete <branch> (since Git v1.7.0)
```

##### Publish your tags:
##### Publique suas tags:
```
$ git push --tags
```
<hr>

#### Configure the merge tool globally to meld (editor)
#### Configure globalmente a ferramenta de mesclagem para mesclar (editor)
```bash
$ git config --global merge.tool meld
```

##### Use your configured merge tool to solve conflicts:
##### Use sua ferramenta de mesclagem configurada para resolver conflitos:
```
$ git mergetool
```

## Merge & Rebase
## Mesclar e refazer

##### Merge branch into your current HEAD:
##### Mesclar ramificação em seu HEAD atual:
```
$ git merge <branch>
```

##### Rebase your current HEAD onto &lt;branch&gt;:<br>
##### Rebase seu HEAD atual em & lt; branch & gt ;: <br>
<em><sub>Don't rebase published commit!</sub></em>
<em><sub>Não rebase o commit publicado!</sub></em>

```
$ git rebase <branch>
```

##### Abort a rebase:
##### Interrompa uma nova rebase:
```
$ git rebase --abort
```

##### Continue a rebase after resolving conflicts:
##### Continue uma nova refazer após resolver conflitos:
```
$ git rebase --continue
```

##### Use your editor to manually solve conflicts and (after resolving) mark file as resolved:
##### Use seu editor para resolver manualmente conflitos e (depois de resolver) marcar o arquivo como resolvido:
```
$ git add <resolved-file>
```

```
$ git rm <resolved-file>
```

##### Squashing commits:
##### O Squash confirma:
```
$ git rebase -i <commit-just-before-first>
```

Now replace this,
Agora substitua isso,

```
pick <commit_id>
pick <commit_id2>
pick <commit_id3>
```

to this,
para isso,

```
pick <commit_id>
squash <commit_id2>
squash <commit_id3>
```
<hr>

## Undo
## Desfazer

##### Discard all local changes in your working directory:
##### Descarte todas as alterações locais no seu diretório de trabalho:
```
$ git reset --hard HEAD
```

##### Get all the files out of the staging area(i.e. undo the last `git add`):
##### Retire todos os arquivos da área de teste (ou seja, desfaça o último `git add`):
```
$ git reset HEAD
```

##### Discard local changes in a specific file:
##### Descartar alterações locais em um arquivo específico:
```
$ git checkout HEAD <file>
```

##### Revert a commit (by producing a new commit with contrary changes):
##### Reverta uma confirmação (produzindo uma nova confirmação com alterações contrárias):
```
$ git revert <commit>
```

##### Reset your HEAD pointer to a previous commit and discard all changes since then:
##### Redefina seu ponteiro HEAD para um commit anterior e descarte todas as alterações desde então:
```
$ git reset --hard <commit>
```

##### Reset your HEAD pointer to a remote branch current state.
##### Redefina o ponteiro HEAD para um estado atual da ramificação remota.
```
$ git reset --hard <remote/branch> e.g., upstream/master, origin/my-feature
```

##### Reset your HEAD pointer to a previous commit and preserve all changes as unstaged changes:
##### Redefina seu ponteiro HEAD para uma confirmação anterior e preserve todas as alterações como alterações não-estágios:
```
$ git reset <commit>
```

##### Reset your HEAD pointer to a previous commit and preserve uncommitted local changes:
##### Redefina seu ponteiro HEAD para um commit anterior e preserve as alterações locais não confirmadas:
```
$ git reset --keep <commit>
```

##### Remove files that were accidentally committed before they were added to .gitignore
##### Remova os arquivos que foram acidentalmente confirmados antes de serem adicionados ao .gitignore
```
$ git rm -r --cached .
$ git add .
$ git commit -m "remove xyz file"
```
<hr>

## Git-Flow
Improved [Git-flow](https://github.com/petervanderdoes/gitflow-avh)

### Index
* [Setup](#setup)
* [Getting Started](#getting-started)
* [Features](#features)
* [Make a Release](#make-a-release)
* [Hotfixes](#hotfixes)
* [Commands](#commands)

<hr>

### Setup
### Configuração
###### You need a working git installation as prerequisite. Git flow works on OSX, Linux and Windows.
###### Você precisa de uma instalação funcional do git como pré-requisito. O fluxo Git funciona no OSX, Linux e Windows.

##### OSX Homebrew:
```
$ brew install git-flow-avh
```

##### OSX Macports:
```
$ port install git-flow
```

##### Linux (Debian-based):
```
$ sudo apt-get install git-flow
```

##### Windows (Cygwin):
###### You need wget and util-linux to install git-flow.
###### Você precisa do wget e do util-linux para instalar o git-flow.
```bash
$ wget -q -O - --no-check-certificate https://raw.githubusercontent.com/petervanderdoes/gitflow/develop/contrib/gitflow-installer.sh install <state> | bash
```
<hr>

### Getting Started
### Começando
###### Git flow needs to be initialized in order to customize your project setup. Start using git-flow by initializing it inside an existing git repository:
###### O fluxo Git precisa ser inicializado para personalizar a configuração do seu projeto. Comece a usar o git-flow inicializando-o em um repositório git existente:
##### Initialize:
##### Inicialize:
###### You'll have to answer a few questions regarding the naming conventions for your branches. It's recommended to use the default values.
###### Você terá que responder algumas perguntas sobre as convenções de nomenclatura para suas filiais. É recomendável usar os valores padrão.
```shell
git flow init
```
OR
###### To use default
###### Para usar o padrão
```shell
git flow init -d
```
<hr>

### Features
### Recursos
###### Develop new features for upcoming releases. Typically exist in developers repos only.
###### Desenvolva novos recursos para os próximos lançamentos. Normalmente existem apenas nos repositórios de desenvolvimento dos desenvolvedores.
##### Start a new feature:
##### Inicie um novo recurso:
###### This action creates a new feature branch based on 'develop' and switches to it.
###### Esta ação cria um novo ramo de recurso com base em 'desenvolver' e muda para ele.
```
git flow feature start MYFEATURE
```

##### Finish up a feature:
##### Concluir um recurso:
###### Finish the development of a feature. This action performs the following:
###### Conclua o desenvolvimento de um recurso. Esta ação executa o seguinte:
###### 1) Merged MYFEATURE into 'develop'.
###### 1) Mesclou MYFEATURE em 'develop'.
###### 2) Removes the feature branch.
###### 2) Remove o ramo do recurso.
###### 3) Switches back to 'develop' branch
###### 3) Volta para a ramificação 'develop'
```
git flow feature finish MYFEATURE
```

##### Publish a feature:
##### Publique um recurso:
###### Are you developing a feature in collaboration? Publish a feature to the remote server so it can be used by other users.
###### Você está desenvolvendo um recurso em colaboração? Publique um recurso no servidor remoto para que ele possa ser usado por outros usuários.
```
git flow feature publish MYFEATURE
```

##### Getting a published feature:
##### Obtendo um recurso publicado:
###### Get a feature published by another user.
###### Obtenha um recurso publicado por outro usuário.
```
git flow feature pull origin MYFEATURE
```

##### Tracking a origin feature:
##### Rastreando um recurso de origem:
###### You can track a feature on origin by using
###### Você pode rastrear um recurso na origem usando
```
git flow feature track MYFEATURE
```
<hr>

### Make a Release
### Faça um lançamento
###### Support preparation of a new production release. Allow for minor bug fixes and preparing meta-data for a release
###### Suporte a preparação de um novo release de produção. Permitir pequenas correções de erros e preparar metadados para uma liberação

##### Start a release:
##### Inicie um release:
###### To start a release, use the git flow release command. It creates a release branch created from the 'develop' branch. You can optionally supply a [BASE] commit sha-1 hash to start the release from. The commit must be on the 'develop' branch.
###### Para iniciar um release, use o comando git flow release. Ele cria uma ramificação de liberação criada a partir da ramificação 'develop'. Opcionalmente, você pode fornecer um hash sha-1 de confirmação [BASE] para iniciar a liberação. A confirmação deve estar no ramo 'desenvolver'.
```
git flow release start RELEASE [BASE]
```
###### It's wise to publish the release branch after creating it to allow release commits by other developers. Do it similar to feature publishing with the command:
###### É aconselhável publicar o ramo de lançamento após criá-lo para permitir confirmações de lançamento por outros desenvolvedores. Faça o mesmo da publicação de recursos com o comando:
```
git flow release publish RELEASE
```
###### (You can track a remote release with the: ```git flow release track RELEASE``` command)
###### (Você pode rastrear uma liberação remota com o comando: `` `git flow release track RELEASE```)

##### Finish up a release:
##### Concluir um release:
###### Finishing a release is one of the big steps in git branching. It performs several actions:
###### Terminar um release é um dos grandes passos na ramificação do git. Ele executa várias ações:
###### 1) Merges the release branch back into 'master'
###### 1) Mescla o ramo de lançamento novamente em 'master'
###### 2) Tags the release with its name
###### 2) Marca a versão com seu nome
###### 3) Back-merges the release into 'develop'
###### 3) Mescla novamente o release em 'develop'
###### 4) Removes the release branch
###### 4) Remove o ramo de lançamento
```
git flow release finish RELEASE
```
###### Don't forget to push your tags with ```git push --tags```
###### Não se esqueça de enviar suas tags com `` `git push --tags```

<hr>

### Hotfixes
### Correções
###### Hotfixes arise from the necessity to act immediately upon an undesired state of a live production version. May be branched off from the corresponding tag on the master branch that marks the production version.
###### Os hotfixes surgem da necessidade de agir imediatamente em um estado indesejado de uma versão de produção ao vivo. Pode ser ramificado da tag correspondente na ramificação principal que marca a versão de produção.

##### Git flow hotfix start:
##### Início do hotfix do fluxo Git:
###### Like the other git flow commands, a hotfix is started with
###### Como os outros comandos do git flow, um hotfix é iniciado com
```
$ git flow hotfix start VERSION [BASENAME]
```
###### The version argument hereby marks the new hotfix release name. Optionally you can specify a basename to start from.
###### O argumento da versão aqui marca o novo nome da versão do hotfix. Opcionalmente, você pode especificar um nome de base para começar.

##### Finish a hotfix:
##### Conclua um hotfix:
###### By finishing a hotfix it gets merged back into develop and master. Additionally the master merge is tagged with the hotfix version
###### Ao concluir um hotfix, ele é mesclado novamente no develop e master. Além disso, a mesclagem mestre é marcada com a versão do hotfix
```
git flow hotfix finish VERSION
```
<hr>

### Commands
### Comandos
<p align="center">
    <img alt="Git" src="./Img/git-flow-commands.png" height="270" width="460">
</p>
<hr>

### Git flow schema
### Esquema de fluxo Git

<p align="center">
    <img alt="Git" src="Img/git-flow-commands-without-flow.png">
</p>
<hr>

# Github
>working directory
>staging area
>git directory
## configurações Gerais
> setar usuário
```
git config --global user.name "01101-Kairo"
```
> Setar email
```
git config --global user.email kairomilhomem@gmail.com
```
> Listar configurações
```
git config --list
```
## gitignore
```
.gitignore
adicionar nome de arquivos que nao quero no meu git
```
## Comandos + usados no Git
### Repositório Local
> Vincular repositório local com um repositório remoto
```
git remote add origin git@github.com:01101-kairo/Templats.git
```
> Clonar um repositório remoto já existente
```
git clone git@github.com:01101-kairo/Templats.git
```
> Criar novo repositório
```
git init
```
> Verificar estado dos arquivos/diretórios
```
git status
```
> Adicionar arquivo
```
> Adicionar um arquivo em específico
git add meu_arquivo.html
> Adicionar todos os arquivos/diretórios
git add .
```
> Reset
```
git reset meu_arquivo.html
```
> Reverter motificacoes
```
git checkout -- meu_arquivo.html
```
> Remocao de arquivo
```
git rm meu_arquivo.html
```
> Comitar
```
git commit -m "minha mensagem de commit"
Edit comit:
  git comit --amend -m "mensagem"
```
> Consutar alteracoes
```
git diff
git diff --staged

exibe o log:
  git log
  git log -p
  git log --pretty=online
```
> Enviar arquivos
```
git push
```
> Atualizar reositório atual
```
git pull
git fetch origin nomeDaBranch
```
> Branches
```
listar as branches
  git branch
Modificar nome da branche
  git branch -M newName
criar branche
  git branch nomeDaBranch
ir pra branch
  git checkout nomeDaBranch
criat e ir pra branch
  git checkout -b nomeDaBranch
unir as branch(deve ser feito estando na branch de destino)
  git merge nomeDaBranch
delet branch
  git branch -d nomeDaBranch
```
> Tag
```
lista as tags
  git tag
criar tag
  git tag -a v1.0 -m "versao 1.0"
criar tag com comit antigo
  git tag -a v0.0 chave -m "versao 0.0"
info da tag
  git show v0.0
ir pra tag
  git checkout v0.0
delet tag
  git tag -d v0.0
```

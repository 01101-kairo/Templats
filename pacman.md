
## update

```
~#pacman -Sy = sincroniza os repositórios.
~#pacman -Su = procura por atualização.
~#pacman -Syu = sincroniza os repositórios/procura por atualização.
```

## upgrade

```
~#pacman -Syyu = sincronização total/procura por atualização.
~#pacman -Syy = sincroniza os repositórios do Manjaro Linux.
```

## search

```
~#pacman -Ss nome_do_pacote = procura por um pacote.
```

## install

```
~#pacman -S nome_do_pacote = instala um pacote
~#pacman -Sw nome_do_pacote = apenas baixa o pacote e não o instala.
```

## show

```
~#pacman -Si nome_do_pacote = mostra informações de um pacote não instalado.
~#pacman -Qi nome_do_pacote = mostra informações do pacote já instalado.
~#pacman -Se nome_do_pacote = instala apenas as dependências.
```

## remove

```
~#pacman -R nome_do_pacote = remove um pacote.
~#pacman -Rs nome_do_pacote = remove o pacote junto com as dependências não usadas por outros pacotes.
```
```
commands |	Ubuntu |	Arch
install |	apt-get install |	pacman -S
search |	apt-cache search |	pacman -Ss
update |	apt-get update |	pacman -Syy
upgrade |	apt-get upgrade |	pacman -Syu
remove |	apt-get remove |	pacman -Rsn
autoremove| 	apt-get autoremove |	pacman -R
list| 	apt list –installed |	pacman -Qe

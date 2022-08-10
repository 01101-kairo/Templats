permissões  links	proprietario grupo  tamanho  data/hora	  nome 
-rw-r--r--  1       kairo        users  334      Jun 29 15:05 'permiss'$'\303\265''es'

d = diretorio
- = arquivo comum de usuario
c = arquivo de carctere
b = arquivo de bloco
l = link

===================================================================
*O que significa cada número ?
proprietario
grupo
outros

rwx
421
--- = 0
	0 ou - sem permissões
r-- = 4
	4 ou r read     (leitura)
-w- = 2
	2 ou w write    (escrita)
--x = 1
    1 ou x exection (execução)

rwx = 7
r-x = 5
rw- = 6
-wx = 3

===================================================================
Permissões de arquivos
        chmod permite alterar as permissões de arquivo.
        chown altera o dono do arquivo.

Mudando o dono de um arquivo: ~#chown usuario:grupo arquivo ou diretório

O parâmetro -R faz com que a alteração seja recursiva.
Isto é, afete todas as pastas e arquivos dentro de uma pasta especificada.
        chmod -R 777 arquivo ou /diretório

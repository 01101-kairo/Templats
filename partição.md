CRIANDO E MONTANDO UMA PARTIÇÃO
# cfdisk ou fdisk [disco]
Suponha que você adicionou um outro HD ou criou um disco em uma VM.

1. Verificar se o Linux identificou o disco com o comando:

# fdisk -l ou blkid

2. Após verificar, efetuar o seguinte comando com o fdisk para dar início a criação da partição:

# fdisk /dev/sdb1

(mude /dev/sdb1 de acordo com sua configuração de discos)

3. Após executar o comando acima o mesmo irá mostrar várias opções que o fdisk possui, utilizarem a seguintes neste exemplo:
opção p --> mostra qual disco será criada a partição. Sempre utilize essa opção para ter certeza em qual disco você se encontra.
opção n --> utilizado para criar uma nova partição, logo em seguida aparecerão várias perguntas se deseja que a partição seja primária ou estendida etc.

4. Após criar a partição digite w para gravar.

5. Formataremos a partição com o tipo de sistema de arquivo desejado:

# mkfs -t ext4 /dev/sdb1

6. Agora execute o comando para montar a partição:

# mount /dev/sdb1 /opt/

7. Pronto, foi feita a criação de uma partição e a sua montagem, se tudo ocorrer bem a partição será exibida com o comando:

# df -h

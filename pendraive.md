1º passo: identificar o dispositivo.

# fdisk -l

Seu pendrive deve aparecer na lista, de acordo com sua capacidade, exemplo: 8gb deve ter uns 7.5GB como no meu caso.
Feito isso, ele deve ser algo do tipo:
/dev/sdb; ou
/dev/sdc (no caso de você usar um hd externo ou mais de um pendrive)

2º passo: formatar o dispositivo.

# mkfs.vfat /dev/sdx -I

3º passo: gravar a imagem via comando.

Vamos usar dois comandos, o dd e o pv.

O x representa a letra de teu dispositivo!

/dev/sdx

Comando dd de maneira simples e direta!

# dd if=sua_imagem.iso of=/dev/sdx

Comando pv de forma simples e direta (este comando mostra a barra de progresso):

# pv -EE sua_imagem.iso > /dev/sdx


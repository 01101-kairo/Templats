Olá pessoal, tudo bem?!

Não é nada fora do comum que nós desenvolvedores  tenhamos que manipular/modificar/criar bancos de dados, com certeza isso é o pesadelo de qualquer DBA. Particularmente gosto de trabalhar com front, back e banco de dados pois isso me permite a ter acesso a conteúdos fantásticos aprendendo coisas novas sempre.

Como podemos manipular o banco de dados? Bom, particularmente para atividades corriqueira utilizo o terminal, sim o terminal, é simples e rápido.

Caso você seja usuário Windows recomento que utilize o cmder software portable que emula o terminal como se fosse no Linux, caso você seja usuário Linux ou Mac, bom, sua vida com o terminal já é tranquila 🙂

Conectar no MySQL

Abra o terminal e digite:

mysql -u root -p
1
mysql -u root -p
Parâmetro: -u
Indica o usuário ao qual desejamos utilizar para conectar ao banco.
Parâmetro: root
Nome do usuário que estamos utilizando para realizar a conexão com o banco de dados. Onde pode ser qualquer usuário cadastrado no MySQL.
Parâmetro: -p
Indica a senha do usuário para conexão com o banco, este parâmetro é opcional, pois caso o usuário desejado não utilize senha para se conectar basta omitir este parâmetro, porem não é nada recomendado utilizar usuários sem senha 🙂
Conectar no MySQL acessando  direto o banco de dados desejado

Abra o terminal e digite:

mysql -u root -p nome_do_banco_de_dados
1
 mysql -u root -p nome_do_banco_de_dados
Parâmetro: nome_do_banco_de_dados
Como descrito, refere-se ao nome do banco de dados que desejamos acessar.
Após execução do comando é realizado a conexão e acesso ao banco de dados que desejamos utilizar.

Listar os banco de dados

Abra o terminal acesso o MySQL e digite:

show databases;
1
show databases;
Abaixo segue um exemplo de retorno do comando, podemos observar que é listado todos os bancos de dados até mesmo os utilizados pelo MySQL.

+--------------------+
| Database           |
+--------------------+
| information_schema |
| banco_01           |
| livraria           |
| mysql              |
| performance_schema |
| post_sql           |
| sys                |
| banco_02           |
+--------------------+
1
2
3
4
5
6
7
8
9
10
11
12
+--------------------+
| Database           |
+--------------------+
| information_schema |
| banco_01           |
| livraria           |
| mysql              |
| performance_schema |
| post_sql           |
| sys                |
| banco_02           |
+--------------------+
Listar as tabelas do banco de dados

Abra o terminal acesso o MySQL, em seguida acesse o banco de dados desejado e digite:

show tables;
1
 show tables;
Exemplo de resultado.

+--------------------+
| Tables_in_livraria |
+--------------------+
| autores            |
| capitulos          |
| livros             |
| vendas             |
+--------------------+
1
2
3
4
5
6
7
8
+--------------------+
| Tables_in_livraria |
+--------------------+
| autores            |
| capitulos          |
| livros             |
| vendas             |
+--------------------+
Visualizar estrutura da tabela

Abra o terminal acesso o MySQL, em seguida acesse o banco de dados desejado e digite:

describe table_name;
1
describe table_name;
Parâmetro: table_name
Substitua pelo nome da tabela desejada.
Exemplo de resultado.

+--------------------+---------------+------+-----+---------+----------------+
| Field              | Type          | Null | Key | Default | Extra          |
+--------------------+---------------+------+-----+---------+----------------+
| id                 | int(11)       | NO   | PRI | NULL    | auto_increment |
| nome               | varchar(100)  | NO   |     | NULL    |                |
| data_de_lancamento | date          | NO   |     | NULL    |                |
| autor_id           | int(11)       | NO   |     | NULL    |                |
| preco              | decimal(10,2) | NO   |     | NULL    |                |
+--------------------+---------------+------+-----+---------+----------------+
5 rows in set (0,00 sec)
1
2
3
4
5
6
7
8
9
10
+--------------------+---------------+------+-----+---------+----------------+
| Field              | Type          | Null | Key | Default | Extra          |
+--------------------+---------------+------+-----+---------+----------------+
| id                 | int(11)       | NO   | PRI | NULL    | auto_increment |
| nome               | varchar(100)  | NO   |     | NULL    |                |
| data_de_lancamento | date          | NO   |     | NULL    |                |
| autor_id           | int(11)       | NO   |     | NULL    |                |
| preco              | decimal(10,2) | NO   |     | NULL    |                |
+--------------------+---------------+------+-----+---------+----------------+
5 rows in set (0,00 sec)
Dump da base de dados

Para criar uma cópia da base de dados desejados abara o terminal, acesse o diretório no qual deseja criar o arquivo em seguida digite o comando:

mysqldump -u root -p database_name > database_name.sql;
1
mysqldump -u root -p database_name > database_name.sql;
Parâmetro: database_name
Substitua pelo nome do banco de dados ao qual deseja realizar a cópia.
Após executar o comando, será criado um arquivo .sql no local de desetino desejado. Caso você tenha o costume de utilizar por exemplo o PHPMyAdmin para gear o dump, recomendo que passe a utilizar o terminal, pois a interface gráfica em alguns casos pode gerar um arquivo .sql que ao ser importado por outro membro da sua equipe pode conter erros. Já o arquivo gerado pelo terminal as chances são mínimas, pois se o comando executado não apresentar erro seu resultado será correto e o arquivo gerado poderá ser importado sem maiores eventualidades.

Dump somente da estrutura da base de dados

Abra o terminal vá ao diretório onde deseja criar o arquivo de backup e digite:

mysqldump -u root -p database_name --no-data > database_name.sql;
1
 mysqldump -u root -p database_name --no-data > database_name.sql;
Parâmetro: –no-data
Indica que desejamos criar uma cópia do bando de dados sem as informações contidas nas tabelas.
Este comando é bem similar ao mencionado anteriormente, porém com a diferença que ele criar uma cópia da estrutura do banco de dados não realizando a exportação dos dados contidos nas tabelas.

Importar banco de dados

Abra o terminal vá ao diretório onde encontra-se o bando de dados que deseja importar e digite:

mysql -u root -p database_name < database_name.sql;
1
mysql -u root -p database_name < database_name.sql;
Após execução do comando e o arquivo a ser importado não conter erros, sua importação será realizada com sucesso. Em casos de importação onde as tabelas do banco de dados contenham 100, 200, 300 mil (esse volume é até pequeno em comparação com banco de milhões de registros) ou mais registros isso acarretará em um tempo maior de processamento, basta aguardar até a finalização e liberação do terminal pelo processo.

Dump de todos os bancos de dados

Abra o terminal, entre no diretório desejado para armazenar o arquivo de backup e digite:

mysqldump -u user -p --all-databases > full_path_to\file.sql
1
mysqldump -u user -p --all-databases > full_path_to\file.sql
Parâmetro: –all-databases

Indica que desejamos exportar todas as bases de dados disponíveis no MySQL.
Após término da execução, será gerado um arquivo conforme especificado contento todos os bancos de dados do MySQL.

Apagar tabela

Abra o terminal acesse o MySQL em seguida o banco de dados desejado e digite:

drop table nome_da_tabela;
1
 drop table nome_da_tabela;
Parâmetro: drop table
Responsável por apagar a tabela do banco de dados.
Parâmetro: nome_da_tabela
Nome da tabela ao qual se deseja apagar.
Utilize com muita cautela, pois após executar o comando a tabela será apagada do seu banco de dados!

Apagar a base de dados

Abra o terminal acesse o MySQL e digite:

drop database nome_do_banco_de_dados;
1
 drop database nome_do_banco_de_dados;
Parâmetro: drop database
Responsável por apagar o banco de dados.
Parâmetro: nome_do_banco_de_dados
Nome do banco de dados ao qual se deseja apagar.
Utilize com muita cautela, pois após executar o comando o banco de dados será apagado!

Limpar o terminal

Acesse o terminal e pressione o seguinte comando:

ctrl+l
1
ctrl+l
Este é um comando do terminal, porém muito útil quando estamos trabalhando com o MySQL ou qualquer banco de dados ou atividade no terminal, pois o mesmo limpa a tela do terminal para que possamos utilizá-lo com mais clareza e sem poluição de informações na tela.

Todos os comandos listados acima são recomendados para uso em ambiente local, não recomendo seu uso em ambiente de produção, caso vá utilizar tenha MUITA CAUTELA e PARCIMÔNIA com os comandos utilizados. Siga as boas práticas e com isso você verá que o uso do terminal irá maximizar sua performance.

Não tenha medo do terminal, sabendo utilizá-lo é uma ferramenta poderosíssima, podendo abrir um leque de opções fantásticas.

Espero que tenham apreciado este post e caso tenham alguma duvidas, sugestões ou crítica por favor deixe nos comentários e com isso podemos debater e aprender cada vez mais.

Grande abraço e até a próxima 

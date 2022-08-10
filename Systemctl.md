O Systemd é um gerenciador de sistema de inicialização que é amplamente usado tornando-se o novo padrão para computadores com Linux. Embora existam opiniões consideráveis sobre se systemd é uma melhoria ao longo dos tradicionais sistemas de inicialização SysVinit, a maioria das distribuições pretendemos adotá-la ou já o fizeram.

Devido à sua forte adoção, familiarizar-se com systemd vale bem a pena, pois ele vai tornar o gerenciamento dos serviços consideravelmente mais fácil. Conhecer e utilizar as ferramentas e daemons que compõem Systemd irá ajudá-lo a apreciar melhor o poder, flexibilidade e capacidades de que dispõe, ou pelo menos ajudá-lo a fazer o seu trabalho com o mínimo de confusão possível.

Neste guia a DigitalOcean mostra alguns aspectos e como usar o Systemctl, a ideia central é discutir o comando systemctl, que é a ferramenta de gerenciamento central para controlar o sistema de inicialização.
Iniciar e parar serviços com o systemctl
 

Para iniciar um serviço do systemd, executando instruções no arquivo de unidade do serviço, use o prefixo start no comando. Se você estiver executando como um usuário não-root, você terá que usar o sudo uma vez que este irá afetar o estado do sistema operacional:

sudo systemctl start application.service
Como mencionado acima, systemd sabe que procurar os arquivos *.service para os comandos de gerenciamento de serviços, portanto, o comando poderia facilmente ser digitado como este:

sudo systemctl start application
Embora você possa usar o formato acima para administração geral, para maior clareza, vamos usar o sufixo.service para o restante dos comandos para ser explícito sobre o alvo estamos operando.
Para parar um serviço em execução, você pode usar o comando prefixo stop no comando:

sudo systemctl stop application.service
Reiniciando e Recarregando com o systemctl
 

Para reiniciar um serviço em execução, você pode usar o comando restart:

sudo systemctl restart application.service
Se a aplicação em questão é capaz de recarregar seus arquivos de configuração (sem reiniciar), você pode usar o comando reload comando para iniciar esse processo:

sudo systemctl reload application.service
Se você não tem certeza se o serviço tem a funcionalidade para recarregar sua configuração, você pode usar o comando reload-or-restart. Isto irá recarregar a configuração no local, se disponível. Caso contrário, ele irá reiniciar o serviço para que a nova configuração tome efeito:

sudo systemctl reload-or-restart application.service
Como ativar e desativar serviços com o Systemctl
 

Os comandos acima são úteis para iniciar ou parar comandos durante a sessão atual. Para dizer ao systemd para iniciar os serviços automaticamente no boot, você deve habilitá-los.

Para iniciar um serviço no boot, utilize o comando enable:

sudo systemctl enable application.service
Isto irá criar um link simbólico de cópia do sistema do arquivo de serviço (normalmente em /lib/systemd/system ou /etc/systemd/system) para o local no disco onde systemd procura por arquivos de inicialização automática (geralmente /etc/systemd/system/some_target.target.wants . Mas vou passar o que um target mais adiante neste guia).
Para desativar o serviço que é iniciado automaticamente, você pode usar o disable:

sudo systemctl disable application.service
Isto irá remover o link simbólico que indica que o serviço deve ser iniciado automaticamente.
Tenha em mente que habilitar um serviço com o comando enable não irá iniciá-lo na sessão atual. Se você deseja iniciar o serviço e habilitá-lo no boot, você terá que usar os comandos start e enable.
Verificando o Status de Serviços com o Systemctl
 

Para verificar o status de um serviço em seu sistema, você pode usar o comando status:

systemctl status application.service
Isto irá fornecer-lhe com o estado do serviço, a hierarquia cgroup, e as primeiras linhas de log.
Por exemplo, ao verificar o status de um servidor Nginx, você poderá ver uma saída como esta:

nginx.service – A high performance web server and a reverse proxy server
Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
Active: active (running) since Tue 2015-01-27 19:41:23 EST; 22h ago
Main PID: 495 (nginx)
CGroup: /system.slice/nginx.service
??495 nginx: master process /usr/bin/nginx -g pid /run/nginx.pid; error_log stderr;
??496 nginx: worker process
Jan 27 19:41:23 desktop systemd[1]: Starting A high performance web server and a reverse proxy server…
Jan 27 19:41:23 desktop systemd[1]: Started A high performance web server and a reverse proxy server.
Isso lhe dá uma boa visão geral do status atual da aplicação, notificando-o de todos os problemas e quaisquer ações que possam ser necessárias.
Existem também métodos para a verificação de estados específicos. Por exemplo, para verificar se a unidade está ativa (em execução), você pode usar o comando is-active:

systemctl is-active application.service
Isto irá lhe retornar o estado da unidade atual, que é geralmente active ou inactive. O código de saída será “0” se ele estiver ativo, tornando o resultado mais simples para analisar programaticamente.
Para ver se a unidade for ativada, você pode usar o comando is-enabled:

systemctl is-enabled application.service
A saída será se o serviço está enabled ou disabled e voltará a definir o código de saída para “0” ou “1”, dependendo da resposta à pergunta do comando.

Uma terceira verificação é se a unidade está em um estado de falha. Esta indicará se existe um problema ao iniciar a unidade em questão:

systemctl is-failed application.service
Isso irá retornar active se estiver funcionando corretamente ou failed se ocorreu um erro. Se a unidade foi intencionalmente parada, ele pode retornar unknow ou inactive. Um status de saída “0” indica que ocorreu uma falha e um status de saída “1” indica qualquer outro status.
Visão Geral do Status do Sistema com o Systemctl
 

Os comandos até agora têm sido úteis para o gerenciamento de serviços individuais, mas eles não são muito úteis para explorar o estado atual do sistema. Há uma série de comandos systemctl que fornecem essas informações.

Listagem Unidades Atuais com o Systemctl
Para ver uma lista de todas as unidades ativas que o Systemd conhece, podemos usar o comando list-units:

systemctl list-units
Isto irá mostrar uma lista de todas as unidades que Systemd tem atualmente ativas no sistema. A saída será algo parecido com isto:

UNIT LOAD ACTIVE SUB DESCRIPTION
atd.service loaded active running ATD daemon
avahi-daemon.service loaded active running Avahi mDNS/DNS-SD Stack
dbus.service loaded active running D-Bus System Message Bus
dcron.service loaded active running Periodic Command Scheduler
dkms.service loaded active exited Dynamic Kernel Modules System
getty@tty1.service loaded active running Getty on tty1
. . .
A saída possui as seguintes colunas:

UNIT: O nome da unidade do systemd
LOAD: Se a configuração da unidade foi analisada pelo systemd. A configuração das unidades carregadas são mantida na memória.
ACTIVE: Um resumo do estado se a unidade estiver ativa. Isso geralmente é uma maneira bastante básica para mostrar se a unidade foi iniciado com êxito ou não.
SUB: Este é um estado de nível inferior que indica informações mais detalhadas sobre a unidade. Isso muitas vezes varia por tipo de unidade, estado, e o método real em que a unidade funciona.
DESCRIPTION: Uma breve descrição textual do que a unidade é/faz.
Uma vez que o comando list-units mostra apenas as unidades ativas, por padrão, todas as entradas acima irão mostrar “loaded” na LOAD e “active” na coluna ACTIVE. Esta exposição é, na verdade, o comportamento padrão do systemctl quando chamado sem comandos adicionais, então você vai ver a mesma coisa se você chamar systemctl sem argumentos:

systemctl
Podemos dizer systemctl trás informações de saídas diferentes, adicionando flags adicionais. Por exemplo, para ver todas as unidades que Systemd carregou (ou tentou carregar), independentemente de se eles estão ativos, você pode usar a flag –all, como neste exemplo:

systemctl list-units --all
Isto irá mostrar qualquer unidade que Systemd carregou ou tentou carregar, independentemente do seu estado atual no sistema. Algumas unidades se tornam inativas após a execução, e algumas unidades que Systemd tentou carregar e pode por não ter sido encontrada no disco.
Você pode usar outras flags para filtrar esses resultados. Por exemplo, podemos usar o “–state =” para indicar os estados LOAD, ativos ou SUB que desejar ver. Você terá que manter o sinalizador –all para que o systemctl permita que as unidades não ativas sejam exibidas:

systemctl list-units --all --state=inactive
Outro filtro comum é o filtro –type=. Podemos dizer ao systemctl para mostrar somente unidades do tipo que estamos interessados em ver. Por exemplo, para ver apenas as unidades do serviço ativas, nós podemos usar:

systemctl list-units --type=service
Listando Todos os Arquivos da Unidade com o Systemctl
 

O comando list-units exibe apenas unidades que Systemd tentou analisar e carregar na memória. Então, o systemd só vai ler unidades que acha que precisa, e isso não vai necessariamente incluir todas as unidades disponíveis no sistema. Para ver todos os arquivo de unidade disponíveis dentro dos caminhos de pasta do Systemd, incluindo aqueles que systemd não tentou carregar, você pode usar o comando list-units-files:

systemctl list-units-files
Unidades são representações de recursos que o Systemd conhece. O systemd não necessariamente lê todas as definições de unidade neste ponto de vista, só apresenta informações sobre os próprios arquivos. A saída tem duas colunas: o arquivo de unidade e o estado.
UNIT FILE STATE
proc-sys-fs-binfmt_misc.automount static
dev-hugepages.mount static
dev-mqueue.mount static
proc-fs-nfsd.mount static
proc-sys-fs-binfmt_misc.mount static
sys-fs-fuse-connections.mount static
sys-kernel-config.mount static
sys-kernel-debug.mount static
tmp.mount static
var-lib-nfs-rpc_pipefs.mount static
org.cups.cupsd.path enabled
O estado geralmente será “enabled”, “disabled”, “static”, ou “masked”. Neste contexto, “static” significa que o arquivo unidade não contém uma seção “install”, que é usado para ativar uma unidade. Como tal, estas unidades não podem ser ativadas. Geralmente, isto significa que a unidade efetua uma ação de uma única vez ou é utilizado apenas como uma dependência de outra unidade e não deve ser administrada por si só. E vamos dizer que o “masked” significa momentaneamente.

Gestão de unidade
Até agora, temos trabalhado com os serviços e exibido informações sobre os arquivos e unidades que o Systemd conhece. No entanto, podemos encontrar informações mais específicas sobre as unidades que usam alguns comandos adicionais.

Exibindo Um Arquivo Unit
Para exibir que o arquivo de unidade do systemd foi carregado no seu sistema, você pode usar o comando cat (este foi adicionado em systemd versão 209). Por exemplo, para ver o arquivo unidade do daemon atd , poderíamos escrever:

systemctl cat atd.service
[Unit]
 Description=ATD daemon

[Service]
 Type=forking
 ExecStart=/usr/bin/atd

[Install]
 WantedBy=multi-user.target
A saída é o arquivo de unidade como é conhecido na atualmente na execução do processo do systemd. Isso pode ser importante se você tiver modificado arquivos da unidade recentemente ou se você está substituindo determinadas opções em um fragmento de arquivo da unidade (nós iremos cobrir isso mais tarde).

Exibindo Dependências
 

Para ver árvore de dependências de uma unidade, você pode usar o comando list-dependencies:

systemctl list-dependencies sshd.service
Isto irá exibir uma hierarquia mapeando as dependências que devem ser tratadas com a fim de iniciar a unidade em questão. Dependências, neste contexto, incluem as unidades que são ou “necessárias” ou “requeridas” pelas unidades acima dela.

sshd.service
??system.slice
??basic.target
??microcode.service
??rhel-autorelabel-mark.service
??rhel-autorelabel.service
??rhel-configure.service
??rhel-dmesg.service
??rhel-loadmodules.service
??paths.target
??slices.target
As dependências recursivas são exibidas apenas por unidades .TARGET, que indicam estados do sistema. Para listar recursivamente todas as dependências, inclua a flag –all.
Para mostrar dependências reversas (unidades que dependem da unidade especificada), você pode adicionar o sinalizador –reverse ao comando. Outras opções que são úteis são os –before e –after, que podem ser usadas para mostrar unidades que dependem da unidade especificada, começando antes e depois dela, respectivamente.
Verificação das Propriedades da Unidade
 

Para ver as propriedades de baixo nível de uma unidade, você pode usar o programa de comando. Isto irá exibir uma lista de propriedades que estão definidas para a unidade especificada usando um formato chave=valor:

systemctl show sshd.service
Id=sshd.service
Names=sshd.service
Requires=basic.target
Wants=system.slice
WantedBy=multi-user.target
Conflicts=shutdown.target
Before=shutdown.target multi-user.target
After=syslog.target network.target auditd.service systemd-journald.socket basic.target system.slice
Description=OpenSSH server daemon
Se você quiser exibir uma única propriedade, você pode usar a flag -p com o nome da propriedade. Por exemplo, para ver os conflitos que a unidade sshd.service tem, você pode digitar:

systemctl show sshd.service -p Conflicts
Conflicts=shutdown.target
 

Mascaramento e Desmascarando Unidades
 

Vimos na seção de gerenciamento de serviços como parar ou desativar um serviço, mas o systemd também tem a capacidade de marcar uma unidade como completamente não-iniciável, automaticamente ou manualmente, ligando-a à /dev/null. Isto é chamado de mascaramento da unidade, e é possível com o comando mask:

sudo systemctl mask nginx.service
Isso irá impedir que o serviço Nginx seja iniciado, manual ou automaticamente, durante o tempo que ele é mascarado.
Se você verificar as list-unit-files, você vai ver o serviço agora está listado como mascarado:

systemctl list-unit-files
kmod-static-nodes.service static
ldconfig.service static
mandb.service static
messagebus.service static
nginx.service masked
quotaon.service static
rc-local.service static
rdisc.service disabled
rescue.service static
Se você tentar iniciar o serviço, você verá uma mensagem como esta:

sudo systemctl start nginx.service
Failed to start nginx.service: Unit nginx.service is masked.
Para desmascarar uma unidade, tornando-a disponível para uso novamente, basta usar o comando unmask:

sudo systemctl unmask nginx.service
Isso irá retornar a unidade ao seu estado anterior, permitindo-lhe ser habilitada.
Editando Arquivos das Unidades
Enquanto o formato específico para arquivos de unidade está fora do escopo deste tutorial, o systemctl fornece mecanismos integrados para editar e modificar os arquivos da unidade se você precisar fazer ajustes. Esta funcionalidade foi adicionada no systemd versão 218.

O comando edit, por padrão, irá abrir para edição a unidade em questão:

sudo systemctl edit nginx.service
Este será um arquivo em branco que pode ser usado para substituir ou adicionar diretrizes para a definição da unidade.

Um diretório será criado dentro da etc/systemd/system/ que irá conter o nome da unidade com o sufixo “.d”. Por exemplo, para o nginx.service , um diretório chamado nginx.service.d será criado.

Dentro deste diretório, um arquivo será criado chamado override.conf. Quando a unidade for carregada, o systemd vai, na memória, mesclar o arquico de substituição com o arquivo unidade completo. Diretivas do arquivo de configuração override.conf terá precedência sobre os encontrados no arquivo unidade original.

Se você deseja editar o arquivo unidade completamente, em vez de criar um arquivo de override, você pode usar a flag –full:

sudo systemctl edit --full nginx.service
Isto irá carregar o arquivo de unidade atual para o editor, onde ele poderá ser modificado. Ao sair do editor, o arquivo alterado será gravado em /etc/systemd/system, que terá precedência sobre definição de unidade do sistema (geralmente encontrado em /lib/systemd/system).

Para remover todas as adições que você tenha feito, exclua o diretório de configuração da unidade .d ou o arquivo de serviço modificado a partir de /etc/systemd/system. Por exemplo:

sudo rm -r /etc/systemd/system/nginx.service.d
 

Para remover completamente um arquivo de unidade modificada, use:

sudo rm /etc/systemd/system/nginx.service
 

Depois de excluir o arquivo ou pasta, você deve recarregar o processo do systemd para que ele não tente fazer referência a esses arquivos e reverter usando cópias do sistema. Você pode fazer isso digitando:

sudo systemctl daemon-reload
Ajustando o Estado do Sistema (Nível de Execução) com Targets
 

Os targets são arquivos de unidade especiais que descrevem um ponto do estado ou sincronização. Como outras unidades, os arquivos que definem os targets podem ser identificados por seu sufixo, que neste caso é o .TARGET.

Targets não fazem muito a si mesmos, mas são usados para agrupar unidades em conjunto.
Isto pode ser utilizado, a fim de levar o sistema para certos estados, assim como outros sistemas de inicialização como o init usam níveis de execução (runlevel). Eles são usados como referência para quando certas funções estão disponíveis, permitindo que você especifique o estado desejado, em vez de unidades individuais necessárias para produzir esse estado.

Por exemplo, há um swap.target que é usado para indicar que o swap está pronto para uso. Unidades que fazem parte deste processo pode sincronizar com este target, indicando na sua configuração que eles são “WantedBy=” ou “RequiredBy=” (Necessários ou requeridos) para que funcione o swap.target. Unidades que requerem o swap podem especificar esta condição usando os WantedBy= ou RequiredBy=, e especificações do After= para indicar a natureza de seu relacionamento.

Obtendo e Definindo o Target Padrão
 

O processo do systemd tem um destino padrão que ele usa durante a inicialização do sistema. Satisfazendo a cascata de dependências a partir desse único target vai trazer o sistema para o estado desejado. Para encontrar o destino padrão para o seu sistema, digite:

systemctl get-default
multi-user.target
 

Se você deseja definir um target padrão diferente, você pode usar o set-default. Por exemplo, se você instalou um ambiente gráfico desktop e você deseja que o sistema inicialize-o por padrão, você pode mudar seu target padrão:

sudo systemctl set-default graphical.target
 

Listando Targets Disponíveis
Você pode obter uma lista dos targets disponíveis no seu sistema digitando:

systemctl list-units-files --type=target
 

Ao contrário de níveis de execução, alvos múltiplos podem estar ativos ao mesmo tempo. Um alvo ativo indica que systemd tentou começar a todas as unidades ligadas ao alvo e não tentou derrubá-las novamente. Para ver todos os alvos ativos, digite:

systemctl list-units --type=target
Isolando Targets
 

É possível iniciar todas as unidades associadas com um alvo e parar todas as unidades que não são parte da árvore de dependência. O comando que nós precisamos de fazer isso é chamado, apropriadamente, isolate. Isto é semelhante à mudar o runlevel (nível de execução) em outros sistemas de inicialização.

Por exemplo, se você estiver operando em um ambiente gráfico com graphical.target ativo, você pode desligar o sistema gráfico e colocar o sistema em um estado de linha de comando multi-user, isolando o multi-user.target. Como o graphical.target depende do multi-user.target, (mas não o contrário), todas as unidades gráficas serão interrompidas.

Você pode querer dar uma olhada nas dependências do alvo que você está isolando antes de realizar este procedimento para garantir que você não está parando serviços vitais:

systemctl list-dependencies multi-user.target
 

Quando estiver satisfeito com as unidades que serão mantidas ativas, você pode isolar o alvo digitando:

sudo systemctl isolate multi-user.target
Usando Atalhos Para Eventos Importantes
 

Há targets definidos para eventos importantes como desligar ou reiniciar. No entanto, o systemctl também tem alguns atalhos que adicionam um pouco de funcionalidades adicionais.

Por exemplo, para colocar o sistema no modo de recuperação (de um único usuário), você pode simplesmente usar o comando rescue em vez do isolate rescue.target:

sudo systemctl rescue
Isto irá fornecer a funcionalidade adicional de alertar todos os usuários logados sobre o evento.
Para parar o sistema, você pode usar o comando halt:

sudo systemctl halt
 

Para iniciar um desligamento completo, você pode usar o comando poweroff:

sudo systemctl poweroff
 

Uma reinicialização pode ser iniciada com o comando reboot:

sudo systemctl reboot
Todos estes comandos alertam os usuários logados que o evento está ocorrendo, algo que simplesmente executando ou isolando o target não iria fazer. Note que na maioria das máquinas que usam systemd, os comandos mais curtos, são abreviações dos comandos do systemd, para estas operações e funcionam corretamente também.

Por exemplo, para reiniciar o sistema, normalmente você pode digitar:

sudo reboot

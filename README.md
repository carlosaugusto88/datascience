# datascience
machinelearning

Carlos Augusto de Oliveira

Esse trabalho tem como objetivo coletar as principais informações do servidor, padronizar essas informações e aplicar 
nos metodos referentes a Decision Tree e Random Forest.
Com o resultado desses algoritmos conseguimos alarmar de forma proativa um possivel problema.

Informações do conjunto de dados:

A coleta dos dados será através do programa sysstat/sar(Linux), no qual gera os logs referentes a memoria e processamento, com esses dados 
utilizaremos para classificar um possível impacto no ambiente.
Os dados sao retirados via shell script infosystem.sh, utilizando alguns comandos SAR(SYSSTAT) 
responsavel por dados referentes a processamento e disco dos servidores.
A solução para esse cenário é desenvolver um algoritmo Machine Learning para acurácia e classificação dos casos em que a probabilidade de problema seja detectada, 
atuando de forma proativa e antecipada para evitar o problema.


Problema:
Atualmente temos algumas aplicações que sem motivo aparente travam e impactam os processos de negocio, 
sendo necessario o restart dos servidores para normalização.

Nesse trabalho coletamos 32 caracteristicas de ambiente, a base das informações possuem dados de 2 semanas e 17000 registros, no qual com o conjuntos de todas as caracteristicas aplicadas nos modelos de aprendizados é possivel identificar um possivel desvio referente ao problema.

Os dados sao retirados via shell script infosystem.sh, esse script foi criado exclusivamente para coletar as informacoes
desejadas nesse projeto, esse script executa alguns comandos SAR(SYSSTAT) responsavel por extrair os dados referentes a processamento, rede e disco, atualmente o mesmo é executado nos servidores monitorados gerando uma base com as informações a 
cada 2 minutos de frenquencia.

Segue as informações coletadas:
DIA = Referente ao dia da semana ex: 1= domingo , 2=segunda , 3= terça e etc.
MES = Referente ao numero do mes ex: 1= janeiro , 2=fevereiro ,3 = março  e etc.
HORA = Referente a hora do evento
MINUTO = Referente ao minuto do evento
MEM_TOT_X= Referente ao total de Memoria em MB do servidor         
MEM_USED_X=Referente ao total de Memoria Utilizada em Mb do servidor   
MEM_FREE_X=Referente ao total de Memoria Livre em Mb do servidor        
SWP_TOT_X= Referente ao Total Swap em Mb           
SWP_USED_X=Referente ao Swap Utilizado em Mb       
SWP_FREE_X=Referente ao Swap Livre em Mb
CPU_IDLE_X=Referente a CPU Livre
CPU_USER_X=Referente a CPU USER 
CPU_SYST_X=Referente a CPU SYSTEM
DSK_TPS_X=Referente a Transacao Por/Segundo Disco        
FILE_SZ_X=Referente ao Total de Arquivos abertos
INODE_SZ_X=Refeente ao Total de Inodes Utilizados pelo Kernel
UPTIME_X=Referente ao tempo que o servidor esta no ar.
SERVIDOR= Referente a informação do host do servidor.
COLISAO_NIC_X=Quanto mais colisões ocorrem menor é a eficiência da rede.
RX_NIC_X=Pacotes RX (ifconfig) recepcao de dados (Download)
TX_NIC_X=Pacotes TX (ifconfig) envio de dados (Upload)
NIC_RX_PCK_X=Pacotes RX (sar)
NIC_TX_PCK_X=Pacotes TX (sar)
ACTIVE_CONNECTIONS_OPENINGS_X=Conexao aberta e ativas(sar) 
PASSIVE_CONNECTION_OPENINGS_X=Conexao aberta e inativas (sar) 
FAILED_CONNECTION_ATTEMPTS_X=Falha de conexao (sar)   
CONNECTION_RESETS_RECEIVED_X=Tentativas de conexao (sar)  
CONNECTIONS_ESTABLISHED_X=Conexoes estabilizadas (sar)	  
SEGMENTS_RECEIVED_X=Segmentos recebidos(sar)
SEGMENTS_SEND_OUT_X=Segmentos enviados (sar)
SEGMENTS_RETRANSMITED_X=Segmentos retransferidos (sar)
BAD_SEGMENTS_RECEIVED_X=Segmentos nao estavel(sar)

A padronizacao dos dados foram aplicados diretamente no shell-script com objetivo de facilitar as informações coletadas.

Solucao
Para identificar um comportamento estavel e um comportamento com desvio, após a coleta de dados, mapeamos os registros que em algum momento tiveram algum incidente no ambiente(critico), registrando aqueles periodos como instavel, agora com o modelo devidamente mapeado, aplicamos nos metodos selecionados como Decision Tree, Random Forest e Network Neural.
Dessa forma para cada metodo geramos um modelo de aprendizado, no qual ao receber os 32 parametros de caracteristicas nos 
retorna o resultado daquela avaliação.

Exemplificando o mapeamento da base para incidentes criticos: no qual o status 0 é estavel e 1 é instavel.
DIA;HORA;TIVEMOS_INCIDENTE: 
01;04;0;
02;01;0;
04;05;1;(dia e hora com um registro de incidente no ambiente de produção-necessario o restart)
06;03;0;

Após os modelos criados, o processo passa a receber as 32 caracteristicas coletadas, nos informando qual é o comportamento esperado para aquelas informações injetadas no modelo.

Conclusao
A conclusão desse trabalho está na comparação dos algoritmos utilizados Decision Tree e Random Forest, no qual nos possibilitou criar os modelos de aprendizados para todos os algoritmos e após aplicar 
as novas instancias para validação, temos a seguinte conclusao de qual algoritmo utilizar nesse trabalho e para a base coletada.
O primeiro algoritmo Decision Tree é o que conseguimos chegar a melhor performance e confiança 100%, logo que o mesmo é destinado 
exatamente para o cenario de classificação, no qual atende o objetivo do projeto que é inserir um comportamento e nos retornar se aquele comportamento faz parte de um cenario estavel ou nao, permitindo um alerta de forma proativa.

O segundo algoritmo Random forest, é o que conseguimos chegar a segunda melhor performance e confiança 97%, esse algoritmo bastante utilizado para regressão e classificação, atende muito bem o trabalho, possibilitando utilizar os 2 metodos para melhorar o nosso acionamento proativo e entendimento de aprendizado dos modelos.

Desas maneira nossa conclusão esta em utilizar o algoritmo Decision Tree no qual tem como objetivo diretamente 
a classificação e atende nossas expectativas para o resultado do trabalho.

Obrigado.

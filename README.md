# PrintService

Sistema para impressão de arquivos direto de uma aplicação que use MySQL

###config.ini###############################################################################

--ABRA COM O BLOCO DE NOTAS O ARQUIVO config.ini PARA CADASTRAR SUAS CREDENCIAIS DO BANCO DE DADOS. <BR>
--NOVA VERSÃO, cadastrar no arquivo também;<BR>
-[ticket_type]: O TIPO DE CREDENCIAL SENDO 0 = PUSELIRA, 1 = ETIQUETA 90x40x1, 2 = HOMOLOGAÇÃO<BR>
-FUNÇÃO DE HOMOLOGAÇÃO GERA UM PDF PARA QUE VOCÊ TESTE A COMUNICAÇÃO DOS SISTEMAS.<BR>
-[printer_port]: COLOCAR A PORTA ONDE A ARGOX ESTA INSTALADA EX: com1, usb001, lpt1...<BR>
-[table_name]: cadastrar nesse campo o nome da tabela que consta os itens 'id' e 'impresso' <BR>
para que o sistema possa fazer a consulta.<BR>

 
###database#############################################################################

A RELAÇÃO ENTRE O SISTEMA DE CREDENCIAMENTO E SISTEMA DE IMPRESSÃO É FEITA ATRAVES DO 'IP LOCAL',
SUA APLICAÇÃO PRECISA ENCONTRAR O IP LOCAL DE ONDE O USUARIO VAI IMPRIMIR E SALVAR EM UMA COLUNA 'ip_user'
SENDO O IP NO BANCO DE DADOS UM 'VARCHAR(50)' NO FORMATO '19216801' SEM PONTOS E ESPAÇOS.

O PRINTSERVICE ESTA EM LOOP CONSULTANDO DUAS COLUNAS DE SEU BANCO DE DADOS ESSAS COLUNAS PRECISAM SE CHAMAR RESPECTIVAMENTE
'id' e 'impresso', esses campos devem estar dentro da tabela cadastrada no arquivo config.ini. 

###FORA DE OPERAÇÃO#######################################################################

****QUERY QUE BUSCA OS DADOS PARA A CREDENCIAL

<strike>SELECT <BR>
	<pre>id, nome, funcao, evento, impresso, obs, data_evt, qr_code </pre><BR>
FROM <BR>
	<pre>credencial</pre> <BR>
WHERE <BR>
	<pre>ip_user = IP_LOCAL</pre> <BR>
AND <BR>
	<pre>impresso < 2 AND impresso = 1</pre></strike><BR>
#####PROCEDURE############################################################################
AGORA PARA GERAR A CREDENCIAL É NECESSARIO QUE SEJA CRIADA UMA PROCEDURE: <BR>
	
<b>CREATE</b> DEFINER=```SEU_DEFINER`@`%` <b>PROCEDURE</b> `printservice`<BR>
(IN `IP_USER_LOCAL` VARCHAR(50), <BR>
OUT `NOME_CRED` VARCHAR(220), OUT `FUNC_CRED` VARCHAR(220), OUT `EVT_CRED` VARCHAR(220),<BR>
OUT `OBS_CRED` TEXT, OUT `DATA_EVT_CRED` DATETIME, OUT `QR_CODE_CRED``` VARCHAR(50))<BR>
	
<b>BEGIN</b><BR>
<pre><b>SELECT</b> nome, funcao, evento, obs, data_evt, qr_code<BR>    
<b>INTO</b> NOME_CRED, FUNC_CRED, EVT_CRED, OBS_CRED, DATA_EVT_CRED, QR_CODE_CRED<BR>
<b>FROM</b> NOME_CADASTRADO_NO_CONFIG.INI <BR>
<b>WHERE</b> ip_user = IP_USER_LOCAL AND impresso < 2 AND impresso = 1;<BR></pre>
<b>END</b><BR>

O VALOR QUE A PROCEDURE ESTA ESPERANDO É O IP LOCAL O UNICO VALOR DE ENTRADA QUE ELA TEM
O SISTEMA VAI ESPERAR POR 6 SAIDAS QUE DEVEM CONTER OS DADOS DA CREDENCIAL NA SEGUINTE ORDEM:<BR> 
NOME, FUNCAO, EVENTO, OBS, DATA EVENTO, QR CODE. <BR>
DESTA FORMA FICA MAIS FACIL PARA QUE O SERVIDOR JUNTE OS DADOS DA CREDENCIAL E OS ENVIE PARA O CLIENTE DE IMPRESSÃO.
	

##########################################################################################

<strike>****ARRAY COM DADOS NECESSARIO PARA SE GERAR UMA CREDENCIAL<BR>
0 = ID<BR>
1 = NOME CREDENCIADO<BR>
2 = FUNÇÃO CREDENCIADO <BR>
3 = EVENTO <BR>
4 = IMPRESSO (O=NÃO IMPRESSO, 1=IMPRESSAO SOLICITADA, 2=JÁ IMPRESSO)<BR>
5 = OBSERVAÇÃO<BR>
6 = DATA DO EVENTO<BR>
7 = VALOR DO QR CODE<BR></strike>
###########################################################################################

<strike>BETA VERSÃO 1.1.0</strike><BR>
BETA VERSÃO 1.2.0

ESSE MODELO SERVE PARA HOMOLOGAÇÃO EM IMPRESSÃO FINAL. 

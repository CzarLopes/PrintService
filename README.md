# PrintService

Sistema para impressão de arquivos direto de uma aplicação que use MySQL

##########################################################################################

ABRA COM UM BLOCO DE NOTAS O ARQUIVO config.ini PARA CADASTRAR SUAS CREDENCIAIS DO BANCO DE DADOS. 

##########################################################################################

A RELAÇÃO ENTRE O SISTEMA DE CREDENCIAMENTO E SISTEMA DE IMPRESSÃO É FEITA ATRAVES DO 'IP LOCAL',
SUA APLICAÇÃO PRECISA ENCONTRAR O IP LOCAL DE ONDE O USUARIO VAI IMPRIMIR E SALVAR EM UMA COLUNA 'ip_user'
SENDO O IP NO BANCO DE DADOS UM 'VARCHAR(50)' NO FORMATO '19216801' SEM PONTOS E ESPAÇOS.

##########################################################################################

****QUERY QUE BUSCA OS DADOS PARA A CREDENCIAL

SELECT <BR>
	<pre>id, nome, funcao, evento, impresso, obs, data_evt, qr_code </pre><BR>
FROM <BR>
	<pre>credencial</pre> <BR>
WHERE <BR>
	<pre>ip_user = IP_LOCAL</pre> <BR>
AND <BR>
	<pre>impresso < 2 AND impresso = 1</pre><BR>

##########################################################################################

****ARRAY COM DADOS NECESSARIO PARA SE GERAR UMA CREDENCIAL<BR>
0 = ID<BR>
1 = NOME CREDENCIADO<BR>
2 = FUNÇÃO CREDENCIADO <BR>
3 = EVENTO <BR>
4 = IMPRESSO (O=NÃO IMPRESSO, 1=IMPRESSAO SOLICITADA, 2=JÁ IMPRESSO)<BR>
5 = OBSERVAÇÃO<BR>
6 = DATA DO EVENTO<BR>
7 = VALOR DO QR CODE<BR>
###########################################################################################

BETA VERSÃO 1.1

ESSE MODELO SERVE PARA HOMOLOGAÇÃO. 

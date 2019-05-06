# PrintService
Sistema para impressão de arquivos direto de uma aplicação que use MySQL

##########################################################################################

ABRA COM UM BLOCO DE NOTAS O ARQUIVO config.ini PARA CADASTRAR SUAS CREDENCIAIS DO BANCO DE DADOS. 

##########################################################################################

A RELAÇÃO ENTRE O SISTEMA DE CREDENCIAMENTO E SISTEMA DE IMPRESSÃO É FEITA ATRAVEZ DO 'IP LOCAL',
SUA APLICAÇÃO PRECISA ENCONTRAR O IP LOCAL DE ONDE O USUARIO VAI IMPRIMIR E SALVAR EM UMA COLUNA 'ip_user'
SENDO O IP NO BANCO DE DADOS UM 'VARCHAR(50)' NO FORMATO '19216801' SEM PONTOS E ESPAÇOS.

##########################################################################################

****QUERY QUE BUSCA OS DADOS PARA A CREDENCIAL

SELECT 
	id, nome, funcao, evento, impresso, obs, data_evt, qr_code 
FROM 
	credencial 
WHERE 
	ip_user = IP_LOCAL 
AND 
	impresso < 2 AND impresso = 1

##########################################################################################

****ARRAY COM DADOS NECESSARIO PARA SE GERAR UMA CREDENCIAL
0 = ID
1 = NOME CREDENCIADO
2 = FUNÇÃO CREDENCIADO 
3 = EVENTO 
4 = IMPRESSO (O=NÃO IMPRESSO, 1=IMPRESSAO SOLICITADA, 2=JÁ IMPRESSO)
5 = OBSERVAÇÃO
6 = DATA DO EVENTO
7 = VALOR DO QR CODE
###########################################################################################

BETA VERSÃO 1.1

ESSE MODELO SERVE PARA HOMOLOGAÇÃO. 

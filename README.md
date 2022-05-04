**DESCRIÇÃO**:

**1-** SÃO GERADOS N NUMEROS ALEATORIOS, OS QUAIS SÃO ARMAZENADOS EM OLD_FILE.TXT

**2-** SÃO LIDOS M REGISTROS DE OLD_FILE, DE TAMANHO DA MEMORIA INTERNA (RAM[QTD]), ORDENADOS PELO METODO
   "MERGESORT" E COLOCADOS EM UM DOS BLOCOS AUXILIARES (FITA1 OU FITA2, INICIALMENTE, "INTERCALAC_1" E 2),
   ENQUANTO OLD CONTENHA ELEMENTOS A SEREM LIDOS.

**3-** ENTÃO, TEM-SE DOIS ARQUIVOS, FITA1 E FITA2, CONTENDO BLOCOS ORDENADOS DE MANEIRA INTERCALADA.

**4-** SÃO CRIADOS MAIS DOIS ARQUIVOS AUXILIARES (ARQAUX1 E ARQAUX2), QUE RECEBERÃO, DE MANEIRA INTERCALADA,
   COM "CORTE" INICIAL (FATIA) DE TAMANHO DA MEMORIA, A JUNÇÃO DOS BLOCOS DE FITA1 E 2.

**5-** ENQUANTO FITA1 E FITA2 NÃO CHEGAM AO FIM, ARQAUX1 E ARQAUX2 RECEBEM O MERGE DOS BLOCOS.

**6-** QUANDO NÃO RESTAM MAIS BLOCOS A SEREM INTERCALADOS DE FITA1 E 2, NA PROXIMA ITERAÇÃO FATIA
   DOBRA DE VALOR, POIS PROXIMO BLOCO TERÁ O DOBRO DE TAMANHO. FITA1 E 2 SÃO REMOVIDOS,
   JÁ QUE TODOS DADOS ESTÃO PRESENTES EM ARQAUX1 E 2.
 
**7-** DE MANEIRA A PRESERVAR A INTERCALAÇÃO INICIAL PARA FINS DE VISUALIZAÇÃO, OS ARQUIVOS INTERCALAC_1 E 2 SÃO MANTIDOS.
   A REPETIÇÃO DESSA FASE OCORRE "MERGES¹" VEZES, VARIAVEL QUE CONTEM A QUANTIDADE DE JUNÇÕES
   QUE DEVEM OCORRER.


**¹MERGES** = 	CONTARQ/TAM, CASO NÃO SOBREM RESTOS;
	  	CONTARQ/TAM + 1, CASO SOBREM.
          
          	**CONTARQ** = NUMERO TOTAL DE REGISTROS;
	  	**TAM** = TAMANHO DA MEMORIA INTERNA.

UM DOS CRITERIOS A SE AVALIAR SOBRE O CUSTO DA SOLUÇÃO ENVOLVIDA É O NUMERO DE PASSADAS. UMA PASSADA CARACTERIZA-SE
PELO NUMERO DE VEZES EM QUE UM ARQUIVO É LIDO POR COMPLETO.
A VARIÁVEL "fatia", POR ACOMPANHAR CADA PROCESSO DE "PASSADA" DO ARQUIVO, DOBRANDO A CADA ITERAÇÃO, APROXIMA-SE
DO VALOR ESTIPULADO PELA FORMULA. VAMOS APROVEITÁ-LA EM NOSSAS CONSTATAÇOES:
NO INICIO DE CADA PRIMEIRO LOOP WHILE, NA "FASE MERGE" DO PROCESSO, HÁ UM CONTADOR (contapass) QUE INCREMENTA-SE
ENQUANTO O VALOR DA FATIA É MENOR QUE A QUANTIDADE DE REGISTROS.

EX.:
	REGISTROS: 2 000
	MEMORIA  : 100
	FATIA    : 100
	
	1ª ITERAÇÃO: FATIA = 100
	2ª   "     :  "    = 200
	3ª   "     :  "    = 400
	4ª   "     :  "    = 800
	5ª   "     :  "    = 1 600  -> 5º VALOR ESCOLHIDO
	6ª   "     :  "    = 3 200
 
FORMULA MATEMÁTICA FORMAL PARA CALCULO DE PASSADAS: LOG(N/M)/LOG(K), ONDE:

**N** = *NUMERO DE REGISTROS DO ARQUIVO*;

**M** = *TAMANHO DA MEMORIA*;

**K** = *NUMERO DE ARQUIVOS AUXILIARES (AQUI COMO SENDO 2)*. 


**TESTES DE CASO:**

**NUMERO DE REGISTROS** ------------|--2 000-|-2 000-|-2 000-|-50 000-|--100 000
--------------------------------------------------------------------------------
**TAMANHO DA MEMORIA**  ------------|--100---|--500--|--800--|-3 000--|--18 000
--------------------------------------------------------------------------------
**ARQUIVOS AUXILIARES** ------------|---2----|---2---|---2---|---2----|--2-------   
--------------------------------------------------------------------------------
**PASSADAS (CALC. FORM.)** ---------|--5,3---|---2---|--1,3--|--4,05--|--2,47----  
--------------------------------------------------------------------------------
**PASSADAS (COM contapass)** -------|---5----|--3----|--2----|---5----|--3-------

NOTA-SE QUE, CONSIDERANDO A UTILIZAÇÃO DE 2 ARQUIVOS AUXILIARES,
QUANTO MAIOR A DIFERENÇA ENTRE MEMORIA E REGISTROS, MAIOR SERÁ
O NÚMERO DE PASSADAS.  

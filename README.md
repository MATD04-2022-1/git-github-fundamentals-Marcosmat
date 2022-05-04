## Descrição:

**1-** São gerados n numeros aleatorios, os quais são armazenados em old_file.txt

**2-** São lidos m registros de old_file, de tamanho da memoria interna (ram[qtd]), ordenados pelo metodo
   "mergesort" e colocados em um dos blocos auxiliares (fita1 ou fita2, inicialmente, "intercalac_1" e 2),
   enquanto old contenha elementos a serem lidos.

**3-** Então, tem-se dois arquivos, fita1 e fita2, contendo blocos ordenados de maneira intercalada.

**4-** São criados mais dois arquivos auxiliares (arqaux1 e arqaux2), que receberão, de maneira intercalada,
   com "corte" inicial (fatia) de tamanho da memoria, a junção dos blocos de fita1 e 2.

**5-** Enquanto fita1 e fita2 não chegam ao fim, arqaux1 e arqaux2 recebem o merge dos blocos.

**6-** Quando não restam mais blocos a serem intercalados de fita1 e 2, na proxima iteração fatia
   dobra de valor, pois proximo bloco terá o dobro de tamanho. Fita1 e 2 são removidos,
   já que todos dados estão presentes em arqaux1 e 2.
 
**7-** De maneira a preservar a intercalação inicial para fins de visualização, os arquivos intercalac_1 e 2 são mantidos.
   a repetição dessa fase ocorre "merges¹" vezes, variavel que contem a quantidade de junções
   que devem ocorrer.


**¹merges** = 	contarq/tam, caso não sobrem restos;
	  	contarq/tam + 1, caso sobrem;
          	contarq = numero total de registros;
	  	am = tamanho da memoria interna.

Um dos criterios a se avaliar sobre o custo da solução envolvida é o numero de passadas. Uma passada caracteriza-se
Pelo numero de vezes em que um arquivo é lido por completo.
A variável "fatia", por acompanhar cada processo de "passada" do arquivo, dobrando a cada iteração, aproxima-se
Do valor estipulado pela formula. Vamos aproveitá-la em nossas constataçoes:
No inicio de cada primeiro loop while, na "fase merge" do processo, há um contador (contapass) que incrementa-se
Enquanto o valor da fatia é menor que a quantidade de registros.

Ex.:
	registros: 2 000
	memoria  : 100
	fatia    : 100
	
	
1ª iteração: fatia = 100

2ª - - - - - - - - - = 200

3ª - - - - - - - - - = 400

4ª - - - - - - - - - = 800

5ª - - - - - - - - - = 1 600  -> 5º valor escolhido

6ª - - - - - - - - - = 3 200

 
Formula matemática formal para calculo de passadas:  l o g ( n / m ) / l o g ( k ), onde:

**n** = *numero de registros do arquivo*;

**m** = *tamanho da memoria*;

**k** = *numero de arquivos auxiliares (aqui como sendo 2)*. 




**testes de caso:**



Numero de registros: - - 2 000 - | - 2 000 - | - 2 000 - | - 50 000 - | - 100 000

--------------------------------------------------------------------------------

Tamanho da memoria: - - 100 - - |- - 500 - -| - - 800 - - | - 3 000 - - | - - 18 000

--------------------------------------------------------------------------------

Arquivos auxiliares: - - -2 - - | - - 2 - - - | - - - 2 - - - | - - 2 - - - | - - 2 - -    

--------------------------------------------------------------------------------
Passadas (calc. Form.): - - 5,3 - - | - - 2 - - - | - - 1,3 - - - | - - 4,05 - - - | - - 2,47 - - - -  

--------------------------------------------------------------------------------

Passadas (com contapass): - - - 5 - - - - | - - 3 - - - - | - - 2 - - - - | -  - - 5 - - - - | - - 3 - - -


Nota-se que, considerando a utilização de 2 arquivos auxiliares,
Quanto maior a diferença entre memoria e registros, maior será
O número de passadas.  

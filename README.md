# CienciadeDadosPUC
Trabalho de Conclusão de Curso apresentado ao Curso de Especialização em Ciência de Dados e Big Data como requisito parcial à obtenção do título de especialista.
PONTIFÍCIA UNIVERSIDADE CATÓLICA DE MINAS GERAIS
NÚCLEO DE EDUCAÇÃO A DISTÂNCIA
Pós-graduação Lato Sensu em Ciência de Dados e Big Data







Miriam Félix Lemes da Silva






ANÁLISE DO BANCO DE DADOS DE SÍNDROME RESPIRATÓRIA GRAVE 
 












Belo Horizonte
  2022 
 
Miriam Félix Lemes da Silva






ANÁLISE DO BANCO DE DADOS DE SÍNDROME RESPIRATÓRIA GRAVE 
 





Trabalho de Conclusão de Curso apresentado ao Curso de Especialização em Ciência de Dados e Big Data como requisito parcial à obtenção do título de especialista.













Belo Horizonte
  2022  
SUMÁRIO



1.	Introdução	6
1.1.	Contextualização	6
1.2.	O problema proposto	8
1.3.	Objetivos	8
2.	Coleta de Dados	8
3.	Processamento/Tratamento de Dados	11
4.	Análise e Exploração dos Dados	14
6.	Interpretação dos Resultados	23
6.1.	Medidas de desempenho	23
6.2.	Validação cruzada	24
7.	Apresentação dos Resultados	26
8.	Links	30
APÊNDICE	31













Índice de Tabelas

Tabela 1 - Dados coletados	10
Tabela 2 - Resultado do comando discribe	12
Tabela 3 - Classificação colunas	12
Tabela 4 - Valores nulos	13
Tabela 5 - Resultados execução modelo.	29
Tabela 6 - Comparação de resultados.	29






























Índice de Ilustrações

Figura 1 - Síndrome Respiratória Aguda Grave - SRAG. Fonte: https://www.prefeitura.sp.gov.br/cidade/secretarias/saude/vigilancia_em_saude/index.php?p=244834	7
Figura 2 - Tratamento coluna CLASSI_FIN	13
Figura 3 - Determinar o tamanho da amostra.	15
Figura 4 - Divisão da amostra.	15
Figura 5 - Definindo dados do gráfico.	16
Figura 6 - Gráfico Influenza.	16
Figura 7 - Gráfico outras doenças.	17
Figura 8 - Gráfico Covid.	18
Figura 9 - Gráfico internações.	19
Figura 10 - Contagem dos dados por grupo.	19
Figura 11 - Comparação conjunto de sintomas 1.	20
Figura 12 - Comparação conjunto de sintomas 2.	21
Figura 13 - Teorema de Bayes.	22
Figura 14 - Naïve Bayes	22
Figura 15 - Árvore de decisão.	23
Figura 166 - Validação k-fold Scikit-Learn. https://scikit-learn.org/stable/modules/cross_validation.html#cross-validation.	25
Figura 17 - Importação das bibliotecas.	26
Figura 18 - Cross validation Naïve Bayes.	26
Figura 19 - Cross validation árvore de decisão.	27
Figura 20 - Analise dos dados obtidos.	30
 
	Introdução

No atual contexto pandêmico, a análise de dados relacionados à saúde e síndromes respiratórias nunca foi tão relevante. Muito pouco se sabe sobre o novo vírus Covid-19 e muito tem se especulado sobre sintomas envolvendo síndromes respiratórias, como estes vírus têm se modificado e como isso afeta a vida humana. 
Desde o início do atual surto de coronavírus (SARS-CoV-2), causador da Covid-19, houve uma grande preocupação diante de uma doença que se espalhou rapidamente em várias regiões do mundo, com diferentes impactos. De acordo com a Organização Mundial da Saúde (OMS), em 18 de março de 2020, os casos confirmados da Covid-19 já haviam ultrapassado 214 mil em todo o mundo. Não existiam planos estratégicos prontos para serem aplicados a uma pandemia de coronavírus, tudo é novo. Recomendações da OMS, do Ministério da Saúde do Brasil, do Centers for Disease Control and Prevention (CDC, Estados Unidos) e outras organizações nacionais e internacionais têm sugerido a aplicação de planos de contingência de influenza e suas ferramentas, devido às semelhanças clínicas e epidemiológicas entre esses vírus respiratórios. Esses planos de contingência preveem ações diferentes de acordo com a gravidade das pandemias. (Ricardo Ribas Freitas, Napimoga, Donalisio, André, Marcelo, Maria Rita. Análise da gravidade da pandemia de Covid-19.)


	Contextualização

Em todo país tem se notado crescente aumento de casos de síndrome respiratória grave. 
  
Figura 1 - Síndrome Respiratória Aguda Grave - SRAG. Fonte: https://www.prefeitura.sp.gov.br/cidade/secretarias/saude/vigilancia_em_saude/index.php?p=244834
O insuficiente conhecimento científico sobre o novo coronavírus, sua alta velocidade de disseminação e capacidade de provocar mortes em populações vulneráveis, geram incertezas sobre quais seriam as melhores estratégias a serem utilizadas para o enfrentamento da epidemia em diferentes partes do mundo. No Brasil, os desafios são ainda maiores, pois pouco se sabe sobre as características de transmissão da COVID-19 num contexto de grande desigualdade social, com populações vivendo em condições precárias de habitação e saneamento, sem acesso sistemático à água e em situação de aglomeração. (Guilherme Loureiro Werneck, Marilia Sá Carvalho. A pandemia de COVID-19 no Brasil: crônica de uma crise sanitária anunciada.) 

Devido a pandemia de coronavírus, levanta-se a questão sobre as doenças respiratórias sua alta transmissibilidade e letalidade. 
Torna-se necessário o estudo e desenvolvimento de ferramentas capazes de auxiliar na detecção, classificação e análise de doenças respiratórias.

	O problema proposto

Analisando o contexto levanta-se a seguinte questão, é possível classificar as doenças respiratórias apenas analisando os sintomas apresentados pelos pacientes, de forma geral, e assim agilizar a triagem e tratamento desses pacientes?
A proposta deste projeto é desenvolver um algoritmo de classificação capaz de classificar diferentes doenças respiratórias de acordo com os sintomas apresentados. 
Os dados utilizados nessa classificação são do ano de 2021 e foram disponibilizados pelo Ministério da Saúde pelo site openData SUS. 
Foram analisados os sintomas de cada paciente afim de classificar de qual síndrome respiratória se trata, com o objetivo de auxiliar a detecção, diagnostico, triagem dessas doenças. 

	Objetivos

Classificar o conjunto de dados de Síndrome Respiratória Aguda Grave, por meio de um classificador supervisionado, com base nos sintomas apresentados por cada paciente.
Por meio desse estudo auxiliar na análise de dados sobre doenças respiratórias. 

	Coleta de Dados

Os dados foram obtidos no site openData SUS e distribuídos via Creative Commons Attribution License em formato .csv. 
O DataSUS disponibiliza informações que podem servir para subsidiar análises objetivas da situação sanitária, tomadas de decisão baseadas em evidências e elaboração de programas de ações de saúde. 
Os dados foram coletados por meio da Secretaria de Vigilância em Saúde (SVS), que desenvolveu a vigilância da Síndrome Respiratória Aguda Grave (SRAG) no Brasil, a qual a partir de 2020, incorporou a vigilância do Covid-19 a base de dados. 
O Ministério da Saúde (MS), por meio da Secretaria de Vigilância em Saúde (SVS), desenvolve a vigilância da Síndrome Respiratória Aguda Grave (SRAG) no Brasil, desde a pandemia de Influenza A(H1N1). A partir disso, a vigilância de SRAG foi implantada na rede de vigilância de Influenza e outros vírus respiratórios, que anteriormente atuava exclusivamente com a vigilância sentinela de Síndrome Gripal (SG). Em 2020, a vigilância da COVID-19, a infecção humana causada pelo novo coronavírus, que vem causando uma pandemia, foi incorporada na rede de vigilância da Influenza e outros vírus respiratórios.
Foi escolhida a base de dados do ano de 2021 para análise e podemos visualizar na Tabela 1 a relação do dicionário de dados utilizado, também pode-se visualizar o dicionário completo	 no	 endereço	 <https://s3.sa-east-1.amazonaws.com/ckan.saude.gov.br/SRAG/pdfs/dicionario_de_dados_srag_hosp_17_02_2022.pdf.>
A base de dados extraída do site openData SUS, possui 1199291 registros com 152 colunas sendo elas: DT_NOTIFIC, SEM_NOT, DT_SIN_PRI, SEM_PRI, SG_UF_NOT, ID_REGIONA, CO_REGIONA, ID_MUNICIP, CO_MUN_NOT, ID_UNIDADE, CO_UNI_NOT, CS_SEXO, DT_NASC, NU_IDADE_N, TP_IDADE, COD_IDADE, CS_GESTANT, CS_RACA, CS_ETINIA, CS_ESCOL_N, ID_PAIS, CO_PAIS, SG_UF, ID_RG_RESI, CO_RG_RESI, ID_MN_RESI, CO_MUN_RES, CS_ZONA, SURTO_SG, NOSOCOMIAL, AVE_SUINO, FEBRE, TOSSE, GARGANTA, DISPNEIA, DESC_RESP, SATURACAO, DIARREIA, VOMITO, OUTRO_SIN, OUTRO_DES, PUERPERA, FATOR_RISC, CARDIOPATI, HEMATOLOGI, SIND_DOWN, HEPATICA, ASMA, DIABETES, NEUROLOGIC, PNEUMOPATI, IMUNODEPRE, RENAL, OBESIDADE, OBES_IMC, OUT_MORBI, MORB_DESC, VACINA, DT_UT_DOSE, MAE_VAC, DT_VAC_MAE, M_AMAMENTA, DT_DOSEUNI, DT_1_DOSE, DT_2_DOSE, ANTIVIRAL, TP_ANTIVIR, OUT_ANTIV, DT_ANTIVIR, HOSPITAL, DT_INTERNA, SG_UF_INTE, ID_RG_INTE, CO_RG_INTE, ID_MN_INTE, CO_MU_INTE, UTI, DT_ENTUTI, DT_SAIDUTI, SUPORT_VEN, RAIOX_RES, RAIOX_OUT, DT_RAIOX, AMOSTRA, DT_COLETA, TP_AMOSTRA, OUT_AMOST, PCR_RESUL, DT_PCR, POS_PCRFLU, TP_FLU_PCR, PCR_FLUASU, FLUASU_OUT, PCR_FLUBLI, FLUBLI_OUT, POS_PCROUT, PCR_VSR, PCR_PARA1, PCR_PARA2, PCR_PARA3, PCR_PARA4, PCR_ADENO, PCR_METAP, PCR_BOCA, PCR_RINO, PCR_OUTRO, DS_PCR_OUT, CLASSI_FIN, CLASSI_OUT, CRITERIO, EVOLUCAO, DT_EVOLUCA, DT_ENCERRA, DT_DIGITA, HISTO_VGM, PAIS_VGM, CO_PS_VGM, LO_PS_VGM, DT_VGM, DT_RT_VGM, PCR_SARS2, PAC_COCBO, PAC_DSCBO, OUT_ANIM, DOR_ABD, FADIGA, PERD_OLFT, PERD_PALA, TOMO_RES, TOMO_OUT, DT_TOMO, TP_TES_AN, DT_RES_AN, RES_AN, POS_AN_FLU, TP_FLU_AN, POS_AN_OUT, AN_SARS2, AN_VSR, AN_PARA1, AN_PARA2, AN_PARA3, AN_ADENO, AN_OUTRO, DS_AN_OUT, TP_AM_SOR, SOR_OUT, DT_CO_SOR, TP_SOR, OUT_SOR, DT_RES, RES_IGG, RES_IGM, RES_IGA.
Nome da coluna/ campo	Descrição	Tipo
FEBRE	Paciente apresentou febre?	Varchar2(1) 
TOSSE	Paciente apresentou tosse?	Varchar2(1) 
GARGANTA	Paciente apresentou dor de garganta?	Varchar2(1) 
DISPNEIA		Paciente apresentou dispneia?	Varchar2(1)
DESC_RESP	Paciente apresentou desconforto respiratório?	Varchar2(1)
SATURACAO	Paciente apresentou saturação O2 < 95%?	Varchar2(1)
DIARREIA	Paciente apresentou diarreia?	Varchar2(1)
VOMITO	Paciente apresentou vômito?	Varchar2(1)
DOR_ABD	Paciente apresentou dor abdominal?	Varchar2(1)
FADIGA	Paciente apresentou fadiga?	Varchar2(1)
PERD_OLFT	Paciente apresentou perda de olfato?	Varchar2(1)
PERD_PALA	Paciente apresentou perda de paladar?	Varchar2(1)
RAIOX_RES	Raio X do tórax.	Varchar2(1)
HOSPITAL	Paciente foi internado?	Varchar2(1)
HISTO_VGM	Paciente tem histórico de viagem internacional até 14 dias antes do início dos sintomas?	Varchar2(1)
TOMO_RES	Tomografia	Number(3)
CLASSI_FIN
	Diagnóstico final	Varchar2(1)
Tabela 1 - Dados coletados

 
	Processamento/Tratamento de Dados

Para importação dos dados e desenvolvimento do algoritmo foi utilizada a linguagem Python, e a IDE utilizada para desenvolvimento foi o google Colab. 
Para a importação dos dados foi utilizada a biblioteca Pandas, que é uma biblioteca de código aberto do Python. Primeiramente foi realizado um filtro das colunas que eram interessantes para a nossa análise, e para definir quais colunas utilizar foi levado em consideração a questão; com base nos sintomas podemos classificar qual síndrome respiratória? As colunas elencadas foram; FEBRE, TOSSE, GARGANTA, DISPNEIA, DESC_RESP, SATURACAO, DIARREIA, VOMITO, DOR_ABD, FADIGA, PERD_OLFT, PERD_PALA, RAIOX_RES, HOSPITAL, HISTO_VGM, TOMO_RES, CLASSI_FIN. Sendo a coluna CLASSI_FIN considerada o rótulo, ou seja, o objeto final da classificação e as demais a features. 
Com as features e o rótulo definidos, importei somente os dados relacionados a essas colunas. Foram importados os dados diretamente de um arquivo .CSV salvo no Google Drive, os dados foram atribuídos a variável df que passa a ser o DataFrame com os dados que foram trabalhados, na sequência analisei os dados importados, por meio do comando info. 
Em seguida foi realizada a ordenação das colunas e executado comando do pandas drop_duplicates para remover possíveis dados duplicados, e executado o comando discribe para apresentar os dados, como podemos visualizar na Tabela 2, assim podendo visualizar se existe algum valor fora do padrão e qual padrão deveria ser o tratamento adotado para nulos. 
Index	count	Mean	Std	min	25,00%	50,00%	75,00%	max
FEBRE	1041291.0	1.4676579361580961	1.1041203141260905	1.0	1.0	1.0	2.0	9.0
TOSSE	1066111.0	1.351380859966739	1.0200547240806432	1.0	1.0	1.0	1.0	9.0
GARGANTA	902813.0	2.0229039679313434	1.3905056526115618	1.0	2.0	2.0	2.0	9.0
DISPNEIA	1065159.0	1.3298681229750675	0.9724918139941165	1.0	1.0	1.0	1.0	9.0
DESC_RESP	1002637.0	1.4555756470188115	1.1050058220929335	1.0	1.0	1.0	2.0	9.0
SATURACAO	1009137.0	1.5070074727217415	1.2203137625262335	1.0	1.0	1.0	2.0	9.0
DIARREIA	889994.0	2.0688049582356736	1.3430785057312502	1.0	2.0	2.0	2.0	9.0
VOMITO	878670.0	2.1266926149749055	1.3534962217165845	1.0	2.0	2.0	2.0	9.0
DOR_ABD	532905.0	2.237759075257316	1.4960078606352947	1.0	2.0	2.0	2.0	9.0
FADIGA	548253.0	2.0511771025420744	1.5295796916400086	1.0	2.0	2.0	2.0	9.0
PERD_OLFT	538743.0	2.262013613169916	1.6213824775871895	1.0	2.0	2.0	2.0	9.0
PERD_PALA	537564.0	2.265047510621991	1.6303474160352611	1.0	2.0	2.0	2.0	9.0
RAIOX_RES	792055.0	4.956110371123217	2.4315970302172274	1.0	2.0	6.0	6.0	9.0
HOSPITAL	1169632.0	1.0640440754014937	0.5212106462124021	1.0	1.0	1.0	1.0	9.0
HISTO_VGM	1199291.0	2.220708735411172	2.5330043362138523	0.0	0.0	2.0	2.0	9.0
TOMO_RES	445961.0	3.6821493359284783	2.849455444039647	1.0	1.0	2.0	6.0	9.0
CLASSI_FIN	1146326.0	4.599984646601403	0.5441258067548859	1.0	4.0	5.0	5.0	5.0
Tabela 2 - Resultado do comando discribe
De acordo com o dicionário de dados, contido no OpenData SUS as colunas são classificadas com as condições listadas na tabela 3.
FEBRE, TOSSE, GARGANTA, DISPNEIA, DESC_RESP, SATURACAO, DIARREIA, VOMITO, DOR_ABD, FADIGA, PERD_OLFT, PERD_PALA, HOSPITAL, HISTO_VGM	1-Sim
2-Não
9-Ignorado
RAIOX_RES	 1-Normal 2-Infiltrado intersticial 3-Consolidação 4-Misto 5-Outro 6-Não realizado 9-Ignorado
TOMO_RES	1-Tipico COVID-19 2- Indeterminado COVID-19 3- Atípico COVID-19 4- Negativo para Pneumonia 5- Outro 6-Não realizado 9-Ignorado
CLASSI_FIN	1-SRAG por influenza 2-SRAG por outro vírus respiratório 3-SRAG por outro agente etiológico, qual: 4-SRAG não especificado 5-SRAG por COVID-19
Tabela 3 - Classificação colunas
Com base nos dados obtidos na tabela 2 e da classificação da tabela 3, verificou-se que não existia nenhum valor fora dos valores definidos na classificação de cada coluna. 
A coluna CLASS_FIN apresenta as opções, 2-SRAG por outro vírus respiratório, 3-SRAG por outro agente etiológico, 4-SRAG não especificado, as três colunas apontam para a lógica de um resultado não especificado, afim de aumentar a precisão do modelo foi realizado a união dessas três colunas definindo com o valor 2, como podemos ver na figura 1.
 
Figura 2 - Tratamento coluna CLASSI_FIN
Então com o comando df.isnull().sum() retornou a soma de todos os valores nulos de cada coluna, podemos verificar os valores obtidos na Tabela 4.
FEBRE	158000
TOSSE	133180
GARGANTA	296478
DISPNEIA	134132
DESC_RESP	196654
SATURACAO	190154
DIARREIA	309297
VOMITO	320621
DOR_ABD	666386
FADIGA	651038
PERD_OLFT	660548
PERD_PALA	661727
RAIOX_RES	407236
HOSPITAL	29659
HISTO_VGM	0
TOMO_RES	753330
CLASSI_FIN	52965
Tabela 4 - Valores nulos
 Levando em consideração esses dados ao tratar os dados nulos foi atribuído o valor 9 ignorado para as features e 2 na coluna de rótulo no lugar dos valores nulos, utilizando a função fillna.

	Análise e Exploração dos Dados

Para iniciar a análise dos dados vamos primeiramente determinar uma amostra, pois são muitos dados e seria difícil visualizar um gráfico com mais de um milhão de resultados. Para determinar o tamanho da amostra será utilizada uma formula considerando a população finita:
n=(N.p ̂(1-p ̂ ).(z)^2)/(p ̂(1-p ̂ )⋅(z)^2+(N-1)⋅ⅇ^2 )
Onde:
n = O tamanho da amostra que queremos calcular
N = Tamanho da população
Z = É o desvio do valor médio que aceitamos para alcançar o nível de confiança desejado. Em função do nível de confiança que buscamos, usaremos um valor determinado que é dado pela forma da distribuição de Gauss: Nível de confiança 95% -> Z=1,96
e = É a margem de erro máximo que eu quero admitir.
p = É a proporção que esperamos encontrar.
Para realizar o calculo foi desenvolvida a função em Pyhton tamanhoAmostra, onde foram passados os parâmetros N tamanho da minha população, Z como definido 1.96, e padrão 0.05(5%) e p a proporção de 0.5. 
 
Figura 3 - Determinar o tamanho da amostra.
O resultado obtido foi o número 384.0373043960536, considerando a regra de sempre aumentar o valor de n para o próximo inteiro maior que se baseia no princípio de que, quando o arredondamento se faz necessário, o tamanho da amostra deve ser arredondado para cima, a fim de ser ao menos adequadamente grande, em oposição à ligeiramente menor. Foi aplicada a função math.ceil. Que retornou o tamanho da amostra 385 para manter-me dentro dos níveis de erro definidos.
Para extrair a amostra foi utilizada a função sample, e em seguida a função groupby para dividir a amostra em três classes; COVID, INFLUENZA e OUTRO. 
 
Figura 4 - Divisão da amostra.
Primeiramente foi realizada a análise das três amostras com base dos sintomas apresentados e para isso foi utilizada a biblioteca matplotlib. Foram importadas para o dataframe filtered_df todas as linhas que apresentavam uma opção igual a 1, o que significa que apresenta aquele sintoma. 
 
Figura 5 - Definindo dados do gráfico.
O primeiro grupo da amostra a ser analisada foi a INFLUENZA. 
 
Figura 6 - Gráfico Influenza.
O segundo grupo a ser analisado foi OUTRO. 
 
Figura 7 - Gráfico outras doenças.
E o terceiro e último grupo foi COVID. 
 
Figura 8 - Gráfico Covid.
Nesse primeiro ponto de vista podemos visualizar nos gráficos a forma como o grupo COVID se destaca dos demais quando se trata dos sintomas, FADIGA, PERD_OUFT, PERD_PALA e SATURACAO. 
Também foi analisada a coluna HOSPITAL que se refere a internações decorrentes da doença. 
Para isso foi realizado o filtro apenas dessa coluna do dataframe e foi utilizado a mesma biblioteca da analise anterior. 
 
Figura 9 - Gráfico internações.
Nessa analise podemos visualizar claramente como o grupo COVID se destaca em relação a outras doenças no cenário de internação. 
Pode ser observado também pelo comando len em cada um dos dataframes agrupados, que os casos de diagnostico de influenza nesse período foi muito menor que outros casos de doenças respiratórias e covid-19.
 
Figura 10 - Contagem dos dados por grupo.
Observando os dados anteriores podemos perceber a similaridade em alguns sintomas entre os três casos e a raridade de alguns dos sintomas entre os três casos, com base nessa observação foram divididos os dados em dois conjuntos, também para facilitar a visualização do gráfico. 
Então nesse primeiro conjunto temos as colunas 'FEBRE','TOSSE','GARGANTA','DISPNEIA','DESC_RESP','SATURACAO'.
 
Figura 11 - Comparação conjunto de sintomas 1.
Nesse segundo conjunto temos as colunas ‘DIARREIA','VOMITO','DOR_ABD','FADIGA','PERD_OLFT','PERD_PALA'.
 
Figura 12 - Comparação conjunto de sintomas 2.
Observando os gráficos podemos constatar que não conseguimos traçar uma reta para dividir os dados, também que em relação aos outros dados a base covid se destaca em todos os casos. 

	Criação de Modelos de Machine Learning

Para a criação do modelo foi utilizado o dataframe original df, já tratado anteriormente, para realizar esse processo foi utilizado a biblioteca scikit-learn do Python.

	Naïve Bayes

Naïve Bayes é um algoritmo de aprendizado supervisionado baseados na aplicação do teorema de Bayes. O teorema de Bayes Gausiano implementa a seguinte função:
 
Figura 13 - Teorema de Bayes.
Onde os parâmetros σ, y e μy são estimados usando a máxima verossimilhança.
Para implementar o algoritmo de classificação Naïve Bayes primeiramente foi importada a biblioteca do sklearn GaussianNB.
Em seguida instanciado o modelo, aplicado ao conjunto de treinamento e realizado a predição no conjunto de teste. 
 
Figura 14 - Naïve Bayes

	Árvore de decisão

Árvore de decisão é um método de aprendizado supervisionado usado para classificação e regressão, prevendo o valor de uma variável de destino aprendendo regras de decisão simples, inferidas a partir dos recursos de dados. 
Para implementar o algoritmo de classificação primeiramente foi importada a biblioteca do skeatlearn.
Em seguida instanciado o modelo, aplicado ao conjunto de treinamento e realizado a predição no conjunto de teste. 
 
Figura 15 - Árvore de decisão.
 
	Interpretação dos Resultados

Um dos principais desafios em se trabalhar com Machine Learning é escolher o algoritmo de aprendizado, e garantir o que não exista subajuste (Underfitting) ou sobreajuste (Overfitting). 
Para definir se o algoritmo é bom devemos primeiramente definir o que é considerado bom de acordo com nosso problema. 

	Medidas de desempenho

Para validar meu modelo foram utilizadas medidas de desempenho, uma das medidas de desempenho utilizadas é a acurácia, a acurácia representa a fração de previsões corretas realizadas pelo conjunto de teste. 
Acurácia=(Número de previsões corretas)/(Número total de previsões)
Mas a acurácia não pode ser a única medida de desempenho levada em consideração outra medida de desempenho utilizada é a revocação se justifica pois não seria interessante para o algoritmo um número alto de falsos negativos, o que significaria por exemplo classificar um caso de COVID como influenza e uma pessoa ser privada do tratamento especifico, seria melhor que fosse um falso positivo e se descobrisse que não se trata da doença mais grave. A formula considerada para revocação no numerador possui os verdadeiros positivos (VP) e no denominador todos os reais positivos, ou seja, VP mais falsos negativos (FN).
Revocação=VP/(VP+FN)
 Outra medida é a precisão, onde no numerador teremos os verdadeiros positivos e no denominador todos os positivos previstos, ou seja, a soma entre verdadeiros positivos (VP) e falsos positivos (FP). 
Precisão=VP/(VP+FP)
Para identificar uma média harmônica entre essas duas medidas, precisão e revocação, vamos utilizar a formula da pontuação F1. 
Pontuação F1=2/(1/Precisão+1/Revocação)

	Validação cruzada

Na técnica houldout são dividos os dados de teste e treinamento de forma estática, a desvantagem dessa técnica é que podem existir dados no meu conjunto de testes que não existem no meu conjunto de treinamento.
No crossvalidation, apesar de ser mais caro para o algoritmo, garante que todos os dados serão utilizados no treinamento e teste. A validação cruzada começa com a divisão de um conjunto de dados rotulado em k partes, subconjuntos mutuamente exclusivos chamados dobras. Por meio da realização de várias divisões e trocando sistematicamente amostra para testes. Em seguida, cada parte é usada em sua vez, como conjunto de teste, com as outras quatro usadas para treinar em modelo. Isso dá cinco diferentes resultados de precisão, que, então, podem ser utilizados para calcular a precisão média e sua variância.
 
Figura 166 - Validação k-fold Scikit-Learn. https://scikit-learn.org/stable/modules/cross_validation.html#cross-validation.

Para aplicação dos modelos foi utilizada a função cross_validate que permite definir várias métricas por validação cruzada e também registre os tempos de ajuste (fit( ))/ pontuação (score( )). 
Previamente foi importada as tabelas que foram usadas em todos os modelos, também definidos os valores de X e y e definido o valor de cv que é o numero de partições que será executada a validação cruzada e definidas as métricas.
É importante entender que o modelo não pega simplesmente as primeiras linhas e atribui para treinamento e o restante pra teste, por que poderia acontecer das classes estarem ordenadas, e isso seria ruim para meu modelo por que por exemplo poderia ocorrer de o conjunto de treinamento possuir certas classes e o conjunto de teste outras e então meu modelo seria falho por que não iria saber que existiria as classes que ficassem separadas no modelo de teste, então é importante que exista aleatoriedade na criação do modelo, e o parâmetro random_state é uma semente passada justamente para tratar essa aleatoriedade e garante a reprodução dos experimentos.
 
Figura 17 - Importação das bibliotecas.
Em seguida foi executado para os três modelos. 
 
Figura 18 - Cross validation Naïve Bayes.

 
Figura 19 - Cross validation árvore de decisão.
Para os dois modelos foi instanciado o modelo, aplicada a função cross_validate e gerada a impressão das métricas atribuídas. 

	Apresentação dos Resultados

Os dois modelos retornaram valores de acurácia, revocação, f1_score de acordo com o modelo aplicado e os parâmetros passados para o cross validation, foram retornados 5 valores para cada métrica e então calculada a média e desvio padrão de cada uma. 
Modelo	Resultados
Árvore de decisão	- fit_time:
-- [5.2497375  5.26732612 5.31273985 5.2073555  5.21596217]
-- 5.2506242275238035 +- 0.03797823269364871

- score_time:
-- [0.42542243 0.4237082  0.43075681 0.42199564 0.42924309]
-- 0.4262252330780029 +- 0.003301878778683042

- test_accuracy:
-- [0.62698919 0.62753379 0.62764636 0.62732533 0.627317  ]
-- 0.627362333556363 +- 0.00022482353744093697

- test_precision_macro:
-- [0.44484071 0.42000006 0.41865283 0.45453307 0.41528725]
-- 0.4306627837547943 +- 0.015906877897007222

- test_recall_macro:
-- [0.40660555 0.40445004 0.40389156 0.40806464 0.40270105]
-- 0.40514256926470865 +- 0.0019331029623075589

- test_f1_macro:
-- [0.41106244 0.40641037 0.40549025 0.41327877 0.40379711]
-- 0.4080077902286571 +- 0.0035702566506225965
Naïve Bayes	- fit_time:
-- [0.50765896 0.43336368 0.43429232 0.43209147 0.42228866]
-- 0.4459390163421631 +- 0.031158401759182247

- score_time:
-- [0.41129041 0.39233088 0.40192151 0.38276577 0.38554001]
-- 0.39476971626281737 +- 0.010576497735216933

- test_accuracy:
-- [0.47280694 0.47412636 0.46914841 0.47823712 0.4802258 ]
-- 0.4749089271094224 +- 0.003938535722013798

- test_precision_macro:
-- [0.37292486 0.37067028 0.37188628 0.37510721 0.37463721]
-- 0.3730451681243141 +- 0.0016603752743642407

- test_recall_macro:
-- [0.47758861 0.4730657  0.45987835 0.48918349 0.47667439]
-- 0.4752781083493366 +- 0.009409515389239518

- test_f1_macro:
-- [0.32210552 0.31963191 0.31816961 0.32511373 0.32403509]
-- 0.3218111713761949 +- 0.0026057442176094544
Tabela 5 - Resultados execução modelo.
Como podemos observar em tempo de execução o modelo o modelo Naïve Bayes teve o melhor desempenho. 
Analisando de forma mais detalhada na próxima tabela podemos ver as médias de cada um dos modelos nas métricas estabelecidas. 
Como podemos observar o modelo árvore de decisão obteve um melhor desempenho em relação a acurácia e a precisão e pouca variação em relação ao Naïve Bayes na métrica revoção, o que permitiu seu score-F1 mais alto. 
	Acurácia	Precisão 	Revocação	Score-F1
Naïve Bayes	0.4749089271094224	0.3730451681243141	0.4752781083493366	0.3218111713761949
Árvore de decisão	0.627362333556363	0.4306627837547943	0.40514256926470865	0.4080077902286571
Tabela 6 - Comparação de resultados.
Podemos observar também no gráfico que o modelo árvore de decisão se destaca.
 
Figura 20 - Analise dos dados obtidos.
Conclui-se então que a melhor performance do modelo árvore de decisão, pois possui uma melhor acurácia e precisão, entre os dois modelos perde muito pouco na métrica revocação em comparação ao Naïve Bayes, sendo a revocação no caso uma métrica importante, pois prefere-se gerar um falso positivo e o paciente ser tratado pela doença e se descobrir que não está doente, do que um falso positivo e ser negado atendimento, mas isso se balanceia com as outras métricas, o que gera uma média maior no score-F1 para a árvore de decisão.  
Apesar da melhor performance nenhum modelo conseguiu classificar com uma acurácia maior que 60%, isso se deve pela similaridade dos sintomas entre as doenças.
Ainda assim, deve se destacar que o diagnostico final deve ser feito por um profissional responsável e um algoritmo de classificação deve apenas ser um auxilio ao encaminhamento e previsão de possíveis similaridades com a doença final. 


# TCC
Repositório para desenvolvimento do Trabalho de Conclusão de Curso da Pós Graduação em Business Intelligence da Puc-Rio

## Objetivo:
O presente projeto tem como objetivo superar a relação risco/retorno do índice Bovespa através da variação da alocação de uma carteira contendo quase todos os ativos que formam esse índice.
Para esse objetivo serão usadas ferramentas de machine learning no intuito estimar o desempenho futuro do índice Bovespa, determinando assim uma postura mais agressiva na alocação caso a estimativa seja de alta no índice, e uma postura mais conservadora caso a estimativa seja na direção contrária.
Através de um script desenvolvido na linguagem python encontraremos o Beta de cada ativo para que possa ser calculado o Beta total da carteira que será o parâmetro a ser utilizado como referência de exposição ao risco em relação ao risco sistêmico inerente aos ativos e suas alocações no índice Bovespa.
Utilizando esses dados juntamente com a informação do desempenho individual de cada ativo que compõe a carteira em períodos anteriores, serão utilizados algoritmos genéticos que resultarão na melhor alocação possível desses ativos para que tenhamos um retorno maior que o índice Bovespa, sem que o Beta da carteira supere o índice de risco previamente definido.

## Proposta de Trabalho de Conclusão de Curso:
Pretende-se atingir o objetivo acima definido, dividindo o projeto em 4 etapas, as quais estão resumidas a seguir:

### ETAPA I – Previsão do Desempenho do Índice Bovespa:
O objetivo dessa etapa é, utilizando técnicas de aprendizado de máquina, prever a direção do movimento do Ibovespa no período seguinte.
O produto dessa etapa servirá de insumo para o algoritmo genético da seguinte maneira: previsões de alta do ibovespa permitirão que o algoritmo genético proponha alocações onde o Beta da carteira seja mais elevado, o que, em tese, acompanharia o movimento previsto de forma mais acelerada, porém com maiores riscos. Já em previsões de baixa do ibovespa o algoritmo genético ficará limitado a valores mais baixos de beta levando a uma tendência de resultados inferiores, mas com riscos limitados.
Serão testadas diversas ferramentas de redes neurais como KNN, Random Forrest e LSTM, em diversas configurações com o intuito de chegar a previsões mais efetivas.
A dificuldade dessa etapa está em conseguir que as redes neurais encontrem padrões nos dados dos preços das ações devido ao caráter errático do mercado. Para superá-las, a intenção é aliar técnicas diferentes de redes neurais com tratamento de dados, a fim de facilitar a busca por esses padrões.

### Etapa II – Cálculo do Beta de cada Ativo da carteira
O objetivo dessa etapa é encontrar o valor do Beta de cada ativo que comporá a carteira. 
Pretende-se desenvolver um script na linguagem Python que automatize esse cálculo.
A informação do Beta individual servirá de insumo para o algoritmo genético que em seus cálculos chegará ao beta total da carteira em cada indivíduo da população gerada, filtrando apenas os que possuem Beta em uma certa faixa de valores, que dependerá do movimento previsto do iBovespa na Etapa I.

### Etapa III – Cálculo do desempenho passado de cada ativo da carteira
Nessa etapa, da base de dados da B3, serão calculados os resultados passados de cada um dos ativos que comporão a carteira.
Baseado na teoria que diz que o movimento de um ativo segue uma tendencia, ou seja, ativos que em períodos recentes estão em movimento de alta, tendem a seguir em alta, e o inverso para casos de baixas, o algoritmo genético aumentará a alocação de ativos com melhores retornos no período anterior sempre controlando o impacto que esse ativo traz à carteira em termos de Beta, ou seja, como o ativo impacta no nível de risco da carteira. 

### Etapa IV – Desenvolvimento do algoritmo genético que definirá a alocação ótima da carteira
Etapa final do projeto que receberá como insumos os resultados das etapas anteriores sendo aplicados algoritmos genéticos no intuito de se chegar a uma alocação que aposta em ativos que vêm apresentando bom desempenho em períodos anteriores balanceando-os com ativos com Beta baixo na intenção de chegar a uma carteira que promete bom desempenho, sem que o risco supere um limite previamente definido.

## Cronograma

•	Novembro e dezembro: 

o	Estudo da teoria

•	Janeiro

o	Prospecção de técnicas e ferramentas mais adequadas

o	Pesquisa de algoritmos e scripts correlatos 

•	Fevereiro

o	Início do Desenvolvimento dos algoritmos e ferramentas a serem aplicados no projeto

•	Março

o	Finalização dos algoritmos necessários a cada etapa do projeto

o	Backtests de comparação com o Índice Bovespa

o	Correção de falhas 

o	Realização de testes massivos para melhoria de desempenho

•	Abril 

o	Finalização do material

o	Apresentação

## Desenvolvimento
Como se trata de modificações na alocação de ativos de uma carteira bem grande, entendi que o periodo de avaliação e realocação da carteira deveria ser semanal, pois períodos mais curtos exigiriam muito trabalho para atualização das quantidades dos ativos além de altos custos de corretagem e taxas. Períodos mais longos, por sua vez, reduziriam a disponibilidade de dados históricos, tornando muito difícil o treinamento dos algoritmos de machine learning.


### Etapa de Previsão
Foram estudadas diversas técnicas de machine Learning, dentre elas LSTM, MPLS e KNN, sendo a Random Forest a que 	obteve os melhores resutados, trazendo uma precisão de quase 80% nos testes realizados. Esse algoritmo tem como produto a 	previsão de alta (1) ou baixa (-1) da semana T+1 com base nos indicadores calculados com os dados da semana T. O Algoritmo genético utiliza essa previsão da seguinte maneira: Se a previsão do ibovespa é de alta, o Beta da carteira rebalanceada pode variar até 	1.1, mas se a previsão for de baixa, o limite para o beta da carteira é de 0.9. A intenção é que quando prevemos um alta, podemos	aumentar nosso nivel de risco trazendo melhores resultados para a carteira, assim como reduzir o nivel de risco quando a previsão for	de baixa. 
Para chegar a um resultado com boa acurácia, além de testar várias técnicas de machine learning, foi necesário calcular vários indicadores técnicos comumente utilizados para análise de ácões, pois esses indicadores seriam os insumos dados aos algoritmos no intuito de mapear padrões que resultariam em previsões mais precisas.
Para essa função notou-se que os indicadores de momento foram os mais eficazes, e ao final os seguintes indicadores foram utilizados:
-Oscilador Estocástico
-Relative Strength Index
-MACD
-Price Rate of Change
-On Balance Volume
Os indicadores Momentrum são ferramentas de análise técnica usadas para determinar a força ou a fraqueza do preço de uma ação. O momentum mede a taxa de aumento ou queda dos preços das ações. 
O algoritmo resultante dessa etapa foi o "V2 - Previsão_Random_Forrest_aprimorada_Melhor_Resultado.ipynb" constante do branch "Predict".

### Cálculo do Beta
A volatilidade que uma carteira de referência (para o nosso caso o iBovespa) ou uma carteira de mercado exibe é conhecida como risco sistemático. Beta é a medida histórica de risco de qualquer ação ou carteira individual em relação ao risco da carteira de mercado. Em outras palavras, ele mede a volatilidade de qualquer título em relação à volatilidade geral do mercado.
Esse índice é bastante utilizado para gestores de carteira em todo mundo e, por isso, já havia diversas opções de algoritmos disponíveis para serem utilizados. Após testarmos alguns desses algoritmos, optamos por usar o disponível no seguinte site: https://blog.quantinsti.com/asset-beta-market-beta-python/. O método utilizado é o do cálculo da regressão linear e apresentou excelentes resultados para a nossa necessidade.
Para o cálculo do beta define-se um período de comparação com a carteira de referência, para o presente estudo utilizamos o período padrão de 5 anos.
O algoritmo resultante dessa etapa foi o "Calculo de Beta com exportação - BVSP Completo.ipynb" constante do branch "Beta".

### Cálculo do desempenho passado de cada ativo da carteira
Nessa etapa, utilizamos um API do portal Yahoo Finance que nos possibilita obter dados passados de todos os ativos listados no iBovespa. A importação desses dados forneceu informações históricas de cada ativo como preço de fechamento, preço máximo e volume. 
De posse dessas informações gfoi gerado um banco de dados contendo a performance semana a semana de cada um dos ativos em diversas datas diferentes.
Essa banco foi exportado para um arquivo excel que foi, em seguida, utilizado pelo algoritmo genético explicado na próxima etapa.
O algoritmo resultante dessa etapa foi o "V2-calculo_dos_retornos_semanais.ipynb" constante do branch "Performance".

### Algoritmo Genético para definição das alocações
Etapa final do projeto que rcebeu como insumos os resultados das etapas anteriores sendo aplicados algoritmos genéticos no intuito de se chegar a uma alocação que aposta em ativos que vêm apresentando bom desempenho em períodos anteriores balanceando-os na intenção de se manter o Beta dentro de uma faixa definida na intenção de chegar a uma carteira que promete bom desempenho, sem que o risco supere um limite previamente definido.
Apesar de ter rodado o algoritmo python que calcula a rentabilidade dos ativos para um período grande, devido ao grande número de ativos que compõem o índice bovespa, a cada Nan recebido do servidor da yahoo correspondia a eliminação daquela semana específica, pois para podermos comparar o índice com a carteira rebalanceada, era necessário que todos as semanas estudadas contivessem dados de todos os ativos. Por esse motivo no primeiro teste só conseguimos aproveitar 7 semanas para a avaliação do projeto. Foram feitos testes com essas poucas semanas para ter uma primeira idéia se o caminho seguido tinha boas perspectivas. Os resultados conseguidos nesse primeiro teste foram animadores e constam da aba de resultados do arquivo "planilha1" do branch "Genetic". 
Na nova planilha, foi ampliado o período de análise até o final de 2019 para que fosse possível testar mais semanas, chegando a um total de 15 semanas testadas.

Como insumos tivemos os seguintes dados:
-Previsão: Script Python que utilizou Ramdom Forest para a previsão da direção do índice bovespa na semana em que a carteira rebalanceada era testada. Foramam estudadas diversas técnicas de machine Learning, dentre elas LSTM, MPLS e KNN, sendo a Random Forest a que 	obteve os melhores resutados, trazendo uma precisão de quase 80% nos testes realizados. Esse algoritmo tem como produto a previsão de alta (1) ou baixa (-1) da semana T+1 com base nos indicadores calculados com os dados da semana T. O Algoritmo genético utiliza essa previsão da seguinte maneira: Se a previsão do ibovespa é de alta, o Beta da carteira rebalanceada pode variar até 1.1, mas se a previsão for de baixa, o limite para o beta da carteira é de 0.9. A intenção é que quando prevemos um alta, podemos aumentar nosso nivel de risco trazendo melhores resultados para a carteira, assim como reduzir o nivel de risco quando a previsão for de baixa. Pelos resultados encontrados, parece comprovada a teoria, pois a volatilidade da carteira balanceada foi muito menor do que a do indice.
-Beta: Script Python que utilizou dados dos últimos 5 anos de cada um dos ativos que compõem o índice bovespa para calcular o beta de cada um deles. Como o Beta é baseado em dados de um longo período, não foi necessário reclacular o Beta para cada semana, pois a variação	seria muito pequena, por esse motivo, o mesmo beta para cada ativo pode ser utilizado no cálculo do algoritmo genético de todas as semanas.
-Performance dos ativos: Script Python que gerou um .CSV contendo a variação período a período de cada um dos ativos que compões o Índice Bovespa. Essa informação foi utilizada para calcular o desempenho de cada variável no algoritmo genético, na medida que ativos que	performaram melhor na semana T, eram valorizados frente aos ativos que performaram mal. Aqui a intenção é aplicar a teoria muito 	utilizada na análise gráfica de que um ativo mantem a tendencia do seu movimento, ou seja, ativos que vinham subindo tendem a 	manter-se subindo. Desa forma o algoritmo aumentava a alocação da carteira em ativos de alto retorno, balanceando ativos com diferentes Betas, para que o limite do Beta da carteira, imposto pela previsão para a semana seguinte, não fosse ultrapassado.

Algumas restrições foram necessárias para o bom funcionamento do algoritmo, as quais seguem abaixo:
-Mínimo e Máximo de alocação para cada ativo: Foi definido que cada ativo deveria ter uma participação mínima 0,7% e máxima de 10%. Essa restrição foi necessária para manter a diversificação da carteira, evitando que o algoritmo montasse carteiras com poucos	ativos, aumentando o risco total.
-Beta: Como explicado anteriormente, o algoritmo respeitava a restrição de limite de valor do Beta da Carteira que variava entre 0,9 para cenários previstos de queda e de 1,1 para cenários de alta.

Função objetivo: A função objetivo utilizada foi o máximo retorno da carteira na semana anterior (T). Ou seja, o algoritmo deveria aumentar o retorno da carteira da semana T variando as alocações de cada ativo e repeitando as restrições. Dessa forma, esperáva-se encontrar a alocação de melhor retorno na semana T que, de acordo com a teoria das tendências, aumentaria o retorno da carteira em T+1.

Variáveis: As variáveis eram as porcentagens de alocação de cada ativo da carteira.
O algoritmo resultante dessa etapa foi o "planilha2.xlsx" constante do branch "Genetic".


## Resultados Alcançados

![image](https://user-images.githubusercontent.com/78120810/112415532-b8835d80-8d02-11eb-968e-08513252855f.png)

![image](https://user-images.githubusercontent.com/78120810/112415636-e8326580-8d02-11eb-8a5d-4404c7786a2b.png)

Como pode-se constatar da tabela e do gráfico acima, os resultados obtidos foram excelentes. Apesar de o retorno final ter sido muito próximo para ambas as certeiras, o desvio padrão da carteira rebalanceada foi muito menor reduzindo a volatilidade dos retornos e consequentemente o risco total da carteira. 
A tabela acima, assim como o gráfico de performance podem ser encontrados na aba "Resultados" de ambas as planilhas (1 e 2) constantes do branch "Genetic".

## Conclusões

Do presente projeto pôde-se concluir que os algoritmos de machine learning são boas ferramentas para a previsão de tendências de movimentos de ações e índices e por isso merecem ser estudadas a fundo a fim de melhorar sua acurácia e ampliar sua gama de utilizações.
Concluímos também que os algoritmos genéticos são bastante eficientes na definição de alocação de grandes carteiras sendo um método de baixo custo computacional e extremamente flexível para o tratamento de restrições impostas.
O trabalho experimental em questão se mostrou bastante aplicável à realidade trazendo expectativas de resultados extremamente positivos, tendo em vista que, segundo a revista exame invest, em reportagem do dia 16/01/2021, metade dos fundos de ações geridos por grandes gestores de mercado perderam para o índice Bovespa.

# TCC
Repositório para desenvolvimento do Trabalho de Conclusão de Curso da Pós Graduação em Business Intelligence da Puc-Rio

## Objetivo:
O presente projeto tem como objetivo superar a relação risco/retorno do índice Bovespa através da variação da alocação de uma carteira contendo ativos selecionados de forma aleatória entre vários setores de negócios disponíveis na bolsa de valores de São Paulo.
Para esse objetivo serão usadas ferramentas de machine learning no intuito estimar o desempenho futuro do índice Bovespa, determinando assim uma postura mais agressiva na alocação caso a estimativa seja de alta no índice, e uma postura mais conservadora caso a estimativa seja na direção contrária.
Através de um script desenvolvido na linguagem python encontraremos o Beta de cada ativo para que possa ser calculado o Beta total da carteira que será o parâmetro a ser utilizado como referência de exposição ao risco em relação ao risco sistêmico inerente aos ativos e suas alocações no índice Bovespa.
Utilizando esses dados juntamente com a informação do desempenho individual de cada ativo que compõe a carteira em períodos anteriores, serão utilizados algoritmos genéticos que resultarão na melhor alocação possível desses 30 ativos para que tenhamos um retorno maior que o índice Bovespa, sem que o Beta da carteira supere o índice de risco previamente definido.

## Proposta de Trabalho de Conclusão de Curso:
Pretende-se atingir o objetivo acima definido, dividindo o projeto em 4 etapas, as quais estão resumidas a seguir:

### ETAPA I – Previsão do Desempenho do Índice Bovespa:
O objetivo dessa etapa é, utilizando redes neurais, prever a direção do movimento do Ibovespa no período seguinte.
O produto dessa etapa servirá de insumo para o algoritmo genético da seguinte maneira: movimentos de alta do ibovespa permitirão que o algoritmos genético proponha alocações onde o Beta da carteira seja mais elevado, o que, em tese, traz resultados superiores, porém com maiores riscos. Já em movimentos de baixa do ibovespa o algoritmo genético ficará limitado a valores mais baixos de beta levando a uma tendencia de resultados inferiores, mas com riscos limitados.
Serão testadas diversas ferramentas de redes neurais como KNN, Random Forrest e LSTM, em diversas configurações com o intuito de chegar a previsões mais efetivas.
A dificuldade dessa etapa está em conseguir que as redes neurais encontrem padrões nos dados dos preços das ações devido ao caráter errático do mercado. Para superá-las, a intenção é aliar técnicas diferentes de redes neurais com tratamento de dados, a fim de facilitar a busca por esses padrões.

### Etapa II – Cálculo do Beta de cada Ativo da carteira
O objetivo dessa etapa é encontrar o valor do Beta de cada ativo que comporá a carteira. 
Pretende-se desenvolver um script na linguagem Python que automatize esse cálculo.
A informação do Beta individual servirá de insumo para o algoritmo genético que em seus cálculos chegará ao beta total da carteira em cada indivíduo da população gerada, filtrando apenas os que possuem Beta em uma certa faixa de valores, que dependerá do movimento previsto do iBovespa na Etapa I.

### Etapa III – Cálculo do desempenho passado de cada ativo da carteira
Nessa etapa, da base de dados da B3, serão calculados os resultados passados de cada um dos ativos que comporão a carteira.
Baseado na teoria que diz que o movimento de um ativo segue uma tendencia, ou seja, ativos que em períodos recentes estão em movimento de alta, tendem a seguir em alta, o algoritmo genético aumentará a alocação de ativos com melhores retornos no período anterior sempre controlando o impacto que esse ativo traz à carteira em termos de Beta, ou seja, como o ativo impacta no nível de risco da carteira. 

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

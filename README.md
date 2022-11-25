<h1 align="center">
  House Guide - Projeto de Insights
</h1>

<h1 align="center">
  <img alt="houseguidelogo" title="#logo" src="./images/house_guide.jpg" />
</h1>

## 1. Problema de Negócio
    
A House Guide é uma empresa que realiza investimentos no mercado imobiliário. Tem por modelo de negócio realizar estudos sobre regiões onde deseja realizar operações e ter assertividade no portfólio de ativos imobiliários. Sua estratégia é comprar bons imóveis com lacuna de oportunidade de crescimento no preço para vender e obter lucros.

### 1.1 Contexto de Negócio
   O desafio no momento é iniciar operações no estado de Washington - EUA, na cidade de Seattle. Para isso, possui a disposição uma base de dados para análise que consiste em 21.613 vendas de imóveis realizadas entre as datas de 02/05/2014 à 27/05/2015 na cidade de Seattle - EUA. Essa base de dados conta com informações de venda de 21.436 imóveis distintos.

### 1.2 Questão de Negócio
   - Quais são os imóveis que a House Guide deveria comprar e por qual preço?
   - Uma vez a casa comprada, qual o melhor preço para vendê-las?

## 2. Planejamento Prévio

### 2.1 Ferramentas
  - Python 3.8
  - Mapas interativos com Plotly e Folium
  - Geopandas 
  - Jupyter Notebook
  - Spyder
  - Framework Streamlit Web Apps
  - Heroku Cloud 

### 2.2 Produto Final
   - [Dashboard interativo em Página Web](https://analytics-house-guide.herokuapp.com/) contendo:
      
      - Visão geral dos dados com valores médios e análise descritiva;
      
      - Mapa com visão geral da região, contendo:
        - Densidade do portfolio: Análise da distribuição dos imóveis vendidos.
        - Densidade de preço: Análise do preço por área (em metros quadrados) médio por região.
      
      - Gráficos contendo:
        - Preço médio por ano de construção
        - Preço médio por dia
        - Distribuição de preços
        - Atributos da casa: casas por quartos, casas por banheiros, casas por andares e casas com vista para a água.

## 3. Dados
Os dados para esse projeto foram coletados na plataforma do Kaggle: https://www.kaggle.com/harlfoxem/housesalesprediction

### 3.1 Atributos de origem

|    Atributos    |                         Definição                            |
| :-------------: | :----------------------------------------------------------: |
|       id        |           Identificação única para cada imóvel vendido
|      date       |                    Data da venda do imóvel                   |
|      price      |                 Preço que o imóvel foi vendido               |
|    bedrooms     |                      Número de quartos                       |
|    bathrooms    |                    Número de banheiros                       |
|   sqft_living   | Tamanho (em pés quadrado) do espaço interior (área construída) dos imóveis |
|    sqft_lot     |     Tamanho (em pés quadrado) do terreno onde o imóvel está situado     |
|  sqft_basement  |     Tamanho (em pés quadrado) do espaço interior que se encontra abaixo do nível do solo     |
|    sqft_above   |     Tamanho (em pés quadrado) do espaço interior que se encontra acima do nível do solo. (sqft_living - sqft_basement)     |
|     floors      |                 Número de andares do imóvel                  |
|   waterfront    |   Variável que indica a presença ou não de vista para água   |
|      view       |    Um índice de 0 a 4 de quão boa era a visão do imóvel      |
|    condition    |      Um índice de 1 a 5 que indica a condição do imóvel      |
|      grade      | Um índice de 1 a 13 que indica a qualidade da construção e o design do imóvel. |
|    yr_built     |               Ano de construção de cada imóvel               |
|  yr_renovated   |                 Ano de reforma de cada imóvel                |
|     zipcode     |                   Código Postal do imóvel                    |
|       lat       |                           Latitude                           |
|      long       |                           Longitude                          |
| sqft_livining15 | Tamanho (em pés quadrado) do espaço interno de habitação para os 15 vizinhos mais próximo |
|   sqft_lot15    | Tamanho (em pés quadrado) dos terrenos dos 15 vizinhos mais próximo |

### 3.2 Detalhamento atributos de origem

- waterfront:
    - 0 = não 
    - 1 = sim
- view:
    - 0 = Sem vista
    - 1 = Razoável
    - 2 = Média
    - 3 = Boa 
    - 4 = Excelente
- yr_renovated: 
    - 0 se nunca renovado.
- condition:
    - 1 = Pobre/Desgastado. Reparação e revisão necessária em superfícies pintadas, coberturas, canalizações, aquecimento e numerosas insuficiências funcionais. Manutenção e abuso excessivos, valor em uso limitado, abandono ou reconstrução importante; reutilização ou mudança de ocupação é iminente. A idade efetiva está próxima do fim da escala, independentemente da idade cronológica real.
    - 2 = Bastante desgastado. É necessária muita reparação. Muitos itens necessitam de retoque ou revisão, manutenção diferida óbvia, utilidade de construção inadequada e sistemas, todos encurtando a esperança de vida e aumentando a idade efetiva.
    - 3 = Média. Algumas provas de manutenção diferida e obsolescência normal com a idade, na medida em que algumas pequenas reparações são necessárias, juntamente com alguns retoques. Todos os componentes principais ainda funcionam e contribuem para uma esperança de vida prolongada.
    - 4 = Bom. Não é necessária manutenção óbvia, mas também não é tudo novo. A aparência e utilidade estão acima do padrão e a idade efetiva global será mais baixa do que a propriedade típica.
    - 5 = Muito Bom. Todos os artigos bem conservados, muitos dos quais foram renovados e reparados à medida que mostraram sinais de desgaste, aumentando a esperança de vida e diminuindo a idade efetiva com pouca deterioração ou obsolescência evidente com um elevado grau de utilidade.
- grade:
    - (1-3): abaixo dos padrões mínimos de construção.
    - 4: Geralmente mais antiga, construção de baixa qualidade.
    - 5: Baixos custos de construção e mão-de-obra. Projeto pequeno e simples.
    - 6: A avaliação mais baixa que cumpre atualmente o código de construção. Materiais de baixa qualidade e projeto arquitetônico simples.
    - 7: tem um nível médio de construção e concepção.
    - 8: Um pouco acima da média em construção e concepção. Normalmente melhores materiais tanto no trabalho de acabamento exterior como interior.
    - 9: Melhor design arquitetônico com design e qualidade extra no interior e exterior.
    - 10: Casas com esta qualidade têm geralmente características de alta qualidade. Os trabalhos de acabamento são melhores e mais qualidade de design é vista nas plantas dos pisos. Geralmente têm um tamanho maior.
    - 11: Desenho personalizado e trabalhos de acabamento de maior qualidade com comodidades acrescidas de madeiras maciças, instalações sanitárias e opções mais luxuosas.
    - 12: Desenho à medida e excelentes construtores. Todos os materiais são da mais alta qualidade e todas as conveniências estão presentes.
    - 13: Geralmente concebidos e construídos à medida. Nível de mansão. Grande quantidade de trabalho de armário da mais alta qualidade, acabamentos em madeira, mármore, formas de entrada, etc.

### 3.3 Atributos criados

|    Atributos    |                         Definição                            |
| :-------------: | :----------------------------------------------------------: |
|      month      |                    Mês da venda do imóvel                    |
|      year       |                    Ano da venda do imóvel                    |
|      age        |       Idade do imóvel. (Ano atual - Ano Construção)          |
|  is_renovated   |  Variável que indica se imóvel foi renovado sim (1) ou não (0)   |
|     seasons     |             Estação do ano que imóvel foi vendido            |    
|    sqft_lot_m2       |     Tamanho (em metros quadrados) do terreno onde o imóvel está situado     |
|  price_sqft_lot_m2     |      Preço do imóvel por metro quadrado de área construída       |


### 3.4 Detalhamento atributos criados

- seasons:
    - Verão = de junho a agosto.
    - Outono = de setembro a novembro.
    - Inverno = de dezembro a fevereiro.
    - Primavera = de março a maio.
- sqft_lot_m2:
    - Conversão da unidade de medida de área em pé para metro quadrado, calculo utilizado sqft_lot * 0.093.
- price_sqft_lot_m2:
    - Preço dividido pela área construída(m2).  

## 4. Premissas

- Dados Faltantes: 
    - Nenhum dos atributos do dataset possui dados faltantes
- Imóveis Duplicados:
    - Existem 177 imóveis que estão duplicados no dataset, ou seja, significa que foram vendidos mais de uma vez em períodos distintos ao longo do tempo que abrange a coleta de dados dos imóveis. Realizou-se uma análise com o intuito de compreender a variação de atributos como condição, tamanho de interior de casa ou grade entre as vendas realizadas, porém apenas o atributo "price" varia ao comparar as vendas com mesmos imóveis. 
    - Sendo assim, optou-se por manter os imóveis de forma duplicada no dataset para fins de análise de venda por período a qual as duas vendas duplicadas são importantes.
- Valor Outlier para número de quartos:
    - Encontrou-se o valor de 33 quartos informados em um determinado imóvel do dataset, avaliando a veracidade do dado buscou-se verificar o valor máximo de quartos em um imóvel abaixo dos 33 encontrados, sendo assim, existem imóveis com no máximo 11 quartos na base de dados. 
    - Dessa forma, o valor de 33 será substituído por 3 assumindo possível erro de digitação.

## 5. Cinco Principais Insights 

   - **H1:** Imóveis com vista para a água, são em média 30% mais caros.
      
      ❌ **Falsa:** 
      - Considerando o **preço médio**, ao invés de 30%, são 3x mais caros ou aproximadamente 212,63% mais caros, na média.


   - **H2:** Imóveis com data de construção menor que 1955, são 50% mais baratos, na média.
      
      ❌ **Falsa:** 
      - Considerando o **preço médio**, imóveis com data de construção menor que 1955, possuem preços 0,79% mais baratos


   - **H3:** O crescimento do preço dos imóveis YoY ( Year over Year ) é de 10%.
      
      ❌ **Falsa:** 
      - O crescimento do preço médio dos imóveis (YoY - Year over Year) é de 0.52%.


   - **H4:** Imóveis com mais de 50 anos com reforma feita são 20% mais caros, em média, que os sem reforma feita.
      
      ❌ **Falsa:** 
      - Considerando o **preço médio**, ao invés de 20% mais caras, são 53,71% mais caras.
      
   
   - **H5:** 40% das vendas de imóveis ocorrem no verão.
      
      ❌ **Falsa:** 
      - As vendas representam aproximadamente 30% no Verão.
      - E juntos as estações Verão e Primavera representam 60% de toda a receita de vendas.


## 6. Planejamento da Solução

Para responder as questões de negócio, utilizou-se pensamento analítico e análise de dados.

**Quais são os imóveis que a House Guide deveria comprar e por qual preço** ?

1. Agrupar os imóveis por região (zipcode).
   - Encontrar a mediana dos preços por área construída dentro de cada região.

2. Sugerir os imóveis que:
   - Possuem preço por área construída abaixo da mediana da região;
   - Que estejam em boas condições (coluna condition acima de 3);
   - Se mais de 50 anos (coluna age):
      - Verificar se possui reforma feita para comprar.
            
**Uma vez a casa comprada, qual o melhor momento para vendê-las e por qual preço?**?

1. Agrupar os imóveis por região (zipcode) e por estação.
   - Calcular a mediana do preço para venda, dentro de cada região e estação.

2. Agrupar os imóveis por região (zipcode) e calcular a média de grade por região.
    
3. Condições de venda:
    1. Se o preço da compra por metro quadrado for maior que a mediana da região + sazonalidade:
        - O preço da venda será igual ao preço da compra + 5%.
        - + 5% se a grade da casa estiver acima da média da região.

    2. Se o preço da compra por metro quadrado for menor que a mediana da região + sazonalidade:
        - O preço da venda será igual ao preço da compra + 15%.
        - + 5% se o grade da casa estiver acima da média da região.
   
## 7. Resultados Financeiros 

Considerando todos os imóveis recomendados como compra para o investimento:


| Custo do Investimento  |   Lucro com as vendas   |   Return on Investiment (ROI) |
|------------------------|-------------------------|-------------------------|
|   $ 2.365.263.837,00   |    $ 409.181.453,09     |          17,30%         |

## 8. Conclusão

Os objetivos almejados inicialmente foram cumpridos no que tange a lista de recomendações de imóveis para compra, bem como, a projeção do valor de venda desses imóveis. As hipóteses levantadas foram respondidas. Além disso, os dados foram disponibilizados em um dashboard interativo em uma [aplicação na nuvem](https://analytics-house-guide.herokuapp.com/) o que facilita o acesso as análises.

## 9. Próximos Passos

 Usar algoritmos de machine learning para recomendar o preço estimado de venda e compra. Usar clusterização para fazer análise de comparação de imóveis. 

## Análise da Produção de Café no Estado de São Paulo

O café é um dos produtos queridinhos e está bem presente nas mesas brasileiras. Já foi cenário político, entre os período de 1894 e 1930, da República Oligárquica, período marcado pela alternância de poder entre as oligarquias de São Paulo e Minas Gerais. Nessa época, São Paulo era conhecido por ser um dos maiores produtores de café, enquanto Minas Gerais, pela produção de leite. Esse período ficou conhecido também como Política do Café com Leite. Motivado por esse fato da história brasileira, surge a seguinte questão: E nos dias de hoje, São Paulo ainda é um grande produtor de café ?

O dataset utilizado foi o [Censo Agropecuário](https://basedosdados.org/dataset/br-ibge-censo-agropecuario?bdm_table=municipio) e está disponível em [Base dos Dados](https://basedosdados.org/).

>O Censo Agropecuário, realizado pelo Instituto Brasileiro de Geografia e Estatística (IBGE), é a principal e mais completa investigação estatística e territorial sobre a produção agropecuária do país. Visa obter informações sobre a estrutura, a dinâmica e o nível de produção da atividade agropecuária brasileira.


Para atividade foi utilizado as seguintes bibliotecas: 
```
import basedosdados as db
from matplotlib import pyplot as plt
import numpy as np
```
E a seguinte query em SQL para reduzir o tamanho do download:
```
query =" SELECT ano, sigla_uf,id_municipio, producao_cafe,area_cafe,valor_total_producao_cafe,producao_total_arroz,producao_total_feijao,producao_total_milho,producao_total_mandioca,producao_total_soja,producao_total_algodao,producao_total_cana,producao_total_trigo 
FROM `basedosdados.br_ibge_censo_agropecuario.municipio` 
WHERE sigla_uf = 'SP'"
```
Para iniciar o tratamento dos dados foi plotado um histograma das variáveis para analisar a distribuição dos dados. Observou-se que estão bastante concentrados, portanto foi feito uma célula de código que retornasse a quantidade de valores zeros, NA e a proporção desses na amostra. A proporção é interessante para identificar se preencher os dados NA com a média poderia enviesar o resultado. De modo geral, a % de NA desse dataset é abaixo de 10%, e foram substituído por suas respectivas médias.

Entretanto para a variável `producao_total_trigo`, a % de valores NA foi de 20%, o que levantou suspeita se poderiam estar concentrados em algum dos anos em que o censo foi realizado. Então um outro script realizado retornou a seguinte resposta: 

* Quantidade de dados faltantes da produção de trigo no censo de 1985: 0
* Quantidade de dados faltantes da produção de trigo no censo de 1996: 500
* Quantidade de dados faltantes da produção de trigo no censo de 2006: 0
* Quantidade de dados faltantes da produção de trigo no censo de 2017: 5

Como os dados faltantes se concentram no censo de 1996, e para fins de diminuir a complexidade de análise, optou-se por preencher os demais com a média do respectivo ano e não trabalhar com os dados de produção de trigo de 1996, pois as aproximações poderiam gerar uma tendência equivocada dos resultados.

Por fim, gerou-se o gráfico da produção de café registrado nos censos de 1985, 1996, 2006 e 2017 que demonstra uma expressiva queda na produção. Estima-se que o valor da produção de 2017 é cerca de 12% da produção de 1985. Isso deve-se ao fato de que o Estado, ao longo dos anos, deve ter mudado sua estratégia de produção, inserindo novas monoculturas. Dentre as monoculturas analisadas (café, arroz, feijão, milho, mandioca, soja, algodão, cana e trigo) a mandioca é o maior produto agrícola produzido com cerca de 78.0 % de participação.









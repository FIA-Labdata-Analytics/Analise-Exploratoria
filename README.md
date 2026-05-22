# 📊 Análise Exploratória de Dados — Case Papelaria
### Material de Referência Oficial · Disciplina de Fundamentos de Data Science

> **Documento elaborado pela Diretoria Acadêmica** com base no projeto de melhor desempenho da turma. Este README serve como guia de estudo, referência de boas práticas e modelo de documentação profissional para projetos de portfólio e GitHub.

---

## Visão Geral do Projeto

### O Problema de Negócio

Uma rede varejista do segmento de papelaria acumula dados transacionais do último mês de operação e precisa transformá-los em inteligência de negócio. A área de Analytics foi acionada para responder questões estratégicas que orientarão três frentes decisórias distintas:

- **Gestão de Estoque:** Quais produtos precisam de reposição prioritária? Quais estão parados nas prateleiras?
- **Curadoria do Mix:** Quais categorias e seções concentram o faturamento? Quais são candidatas à descontinuação?
- **Precificação e Negociação:** Existe relação entre preço e volume vendido? Como isso varia por seção?

### Por que isso é relevante no mundo real?

No varejo, a ausência de análise de dados resulta em dois tipos clássicos de perda: **ruptura de estoque** (produto esgotado antes do reabastecimento) e **estoque encalhado** (capital imobilizado em produtos sem giro). Ambos impactam diretamente a margem e a experiência do cliente.

Um projeto de EDA bem executado é, muitas vezes, o primeiro passo antes de qualquer modelo preditivo. Ele fornece o entendimento profundo dos dados que sustenta decisões confiáveis — seja manualmente por gestores, seja automaticamente por algoritmos.

### Cenário Simulado

O projeto simula o dia a dia de um analista de dados júnior/pleno que recebe uma base bruta de vendas e precisa entregá-la como um relatório analítico responsivo às perguntas do negócio. Não há modelos de Machine Learning aqui — o foco total está na exploração rigorosa, na construção de raciocínio analítico e na comunicação clara dos achados.

---

## Objetivos do Projeto

### Objetivos Principais

- Realizar uma Análise Exploratória de Dados (EDA) completa sobre vendas mensais de uma papelaria
- Responder 8 questões de negócio específicas utilizando técnicas adequadas de análise e visualização
- Comunicar os resultados com clareza, combinando código, tabelas e conclusões narrativas

### Objetivos Secundários

- Praticar agregações, filtros e transformações com `pandas`
- Criar métricas derivadas (como faturamento bruto) a partir de variáveis existentes
- Identificar padrões, outliers e segmentações relevantes no portfólio de produtos
- Desenvolver raciocínio analítico orientado a negócio

### Resultados Esperados

| Entregável | Descrição |
|---|---|
| Notebook compilado | Código Python executado, com saídas visíveis |
| 8 análises respondidas | Cada questão com código + conclusão narrativa |
| Feature derivada | Coluna `FATURAMENTO_BRUTO` calculada e utilizada nas análises |
| Segmentações por faixas | Variáveis categorizadas para análise cruzada |
| Análise de Pareto | Identificação dos produtos responsáveis por 80% do faturamento |

---

## Estrutura do Projeto

```
📁 case-papelaria-eda/
│
├── 📄 Papelaria.txt                         # Base de dados original (formato TSV)
├── 📓 ESTUDO_DE_CASO_EDA.ipynb              # Notebook com enunciado das questões
├── 📓 ESTUDO_DE_CASO_EDA_Respostas.ipynb    # Notebook com respostas (melhor nota)
└── 📄 README.md                             # Este documento
```

### Arquivos e suas Funções

**`Papelaria.txt`** — Fonte primária de dados. Arquivo delimitado por tabulação (`\t`) com cabeçalho na primeira linha e separador decimal (`.`). Contém 290 registros de produtos únicos.

**`ESTUDO_DE_CASO_EDA.ipynb`** — Template distribuído aos alunos. Contém o enunciado do case, a lista de variáveis, as 8 questões de negócio e células-âncora para o código.

**`ESTUDO_DE_CASO_EDA_Respostas.ipynb`** — Solução de referência, desenvolvida pelo aluno de maior desempenho da turma. Contém todo o código Python executado, os outputs e as conclusões narrativas para cada questão.

---

## Entendimento do Problema de Negócio

### A Perspectiva Empresarial

Para um varejista, cada produto no estoque representa um investimento de capital. A questão central não é apenas "o que vendemos?", mas sim "onde está o valor gerado?", "quais produtos devemos abandonar?" e "onde há oportunidade de precificação?"

A área de Analytics atua, nesse contexto, como uma ponte entre os dados operacionais (transações) e as decisões estratégicas (compras, mix, precificação). Sem essa análise, os gestores operam no escuro, reagindo a problemas depois que eles ocorrem.

### Como a Ciência de Dados ajuda

A EDA permite que padrões invisíveis no volume de dados se tornem evidentes. Com 290 produtos distribuídos em 3 seções e dezenas de categorias, uma análise manual seria inviável e imprecisa. Python e `pandas` tornam possível responder perguntas em segundos que levariam horas em planilhas.

### Riscos e Impactos Potenciais

| Risco sem análise | Impacto financeiro estimado |
|---|---|
| Ruptura de estoque nos top 17% de produtos (49 itens = 80% do faturamento) | Perda direta de receita em itens de alta demanda |
| Manutenção de estoque parado (produtos com 0 unidades vendidas) | Capital imobilizado sem retorno |
| Precificação ineficiente em seções de alta variabilidade | Margem abaixo do potencial |

---

## Entendimento dos Dados

### Fonte dos Dados

| Atributo | Valor |
|---|---|
| Arquivo | `Papelaria.txt` |
| Formato | Texto delimitado por tabulação (TSV) |
| Registros | 290 produtos únicos |
| Período | Último mês de operação |
| Qualidade | Sem valores ausentes · Sem duplicatas |

### Dicionário de Variáveis

| Variável | Tipo | Descrição |
|---|---|---|
| `COD_PRODUTO` | Categórica (identificador) | Código único de identificação do produto (ex: `COD_P_255913`) |
| `CATEGORIA_PRODUTO` | Categórica nominal | Categoria do produto (ex: Notebook Premium, Caneta Simples) |
| `SECAO_PRODUTO` | Categórica nominal | Seção/departamento (Papelaria, Informática, Acessórios) |
| `PRECO_UNITARIO` | Numérica contínua | Preço unitário de venda vigente no mês (em R$) |
| `QTD_UNIDADES_VENDIDAS_MES` | Numérica discreta | Quantidade de unidades vendidas no mês |

### Variável Derivada (criada pelo analista)

| Variável | Tipo | Fórmula |
|---|---|---|
| `FATURAMENTO_BRUTO` | Numérica contínua | `PRECO_UNITARIO × QTD_UNIDADES_VENDIDAS_MES` |

> **Por que criar essa variável?** O negócio não se resume a quantidade vendida nem a preço isoladamente. O **faturamento bruto** integra os dois e mede o valor gerado por produto — sendo a métrica central para priorização de estoque, análise de Pareto e comparação entre seções.

### Qualidade dos Dados

O primeiro passo de qualquer analista responsável é **auditar a base antes de analisá-la**. Aqui está o que foi verificado:

```python
# Verificação de duplicatas por código de produto
database['COD_PRODUTO'].duplicated().sum()  # Resultado: 0

# Verificação de valores ausentes por coluna
database.isna().sum()  # Resultado: 0 em todas as colunas
```

**Conclusão:** A base está íntegra — sem duplicatas e sem nulos. Esse resultado elimina a necessidade de tratamento e aumenta a confiança nas análises subsequentes. Em projetos reais, essa etapa frequentemente revela problemas que invalidariam análises inteiras se não fossem detectados aqui.

---

## Análise Exploratória de Dados (EDA)

A EDA foi estruturada em 8 questões de negócio, cada uma respondida com a técnica mais adequada. A seguir, descrevemos o raciocínio por trás de cada decisão analítica.

---

### Questão 1 — Categorias com maior preço unitário médio

**Pergunta:** Quais categorias de produto possuem o maior preço unitário, em média?

**Por que analisar isso?** O preço médio por categoria indica onde estão os produtos de maior valor percebido. Isso orienta negociações com fornecedores e estratégias de margem.

**Técnica utilizada:** Agrupamento por `CATEGORIA_PRODUTO` e `SECAO_PRODUTO`, com cálculo da média de `PRECO_UNITARIO`, ordenado de forma decrescente.

```python
database.groupby(['CATEGORIA_PRODUTO', 'SECAO_PRODUTO'])['PRECO_UNITARIO'] \
        .mean().round(2).nlargest(15)
```

**Resultados encontrados:**

| Ranking | Categoria | Seção | Preço Médio (R$) |
|---|---|---|---|
| 1 | Notebook Premium | Informática | 5.216,63 |
| 2 | Notebook | Informática | 3.779,90 |
| 3 | Tablet | Informática | 2.919,70 |
| 4 | Impressora a Laser | Informática | 1.479,95 |
| 5 | Monitor | Informática | 887,15 |
| 9 | Mochila Executiva | Acessórios | 254,92 |

**Insight de negócio:** As categorias de maior ticket médio estão concentradas na seção de Informática, com destaque para Notebooks Premium (R$ 5.216) e Notebooks (R$ 3.780). A seção de Acessórios aparece a partir da 9ª posição, e a Papelaria não figura entre os 15 maiores — o que é esperado, dado seu perfil de produtos de baixo valor unitário e alto volume.

> **Lição analítica:** Ao agregar por duas dimensões simultaneamente (`CATEGORIA_PRODUTO` + `SECAO_PRODUTO`), evitamos ambiguidades — pois uma mesma categoria poderia teoricamente aparecer em mais de uma seção. Essa granularidade é uma prática recomendada em análises de portfólio.

---

### Questão 2 — Faturamento bruto por categoria dentro de cada seção

**Pergunta:** Dentro de cada seção, quais categorias mais contribuíram com o faturamento bruto?

**Por que analisar isso?** Volume de vendas e preço alto não garantem, isoladamente, maior faturamento. Um produto barato com altíssimo giro pode superar um produto caro com pouquíssimas vendas. O faturamento bruto integra os dois fatores.

**Técnica utilizada:** Criação da coluna `FATURAMENTO_BRUTO`, agregação por seção e categoria com soma do faturamento e cálculo do percentual em relação ao total da loja.

```python
database_questao2['FATURAMENTO_BRUTO'] = (
    database_questao2['PRECO_UNITARIO'] * database_questao2['QTD_UNIDADES_VENDIDAS_MES']
)
faturamento_total = database_questao2['FATURAMENTO_BRUTO'].sum()
database_questao2['FATURAMENTO_BRUTO%'] = (
    database_questao2['FATURAMENTO_BRUTO'] / faturamento_total * 100
).round(2)
```

**Resultados encontrados — Faturamento por seção:**

| Seção | Faturamento Bruto (R$) | % do Total |
|---|---|---|
| Informática | 160.444,40 | 77,77% |
| Acessórios | 25.684,70 | 12,45% |
| Papelaria | 20.189,91 | 9,79% |

**Insight crítico:** A seção de Informática concentra mais de 3/4 do faturamento total da loja, apesar de trabalhar com produtos de baixo volume de vendas. Isso ocorre porque o ticket médio elevado compensa o giro reduzido. Já a Papelaria, que tem o maior volume de unidades vendidas, contribui com menos de 10% do faturamento — o que levanta uma questão estratégica: a loja está precificando adequadamente seus produtos de papelaria?

> **Lição analítica:** Nunca analise quantidade vendida sem considerar o valor gerado — e nunca analise valor gerado sem entender o volume que o sustenta. O `FATURAMENTO_BRUTO` é sempre o ponto de equilíbrio entre os dois.

---

### Questão 3 — Relação entre preço e quantidade vendida

**Pergunta:** Existe relação entre o preço unitário e a quantidade vendida? Essa relação muda por seção?

**Por que analisar isso?** Em economia, a lei da demanda sugere que preços mais altos estão associados a menor volume de vendas. Mas isso nem sempre se confirma no varejo real — produtos de luxo ou necessidade podem escapar dessa lógica.

**Técnica utilizada:** Criação de variáveis categorizadas (faixas de preço e de quantidade) e construção de tabelas de contingência cruzando as duas dimensões, segmentadas por seção.

```python
# Faixas de preço baseadas em quartis
database_questao3['PRECO_UNITARIO_FAIXAS'] = pd.cut(
    database_questao3['PRECO_UNITARIO'],
    bins=[...],
    labels=['Muito Barato', 'Barato', 'Preço Médio', 'Caro']
)

# Faixas de quantidade vendida
database_questao3['QTD_UNIDADES_VENDIDAS_MES_FAIXAS'] = pd.cut(
    database_questao3['QTD_UNIDADES_VENDIDAS_MES'],
    bins=[...],
    labels=['Nenhum', 'Baixa', 'Média', 'Alta', 'Muito Alta']
)
```

**Resultados — Tabela de contingência (todos os produtos):**

| Qtd Vendida ↓ / Preço → | Muito Barato | Barato | Preço Médio | Caro |
|---|---|---|---|---|
| Nenhum | 0 | 6 | 5 | 6 |
| Baixa | 7 | 24 | 26 | 53 |
| Média | 11 | 17 | 27 | 21 |
| Alta | 32 | 35 | 19 | 16 |
| Muito Alta | 51 | 19 | 22 | 4 |

**Insight:** A tabela confirma a relação inversa entre preço e volume: produtos "Muito Baratos" concentram 51 casos na faixa "Muito Alta" de vendas, enquanto produtos "Caros" só têm 4 casos nessa faixa. A relação, contudo, **muda por seção** — na Informática, o comportamento é mais extremo (poucos produtos, preço muito alto, volume muito baixo), enquanto na Papelaria o padrão se inverte completamente.

> **Lição analítica:** Quando a pergunta inclui "isso muda a depender de X?", sempre segmente a análise por X antes de concluir. Uma relação global pode mascarar comportamentos completamente opostos em subgrupos.

---

### Questão 4 — Análise de Pareto: 80% do faturamento

**Pergunta:** Considerando os produtos com maior faturamento bruto, quantos deles foram responsáveis por 80% do faturamento total?

**Por que analisar isso?** A **Análise de Pareto** (ou princípio 80/20) é uma das ferramentas mais aplicadas no varejo. A premissa é que uma minoria de produtos gera a maioria do valor. Identificar esses produtos permite concentrar esforços de gestão onde o impacto é maior.

**Técnica utilizada:** Ordenação decrescente por faturamento, cálculo do faturamento acumulado e identificação do ponto onde o acumulado atinge 80%.

```python
database_questao4_ordenada['FATURAMENTO_BRUTO_ACUMULADO'] = (
    database_questao4_ordenada['FATURAMENTO_BRUTO'].cumsum()
)
faturamento_total = database_questao4_ordenada['FATURAMENTO_BRUTO'].sum()

database_questao4_ordenada['FATURAMENTO_PCT_ACUMULADO'] = (
    database_questao4_ordenada['FATURAMENTO_BRUTO_ACUMULADO'] / faturamento_total
).round(3)

produtos_80_fat = database_questao4_ordenada[
    database_questao4_ordenada['FATURAMENTO_PCT_ACUMULADO'] <= 0.80
]
```

**Resultado:**

> **49 produtos** são responsáveis por **80% do faturamento bruto total**.
> Isso representa apenas **16,9% do portfólio** (de 290 produtos).

**Insight estratégico:** O princípio de Pareto se confirma com precisão neste dataset. Gestores de estoque devem garantir que esses 49 produtos nunca entrem em ruptura. Do ponto de vista de negociação com fornecedores, esses são os itens prioritários para obtenção de melhores condições comerciais.

> **Lição analítica:** O método `cumsum()` do `pandas` é fundamental para análises de Pareto. Ele acumula valores linha a linha, permitindo identificar o ponto de corte exato em qualquer percentual desejado. Essa técnica é usada em logística, finanças, operações e gestão de riscos.

---

### Questão 5 — Produtos com menor faturamento em cada seção

**Pergunta:** Quais são os 3 produtos com menor faturamento bruto em cada seção?

**Por que analisar isso?** Produtos com faturamento zero ou próximo de zero são candidatos à revisão do mix. Eles imobilizam espaço de prateleira e recursos de gestão sem gerar retorno.

**Técnica utilizada:** Agrupamento por seção, categoria e código de produto, com ordenação crescente por faturamento e seleção dos 3 menores por seção.

```python
database_questao5_agrup = database_questao5.groupby(
    ['SECAO_PRODUTO', 'CATEGORIA_PRODUTO', 'COD_PRODUTO']
).agg(
    PRECO_UNITARIO_MEDIA=('PRECO_UNITARIO', 'mean'),
    QTD_UNIDADES_VENDIDAS_MES_SUM=('QTD_UNIDADES_VENDIDAS_MES', 'sum'),
    FATURAMENTO_BRUTO_SUM=('FATURAMENTO_BRUTO', 'sum')
).round(2).sort_values(
    by=['SECAO_PRODUTO', 'FATURAMENTO_BRUTO_SUM'], ascending=[True, True]
)
```

**Resultado — Produtos com faturamento zero (sem nenhuma venda no mês):**

| Seção | Categoria | Produto | Preço (R$) | Unidades Vendidas |
|---|---|---|---|---|
| Acessórios | Calculadora Científica | COD_P_321815 | 89,90 | 0 |
| Acessórios | Fone de Ouvido sem Fio | COD_P_244216 | 139,80 | 0 |
| Acessórios | Tripé | COD_P_173986 | 63,00 | 0 |
| Informática | Impressora a Jato | COD_P_324413 | 629,90 | 0 |
| Informática | Notebook | COD_P_211988 | 4.399,90 | 0 |
| Informática | Notebook Premium | COD_P_316388 | 4.999,90 | 0 |
| Papelaria | Agenda | COD_P_316501 | 65,90 | 0 |
| Papelaria | Cola e Fita Adesiva | COD_P_153079 | 5,80 | 0 |
| Papelaria | Estilete | COD_P_303835 | 8,90 | 0 |

**Insight:** Todos os produtos de menor faturamento tiveram **zero unidades vendidas** no mês. Isso indica possíveis problemas de disponibilidade, posicionamento na loja, sazonalidade ou precificação inadequada. Um Notebook a R$ 4.999 sem nenhuma venda merece atenção especial — pode estar mal posicionado ou com um preço fora do mercado.

> **Lição analítica:** Separar a análise por seção, categoria e produto ao mesmo tempo (usando índice hierárquico no `groupby`) permite uma visão granular sem perder o contexto estrutural.

---

### Questão 6 — Detecção de outliers

**Pergunta:** Existem produtos com valores atípicos de quantidade vendida, preço unitário ou faturamento bruto?

**Por que analisar isso?** Outliers podem representar erros de cadastro, produtos excepcionais ou fenômenos de mercado. Identificá-los é essencial antes de qualquer análise estatística ou decisão baseada em médias.

**Técnica utilizada:** Método do Intervalo Interquartil (IQR) — amplamente utilizado por ser robusto a distribuições assimétricas como as encontradas em dados de varejo.

```python
def detalhes_variavel(variavel):
    Q1 = variavel.quantile(0.25)
    Q3 = variavel.quantile(0.75)
    IQR = Q3 - Q1
    limite_inferior = Q1 - 1.5 * IQR
    limite_superior = Q3 + 1.5 * IQR
    
    print(f"O mínimo é {variavel.min()}")
    print(f"O máximo é {variavel.max()}")
    print(f"A média é {variavel.mean()}")
    print(f"A mediana é {variavel.median()}")
    print(f"Limite Inferior IQR: {limite_inferior}")
    print(f"Limite Superior IQR: {limite_superior}")
```

**Resultados — Preço Unitário:**

| Métrica | Valor |
|---|---|
| Mínimo | R$ 0,01 |
| Máximo | R$ 5.850,00 |
| Média | R$ 233,67 |
| Mediana | R$ 18,40 |
| Limite Superior IQR | R$ 217,36 |

A diferença expressiva entre média (R$ 233,67) e mediana (R$ 18,40) revela uma **distribuição altamente assimétrica à direita** — confirmada pelos Notebooks Premium com preços acima de R$ 4.800. Pela regra do IQR, todos os produtos acima de R$ 217 são tecnicamente outliers, o que inclui toda a seção de Informática.

**Insight:** Neste caso, os outliers são **legítimos** — não são erros, são produtos de alto valor de uma seção distinta. A decisão analítica correta é **segmentar por seção antes de aplicar análises estatísticas**, evitando que a Informática distorça as métricas das demais seções.

> **Lição analítica:** Outlier não significa erro. Significa "dado incomum que merece investigação". A decisão de removê-lo, mantê-lo ou segmentá-lo é sempre contextual e requer julgamento do analista — não é automática.

---

### Questão 7 — Variabilidade de preços por seção

**Pergunta:** Qual seção tem maior variabilidade de preços unitários?

**Por que analisar isso?** Alta variabilidade indica um portfólio heterogêneo, com produtos de perfis muito distintos. Isso afeta a estratégia de comunicação, a percepção de valor pelo cliente e a complexidade da gestão de categorias.

**Técnica utilizada:** Cálculo do desvio padrão e do coeficiente de variação (CV) por seção, além de boxplots para visualização da dispersão.

```python
database_questao7 = database.groupby('SECAO_PRODUTO')['PRECO_UNITARIO'].agg([
    'mean', 'std', 'min', 'max',
    lambda x: x.quantile(0.25),
    lambda x: x.quantile(0.75)
]).round(2)
```

**Insight:** A seção de Informática apresenta a maior variabilidade absoluta, com produtos que variam de R$ 104,90 (Cartucho de Tinta) a R$ 5.850,00 (Notebook Premium). A Papelaria, por sua vez, tem a maior **homogeneidade** — produtos concentrados em uma faixa estreita de preços baixos. O Coeficiente de Variação (CV = desvio padrão / média) é a métrica mais adequada para comparar variabilidade entre seções de escalas diferentes, pois normaliza a dispersão pelo valor médio.

> **Lição analítica:** Sempre que comparar variabilidade entre grupos com médias muito diferentes, use o Coeficiente de Variação em vez do desvio padrão bruto. Um desvio de R$ 500 é muito diferente dependendo se a média é R$ 200 ou R$ 2.000.

---

### Questão 8 — Segmentação por perfil de preço e volume

**Pergunta:** Existem produtos com alta quantidade vendida e baixo preço? E produtos com baixa quantidade vendida e alto preço?

**Por que analisar isso?** Essa análise revela dois arquétipos opostos de produtos, cada um com uma lógica de gestão completamente diferente. Misturar estratégias entre esses perfis é um erro clássico de gestão de portfólio.

**Técnica utilizada:** Definição de limiar com base nos quartis e filtragem da base em dois grupos distintos.

```python
# Limiar para "alto preço": acima do Q3 de preço
preco_alto = database_questao8['PRECO_UNITARIO'].quantile(0.75)  # > R$ 89,90

# Limiar para "baixa quantidade": abaixo do Q1 de quantidade
baixa_quantidade = database_questao8['QTD_UNIDADES_VENDIDAS_MES'].quantile(0.25)  # < 4 unidades

# Limiar para "alto volume": acima do Q3 de quantidade
alto_volume = database_questao8['QTD_UNIDADES_VENDIDAS_MES'].quantile(0.75)  # > 16 unidades

# Limiar para "baixo preço": abaixo do Q1 de preço
baixo_preco = database_questao8['PRECO_UNITARIO'].quantile(0.25)  # < R$ 4,93
```

**Resultados:**

**Perfil 1 — Alto Volume + Baixo Preço (> 16 unidades · < R$ 4,93):**
- 37 produtos identificados
- Todos pertencem à seção **Papelaria**
- Produtos típicos: canetas, lápis, envelopes, borrachas
- Estratégia recomendada: gestão rigorosa de estoque para evitar ruptura

**Perfil 2 — Baixo Volume + Alto Preço (< 4 unidades · > R$ 89,90):**
- 36 produtos identificados
- Distribuídos entre **todas as seções** (Acessórios, Informática, Papelaria)
- Produtos típicos: monitores, notebooks, tablets, mochilas executivas
- Estratégia recomendada: gestão de capital imobilizado e prazo de reposição

**Insight estratégico:** Esses dois perfis exigem abordagens opostas. O Perfil 1 precisa de frequência de reabastecimento alta e margens baixas — o lucro vem do volume. O Perfil 2 precisa de ciclos de reposição longos e margens altas — o lucro vem do ticket. Tratar os dois da mesma forma é um erro estratégico.

> **Lição analítica:** O uso de quartis como limiar (em vez de médias) é mais robusto em distribuições assimétricas, pois não é afetado por valores extremos. Essa é uma escolha metodológica deliberada que demonstra maturidade analítica.

---

## Pré-processamento dos Dados

Neste projeto, o pré-processamento foi **minimalista e intencional** — o que, na prática, é um sinal positivo de qualidade dos dados originais.

### Verificações realizadas antes de qualquer análise

**Duplicatas:** `database['COD_PRODUTO'].duplicated().sum()` → 0 duplicatas. Como `COD_PRODUTO` é a chave única do dataset, duplicatas indicariam erro de coleta. Resultado: base íntegra.

**Valores ausentes:** `database.isna().sum()` → 0 nulos em todas as colunas. Resultado: sem necessidade de imputação ou remoção de registros.

### Feature Engineering: criação do `FATURAMENTO_BRUTO`

A principal decisão de engenharia de atributos foi a criação da métrica `FATURAMENTO_BRUTO` como produto de `PRECO_UNITARIO` e `QTD_UNIDADES_VENDIDAS_MES`:

```python
database['FATURAMENTO_BRUTO'] = (
    database['PRECO_UNITARIO'] * database['QTD_UNIDADES_VENDIDAS_MES']
)
```

**Justificativa técnica:** Nenhuma das variáveis originais responde sozinha à pergunta "qual produto gera mais valor?". O faturamento bruto é a métrica de síntese que o negócio realmente usa para tomar decisões. Criá-la explicitamente facilita a leitura do código, a reutilização em múltiplas análises e a auditoria por terceiros.

### Categorização de variáveis contínuas (binning)

Para a análise da Questão 3, variáveis contínuas foram transformadas em faixas categóricas usando `pd.cut()`:

```python
# Categorização de preço
database_questao3['PRECO_UNITARIO_FAIXAS'] = pd.cut(
    database_questao3['PRECO_UNITARIO'],
    bins=[0, Q1_preco, mediana_preco, Q3_preco, float('inf')],
    labels=['Muito Barato', 'Barato', 'Preço Médio', 'Caro']
)
```

**Justificativa:** Variáveis categóricas são mais fáceis de cruzar em tabelas de contingência e fornecem insights mais comunicáveis para gestores não-técnicos. O uso dos quartis como pontos de corte é preferível a limiares arbitrários, pois se adapta à distribuição real dos dados.

---

## Avaliação dos Resultados

Este projeto não envolve modelagem preditiva, portanto métricas como Accuracy, Precision, Recall ou ROC-AUC não se aplicam. A avaliação é feita pela **consistência analítica** e pela **relevância dos insights para o negócio**.

| Critério | Avaliação |
|---|---|
| Completude | Todas as 8 questões respondidas com código e narrativa |
| Rigor metodológico | Uso correto de agrupamentos, quartis, acumulados e IQR |
| Qualidade das conclusões | Insights acionáveis, conectados ao contexto de negócio |
| Engenharia de atributos | Feature `FATURAMENTO_BRUTO` criada e justificada |
| Tratamento de outliers | Identificados e contextualizados (não removidos cegamente) |

---

## Resultados do Projeto

### Síntese dos Principais Achados

| Análise | Resultado-chave | Implicação de negócio |
|---|---|---|
| Preço médio por categoria | Notebook Premium: R$ 5.216,63 | Informática domina o ticket médio |
| Faturamento por seção | Informática: 77,77% do total | Dependência crítica de uma seção |
| Relação preço × volume | Inversa — confirmada e segmentada | Papelaria e Informática têm lógicas opostas |
| Análise de Pareto | 49 produtos = 80% do faturamento | Foco em 16,9% do portfólio |
| Produtos sem venda | Múltiplos por seção com fat. = R$ 0 | Candidatos à revisão/descontinuação |
| Outliers de preço | Limite IQR superior: R$ 217 | Toda Informática é "outlier" — segmentar |
| Variabilidade por seção | Informática tem maior dispersão de preços | Portfólio heterogêneo = gestão complexa |
| Perfis de produto | 37 itens (vol alto/preço baixo) + 36 itens (vol baixo/preço alto) | Estratégias de estoque opostas |

### Limitações do Projeto

- **Escopo temporal:** Apenas um mês de dados. Sazonalidade, tendências e comparações históricas não são possíveis.
- **Ausência de custo:** Sem dados de custo de aquisição, não é possível calcular margem líquida — apenas receita bruta.
- **Sem dados de cliente:** Não há informação sobre quem compra o quê, impossibilitando análise de cesta de compras ou segmentação de clientes.
- **Faturamento bruto ≠ lucratividade:** Um produto caro pode ter margem zero se o custo de aquisição for alto.

---

## Conclusão

Este projeto demonstra que uma EDA bem executada vai muito além de calcular médias e gerar gráficos. Trata-se de um processo de **construção de narrativa analítica** — onde cada análise responde uma pergunta, cada pergunta conecta-se a uma decisão de negócio e cada decisão pode impactar resultados financeiros reais.

O case evidenciou um negócio com estrutura de faturamento altamente concentrada: uma seção (Informática) responde por quase 78% da receita, e 49 produtos (17% do portfólio) geram 80% do valor total. Esse padrão é típico do varejo e confirma a universalidade do princípio de Pareto.

Do ponto de vista acadêmico, o projeto exercita competências que são diretamente transferíveis para o mercado: leitura crítica de dados, criação de métricas de negócio, escolha apropriada de técnicas analíticas e comunicação de resultados para audiências não-técnicas.

---

## Tecnologias Utilizadas

| Tecnologia | Versão | Finalidade |
|---|---|---|
| Python | 3.13.1 | Linguagem principal |
| pandas | Última estável | Manipulação e análise de dados |
| numpy | Última estável | Operações matemáticas e estatísticas |
| Google Colab | — | Ambiente de desenvolvimento e execução |
| Jupyter Notebook | — | Formato de entrega do projeto |

---

## Como Executar o Projeto

### Pré-requisitos

- Python 3.8 ou superior instalado
- pip (gerenciador de pacotes do Python)

### Opção 1 — Google Colab (recomendado para iniciantes)

1. Acesse [colab.research.google.com](https://colab.research.google.com)
2. Faça upload do arquivo `ESTUDO_DE_CASO_EDA_Respostas.ipynb`
3. Faça upload do arquivo `Papelaria.txt` na sessão do Colab
4. Execute todas as células em ordem (`Runtime > Run all`)

### Opção 2 — Ambiente local

```bash
# 1. Clone ou baixe o repositório
git clone https://github.com/seu-usuario/case-papelaria-eda.git
cd case-papelaria-eda

# 2. Crie e ative um ambiente virtual (recomendado)
python -m venv venv
source venv/bin/activate       # Linux/macOS
venv\Scripts\activate          # Windows

# 3. Instale as dependências
pip install pandas numpy jupyter

# 4. Inicie o Jupyter Notebook
jupyter notebook

# 5. Abra o arquivo de respostas e execute as células em ordem
```

### Ordem de execução

1. **Carregamento de bibliotecas** — sempre primeiro
2. **Leitura da base de dados** — carrega e valida `Papelaria.txt`
3. **Questões 1 a 8** — executar na ordem sequencial (algumas questões dependem de variáveis criadas anteriormente)

---

## Boas Práticas Aplicadas

### Organização do código

Cada questão foi tratada como uma unidade independente, com variáveis nomeadas de forma descritiva (ex: `database_questao2`, `database_questao4_ordenada`). Isso evita efeitos colaterais entre análises e facilita a depuração.

### Comentários explicativos

Todos os blocos de código incluem comentários em português descrevendo **o que está sendo feito** e **por quê**. Isso não é burocracia — é o que diferencia código profissional de código que só o autor entende.

### Separação de responsabilidades

A criação de métricas derivadas (como `FATURAMENTO_BRUTO`) foi feita antes das análises, em células dedicadas. Isso evita recalcular a mesma operação múltiplas vezes e torna o código auditável.

### Uso de `.copy()` para isolamento de bases

```python
database_questao2 = database.copy()
```

Ao criar cópias explícitas antes de manipular os dados, o analista evita o problema clássico do `SettingWithCopyWarning` do pandas e garante que a base original permaneça intacta para as análises subsequentes.

### Reprodutibilidade

O notebook foi executado de forma linear, sem dependências ocultas entre células. Qualquer pessoa que executar o notebook do início ao fim obterá exatamente os mesmos resultados.

---

## Aprendizados Acadêmicos

### Competências desenvolvidas

**Hard Skills:**
- Leitura de arquivos com `pd.read_table()` e parâmetros específicos de formato
- Agregações com `groupby()` e `agg()` em múltiplos níveis
- Criação de métricas derivadas com operações vetorizadas
- Segmentação de dados com `pd.cut()` e `pd.qcut()`
- Cálculo de faturamento acumulado com `cumsum()`
- Detecção de outliers com o método IQR
- Análise de Pareto aplicada ao varejo
- Construção de tabelas de contingência com `pd.crosstab()`

**Soft Skills:**
- Tradução de perguntas de negócio em operações técnicas
- Comunicação de resultados para audiências não-técnicas
- Pensamento crítico na interpretação de padrões e anomalias
- Gestão de escopo analítico: responder exatamente o que foi perguntado

### Relação com o mercado real

Empresas como Magazine Luiza, Americanas, Grupo Boticário e grandes redes de varejo realizam análises como essas diariamente, em escala muito maior. Os conceitos de Pareto, segmentação por perfil e análise de faturamento por categoria são usados em reuniões de S&OP (Sales and Operations Planning) toda semana.

Um profissional que domina EDA está habilitado para atuar em posições como Analista de Dados, Business Intelligence Analyst, Revenue Analyst ou Customer Insights Analyst.

---

## Próximos Passos

Para quem quiser ir além deste case, as seguintes extensões naturais são recomendadas:

**Enriquecimento do dataset:**
- Incluir dados históricos de múltiplos meses para análise de tendência e sazonalidade
- Incorporar dados de custo de aquisição para calcular margem real (não apenas faturamento bruto)

**Modelagem preditiva:**
- Construir um modelo de previsão de demanda (regressão ou séries temporais) para antecipar necessidades de estoque
- Desenvolver um sistema de classificação de produtos por perfil de giro (ABC Curve)

**Visualização e comunicação:**
- Criar um dashboard interativo com Streamlit ou Power BI para que gestores não-técnicos acessem os insights
- Automatizar a geração do relatório mensal com Python e agendamento via cron job

**Engenharia e escala:**
- Migrar a análise para uma base de dados (PostgreSQL, BigQuery) para suportar volumes maiores
- Implementar um pipeline de dados com Apache Airflow para automação do fluxo analítico
- Containerizar o projeto com Docker para garantir reprodutibilidade em qualquer ambiente

---

*Material oficial elaborado pela Diretoria Acadêmica · Disciplina de Fundamentos de Data Science · Projeto de referência baseado no trabalho de maior desempenho da turma.*

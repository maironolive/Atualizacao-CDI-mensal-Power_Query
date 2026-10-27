# Consulta e Atualização do CDI Mensal com Power Query

Este projeto utiliza a **linguagem M do Power Query** para consultar os valores históricos do CDI (Certificado de Depósito Interbancário) no site [Melhor Câmbio](https://www.melhorcambio.com/cdi), tratar os dados e disponibilizá-los em formato tabular para utilização em uma planilha de investimentos.

O objetivo é automatizar a obtenção do CDI mensal, facilitando a comparação entre o rendimento de diferentes investimentos e o indicador de referência do mercado financeiro.

## Objetivo

Criar uma consulta no Power Query que obtenha os valores históricos do CDI mensal, organize as informações por período e permita atualizar os dados diretamente no Excel, sem a necessidade de inserir os valores manualmente.

## Funcionalidades

- Buscar os dados do CDI na página do Melhor Câmbio.
- Extrair os meses e os respectivos valores do CDI a partir do HTML da página.
- Converter os valores extraídos para números.
- Filtrar os registros a partir de 2015.
- Converter as datas e os valores para os tipos de dados apropriados.
- Criar colunas auxiliares para facilitar análises temporais.
- Organizar os dados em uma tabela pronta para utilização no Excel.
- Permitir a atualização da consulta por meio do Power Query.

## Tecnologias utilizadas

- **Power Query:** ferramenta de extração, transformação e carregamento de dados (ETL).
- **Linguagem M:** linguagem utilizada para construir a consulta e tratar os dados.
- **Microsoft Excel:** ambiente para carregar os dados e comparar os rendimentos dos investimentos.
- **Melhor Câmbio:** fonte utilizada para consultar o histórico do CDI.

## Fonte dos dados

Os dados são obtidos da seguinte página:

- [Histórico do CDI — Melhor Câmbio](https://www.melhorcambio.com/cdi)

A consulta acessa o conteúdo HTML da página e extrai os valores disponibilizados nas opções de seleção dos períodos.

**Importante:** a consulta depende da estrutura HTML do site. Alterações na página podem exigir ajustes no código M.

## Como funciona o código

### 1. Acesso à fonte de dados

A função `Web.Contents` acessa a página que contém os dados do CDI, enquanto `Text.FromBinary` converte o conteúdo recebido em texto para processamento.

### 2. Extração dos dados

O código identifica os elementos HTML `<option>` e extrai duas informações principais:

- `Mes`: período de referência do CDI.
- `CDI`: valor percentual correspondente ao período.

### 3. Tratamento dos valores

O código executa as seguintes operações:

- Remove quebras de linha e espaços desnecessários.
- Extrai o texto referente ao mês.
- Localiza e extrai o valor do CDI.
- Converte o valor para número.
- Remove registros com valores nulos.
- Converte a coluna de período para data.

### 4. Filtro histórico

A consulta mantém os registros a partir de 2015, interpretando o ano informado no sufixo do período.

Esse tratamento permite trabalhar com um histórico de CDI mais adequado para análises de investimentos de longo prazo.

### 5. Criação de colunas auxiliares

Além das colunas originais, o código prepara informações para facilitar a análise temporal:

- `Ano`: ano de referência.
- `Mes_nome`: nome do mês.
- `MesAno`: combinação do nome do mês com o ano.

A tabela final mantém as colunas `Ano`, `Mes`, `Mes_nome` e `CDI`.

## Estrutura dos dados

A consulta retorna uma tabela organizada no seguinte formato:

| Ano | Mes | Mes_nome | CDI |
|---|---|---|---:|
| 2024 | 01/01/2024 | janeiro | Valor obtido na fonte |
| 2024 | 01/02/2024 | fevereiro | Valor obtido na fonte |
| 2024 | 01/03/2024 | março | Valor obtido na fonte |

*Os valores apresentados acima são apenas ilustrativos. Os resultados reais dependem dos dados disponibilizados pela fonte no momento da atualização.*

## Como utilizar no Excel

### 1. Criar a consulta

1. Abra o Excel.
2. Acesse **Dados > Obter Dados > De Outras Fontes > Consulta Nula**, conforme as opções disponíveis na sua versão.
3. Abra o **Editor Avançado** do Power Query.
4. Cole o código M da consulta.
5. Clique em **Concluído**.
6. Aguarde a execução e verifique os dados retornados.

### 2. Carregar os dados

1. No Editor do Power Query, clique em **Fechar e Carregar**.
2. Selecione a forma de carregamento desejada.
3. Carregue os dados em uma tabela do Excel.

### 3. Atualizar o CDI

Para atualizar os dados manualmente:

1. Abra a planilha.
2. Acesse a guia **Dados**.
3. Clique em **Atualizar Tudo**.

A consulta buscará novamente as informações disponíveis na fonte e atualizará a tabela conforme o resultado obtido.

A atualização automática também pode ser configurada nas propriedades da consulta ou integrada a uma rotina de automação com PowerShell e o Agendador de Tarefas do Windows.

## Aplicação na análise de investimentos

Com o histórico do CDI carregado no Excel, é possível utilizá-lo como referência para comparar o desempenho de investimentos.

### Exemplos de análises

- Comparar o rendimento mensal de investimentos com o CDI do mesmo período.
- Calcular o percentual do CDI alcançado por um investimento.
- Analisar o desempenho acumulado de aplicações financeiras.
- Construir gráficos comparativos de rentabilidade.
- Criar indicadores e painéis de acompanhamento de investimentos.

### Exemplo de comparação

Um investimento que rende 110% do CDI tem uma remuneração vinculada ao indicador, conforme as regras do produto financeiro.

Para comparar corretamente os resultados, é importante utilizar o CDI correspondente ao mesmo período de análise e considerar a forma de capitalização, os impostos, as taxas e as condições de cada investimento.

**Observação:** o código M deste projeto obtém e organiza os valores mensais do CDI. Os cálculos de rentabilidade dos investimentos devem ser implementados separadamente na planilha ou em outras consultas.

## Atualização automática

Este projeto pode ser combinado com uma rotina de automação para reduzir a necessidade de intervenção manual.

Uma possibilidade é utilizar:

- **Power Query:** consulta e tratamento dos dados.
- **Excel:** armazenamento e análise das informações.
- **PowerShell:** execução automatizada da atualização da planilha.
- **Agendador de Tarefas do Windows:** definição da frequência e do horário de execução.

O funcionamento depende da disponibilidade da fonte de dados, das configurações do Excel e das permissões do ambiente.

## Limitações e considerações

- A consulta depende da disponibilidade do site Melhor Câmbio.
- Mudanças na estrutura HTML podem interromper a extração.
- A atualização exige acesso à internet.
- Os valores retornados dependem das informações disponibilizadas pela fonte.
- É importante validar os dados após a atualização.
- O CDI utilizado na comparação deve corresponder ao período correto.
- Os resultados da análise não representam garantia de rentabilidade futura.

## Estrutura sugerida do repositório

```text
cdi-power-query/
├── README.md
├── consultas/
│   └── CDI_Mensal.pq
└── .gitignore
```

O arquivo `CDI_Mensal.pq` pode armazenar o código M em formato de texto para facilitar o versionamento e o acompanhamento das alterações pelo Git.

## Possíveis melhorias

- Automatizar o carregamento dos dados no Excel.
- Integrar a consulta com uma rotina PowerShell.
- Criar indicadores de rentabilidade em relação ao CDI.
- Desenvolver gráficos de evolução mensal e acumulada.
- Adicionar validações para identificar falhas na extração.
- Registrar a data e a hora da última atualização.
- Implementar tratamento para alterações na estrutura da fonte.

## Licença

Defina uma licença para o projeto conforme a finalidade e as condições de uso desejadas.

## Autor

Projeto desenvolvido para automatizar a obtenção do CDI mensal e facilitar a comparação de rendimentos de investimentos utilizando Power Query e Microsoft Excel.

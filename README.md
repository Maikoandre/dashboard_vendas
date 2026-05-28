# 📊 Dashboard de Vendas — Power BI Project (PBIP)

[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen?style=for-the-badge)](https://github.com/)
[![Format](https://img.shields.io/badge/Format-PBIP%20%7C%20TMDL-blue?style=for-the-badge)](https://learn.microsoft.com/en-us/power-bi/developer/projects/pvf-dataset)

Um dashboard corporativo de inteligência de vendas desenvolvido no **Power BI Desktop**.

---

## 🗺️ Visão Geral do Dashboard

O painel foi projetado para fornecer uma visão analítica abrangente sobre o desempenho comercial de vendas, permitindo o acompanhamento de faturamento, margem de lucro, volume de vendas e comportamento de clientes por marcas, regiões e períodos de tempo.

A interface visual é construída sobre um layout dinâmico e integrado com um **Plano de Fundo personalizado** (`Plano de Fundo Vendas.png`), garantindo um design premium, limpo e focado na usabilidade (UX).

---

## 📈 Principais Métricas & Indicadores (KPIs)

O painel é composto por **4 cartões principais de indicadores (KPIs)** no topo da página e **3 visuais de detalhamento analítico**:

### 📊 Indicadores Principais (Cards)
*   **💰 Faturamento Total**: Soma acumulada do faturamento bruto das vendas (`Faturamento`).
*   **📈 Lucro Total**: Soma acumulada da margem de lucro líquido das operações (`Lucro Venda`).
*   **📦 Qtd. Vendida**: Volume total de unidades de produtos vendidas no período (`Qtd. Vendida`).
*   **👥 Qtd. Clientes**: Contagem distinta de clientes únicos atendidos (`Codigo Cliente`).

### 🔍 Visuais de Detalhamento Analítico
1.  **📉 Faturamento Mensal (Gráfico de Área)**: Análise temporal da evolução do faturamento bruto ao longo dos meses para identificar tendências, sazonalidade e picos de vendas.
2.  **📊 Faturamento por Marca (Gráfico de Barras)**: Ranking das marcas mais vendidas, facilitando a identificação dos principais fornecedores e parceiros de negócio.
3.  **🗺️ Distribuição Geográfica (Mapa)**: Exibição interativa do faturamento por continente (`Continente`), demonstrando o alcance territorial da empresa.

---

## 🗂️ Estrutura do Modelo de Dados (Data Model)

A tabela principal de fatos é a **`Vendas`**, alimentada a partir de uma planilha Excel externa. Abaixo estão os detalhes dos campos que compõem o modelo semântico:

| Nome do Campo | Tipo de Dado | Formatação | Função Analítica / Descrição |
| :--- | :--- | :--- | :--- |
| **Data da Venda** | `DateTime` | Long Date | Data da transação (Relacionada à tabela de Calendário local). |
| **Produto** | `String` | Texto | Nome/Modelo do produto vendido. |
| **Categoria** | `String` | Texto | Segmento ou categoria de mercado do produto. |
| **Codigo Cliente** | `Int64` | Inteiro | Identificador único do cliente (utilizado para contagem distinta). |
| **PrecoUnitario** | `Double` | Geral | Preço de venda unitário do produto. |
| **Custo Unitário** | `Double` | Geral | Custo de aquisição/produção unitário do produto. |
| **Marca** | `String` | Texto | Fabricante/Marca do produto. |
| **Qtd. Vendida** | `Int64` | Inteiro | Quantidade de itens adquiridos na transação. |
| **Faturamento** | `Double` | Monetário (`R$ #,0.00`) | Receita bruta obtida na venda (Qtd. Vendida * Preço Unitário). |
| **Custo Venda** | `Double` | Geral | Custo total da venda (Qtd. Vendida * Custo Unitário). |
| **Lucro Venda** | `Double` | Monetário (`R$ #,0.00`) | Lucro líquido obtido (Faturamento - Custo Venda). |
| **País** | `String` | Texto | País onde a venda foi realizada. |
| **Continente** | `String` | Texto | Continente de destino da venda. |
| **Tipo da Venda** | `String` | Texto | Canal de distribuição/venda (ex: Físico, E-commerce, Atacado). |

---

## 🔄 Fluxo de ETL (Power Query)

O processo de extração, transformação e carga (ETL) é executado nativamente pelo Power Query com a seguinte lógica configurada na tabela `Vendas`:

1.  **Origem**: Conexão com planilha local do Excel (`Vendas.xlsx`).
2.  **Seleção**: Leitura da aba `Vendas`.
3.  **Promover Cabeçalhos**: Primeira linha convertida em cabeçalhos de coluna.
4.  **Tipagem de Dados**: Definição rigorosa dos tipos de dados para otimização de performance (inteiros, decimais, texto, datas).

---

## 🛠️ Arquitetura do Projeto (Power BI Developer Mode)

Este projeto foi salvo usando o moderno formato **Power BI Project (.pbip)**. A estrutura de arquivos permite versionar o modelo semântico e o relatório separadamente em formato de texto limpo:

*   **`Dashboard_Vendas.pbip`**: O arquivo de entrada principal que orquestra a abertura do projeto no Power BI Desktop.
*   **📂 `Dashboard_Vendas.SemanticModel`**: Contém a definição do modelo de dados.
    *   **`definition.pbism`**: Configuração básica do modelo semântico.
    *   **`definition/`**: Estrutura em formato **TMDL (Tabular Model Definition Language)**, dividindo as definições em arquivos de texto legíveis para humanos (`model.tmdl`, `tables/Vendas.tmdl`, `relationships.tmdl`). Isso facilita a revisão de código (*code review*) e mesclagem de ramificações (*merge*) no Git.
*   **📂 `Dashboard_Vendas.Report`**: Armazena o layout visual e as definições de tela.
    *   **`definition.pbir`**: Configuração de ligação do relatório ao modelo semântico correspondente.
    *   **`definition/report.json` e `pages/`**: Especificações em JSON de cada página e visual do relatório (incluindo cores, tamanhos, fontes e imagens de fundo registradas).

---
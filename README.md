🌐 *Read this documentation in English: [README_EN.md](./README_EN.md)*

---

# 🛒 E-Commerce Data Pipeline | Azure Databricks & Medallion Architecture

Este projeto consiste na construção de uma pipeline de engenharia de dados end-to-end utilizando a **Arquitetura Medallion** (Raw, Bronze, Silver e Gold) para processar e analisar dados de e-commerce. A solução foi desenvolvida no **Azure Databricks** utilizando **PySpark** e **Delta Lake**, integrada ao **Azure Data Lake Storage Gen2 (ADLS Gen2)**.

---

## 🏗️ Arquitetura do Projeto

O fluxo de dados segue a estrutura em camadas para garantir governança, qualidade e alta performance no consumo de analytics:

1. **Camada Raw (ADLS Gen2):** Armazenamento bruto dos arquivos fonte em formato CSV enviados ao Data Lake.
2. **Camada Bronze (Delta Lake):** Ingestão dos dados no formato Delta Lake preservando a estrutura original sem alterações de esquema.
3. **Camada Silver (Delta Lake):** Processamento, tratamento de dados nulos, deduplicação de registros e padronização de tipos de dados.
4. **Camada Gold (Delta Lake):** Agregação de dados orientada ao negócio (KPIs de faturamento, volume de pedidos por país e perfil de gasto dos clientes).

---

## 🛠️ Tecnologias Utilizadas

* **Nuvem:** Microsoft Azure (Azure Data Lake Storage Gen2)
* **Processamento de Dados:** Azure Databricks, PySpark, Spark SQL
* **Formato de Armazenamento:** Delta Lake
* **Linguagem:** Python

---

## 📁 Estrutura dos Notebooks

* `01_Ingestao_Bronze.py`: Conexão com o ADLS Gen2, leitura do arquivo bruto CSV e gravação inicial na camada Bronze em formato Delta.
* `02_Transformacao_Silver.py`: Leitura da camada Bronze, limpeza de registros inválidos (`InvoiceNo` e `CustomerID` nulos), conversão de data/hora e gravações na camada Silver.
* `03_Agregacao_Gold.py`: Leitura dos dados tratados na Silver e geração das visões analíticas de negócio (faturamento por país e métricas de clientes).

---

## 🔒 Nota de Segurança e Boas Práticas

Por questões de segurança e boas práticas de **DevSecOps**, as chaves de acesso (`Storage Account Access Keys`) foram omitidas dos notebooks públicos deste repositório. Em ambientes produtivos, recomenda-se a utilização do **Azure Key Vault** integrado ao **Databricks Secrets** para gerenciar credenciais com segurança.

---

## 🚀 Como Executar este Projeto

1. Crie uma **Storage Account** no Azure habilitada para **Data Lake Storage Gen2** com os contêineres `raw`, `bronze`, `silver` e `gold`.
2. Configure um workspace no **Azure Databricks** e crie um cluster de computação.
3. Importe os notebooks da pasta deste repositório para o seu workspace no Databricks.
4. Insira suas credenciais de acesso do Azure no parâmetro `storage_account_access_key` (ou configure os Databricks Secrets).
5. Execute os notebooks sequencialmente (`01` ➔ `02` ➔ `03`).

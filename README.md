# Pipeline ETL: Processamento de Vendas e Integração Google Sheets

Este projeto implementa um pipeline de dados automatizado (ETL) desenvolvido em Python para a ingestão, tratamento e exportação de dados de vendas provenientes de marketplaces. O sistema converte relatórios brutos em uma base de dados estruturada e atualizável no Google Sheets, ideal para alimentação de ferramentas de Business Intelligence como Power BI e Looker Studio.



## Arquitetura do Sistema

O pipeline é estruturado em três camadas lógicas para garantir a integridade dos dados:

1. **Extração (Extract):** Leitura de arquivos CSV com suporte a codificação Latin-1 e delimitadores customizados, garantindo compatibilidade com sistemas legados de marketplaces.
2. **Transformação (Transform):** Camada de limpeza que utiliza expressões regulares (Regex) para normalizar valores monetários, conversão de tipos de dados (strings para float/datetime) e padronização de nomenclatura de colunas para o formato Snake Case.
3. **Carga (Load):** Integração via API para persistência dos dados, utilizando lógica de verificação de cabeçalho para evitar duplicidade e garantir a continuidade histórica dos registros.

## Funcionalidades Técnicas

* **Normalização Financeira:** Conversão automática de formatos monetários brasileiros (Ex: "R$ 1.250,00") para formato numérico computacional (1250.00).
* **Mapeamento de Schema:** Tradução de colunas de origem para nomes padronizados, facilitando a manutenção e consultas SQL posteriores.
* **Append Inteligente:** Identificação automática da última linha preenchida na planilha de destino para inserção de novos dados sem sobreposição.
* **Auditabilidade:** Inclusão automática da coluna `data_carga` para rastreio cronológico das atualizações.
* **Tratamento de Exceções:** Logs de erro para falhas de leitura, arquivos corrompidos ou problemas de autenticação com a Service Account do Google.

## Tecnologias Utilizadas

* **Python 3.x**
* **Pandas:** Manipulação e estruturação de grandes volumes de dados.
* **Gspread:** Biblioteca de interface para a API do Google Sheets.
* **Google Cloud Platform:** Gerenciamento de credenciais e acesso via Service Account.

## Instalação e Dependências

Instale as bibliotecas necessárias via pip:

```bash
pip install pandas gspread

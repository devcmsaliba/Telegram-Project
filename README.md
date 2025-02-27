# Pipeline de Dados para Telegram

![arch](https://github.com/user-attachments/assets/b6b8c5c0-1f11-40bb-936e-932ac147053e)

Este projeto tem como objetivo criar um pipeline de dados para coletar mensagens de um grupo do Telegram, armazená-las na AWS, realizar transformações e análises, e apresentar resultados.

## 1. **Configuração do Telegram**
   - Crie um grupo no Telegram e adicione um bot para captar as mensagens.
   - O bot coleta mensagens via **API do Telegram** (formato JSON).
   - Configure um **webhook** para redirecionar as mensagens para uma API web.

## 2. **Ingestão de Dados com AWS**
   - **API Gateway**: Recebe as mensagens do Telegram via webhook.
   - **Lambda**: Processa as mensagens e as armazena em um bucket **S3** (zona "raw").
   - **S3**: Armazena as mensagens em formato **JSON**.

## 3. **ETL (Extração, Transformação e Carga)**
   - **S3 (Enriched)**: Armazena os dados processados em formato **Parquet**.
   - **Lambda (ETL)**: Processa as mensagens de um dia, realiza transformações (data wrangling) e as armazena em S3.
   - **EventBridge**: Aciona a função Lambda de ETL diariamente.

## 4. **Análise com AWS Athena**
   - **Athena**: Utiliza consultas SQL para acessar dados armazenados no S3 (camada "enriched").
   - Criação de tabelas externas para consulta de dados via SQL, com **partições diárias** (por data).

## 5. **Apresentação dos Resultados**
   - Relatórios e insights podem ser gerados, como:
     - Quantidade de mensagens por dia e por usuário.
     - Tamanho médio das mensagens.
     - Quantidade de mensagens por hora ou dia da semana.

## **Resumo das Ferramentas Utilizadas**
   - **AWS S3**: Armazenamento de dados em formato bruto e enriquecido.
   - **AWS Lambda**: Processamento e transformação dos dados.
   - **API Gateway**: Recebe dados via webhook.
   - **AWS EventBridge**: Agendamento de tarefas diárias.
   - **AWS Athena**: Execução de consultas SQL para análise de dados.

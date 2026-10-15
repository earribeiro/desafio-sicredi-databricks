\# Desafio da Sicredi para Analista Pleno



\## Visão geral



Projeto desenvolvido no Databricks, utilizando PySpark, Spark SQL e Delta Lake para implementar um pipeline baseado nas três arquiteturas: (Bronze, Silver e Gold).



O cenário simula o processamento de dados financeiros, considerando problemas de duplicidade, inconsistências cadastrais, registros inválidos, estornos e transações recebidas com atraso.



\## Objetivos



\- Construir um pipeline de ingestão, tratamento e disponibilização de dados.

\- Aplicar validações de qualidade e integridade referencial.

\- Identificar duplicidades e encaminhar registros inválidos para quarentena.

\- Processar transações financeiras e estornos.

\- Disponibilizar indicadores analíticos na camada Gold.

\- Demonstrar processamento incremental e idempotência com Delta Lake.

\- Implementar testes automatizados de qualidade.



\## Tecnologias utilizadas



\- Databricks

\- Apache Spark e PySpark

\- Spark SQL

\- Delta Lake

\- Python

\- Git e GitHub



\## Arquitetura:



\*\*Bronze — Inserção de Dados\*\*



Recebe os dados de origem e preserva informações de rastreabilidade, incluindo o arquivo de origem. Mantém registros recebidos, inclusive duplicidades.



\*\*Silver — Tratamento dos Dados em duplicidade\*\*



Realiza conversão de tipos, deduplicação, validação cadastral, integridade referencial e tratamento de transações e estornos. Registros rejeitados são direcionados para tabelas de quarentena.



\*\*Gold — Análise\*\*



Disponibiliza dados consolidados para consultas e indicadores de negócio.



Principais tabelas:



\- 'gold\_transacoes\_cartao'

\- 'gold\_resumo\_cliente\_mes'

\- 'gold\_ranking\_estabelecimento'

\- 'gold\_alertas\_qualidade'



\## Organização do projeto



Os notebooks estão disponíveis no diretório 'notebooks/'.



Os arquivos mantêm a nomenclatura utilizada durante o desenvolvimento no Databricks.



\## Regras de qualidade



As principais verificações implementadas incluem:



\- Validação de clientes e documentos cadastrais.

\- Verificação de contas e cartões associados a entidades válidas.

\- Rejeição de valores financeiros inválidos.

\- Validação de datas de transação.

\- Deduplicação por identificadores de negócio.

\- Tratamento de estornos.

\- Verificação de integridade entre Silver e Gold.



\## Processamento incremental



O projeto demonstra o uso de 'MERGE INTO' para inserir e atualizar registros sem duplicar transações durante o reprocessamento.
\## Consultas analíticas

O projeto explora funções de janela e técnicas SQL para deduplicação, classificação, ranking e análise de evolução mensal.



A demonstração de crescimento entre setembro e outubro utiliza uma tabela complementar de teste, separada do fluxo transacional principal.



\## Resultados dos testes



Na última execução validada:



| Indicador | Resultado |

|---|---:|

| Registros Bronze de transações | 10 |

| Transações válidas Silver | 6 |

| Transações Gold | 6 |

| Valor líquido consolidado | R$ 1.450,00 |

| Registros rejeitados na carga inicial | 10 |

| Testes automatizados | 6 aprovados |



Os valores apresentados correspondem à massa fictícia utilizada no desenvolvimento e podem variar em novas execuções.



\## Como executar



1\. Disponibilizar um ambiente Databricks com suporte a Unity Catalog e Delta Lake.

2\. Criar ou configurar o catálogo e schema utilizados pelo projeto.

3\. Importar os notebooks do diretório 'notebooks/'.

4\. Executar a geração da massa fictícia e a ingestão Bronze.

5\. Executar as transformações Silver e as validações de qualidade.

6\. Construir as tabelas analíticas Gold.

7\. Executar os cenários de processamento incremental.

8\. Executar os testes automatizados.



\*\*Configuração utilizada no desenvolvimento:\*\* catálogo 'workspace' e schema 'desafio\_sicredi'.

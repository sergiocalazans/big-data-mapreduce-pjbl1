# Big Data — Análise de Transações Comerciais com Hadoop MapReduce

![Java](https://img.shields.io/badge/Java-MapReduce-orange)
![Apache Hadoop](https://img.shields.io/badge/Apache%20Hadoop-MapReduce-FFDC00?logo=apachehadoop&logoColor=black)

## 📌 Sobre o projeto

Projeto acadêmico desenvolvido **em equipe de três integrantes** para o **PjBL 1 da disciplina de Big Data**, cursada no **4º período de Ciência da Computação da Pontifícia Universidade Católica do Paraná (PUCPR)**.

O objetivo é aplicar o modelo de programação **MapReduce**, utilizando **Java e Apache Hadoop**, ao processamento de uma base de transações comerciais internacionais. O conjunto de dados descrito no enunciado possui **mais de 8 milhões de registros** e abrange aproximadamente **30 anos** de operações.

O trabalho explora técnicas de processamento distribuído, filtragem, agrupamento, agregação, ordenação e composição de tarefas, com foco em consultas analíticas sobre comércio internacional e operações envolvendo o Brasil.

## 🎓 Contexto acadêmico

- **Instituição:** Pontifícia Universidade Católica do Paraná (PUCPR)
- **Curso:** Ciência da Computação
- **Período:** 4º período
- **Disciplina:** Big Data
- **Atividade:** PjBL 1 — MapReduce
- **Modalidade:** Trabalho em equipe

## 🎯 Objetivos

- Compreender e aplicar o fluxo **Mapper → Shuffle/Sort → Reducer**.
- Processar grandes volumes de registros estruturados em arquivos CSV.
- Realizar contagens, médias, mínimos e máximos por diferentes dimensões.
- Utilizar **tipos `Writable` customizados** para transportar valores compostos.
- Aplicar **`Combiner`** quando exigido para agregações intermediárias.
- Encadear **Jobs MapReduce** para obter resultados ordenados.
- Tratar cabeçalhos e registros com campos ausentes ou inválidos.

## 🗃️ Conjunto de dados

A entrada consiste em um arquivo **CSV delimitado por ponto e vírgula (`;`)**, com dez colunas:

| Coluna | Descrição |
| --- | --- |
| `country` | País envolvido na transação |
| `year` | Ano da transação |
| `commodity_code` | Código da mercadoria |
| `commodity` | Descrição da mercadoria |
| `flow` | Tipo de fluxo, como `Export` ou `Import` |
| `price` | Preço em dólares americanos |
| `weight` | Peso da mercadoria |
| `unit` | Unidade de medida |
| `amount` | Quantidade da mercadoria |
| `category` | Categoria da mercadoria |

## 🧩 Desafios do PjBL 1

O enunciado propõe **nove consultas analíticas**:

| Item | Análise solicitada | Requisito técnico específico |
| :---: | --- | --- |
| 1 | Quantidade de transações envolvendo o Brasil | Contagem com MapReduce |
| 2 | Quantidade de transações por ano | Agrupamento por ano |
| 3 | Quantidade de transações por categoria | Agrupamento por categoria |
| 4 | Quantidade de transações por tipo de fluxo | Agrupamento por `flow` |
| 5 | Valor médio das transações por ano no Brasil | `Writable` customizado |
| 6 | Transação mais cara e mais barata no Brasil em 2016 | `Combiner` e `Writable` customizado |
| 7 | Valor médio anual das exportações brasileiras | `Combiner` e `Writable` customizado |
| 8 | Valor máximo anual das transações brasileiras, em ordem decrescente | Encadeamento de Jobs |
| 9 | Maior e menor valor da coluna `amount` por ano e país | `Comparable Writable` e `Combiner` |

## ⚙️ Como funciona o MapReduce

```text
Arquivo CSV
    │
    ▼
Leitura e validação dos registros
    │
    ▼
Mapper — filtragem e emissão de pares (chave, valor)
    │
    ▼
Combiner — agregação local, quando aplicável
    │
    ▼
Shuffle / Sort — agrupamento por chave
    │
    ▼
Reducer — agregação final
    │
    ▼
Arquivos de saída (part-r-*)
```

### Recursos explorados

**Writable customizado:** estrutura serializável própria para transportar mais de uma informação numérica, por exemplo soma e quantidade para cálculo de média, ou mínimo e máximo para comparação de transações.

**Combiner:** redução intermediária do volume de dados transferidos entre as etapas do processamento. Deve ser usado somente em operações que preservem a correção da agregação.

**Encadeamento de Jobs:** execução de uma etapa de agregação seguida por outra etapa de ordenação, quando a consulta exige resultados ordenados por valor.

**Comparable Writable:** implementação de tipo comparável para representar chaves ou valores compostos de acordo com os requisitos da consulta.

## 🛠️ Tecnologias

- **Java** — implementação dos Mappers, Reducers e estruturas auxiliares.
- **Apache Hadoop MapReduce** — processamento distribuído e execução dos Jobs.
- **Hadoop Distributed File System (HDFS)** — armazenamento de entrada e saída quando utilizado no ambiente de execução.
- **CSV** — formato da base de transações comerciais.

## ▶️ Execução

A execução depende da organização das classes Java, do pacote compilado e da configuração do Hadoop no ambiente utilizado.

[Link para download do CSV](https://drive.google.com/file/d/1N0xJ8YnlsS8BhvtiFc_KrotglyFrelFV/view)

Fluxo geral de execução:

1. Preparar o ambiente Java e Hadoop compatível com o projeto.
2. Disponibilizar o CSV de entrada no sistema de arquivos utilizado pelo Hadoop.
3. Compilar as classes Java e gerar o artefato executável do projeto.
4. Executar o Job correspondente a cada análise, informando os diretórios de entrada e saída.
5. Conferir os arquivos `part-r-*` gerados e comparar os resultados com os requisitos.

> **A completar com o código do repositório:** comandos exatos de compilação, nomes das classes principais, argumentos de execução e caminhos de entrada/saída. Não foram incluídos comandos fictícios para evitar instruções incorretas.

## ✅ Cuidados com os dados

Conforme os critérios do PjBL 1:

- Ignorar o cabeçalho do CSV durante o processamento.
- Tratar registros com campos faltantes ou inválidos.
- Evitar concatenar strings para representar chaves ou valores compostos, utilizando tipos apropriados.
- Registrar os resultados de cada consulta em arquivos `.txt` separados, conforme solicitado na atividade.

## 📚 Aprendizados

O projeto proporciona experiência prática com:

- Processamento de grandes conjuntos de dados.
- Programação distribuída com MapReduce.
- Serialização e comparação de dados em Java.
- Agregações estatísticas e tratamento de registros.
- Planejamento de Jobs e análise de resultados.
- Desenvolvimento colaborativo e organização de entregas acadêmicas.

## 👥 Equipe

Projeto desenvolvido **colaborativamente**.

- [Glaucia Araujo](https://github.com/Glaucia05)
- [Nicolly Cordeiro](https://github.com/ly-ubimyy)
- [Sergio Calazans](https://github.com/sergiocalazans)




# aula-manual-de-dados
# Manual de SQL e Conexão com PostgreSQL usando Java

## 1. Conceitos Básicos

- **Campo**: Um campo é uma unidade de dados dentro de uma tabela. Cada campo tem um nome e um tipo de dados que define o tipo de valor que pode ser armazenado (como texto, número, data, etc.).
  
- **Tabela**: A tabela é uma coleção de campos organizados em linhas e colunas. As tabelas são usadas para armazenar dados em um banco de dados.

- **Linha**: Uma linha (ou tupla) representa uma entrada na tabela. Cada linha contém valores para cada um dos campos definidos na tabela.

- **Coluna**: Uma coluna representa uma característica ou atributo de uma entidade. Cada coluna tem um nome e um tipo de dados.

## 2. Tipos de Dados no Banco de Dados

Os tipos de dados no PostgreSQL incluem:

- `INTEGER`: Números inteiros.
- `VARCHAR(n)`: Texto com até 'n' caracteres.
- `TEXT`: Texto sem limite de tamanho.
- `BOOLEAN`: Valores `TRUE` ou `FALSE`.
- `DATE`: Datas (formato YYYY-MM-DD).
- `TIMESTAMP`: Data e hora (formato YYYY-MM-DD HH:MI:SS).
- `DECIMAL`: Números decimais com precisão definida.

## 3. Conexão em Java com PostgreSQL

### Arquivo `pom.xml`

Para usar o PostgreSQL no Java com Maven, inclua a dependência do driver JDBC no seu `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <version>42.2.23</version>
    </dependency>
</dependencies>

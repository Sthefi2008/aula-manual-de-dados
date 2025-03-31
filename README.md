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
```
### Código para conexão com o banco de dados PostgreSQL
```java
import java.sql.Connection;
import java.sql.DriverManager;

public class ConexaoPostgreSQL {
    public static Connection conectar() throws Exception {
        String url = "jdbc:postgresql://localhost:5432/seu_banco";
        String usuario = "postgres";
        String senha = "sua_senha";
        return DriverManager.getConnection(url, usuario, senha);
    }
}
```

---

## 🏗️ Comandos SQL Essenciais

### Criar Banco de Dados
```sql
CREATE DATABASE exemplo_db;
```

### Excluir Banco de Dados
```sql
DROP DATABASE exemplo_db;
```

### Criar Tabela
```sql
CREATE TABLE usuarios (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(150)
);
```

### Excluir Tabela
```sql
DROP TABLE usuarios;
```

### Executar com Java
```java
try {
  Connection conn = ConexaoPostgreSQL.conectar();
  var stmt = conn.createStatement();
  stmt.executeUpdate("CREATE TABLE exemplo (id SERIAL PRIMARY KEY, nome VARCHAR(50))");
  System.out.println("Tabela criada com sucesso!");
}catch(Exception ex){
  System.out.println(ex.getMessage());
}
```

---

## 🗑️ Comando TRUNCATE TABLE
```sql
TRUNCATE TABLE usuarios;
```
### Executar com Java
```java
try {
  Connection conn = ConexaoPostgreSQL.conectar();
  Statement stmt = conn.createStatement();
  stmt.executeUpdate("TRUNCATE TABLE usuarios");
  System.out.println("Tabela truncada!");
}catch(Exception ex){
  System.out.println(ex.getMessage());
}
```

---

## 📥 Comando INSERT
```sql
INSERT INTO usuarios (nome, email) VALUES ('João Silva', 'joao@email.com');
```
### Executar com Java
```java
try {
  Connection conn = ConexaoPostgreSQL.conectar();
  Statement stmt = conn.prepareStatement("INSERT INTO usuarios (nome, email) VALUES (?, ?)");
  stmt.setString(1, "Maria Souza");
  stmt.setString(2, "maria@email.com");
  stmt.executeUpdate();
  System.out.println("Usuário inserido com sucesso!");
}catch(Exception ex){
  System.out.println(ex.getMessage());
}
```

---

## 🔎 Comando SELECT
```sql
SELECT * FROM usuarios;
```
### Executar com Java e Exibir no Console
```java
try {
  Connection conn = ConexaoPostgreSQL.conectar();
  Statement stmt = conn.createStatement();
  ResultSet rs = stmt.executeQuery("SELECT * FROM usuarios");
  while (rs.next()) {
    System.out.println("ID: " + rs.getInt("id") + ", Nome: " + rs.getString("nome") + ", Email: " + rs.getString("email"));
  }
}catch(Exception ex){
  System.out.println(ex.getMessage());
}
```

---

## 🖼️ Exibindo Dados em JTable no Java

```java
  String[] colunas={ "Nome", "Salário", "Nascimento", "Data Cadastro"};
  DefaultTableModel model = new DefaultTableModel(colunas, 0);
  model.addRow(new Object[]{"Marcelo","28000,50","1979-11-21","2025-03-24"});
  jTable1.setModel(model);
```

ou 
```java
Object[] coluna=new Object[4];
coluna[0] = "Nome";
coluna[1] = "Salário";
coluna[2] = "Nascimento";
coluna[3] = "Data Cadastro";

Object[][] usuario=new Object[10][4];
usuario[0][0]="Marcelo";
usuario[0][1]="28000,50";
usuario[0][2]="1979-11-21";
usuario[0][3]="2025-03-24";

jTable1.setModel(new DefaultTableModel(usuario,coluna));

```

### Exemplo de Exibição com JTable
```java
import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import java.sql.*;

//...
try {
    Connection conn = ConexaoPostgreSQL.conectar();
    var stmt = conn.createStatement();
    var rs = stmt.executeQuery("SELECT * FROM usuarios");
    String[] colunas = {"ID", "Nome", "Email"};
    DefaultTableModel model = new DefaultTableModel(colunas, 0);
    while (rs.next()) {
        model.addRow(new Object[]{rs.getInt("id"), rs.getString("nome"), rs.getString("email")});
    }
    JTable table = new JTable(model);
    JOptionPane.showMessageDialog(null, new JScrollPane(table));
}catch(Exception ex){
  System.out.println(ex.getMessage());
}
```

---

### Exemplo de DELETE
```java
//...
try {
    int id = 1; 
    String comando = "DELETE FROM veiculos WHERE id = ?";
    PreparedStatement pstmt;
    pstmt = conexao.prepareStatement(comando);
    pstmt.setInt(1, id);
    pstmt.executeUpdate();
    JOptionPane.showMessageDialog(this, "Apagado com sucesso");
} catch (Exception e) {
    JOptionPane.showMessageDialog(this, "Erro ao apagar");
}
```
exemplo 2

```java
try {
    String id_ = jLabel1.getText();
    int id = Integer.parseInt(id_);
    String comando = "DELETE FROM veiculos WHERE id = ?";
    PreparedStatement pstmt;
    pstmt = conexao.prepareStatement(comando);
    pstmt.setInt(1, id);
    pstmt.executeUpdate();
    JOptionPane.showMessageDialog(this, "Apagado com sucesso");
    jButton5.doClick();
} catch (Exception e) {
    JOptionPane.showMessageDialog(this, "Erro ao apagar");
}
```

# 🗃️ Análise de Dados de Vendas com SQL

Este repositório contém dados de vendas de uma empresa e exemplos práticos de consultas SQL para análise de dados. Ideal para quem está aprendendo SQL e quer praticar com dados reais de vendas.

## 📁 O que você vai encontrar

### Arquivo de Dados
- **`Dados_vendas_empresa_vF.xlsx`** - Planilha com dados de vendas (pode ser importada para um banco de dados)

### Informações dos Dados
- **200 registros de vendas** de dezembro/2024 a junho/2025
- **Faturamento total**: R$ 1.682.529,38
- **Lucro total**: R$ 673.011,75
- **25 produtos diferentes** em 5 categorias
- **Vendas em 7 estados brasileiros**

## 🗂️ Estrutura da Tabela Principal

A tabela `vendas` contém as seguintes colunas:

```sql
CREATE TABLE vendas (
    data_venda DATE,
    id_cliente INT,
    nome_cliente VARCHAR(100),
    estado CHAR(2),
    categoria VARCHAR(50),
    produto VARCHAR(100),
    quantidade INT,
    preco_unitario DECIMAL(10,2),
    total_venda DECIMAL(10,2),
    ano INT,
    mes INT,
    dia INT,
    dia_semana INT,
    lucro DECIMAL(10,2),
    gastos DECIMAL(10,2),
    ano_mes VARCHAR(10),
    vip VARCHAR(10)
);
```

## 📈 Categorias e Estados

### **5 Categorias de Produtos:**
- Eletrônicos
- Alimentos  
- Brinquedos
- Vestuário
- Móveis

### **7 Estados Atendidos:**
- RS, PR, BA, SP, RJ, PE, MG

## 🎓 Roteiro de Estudos SQL

### **Introdução ao SQL**
Conceitos básicos e sintaxe fundamental do SQL
```sql
-- Exemplo: Visualizar todos os dados
SELECT * FROM vendas;
```

### **Estrutura de um Banco de Dados Relacional**
Entendendo tabelas, colunas e relacionamentos
```sql
-- Exemplo: Estrutura da tabela
DESCRIBE vendas;
```

### **Introdução à Manipulação de Dados com SQL**
Comandos básicos SELECT, INSERT, UPDATE, DELETE
```sql
-- Exemplo: Selecionar apenas algumas colunas
SELECT nome_cliente, produto, total_venda FROM vendas;
```

### **Filtros em Consultas SQL**
Usando WHERE para filtrar dados
```sql
-- Exemplo: Vendas apenas do estado de SP
SELECT * FROM vendas WHERE estado = 'SP';

-- Exemplo: Vendas acima de R$ 1000
SELECT * FROM vendas WHERE total_venda > 1000;
```

### **Operadores Lógicos SQL**
AND, OR, NOT, IN, BETWEEN
```sql
-- Exemplo: Vendas de Eletrônicos OU Móveis
SELECT * FROM vendas 
WHERE categoria = 'Eletrônicos' OR categoria = 'Móveis';

-- Exemplo: Vendas entre R$ 500 e R$ 2000
SELECT * FROM vendas 
WHERE total_venda BETWEEN 500 AND 2000;
```

### **Quantidade de Registros em uma Tabela**
Usando COUNT e outras funções de agregação
```sql
-- Exemplo: Total de vendas realizadas
SELECT COUNT(*) as total_vendas FROM vendas;

-- Exemplo: Vendas por categoria
SELECT categoria, COUNT(*) as quantidade 
FROM vendas 
GROUP BY categoria;
```

### **Funções Matemáticas em SQL**
SUM, AVG, MAX, MIN
```sql
-- Exemplo: Faturamento total
SELECT SUM(total_venda) as faturamento_total FROM vendas;

-- Exemplo: Ticket médio por estado
SELECT estado, AVG(total_venda) as ticket_medio 
FROM vendas 
GROUP BY estado;
```

### **Relacionamento entre Tabelas JOIN**
Conceitos de INNER JOIN
```sql
-- Exemplo básico de JOIN (caso tivéssemos tabela de clientes)
SELECT v.produto, v.total_venda, c.nome_cliente
FROM vendas v
INNER JOIN clientes c ON v.id_cliente = c.id;
```

### **Relacionamento entre 3 Tabelas**
JOINs mais complexos
```sql
-- Exemplo: JOIN entre vendas, clientes e produtos
SELECT v.data_venda, c.nome_cliente, p.categoria, v.total_venda
FROM vendas v
INNER JOIN clientes c ON v.id_cliente = c.id
INNER JOIN produtos p ON v.produto = p.nome;
```

### **Relacionamento entre Tabelas e com Filtro**
Combinando JOINs com WHERE
```sql
-- Exemplo: Vendas de clientes VIP em SP
SELECT v.nome_cliente, v.produto, v.total_venda
FROM vendas v
WHERE v.estado = 'SP' AND v.vip = 'vip';
```

### **LEFT JOIN e CASE WHEN**
JOINs externos e lógica condicional
```sql
-- Exemplo: Classificação de vendas com CASE
SELECT 
    produto,
    total_venda,
    CASE 
        WHEN total_venda > 2000 THEN 'Venda Alta'
        WHEN total_venda > 1000 THEN 'Venda Média'
        ELSE 'Venda Baixa'
    END as classificacao
FROM vendas;
```

## 🛠️ Como Configurar

### **1. Importar os Dados**
- Exporte a planilha Excel para CSV
- Importe para seu SGBD preferido (MySQL, PostgreSQL, SQLite)

## 💡 Dicas para Estudar SQL

### **⚠️ Boas práticas:**
- **Sempre faça backup** antes de UPDATE/DELETE
- **Use nomes descritivos** para aliases
- **Indente seu código** para melhor legibilidade
- **Teste consultas em pequenas amostras** primeiro

## 📋 Script de Criação da Tabela

```sql
-- Script completo para criar e popular a tabela
CREATE TABLE vendas (
    id INT PRIMARY KEY AUTO_INCREMENT,
    data_venda DATE,
    id_cliente INT,
    nome_cliente VARCHAR(100),
    estado CHAR(2),
    categoria VARCHAR(50),
    produto VARCHAR(100),
    quantidade INT,
    preco_unitario DECIMAL(10,2),
    total_venda DECIMAL(10,2),
    ano INT,
    mes INT,
    dia INT,
    dia_semana INT,
    lucro DECIMAL(10,2),
    gastos DECIMAL(10,2),
    ano_mes VARCHAR(10),
    vip VARCHAR(10)
);

-- Índices para melhor performance
CREATE INDEX idx_estado ON vendas(estado);
CREATE INDEX idx_categoria ON vendas(categoria);
CREATE INDEX idx_data ON vendas(data_venda);
CREATE INDEX idx_vip ON vendas(vip);
```

---

**Lembre-se**: SQL é uma habilidade prática - quanto mais você praticar com dados reais, melhor será seu aprendizado! 🎓
# Banco de Dados para E-commerce

Oi! Este é meu projeto de modelagem de banco de dados para um sistema de e-commerce. Eu criei esse banco de dados para gerenciar as informações principais de um e-commerce, como clientes, produtos, pedidos, pagamentos, fornecedores, vendedores e entregas.

## O que tem aqui

- **Banco de dados**: O banco tem várias tabelas e relacionamentos entre elas, que ajudam a organizar os dados do e-commerce.
- **Script SQL**: Tem um script para criar o banco de dados e todas as tabelas.
- **Consultas SQL**: Algumas queries para testar o banco e pegar informações como "quantos pedidos cada cliente fez?" ou "quais produtos estão em falta no estoque?".

## O que foi feito

- **Clientes**: Tem pessoas físicas (PF) e jurídicas (PJ).
- **Pedidos**: Quando um cliente compra algo, cria um pedido.
- **Pagamento**: Cada pedido pode ser pago de várias formas (cartão, boleto, transferência, etc.).
- **Entrega**: Cada pedido tem um status de entrega e um código de rastreio.
- **Fornecedores**: Os fornecedores são as empresas que fornecem os produtos.

## Como usar

1. Primeiro, crie um banco de dados no MySQL com o nome `ecommerce`.
2. Depois, copie o script SQL para criar todas as tabelas no seu banco de dados.
3. Após isso, use as **queries SQL** para testar o banco. As queries estão aqui para mostrar como fazer algumas consultas, como por exemplo, "quantos pedidos foram feitos por cada cliente?".

## O que tem no Script SQL

- **Criação das tabelas**: São criadas as tabelas de Cliente, Produto, Fornecedor, Pedido, Pagamento, Entrega e Vendedor.
- **Relacionamentos**: Coloquei as chaves estrangeiras para conectar as tabelas entre si, tipo a relação entre **clientes e pedidos**.

## Algumas Queries SQL que você pode rodar

```SQL

Quantos pedidos foram feitos por cada cliente?

SELECT 
    c.nome, 
    COUNT(p.id_pedido) AS total_pedidos
FROM 
    Cliente c
JOIN 
    Pedido p ON c.id_cliente = p.id_cliente
GROUP BY 
    c.id_cliente;


### Quantos pedidos foram feitos por cada cliente?


SELECT 
    v.nome AS vendedor_nome, 
    f.nome AS fornecedor_nome
FROM 
    Vendedor v
JOIN 
    Fornecedor f ON v.nome = f.nome;

Relação de produtos, fornecedores e estoques

SELECT 
    p.nome AS produto_nome, 
    f.nome AS fornecedor_nome, 
    p.estoque
FROM 
    Produto p
JOIN 
    Fornecedor f ON p.id_fornecedor = f.id_fornecedor;

Produtos que estão com estoque abaixo de 10 unidades

SELECT 
    p.nome, 
    p.estoque
FROM 
    Produto p
WHERE 
    p.estoque < 10;

### Tabelas e Relacionamentos

- **Cliente**
  - id_cliente (PK)
  - nome
  - tipo_cliente (PF ou PJ)
  - cnpj (para PJ)
  - cpf (para PF)
  - email
  - telefone
  - endereço

- **Produto**
  - id_produto (PK)
  - nome
  - descrição
  - preço
  - estoque
  - id_fornecedor (FK)

- **Fornecedor**
  - id_fornecedor (PK)
  - nome
  - cnpj
  - telefone
  - email

- **Pedido**
  - id_pedido (PK)
  - data_pedido
  - valor_total
  - id_cliente (FK)
  - id_vendedor (FK)

- **Pagamento**
  - id_pagamento (PK)
  - tipo_pagamento (cartão de crédito, boleto, transferência, etc.)
  - valor
  - id_pedido (FK)

- **Entrega**
  - id_entrega (PK)
  - status (pendente, enviado, entregue)
  - codigo_rastreio
  - id_pedido (FK)

- **Vendedor**
  - id_vendedor (PK)
  - nome
  - email
  - telefone

### Relacionamentos

- Um **cliente** pode fazer vários **pedidos**.
- Um **pedido** pode ter vários **pagamentos**.
- Cada **pedido** tem uma **entrega**.
- Um **produto** pode ser fornecido por vários **fornecedores**, e cada **fornecedor** pode fornecer múltiplos **produtos**.

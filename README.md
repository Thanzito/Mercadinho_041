ESTRUTURA GERAL DO BANCO DE DADOS

Vamos criar as seguintes tabelas: 

1.Produtos-informações dos produtos em estoque;

2.Fornecedores-Dados dos fornecedores;

3.Vendas-Resumo das vendas (data, total, etc.);

4.Itens_venda-Itens de cada venda (produto, quantidade, preço...);

5.Usuarios-Login dos funcionários (Para controle de quem faz a venda)


MERCADINHO 041.

Produto: Valor, descrição, data de validade, nome do produto, lote, código de barra.

Fornecedor: Nome do fornecedor, endereço, CNPJ, telefone, email.

Venda: Data, nome do produto, valor do produto, valor total, nome do cliente, CPF do cliente, usuário.

Itens venda: Preço unitário, quantidade.

Usuário: Nome do usuário, email, senha, cargo.


--------------------------------------------------------------------------------------------------------

CREATE DATABASE Mercado_041;

USE Mercado_041;

--Tabela de fornecedor

CREATE TABLE fornecedor(

id_for INT AUTO_INCREMENT PRIMARY KEY,

nome VARCHAR(100) NOT NULL,

telefone VARCHAR(200) NOT NULL,

email VARCHAR(100),

endereco TEXT

);

--Tabela do produto

CREATE TABLE produto(

id_prod INT AUTO_INCREMENT PRIMARY KEY,

nome VARCHAR(100)NOT NULL,

codigo_barra VARCHAR(50)UNIQUE,

descricao TEXT,

categoria VARCHAR(50),

preco_custo DECIMAL(10,2),

preco_venda DECIMAL(10,2),

quantidade INT DEFAULT 0,

validade DATE,

localizacao VARCHAR(100),

unidade VARCHAR(100),

data_entrada DATE,

fornecedor_id INT,

FOREIGN KEY (fornecedor_id) REFERENCES fornecedor(id_for)

);

--Tabela de usuários (funcionário do caixa)

CREATE TABLE usuario(

id_usu INT AUTO_INCREMENT PRIMARY KEY,

nome VARCHAR(100)NOT NULL,

email VARCHAR(100)UNIQUE,

senha VARCHAR(100)NOT NULL,

cargo VARCHAR(50)DEFAULT 'Funcionario'

);

--Tabela Vendas

CREATE TABLE venda(

id_ven INT AUTO_INCREMENT PRIMARY KEY,

data_hora DATETIME DEFAULT CURRENT_TIMESTAMP,

valor_total DECIMAL(10,2),

forma_pagamento VARCHAR(50),

cliente_nome VARCHAR(100),

cliente_cpf VARCHAR(14),

usuario_id INT,

FOREIGN KEY(usuario_id)REFERENCES usuario(id_usu)

);

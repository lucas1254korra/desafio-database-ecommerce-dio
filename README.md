# Desafio de Modelagem de BD para E-commerce - Formação SQL Database Specialist DIO

Projeto desenvolvido para o desafio de modelagem de banco de dados da **Formação SQL Database Specialist DIO**. O objetivo foi criar um esquema relacional robusto e escalável para um sistema de e-commerce, desde o cadastro de clientes até a entrega do pedido.

## 👨‍💻 Analista de Dados | Desenvolvedor do Projeto

- **Nome:** Lucas Santos
- **LinkedIn:** [https://www.linkedin.com/in/lucas-santos-3ab322294/](https://www.linkedin.com/in/lucas-santos-3ab322294/)

---

## 📊 Diagrama Entidade-Relacionamento (DER)

O diagrama abaixo foi desenvolvido na ferramenta **Draw.io (diagrams.net)** e representa a estrutura completa do banco de dados, incluindo todas as tabelas, seus atributos e os relacionamentos com suas respectivas cardinalidades.

![Diagrama ER do E-commerce](diagrama-er-ecommerce.png)

---

## 📂 Arquivos e Ativos do Projeto

Neste repositório, você encontrará todos os ativos relacionados ao projeto de modelagem:

- **[`diagrama-er-ecommerce.png`](diagrama-er-ecommerce.png):** Imagem em alta resolução para visualização rápida do diagrama.
- **[`diagrama-er-ecommerce.svg`](diagrama-er-ecommerce.svg):** Arquivo vetorial escalável, ideal para apresentações e documentação técnica (não perde qualidade com zoom).
- **[`diagrama-er-ecommerce.drawio`](diagrama-er-ecommerce.drawio):** O arquivo-fonte editável. Pode ser aberto no Draw.io para futuras modificações e melhorias.
- **[`schema.sql`](schema.sql):** O script SQL completo com os comandos `CREATE TABLE` e `ALTER TABLE` para construir o banco de dados em um SGBD compatível com MySQL.

---

## 🛠️ Tecnologias Utilizadas

- **Modelagem de Dados:** Draw.io (diagrams.net)
- **Linguagem do Banco de Dados:** SQL (padrão MySQL)
- **Versionamento de Código:** Git & GitHub
- **Diagrama como Código:** Mermaid.js

---

## 📈 Diagrama Renderizado via Código (Mermaid.js)

Como um exercício adicional de "Diagrama como Código", o mesmo esquema foi replicado abaixo utilizando a sintaxe do Mermaid, que o GitHub renderiza automaticamente. Isso demonstra a capacidade de versionar e documentar a infraestrutura de dados de forma textual.

```mermaid
erDiagram
    Cliente {
        INT idCliente PK
        VARCHAR tipoCliente
        VARCHAR email
        VARCHAR telefone
        TIMESTAMP dataCadastro
    }
    ClientePF {
        INT idClientePF PK, FK
        VARCHAR nome
        VARCHAR sobrenome
        CHAR cpf
        DATE dataNascimento
    }
    ClientePJ {
        INT idClientePJ PK, FK
        VARCHAR razaoSocial
        VARCHAR nomeFantasia
        CHAR cnpj
        VARCHAR inscricaoEstadual
    }
    Endereco {
        INT idEndereco PK
        INT idCliente FK
        VARCHAR tipoEndereco
        VARCHAR logradouro
        VARCHAR numero
        VARCHAR cidade
        CHAR estado
        CHAR cep
    }
    FormaPagamento {
        INT idFormaPagamento PK
        INT idCliente FK
        VARCHAR tipoFormaPagamento
        BOOLEAN ativo
    }
    DadosCartao {
        INT idDadosCartao PK
        INT idFormaPagamento FK
        VARCHAR numeroCartao
        VARCHAR nomeCartao
        CHAR validadeMes
        CHAR validadeAno
    }
    Produto {
        INT idProduto PK
        VARCHAR nomeProduto
        VARCHAR categoria
        TEXT descricao
        DECIMAL valorUnitario
    }
    Estoque {
        INT idEstoque PK
        INT idProduto FK
        INT quantidade
        VARCHAR localizacao
    }
    Fornecedor {
        INT idFornecedor PK
        VARCHAR razaoSocial
        CHAR cnpj
        VARCHAR email
    }
    ProdutoFornecedor {
        INT idProduto PK, FK
        INT idFornecedor PK, FK
        DECIMAL precoFornecedor
    }
    Pedido {
        INT idPedido PK
        INT idCliente FK
        VARCHAR statusPedido
        DECIMAL valorTotal
    }
    ItensPedido {
        INT idItemPedido PK
        INT idPedido FK
        INT idProduto FK
        INT quantidade
        DECIMAL valorUnitario
    }
    Pagamento {
        INT idPagamento PK
        INT idPedido FK
        INT idFormaPagamento FK
        DECIMAL valorPago
        VARCHAR statusPagamento
    }
    Entrega {
        INT idEntrega PK
        INT idPedido FK
        INT idEndereco FK
        VARCHAR codigoRastreio
        VARCHAR statusEntrega
    }
    HistoricoEntrega {
        INT idHistorico PK
        INT idEntrega FK
        VARCHAR statusRegistrado
        TIMESTAMP dataHoraRegistro
    }

    Cliente ||--|{ ClientePF : "é"
    Cliente ||--|{ ClientePJ : "é"
    Cliente ||--o{ Endereco : "possui"
    Cliente ||--o{ Pedido : "realiza"
    Cliente ||--o{ FormaPagamento : "cadastra"
    FormaPagamento ||--|{ DadosCartao : "contém"
    FormaPagamento ||--o{ Pagamento : "utiliza"
    Pedido ||--|{ Entrega : "gera"
    Pedido ||--o{ ItensPedido : "contém"
    Pedido ||--o{ Pagamento : "exige"
    Produto ||--|{ Estoque : "tem"
    Produto ||--o{ ItensPedido : "compõe"
    Produto }o--o{ ProdutoFornecedor : "é fornecido por"
    Fornecedor ||--o{ ProdutoFornecedor : "fornece"
    Endereco ||--o{ Entrega : "é destino para"
    Entrega ||--o{ HistoricoEntrega : "registra"

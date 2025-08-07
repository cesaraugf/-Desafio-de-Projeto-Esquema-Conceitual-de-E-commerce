# Projeto de Banco de Dados: Esquema Conceitual para E-commerce

## 1. Visão Geral do Projeto

Este projeto documenta o esquema conceitual de um banco de dados para uma plataforma de e-commerce. O modelo foi refinado para atender a um conjunto de regras de negócio essenciais que permitem uma operação mais completa e realista, focando na gestão de clientes, pagamentos e logística de entrega.

Este documento serve como o entregável principal do desafio de projeto, descrevendo a estrutura das entidades e seus relacionamentos.

## 2. Requisitos Atendidos

O esquema conceitual foi projetado para resolver os seguintes pontos de refinamento:

* **Cliente PJ e PF:** Uma conta pode ser de Pessoa Física (PF) ou Pessoa Jurídica (PJ), mas não pode conter as informações de ambos os tipos. [cite: 5]
* **Pagamento:** Um cliente pode ter mais de uma forma de pagamento cadastrada em sua conta. [cite: 5]
* **Entrega:** O processo de entrega de um pedido deve possuir status e um código de rastreio próprios. [cite: 5]

## 3. Descrição do Esquema Conceitual

Para atender aos requisitos, o modelo conceitual foi estruturado da seguinte forma:

### Módulo de Clientes (PF e PJ)

Para resolver a necessidade de clientes PF e PJ, foi aplicado o padrão de **Generalização/Especialização**:

* **Entidade `Cliente`:** Funciona como uma entidade base, armazenando atributos comuns a todos os clientes, como nome e endereço. Ela contém um atributo "TipoCliente" (discriminador) para identificar se o registro é de uma Pessoa Física ou Jurídica.
* **Entidades `PessoaFisica` e `PessoaJuridica`:** São especializações da entidade `Cliente`.
    * `PessoaFisica` armazena o atributo CPF.
    * `PessoaJuridica` armazena o atributo CNPJ.
* **Relacionamento:** `Cliente` possui um relacionamento de **um-para-um** com `PessoaFisica` e um relacionamento de **um-para-um** com `PessoaJuridica`. [cite_start]A aplicação da regra de negócio, guiada pelo atributo "TipoCliente", garante que um cliente se relacione com apenas uma das duas especializações, cumprindo o requisito. [cite: 5]

### Módulo de Pagamentos

Para permitir múltiplos métodos de pagamento por cliente, a seguinte estrutura foi criada:

* **Entidade `FormaDePagamento`:** Uma nova entidade para armazenar os detalhes de cada método de pagamento (ex: tipo de cartão, últimos 4 dígitos).
* **Relacionamento:** Foi estabelecido um relacionamento de **um-para-muitos** entre `Cliente` e `FormaDePagamento`. [cite_start]Isso significa que um registro de `Cliente` pode estar associado a vários registros de `FormaDePagamento`, atendendo perfeitamente ao requisito. [cite: 5]

### Módulo de Pedidos e Entregas

Para detalhar o processo de entrega, o modelo foi refinado da seguinte maneira:

* **Entidade `Pedido`:** Representa a compra feita pelo cliente.
* **Entidade `Entrega`:** Uma nova entidade criada especificamente para conter os dados logísticos. Seus atributos incluem "Status da Entrega" e "Código de Rastreio".
* **Relacionamento:** Foi definido um relacionamento de **um-para-um** entre `Pedido` e `Entrega`. [cite_start]Cada pedido terá exatamente uma entrega associada, permitindo que o status do pedido (ex: "Pagamento Aprovado") seja independente do status da entrega (ex: "Enviado"), conforme solicitado no requisito. [cite: 5]

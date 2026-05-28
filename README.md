# 🏦 Core Banking API - Simulação de Transações e PIX

![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

## 💻 Sobre o Projeto
Este projeto é uma API RESTful desenvolvida em Java com Spring Boot, simulando o core bancário de uma instituição financeira. O foco principal é garantir a consistência, segurança e rastreabilidade em operações financeiras de alta criticidade, como transferências via PIX, depósitos e saques.

## ⚙️ Arquitetura e Boas Práticas Adotadas
O projeto foi construído focando na manutenibilidade e escalabilidade do código, aplicando:

* **Padrão em Camadas (Layered Architecture):** Separação clara entre `Controllers` (Roteamento), `Services` (Regras de Negócio) e `Repositories` (Acesso a Dados).
* **Clean Code & SOLID:** Nomenclatura descritiva de variáveis e métodos, responsabilidade única por classe e injeção de dependências.
* **Padrão DTO (Data Transfer Object):** Ocultação das entidades de banco de dados e controle rigoroso sobre os dados de entrada/saída da API.
* **Tratamento Global de Exceções:** Utilização de `@ControllerAdvice` para capturar exceções de negócio (ex: `SaldoInsuficienteException`) e padronizar as respostas de erro da API.
* **Transações Seguras:** Uso massivo da anotação `@Transactional` para garantir as propriedades ACID (Atomicidade, Consistência, Isolamento, Durabilidade) do banco de dados em operações de transferência.

## 🔒 Regras de Negócio Implementadas
- [ ] O sistema não permite o cadastro de dois clientes com o mesmo CPF/E-mail.
- [ ] Todo cliente, ao ser criado, recebe automaticamente uma Conta Corrente ativa e com saldo zerado.
- [ ] O sistema bloqueia transações (PIX ou Saque) se o cliente não possuir saldo suficiente, emitindo um erro `400 Bad Request` com mensagem customizada.
- [ ] Uma transferência via PIX debita da conta de origem e credita na conta de destino na mesma transação. Qualquer falha na rede ou no banco de dados durante o processo gera um *rollback* automático.

## 🛠️ Tecnologias Utilizadas
* **Java 17+**
* **Spring Boot 3** (Web, Data JPA, Validation)
* **PostgreSQL** (Banco de Dados Relacional)
* **Flyway / Liquibase** (Versionamento de Banco de Dados) - *Opcional, mas recomendado*
* **Docker & Docker Compose** (Containerização da infraestrutura)
* **JUnit 5 & Mockito** (Testes Unitários)

## 🚀 Como Executar o Projeto Localmente

**Pré-requisitos:** Java 17+, Maven e Docker instalados.

1. Clone este repositório:
   ```bash
   git clone [https://github.com/seu-usuario/core-banking-api.git](https://github.com/seu-usuario/core-banking-api.git)

2. Suba o banco de dados PostgreSQL via Docker:
   ```bash
    docker-compose up -d

3. Compile e execute a aplicação:
  ```bash
   mvn spring-boot:run

A API estará disponível em http://localhost:8080

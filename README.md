# 📢 Saber Sem Idade

## Inclusão digital e alfabetização tecnológica para quem tem história para contar.

O *Saber Sem Idade* é uma plataforma desenvolvida para promover a inclusão digital da terceira idade, oferecendo um ambiente simples, seguro e intuitivo para cadastro de usuários, gerenciamento de cursos e matrículas.

O projeto busca incentivar a autonomia tecnológica das pessoas idosas, contribuindo para a redução da exclusão digital e do isolamento social por meio de uma solução acessível e de fácil utilização.

---

# 👥 Seção 1 - Sobre o Projeto

*Nome do Projeto:* Saber Sem Idade

*ODS Escolhida:* ODS 4 – Educação de Qualidade

*Aluno:* Jose Wilson Lélis de Aragão Neto

## Objetivo

Desenvolver uma plataforma web para gerenciamento de usuários, cursos e matrículas, incentivando a alfabetização digital da terceira idade por meio de uma interface simples, intuitiva e acessível.

## Tecnologias Utilizadas

### Front-end
- React
- Vite
- Tailwind CSS
- Axios
- Wouter

### Back-end
- Java
- Spring Boot
- Spring Data JPA
- Hibernate
- Maven

### Banco de Dados
- MySQL

---

# 🚀 Seção 2 - Como Rodar o Projeto

## 🗄️ Banco de Dados

Na raiz do projeto encontra-se o arquivo:

schema_projetofinal.sql


Execute esse arquivo utilizando o MySQL Workbench (ou outro gerenciador compatível) para criar o banco de dados e todas as tabelas necessárias para o funcionamento da aplicação.

---

## ⚙️ Como Rodar o Back-end

1. Abra um terminal na pasta do back-end.
2. Configure o arquivo:

text
src/main/resources/application.properties


informando o usuário e a senha do seu MySQL.

3. Execute o projeto utilizando o Maven:

bash
./mvnw spring-boot:run


ou, caso utilize o Maven instalado na máquina:

bash
mvn spring-boot:run


A API será iniciada na porta *8080*.

---

## 💻 Como Rodar o Front-end

1. Abra um terminal na pasta do front-end.
2. Instale as dependências do projeto:

bash
npm install


3. Execute a aplicação:

bash
npm run dev


4. Abra o navegador e acesse:

text
http://localhost:5173

---

Seção 3 -SCRIPT SQL (Banco de Dados)

MySQL:

CREATE DATABASE IF NOT EXISTS saber_sem_idade;
USE saber_sem_idade;

CREATE TABLE categorias (
   id int NOT NULL AUTO_INCREMENT,
   nome varchar(255) DEFAULT NULL,
   descricao varchar(255) DEFAULT NULL,
   PRIMARY KEY (id),
   UNIQUE KEY nome (nome)
);

CREATE TABLE instrutores (
   id int NOT NULL AUTO_INCREMENT,
   nome varchar(255) NOT NULL,
   email varchar(255) NOT NULL,
   especialidade varchar(255) DEFAULT NULL,
   biografia varchar(255) DEFAULT NULL,
   PRIMARY KEY (id),
   UNIQUE KEY email (email)
);

CREATE TABLE usuarios (
   id int NOT NULL AUTO_INCREMENT,
   nome varchar(255) NOT NULL,
   email varchar(255) NOT NULL,
   senha varchar(255) NOT NULL,
   data_cadastro timestamp NULL DEFAULT CURRENT_TIMESTAMP,
   PRIMARY KEY (id),
   UNIQUE KEY email (email)
);

CREATE TABLE cursos (
   id int NOT NULL AUTO_INCREMENT,
   titulo varchar(255) NOT NULL,
   descricao varchar(255) DEFAULT NULL,
   categoria_id int DEFAULT NULL,
   instrutor_id int DEFAULT NULL,
   data_criacao timestamp NULL DEFAULT CURRENT_TIMESTAMP,
   PRIMARY KEY (id),
   KEY categoria_id (categoria_id),
   KEY instrutor_id (instrutor_id),
   CONSTRAINT cursos_ibfk_1 FOREIGN KEY (categoria_id) REFERENCES categorias (id) ON DELETE SET NULL,
   CONSTRAINT cursos_ibfk_2 FOREIGN KEY (instrutor_id) REFERENCES instrutores (id) ON DELETE SET NULL
);

CREATE TABLE matriculas (
   id int NOT NULL AUTO_INCREMENT,
   usuario_id int NOT NULL,
   curso_id int NOT NULL,
   data_matricula timestamp NULL DEFAULT CURRENT_TIMESTAMP,
   status varchar(255) DEFAULT NULL,
   PRIMARY KEY (id),
   UNIQUE KEY usuario_id (usuario_id,curso_id),
   KEY curso_id (curso_id),
   CONSTRAINT matriculas_ibfk_1 FOREIGN KEY (usuario_id) REFERENCES usuarios (id) ON DELETE CASCADE,
   CONSTRAINT matriculas_ibfk_2 FOREIGN KEY (curso_id) REFERENCES cursos (id) ON DELETE CASCADE
);

INSERT INTO Categorias (nome, descricao) VALUES
('Usando o Computador', 'Aprenda a enviar mensagens, fotos e fazer chamadas com o WhatsApp.'),
('Usando o Whatsapp', 'Conheça e reconheça palavras importantes para a vida cotidiana.'),
('Como Usar o Caixa Eletrônico', 'Entenda como sacar dinheiro, consultar saldo e fazer pagamentos no caixa eletrônico.');

INSERT INTO Usuarios (nome, email, senha) VALUES
('Maria Silva', 'maria.silva@email.com', 'senha123'),
('João Santos', 'joao.santos@email.com', 'senha456'),
('Ana Souza', 'ana.souza@email.com', 'senha789');

INSERT INTO Instrutores (nome, email, especialidade, biografia) VALUES
('Carlos Oliveira', 'carlos.oliveira@email.com', 'Inclusão Digital', 'Educador especializado em inclusão digital para idosos, auxiliando no uso de celulares, aplicativos e tecnologias do dia a dia.'),
('Fernanda Lima', 'fernanda.lima@email.com', 'Alfabetização de Adultos', 'Professora com experiência em alfabetização de jovens e adultos, utilizando métodos simples e acessíveis para facilitar o aprendizado da leitura e escrita.'),
('Pedro Costa', 'pedro.costa@email.com', 'Educação Financeira e Tecnologia', 'Instrutor voltado ao ensino do uso de caixas eletrônicos, aplicativos bancários e outras ferramentas digitais essenciais para promover a autonomia dos alunos.');

INSERT INTO Cursos (titulo, descricao, categoria_id, instrutor_id) VALUES
('Habilidades Digitais Básicas', 'Aprenda o básico de computadores, internet e redes sociais', 1, 1),
('WhatsApp e Mensagens', 'Como usar WhatsApp para conversas pessoais e profissionais', 2, 2),
('Aplicativos de Banco', 'Entenda como usar aplicativos de banco e fazer transações.', 3, 3);

INSERT INTO Matriculas (usuario_id, curso_id, status) VALUES
(1, 7, 'ATIVO'),
(1, 8, 'ATIVO'),
(2, 7, 'CONCLUIDO'),
(3, 9, 'ATIVO');



## 📁 Estrutura do Projeto

text
Saber-Sem-Idade/
│
├── README.md
├── script.sql
├── backend/
└── frontend/

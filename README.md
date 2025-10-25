# AWS-EC2-EBS-RDS-Management-Documentation
## Documentação da prática de provisionamento e gerenciamento de EC2, EBS e RDS na AWS, incluindo insights e boas práticas de segurança.

### Sobre o Projeto
Este repositório contém a documentação e os *insights* adquiridos durante o desafio prático da DIO **Gerenciando Instâncias EC2 na AWS** 

O objetivo foi consolidar os conhecimentos sobre o ciclo de vida, provisionamento e configuração dos serviços **EC2 (servidor virtual)**, **EBS (armazenamento de bloco)** e sua conexão com o **RDS (banco de dados gerenciado)**.

**Autor:** Bruna Lima Prado

## 🛠️ Serviços e Conceitos Chave

Durante a prática, explorei e documentei o uso dos seguintes recursos:

* **Amazon EC2:** Lançamento, configuração e tipos de instância.
* **Amazon EBS:** Criação, anexo e desanexo de volumes para persistência de dados.
* **Security Groups:** Criação de regras de firewall para controle de tráfego.
* **Key Pairs:** Geração e uso de chaves RDP para acesso seguro.
* **Amazon RDS:** Conexão lógica com um serviço de banco de dados relacional gerenciado.
* **Arquitetura de Alto Nível:** Visualização do fluxo de dados entre os componentes.

* ## 📝 Passos Práticos Documentados

Os seguintes passos foram executados e documentados para completar o desafio:

1.  **Criação do Key Pair:**
    * Geração do par de chaves para conexão segura.

2.  **Configuração do Security Group :**
    * Criação de um Security Group (`launch-wizard-1`) permitindo o tráfego de entrada, restrito ao meu IP.

3.  **Lançamento da Instância EC2:**
    * Escolha da AMI (Windows) e do Tipo de Instância (t3.micro - nível gratuíto).
    * Associação do *Key Pair* e do *Security Group* criados.

4.  **Gerenciamento de Volumes EBS:**
    * Criação de dois volumes EBS adicionais (`D-EBS` e `E-EBS`) na mesma Zona de Disponibilidade (AZ) da EC2.
    * Anexo dos volumes à instância EC2.

5.  **Acesso e Formatação do EBS:**
    * Conexão via **RDP** na instância usando o `Key Pair`.
    * Inicialização e formatação dos novos volumes EBS (via **Gerenciamento de Disco** no Windows) para que o sistema operacional possa usá-los.
  
    * ## 🖼️ Diagrama de Arquitetura

O diagrama a seguir ilustra o fluxo de alto nível dos componentes principais do laboratório:

![Diagrama de Arquitetura EC2, EBS, RDS] (imagens/diagramaEC2.png)
*(A imagem foi salva na pasta `/imagens` do repositório).*

## 🧠 Anotações e Insights 

* **Persistência de Dados vs. Volume Root:** Entendi que o Volume Root é deletado por padrão se a EC2 for terminada, mas os volumes EBS adicionais (como D-EBS e E-EBS) **persistem**, o que exige a criação de políticas de ciclo de vida para evitar cobranças indesejadas.
* **Segurança (Princípio do Menor Privilégio):** A criação de um Security Group restritivo para SSH (apenas o meu IP de origem) é crucial. Em um ambiente de produção, conexões internas (EC2 -> RDS) também são rigidamente controladas.
* **Armazenamento de Arquivos:** Embora o EBS tenha sido usado para praticar o anexo de volumes, em uma arquitetura real para "envio de arquivos", o **Amazon S3** seria a escolha mais robusta e escalável para o armazenamento de objetos.
* **Gestão de Banco de Dados:** O RDS elimina a necessidade de gerenciar o SO, backups e patches do banco de dados, liberando tempo para a equipe de DevOps focar na aplicação e na infraestrutura (EC2).

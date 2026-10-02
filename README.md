<p align="center">
<img width="600" alt="AWS Systems Manager" src="https://github.com/user-attachments/assets/79a6e3f4-df02-4a48-8dab-0b1192d453de" />
</p>



# ☁️ AWS — Usar o AWS Systems Manager

## 📌 Sobre o laboratório

Este laboratório apresenta o **AWS Systems Manager**, serviço da AWS utilizado para centralizar dados operacionais, automatizar tarefas e gerenciar recursos em ambientes de nuvem e ambientes híbridos.

Durante a atividade, foram explorados recursos do Systems Manager para coletar inventário de instâncias, instalar uma aplicação web personalizada, gerenciar configurações por meio do Parameter Store e acessar instâncias EC2 utilizando o Session Manager.

---

## 🎯 Objetivos

Ao concluir este laboratório, os principais objetivos foram:

* 🔍 Verificar configurações e permissões;
* ⚙️ Executar tarefas em instâncias gerenciadas;
* 🛠️ Instalar uma aplicação utilizando o Run Command;
* 🔧 Atualizar configurações de uma aplicação;
* 🔑 Acessar a linha de comando de uma instância EC2;
* 🔐 Explorar formas de acesso remoto sem utilizar SSH diretamente.

---

## ☁️ AWS Systems Manager

O **AWS Systems Manager** reúne recursos para gerenciar instâncias do Amazon EC2, servidores locais (*on-premises*), máquinas virtuais e outros recursos da AWS.

Durante o laboratório, foram utilizados os seguintes recursos:

* 🔍 **Fleet Manager e Inventory:** coleta e consulta de informações sobre o sistema operacional, aplicações instaladas e configurações da instância;
* ⚙️ **Run Command:** execução de comandos para instalar uma aplicação em uma instância gerenciada;
* 🗂️ **Parameter Store:** armazenamento e gerenciamento de parâmetros de configuração da aplicação;
* 💻 **Session Manager:** acesso interativo à linha de comando da instância por meio do navegador.

**Duração aproximada:** 30 minutos.

---

## 🛠️ Configuração utilizada

| Recurso                   | Configuração                    |
| ------------------------- | ------------------------------- |
| Serviço principal         | AWS Systems Manager             |
| Instância gerenciada      | Amazon EC2                      |
| Inventário                | `Inventory-Association`         |
| Aplicação web             | Widget Manufacturing Dashboard  |
| Servidor web              | Apache                          |
| Configuração da aplicação | Parameter Store                 |
| Parâmetro criado          | `/dashboard/show-beta-features` |
| Valor do parâmetro        | `True`                          |
| Acesso à instância        | Session Manager                 |
| Execução de comandos      | Run Command                     |

---

## 🔍 Tarefa 1 — Gerar listas de inventário

Nesta etapa, foi utilizado o recurso **Fleet Manager** para configurar a coleta de inventário de uma instância gerenciada do Amazon EC2.

Foi criada a associação `Inventory-Association`, responsável por coletar informações sobre softwares e configurações da instância.

Após a configuração, foi acessada a guia **Inventário** para consultar as aplicações instaladas e outros dados disponíveis.

**Principais resultados:**

* ✅ Configuração da associação de inventário;
* ✅ Consulta às informações da instância;
* ✅ Visualização das aplicações instaladas;
* ✅ Verificação de configurações sem a necessidade de conexão individual via SSH.

---

## ⚙️ Tarefa 2 — Instalar uma aplicação com Run Command

Nesta etapa, foi utilizado o recurso **Run Command** para executar um documento de comando e instalar a aplicação web personalizada **Widget Manufacturing Dashboard**.

O procedimento utilizou uma instância gerenciada do EC2 e executou as etapas de instalação dos componentes necessários à aplicação, incluindo:

* Servidor web Apache;
* PHP;
* AWS SDK;
* Aplicação web personalizada.

Após a execução do comando, o status foi verificado no console do Systems Manager. Em seguida, o endereço IP público da instância foi utilizado para acessar o painel pelo navegador.

**Principais resultados:**

* ✅ Execução de comandos pelo console da AWS;
* ✅ Instalação da aplicação web personalizada;
* ✅ Verificação do status de execução;
* ✅ Acesso à aplicação pelo navegador sem conexão remota via SSH para realizar a instalação.

---

## 🗂️ Tarefa 3 — Gerenciar configurações com o Parameter Store

Nesta etapa, foi utilizado o **AWS Systems Manager Parameter Store** para armazenar um parâmetro responsável por habilitar um recurso adicional na aplicação.

O parâmetro criado foi:

| Configuração | Valor                           |
| ------------ | ------------------------------- |
| Nome         | `/dashboard/show-beta-features` |
| Descrição    | `Display beta features`         |
| Nível        | Padrão                          |
| Tipo         | Padrão                          |
| Valor        | `True`                          |

Após criar o parâmetro, a página do Widget Manufacturing Dashboard foi atualizada. Com isso, o painel passou a exibir um terceiro gráfico, correspondente ao recurso adicional habilitado pela configuração.

**Principais resultados:**

* ✅ Criação de um parâmetro de configuração;
* ✅ Utilização de um caminho hierárquico;
* ✅ Atualização do comportamento da aplicação;
* ✅ Verificação do recurso adicional no painel web.

---

## 💻 Tarefa 4 — Acessar instâncias com Session Manager

Nesta etapa, foi utilizado o **AWS Systems Manager Session Manager** para acessar a instância EC2 por meio de uma sessão interativa no navegador.

Durante a sessão, foram executados comandos para consultar os arquivos da aplicação e listar informações da instância.

### Comando para listar os arquivos da aplicação

```bash
ls /var/www/html
```

### Comandos para consultar a região e listar instâncias EC2

```bash
# Get region
AZ=`curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone`
export AWS_DEFAULT_REGION=${AZ::-1}

# List information about EC2 instances
aws ec2 describe-instances
```

O primeiro comando permitiu verificar os arquivos instalados no diretório da aplicação. O segundo conjunto de comandos definiu a região padrão da AWS a partir da zona de disponibilidade e consultou informações das instâncias EC2 em formato JSON.

**Principais resultados:**

* ✅ Acesso interativo pelo navegador;
* ✅ Consulta aos arquivos da aplicação;
* ✅ Execução de comandos na instância;
* ✅ Consulta de informações do Amazon EC2;
* ✅ Exploração de uma alternativa de acesso sem conexão SSH tradicional.

---

## 📚 Principais aprendizados

Durante o laboratório, foram praticados conceitos importantes de gerenciamento e automação na AWS:

* 🔍 Coleta de inventário de instâncias gerenciadas;
* ⚙️ Execução remota de comandos com Run Command;
* 🌐 Instalação e verificação de uma aplicação web;
* 🗂️ Gerenciamento de configurações com Parameter Store;
* 💻 Acesso a instâncias EC2 com Session Manager;
* 🔐 Acesso controlado e auditável a instâncias;
* 🧰 Consulta de recursos da AWS por meio da AWS CLI.

---

## 🧠 O que ficou de aprendizado

O principal aprendizado deste laboratório foi compreender como o **AWS Systems Manager centraliza tarefas de gerenciamento e automação de instâncias**, reduzindo a necessidade de acessar cada servidor individualmente.

A atividade demonstrou como coletar informações de inventário, executar comandos para instalar aplicações, alterar configurações por parâmetros e acessar a linha de comando de uma instância EC2 pelo Session Manager.

Também foi possível observar como esses recursos podem apoiar a administração de ambientes AWS, facilitando tarefas operacionais e oferecendo alternativas de acesso que não dependem de uma conexão SSH tradicional.

---

## 📸 Evidências do laboratório

### 🔍 Inventário da instância gerenciada

Registro da configuração do inventário e da consulta às informações coletadas pelo Fleet Manager.

<p align="center">
<img width="1903" height="886" alt="Image" src="https://github.com/user-attachments/assets/0bffb45f-fbb0-4a71-b77f-854173c399fe" />
<img width="1904" height="881" alt="Image" src="https://github.com/user-attachments/assets/1be5a44c-9f90-4af7-9010-c78af3080b27" />
</p>

### ⚙️ Instalação da aplicação com Run Command

Registro da execução do comando utilizado para instalar o Widget Manufacturing Dashboard.

<p align="center">
<img width="1903" height="880" alt="Image" src="https://github.com/user-attachments/assets/ad2dd849-bc65-4248-b9f7-cbde196a5081" />
<img width="1901" height="882" alt="Image" src="https://github.com/user-attachments/assets/ff47e319-7691-4cb9-a055-415a815d6b57" />
<img width="1898" height="880" alt="Image" src="https://github.com/user-attachments/assets/8ec14b23-88e8-46f6-aa92-a5bb1e796023" />
</p>

### 🗂️ Parâmetro da aplicação

Registro da criação do parâmetro `/dashboard/show-beta-features` no Parameter Store.

<p align="center">
  <img width="1901" height="887" alt="Image" src="https://github.com/user-attachments/assets/18d4e19a-96b2-471d-b1c8-2a4a15904f6a" />
</p>

### 💻 Acesso com Session Manager

Registro da sessão interativa e da execução de comandos na instância EC2.

<p align="center">
<img width="1899" height="872" alt="Image" src="https://github.com/user-attachments/assets/d0bb55d0-b34f-4b52-9447-549affa58f58" />
<img width="1900" height="884" alt="Image" src="https://github.com/user-attachments/assets/738a4c9c-3f4b-4adc-bcb1-8b84f6bfcbd3" />
<img width="1920" height="889" alt="Image" src="https://github.com/user-attachments/assets/85b45b6a-a01c-4d4e-a0b3-5b02fa6dcf84" />
<img width="692" height="388" alt="Image" src="https://github.com/user-attachments/assets/33bf6cb1-00ed-404f-b115-f68c2d82dc05" />
</p>

---

## 🧰 Tecnologias e serviços

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?style=for-the-badge\&logo=amazonaws)

![Systems Manager](https://img.shields.io/badge/AWS-Systems_Manager-orange?style=for-the-badge\&logo=amazonaws)

![Amazon EC2](https://img.shields.io/badge/Amazon-EC2-orange?style=for-the-badge\&logo=amazonec2)

![Amazon S3](https://img.shields.io/badge/Amazon-S3-orange?style=for-the-badge\&logo=amazons3)

![AWS CLI](https://img.shields.io/badge/AWS-CLI-orange?style=for-the-badge\&logo=amazonaws)

![Apache](https://img.shields.io/badge/Apache-Web_Server-red?style=for-the-badge\&logo=apache)

**Serviços e conceitos estudados:**

`AWS Systems Manager` • `Fleet Manager` • `Inventory` • `Run Command` • `Parameter Store` • `Session Manager` • `Amazon EC2` • `Amazon S3` • `AWS CLI` • `Apache` • `PHP` • `VPC` • `IAM` • `AWS CloudTrail`

---

## 📖 Referência

**AWS Training and Certification**

Laboratório: **Usar o AWS Systems Manager**.

Material utilizado para a realização das atividades práticas de gerenciamento, automação e acesso a instâncias na AWS.

---

## 🚀 Próximos passos

🔹 Continuar os laboratórios práticos de **AWS Cloud**;

🔹 Aprofundar os estudos em gerenciamento e automação de instâncias;

🔹 Explorar outros recursos do AWS Systems Manager;

🔹 Praticar o gerenciamento de permissões com IAM e o monitoramento de recursos;

🔹 Aplicar os conhecimentos adquiridos em novos laboratórios e projetos práticos.

---

<p align="center">
  ☁️ <strong>Aprendizado contínuo em Cloud Computing</strong> ☁️
</p>

<p align="center">
  <sub>Laboratório realizado para fins educacionais.</sub>
</p>




<p align="center">
  <sub>© 2026 Alessandro Batista Prudente — Todos os direitos reservados.</sub>
</p>



# 🐳 Aplicação Flask com Docker

> Projeto desenvolvido para praticar a criação e execução de uma aplicação Flask dentro de um container Docker.

---

## 🎯 Objetivo

Este projeto apresenta uma aplicação web simples desenvolvida com **Python e Flask**, preparada para ser executada dentro de um **container Docker**.

A atividade teve como objetivo praticar:

- 💻 Configuração de uma máquina virtual
- 🐳 Utilização do Docker
- 📦 Criação de uma imagem Docker
- 🚀 Execução de um container
- 🌐 Acesso à aplicação pelo navegador
- 🔗 Criação de rotas utilizando Flask

Também foi realizada uma expansão da aplicação, com a criação das rotas **`/sobre`** e **`/contato`**, além de melhorias visuais na página inicial.

---

## 🛠️ Tecnologias utilizadas

| Tecnologia | Utilização |
|---|---|
| 🐍 **Python** | Linguagem utilizada no projeto |
| 🌐 **Flask** | Framework para desenvolvimento web |
| 🐳 **Docker** | Criação e execução do container |
| 🐧 **Lubuntu** | Sistema operacional da máquina virtual |
| 📦 **VirtualBox** | Virtualização do sistema |
| 🔐 **SSH** | Acesso ao terminal da máquina virtual |
| 🎨 **HTML e CSS** | Estrutura e estilização das páginas |

---

## 🏗️ Arquitetura do projeto

    🌐 Navegador
         |
         | http://IP_DA_VM:5000
         ↓
    ┌──────────────────────┐
    │   🐳 Docker          │
    │                      │
    │   Python 3.14-slim   │
    │   Flask              │
    │   Porta 5000         │
    │                      │
    └──────────────────────┘

A porta **5000** é utilizada pela aplicação Flask dentro do container.

---

## 📁 Estrutura do projeto

    flask-app/
    ├── 📄 app.py
    ├── 📄 requirements.txt
    ├── 📄 Dockerfile
    └── 📄 .dockerignore

### 📄 Função dos arquivos

| Arquivo | Função |
|---|---|
| `app.py` | Código da aplicação Flask e suas rotas |
| `requirements.txt` | Dependências utilizadas pela aplicação |
| `Dockerfile` | Instruções utilizadas para construir a imagem Docker |
| `.dockerignore` | Arquivos que não devem ser enviados para o build |

---

# 🚀 Desenvolvimento do projeto

## 1️⃣ Preparação da máquina virtual

Foi utilizada uma máquina virtual com **Lubuntu** no **VirtualBox**.

A placa de rede foi configurada e também foi utilizado o acesso por **SSH**, permitindo executar comandos diretamente no terminal da máquina virtual.

---

## 2️⃣ Verificação do Docker

Primeiramente, foi verificada a instalação do Docker utilizando:

    docker --version

Também foi executado o container de teste:

    sudo docker run hello-world

A mensagem apresentada confirmou que o Docker estava funcionando corretamente.

---

## 3️⃣ Criação da aplicação Flask

Foi criada a pasta do projeto:

    mkdir flask-app
    cd flask-app

Dentro dela foi criado o arquivo `app.py`, responsável pela aplicação Flask.

A aplicação inicialmente apresentava uma mensagem de teste com os nomes dos integrantes e a turma.

A aplicação foi configurada para utilizar a porta **5000**.

---

## 4️⃣ Criação do requirements.txt

Foi criado o arquivo `requirements.txt` para informar as dependências utilizadas pela aplicação.

    Flask

Esse arquivo permite que o Docker instale automaticamente o Flask durante a construção da imagem.

---

## 5️⃣ Criação do Dockerfile

O `Dockerfile` define as instruções utilizadas para construir a imagem Docker.

    FROM python:3.14-slim

    WORKDIR /app

    COPY requirements.txt .

    RUN pip install --no-cache-dir -r requirements.txt

    COPY app.py .

    EXPOSE 5000

    CMD ["python", "app.py"]

### 🔎 Principais instruções

| Instrução | Função |
|---|---|
| `FROM` | Define a imagem base utilizada |
| `WORKDIR` | Define o diretório de trabalho dentro do container |
| `COPY` | Copia arquivos para dentro da imagem |
| `RUN` | Executa comandos durante a construção da imagem |
| `EXPOSE` | Indica a porta utilizada pela aplicação |
| `CMD` | Define o comando executado ao iniciar o container |

---

## 6️⃣ Construção da imagem Docker

A imagem foi construída utilizando o comando:

    sudo docker build -t flask-app .

Depois, a imagem criada foi verificada com:

    sudo docker images

A imagem recebeu o nome:

    flask-app

---

## 7️⃣ Criação e execução do container

O container foi executado utilizando:

    sudo docker run -d -p 5000:5000 --name flask-container flask-app

### 🔎 Entendendo o comando

**`-d`**  
Executa o container em segundo plano.

**`-p 5000:5000`**  
Faz a ligação entre a porta **5000 da máquina** e a porta **5000 do container**.

**`--name flask-container`**  
Define o nome do container.

**`flask-app`**  
Indica a imagem utilizada para criar o container.

Para verificar se o container estava funcionando:

    sudo docker ps

O container recebeu o nome:

    flask-container

---

## 8️⃣ Teste da aplicação

Com o container em execução, foi utilizado o comando:

    curl http://localhost:5000

Também foi utilizado o navegador para acessar a aplicação pela porta **5000**.

---

# ✨ Expansão da aplicação - Desafio

Como parte da expansão da atividade, a aplicação foi modificada para possuir novas páginas e uma apresentação visual mais organizada.

Foram criadas três rotas:

| Rota | Página |
|---|---|
| `/` | 🏠 Página inicial |
| `/sobre` | 📖 Sobre |
| `/contato` | 📩 Contato |

---

## 🏠 Página inicial

A página inicial recebeu uma apresentação mais organizada e botões para acessar as páginas **Sobre** e **Contato**.

A interface também recebeu melhorias visuais utilizando **HTML e CSS**.

---

## 📖 Página Sobre

A rota:

    /sobre

apresenta informações sobre o projeto e as tecnologias utilizadas.

---

## 📩 Página Contato

A rota:

    /contato

apresenta informações dos integrantes e possui um espaço destinado ao e-mail.

As páginas receberam estilos próprios utilizando **HTML e CSS**.

---

# 🔄 Rebuild da imagem

Depois das alterações realizadas na aplicação, foi necessário reconstruir a imagem Docker:

    sudo docker build -t flask-app .

O **rebuild** foi necessário para que as alterações realizadas no projeto fossem incluídas na nova imagem.

---

# ✅ Teste final

Depois da reconstrução da imagem, o container atualizado foi executado novamente e verificado com:

    sudo docker ps

As novas rotas foram testadas pelo navegador:

    http://IP_DA_VM:5000/
    http://IP_DA_VM:5000/sobre
    http://IP_DA_VM:5000/contato

Dessa forma, foi possível verificar o funcionamento da aplicação Flask dentro do container Docker.

---

# 💻 Comandos principais

    # Verificar a versão do Docker
    sudo docker --version

    # Executar container de teste
    sudo docker run hello-world

    # Construir a imagem
    sudo docker build -t flask-app .

    # Verificar as imagens
    sudo docker images

    # Executar o container
    sudo docker run -d -p 5000:5000 --name flask-container flask-app

    # Verificar containers em execução
    sudo docker ps

    # Testar a aplicação
    curl http://localhost:5000

---

# 🎯 Resultado final

Ao final da atividade, foi obtida uma **aplicação Flask funcionando dentro de um container Docker**.

O projeto passou pelas seguintes etapas:

- ✅ Configuração da máquina virtual
- ✅ Configuração do acesso por SSH
- ✅ Instalação e teste do Docker
- ✅ Criação da aplicação Flask
- ✅ Criação do `requirements.txt`
- ✅ Criação do `Dockerfile`
- ✅ Construção da imagem Docker
- ✅ Execução do container
- ✅ Teste da aplicação
- ✅ Criação das rotas `/sobre` e `/contato`
- ✅ Melhorias visuais com HTML e CSS
- ✅ Rebuild da imagem
- ✅ Testes finais no navegador

---

# 👥 Integrantes

### Camila e Arthur

🎓 **Turma:** 2° Informática

---

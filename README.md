# Estudo de CI/CD: Deploy na Vercel com GitHub Actions

![Status do Workflow de Deploy](https://github.com/fernanda-vaz/alura-ci-cd/actions/workflows/deploy-vercel.yml/badge.svg)

Este projeto é um exercício prático focado em **Integração Contínua e Deploy Contínuo (CI/CD)**. O objetivo foi criar um pipeline automatizado usando **GitHub Actions** para realizar o deploy de uma aplicação simples em **React + Vite + TypeScript** na plataforma **Vercel**.

O desenvolvimento da aplicação em si foi mínimo, servindo apenas como base para o estudo do processo de automação, inspirado pelos conhecimentos adquiridos no curso **NextJS:** CI e CD para Front-end com Github Actions da plataforma [**Alura**](https://www.alura.com.br/).

## ✨ Tecnologias Utilizadas

* **Frontend:** React com Vite e TypeScript
* **Plataforma de Deploy:** Vercel
* **Automação (CI/CD):** GitHub Actions
* **Gerenciador de Pacotes:** NPM

---

## 🚀 O Pipeline de CI/CD (`deploy-vercel.yml`)

O coração deste estudo é o workflow definido no arquivo `.github/workflows/deploy-vercel.yml`. Este pipeline é acionado automaticamente a cada `push` na branch `main` e utiliza a CLI da Vercel para um controle preciso sobre o processo.

As etapas executadas são:

1.  **Checkout code**: A Action `actions/checkout@v4` baixa o código do repositório para o ambiente de execução do workflow.

2.  **Install Vercel CLI**: Instala a versão mais recente da interface de linha de comando da Vercel, que será usada para os passos seguintes.

3.  **Pull Vercel Environment Information**: O comando `vercel pull` é executado para sincronizar as configurações do projeto Vercel (como `projectId` e `orgId`) e as variáveis de ambiente de produção. Isso garante que o build seja feito com o contexto correto.

4.  **Build Project Artifacts**: O comando `vercel build` é usado para compilar a aplicação. A Vercel CLI é inteligente e detecta que se trata de um projeto React + Vite, executando os comandos de build apropriados (`npm run build`).

5.  **Deploy Project to Vercel**: Por fim, o comando `vercel deploy --prebuilt --prod` faz o upload dos artefatos já compilados na etapa anterior. A flag `--prebuilt` informa à Vercel que não é necessário buildar novamente, e a flag `--prod` promove esta versão diretamente para o ambiente de produção.

### Variáveis de Ambiente (Secrets)

Para que o GitHub Actions pudesse se autenticar e executar os comandos da Vercel, foi necessário configurar os seguintes **Secrets** no repositório do GitHub (em `Settings > Secrets and variables > Actions`):

* `VERCEL_TOKEN`: Token de acesso gerado na conta da Vercel para permitir a autenticação.
* `VERCEL_ORG_ID`: ID da organização (ou do usuário) na Vercel.
* `VERCEL_PROJECT_ID`: ID do projeto específico criado na Vercel.

---

## ⚙️ Como Executar o Projeto Localmente

Embora o foco seja o deploy, a aplicação pode ser executada localmente.

### Pré-requisitos

* [Node.js](https://nodejs.org/en/) (versão 18.x ou superior)
* [NPM](https://www.npmjs.com/) ou [Yarn](https://yarnpkg.com/)

### Passos

1.  Clone o repositório:
    ```bash
    git clone [https://github.com/](https://github.com/)fernanda-vaz/alura-ci-cd.git
    ```
2.  Navegue até a pasta do projeto:
    ```bash
    cd alura-ci-cd
    ```
3.  Instale as dependências:
    ```bash
    npm install
    ```
4.  Inicie o servidor de desenvolvimento:
    ```bash
    npm run dev
    ```
5.  Abra [http://localhost:5173](http://localhost:5173) no seu navegador.

---

## 🌐 Deploy

O deploy é feito automaticamente. Para ver a versão publicada, acesse:

**[https://ci-cd-rho.vercel.app/](https://ci-cd-rho.vercel.app/)**

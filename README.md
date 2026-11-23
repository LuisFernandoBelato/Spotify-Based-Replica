## 🌐 Language | Idioma

[🇺🇸 English (Default)](#en) | [🇧🇷 Português](#pt)

<div id="en"></div>

---

# MusicStream: A Spotify-Based Replica \ ***7th Term - LP 2***

This project is a full-stack web application developed as a simplified replica of Spotify, focused on managing users, songs, and playlists. It is built with a Node.js (Express) backend, a Vue.js frontend, and uses MongoDB as the database, all orchestrated via Docker Compose for a consistent development environment.

## Overview

The application allows users to log in, manage their profiles, upload and organize their songs, and create playlists. The user interface is inspired by Spotify's design, offering an intuitive experience for navigation and interaction with musical content.

## Main Features

### **User Management:**
*   **Creation, Reading, Updating, and Deletion (CRUD):** Total control over user profiles.
*   **Authentication:** Secure login system with password hashing (`bcrypt`) and JSON Web Tokens (JWT) for authenticated sessions.
*   **Address Auto-fill:** Integration with the ViaCEP API for automatic filling of street, neighborhood, and state based on the Zip Code (CEP).

### **Song Management:**
*   **CRUD:** Ability to add, view, edit, and remove songs.
*   **Media Upload:** Support for uploading audio files and thumbnails associated with songs.
*   **Organization by Author:** Songs are associated with an `autorId`, allowing the listing of songs by user.

### **Playlist Management:**
*   **CRUD:** Creation, viewing, editing, and deletion of playlists.
*   **Adding Songs:** Playlists can include multiple songs (by their IDs).
*   **Permissions:** Playlists can be defined as "Public" or "Private".
*   **Thumbnail Upload:** Support for uploading cover images for playlists.

  ---

## Technologies Used

### **Backend (Node.js/Express):**

*   **Docker:** To package and isolate backend, frontend, and database environments.
*   **Docker Compose:** To define and run multi-container Docker applications with a single command line.
*   **Node.js:** JavaScript runtime environment.
*   **Express.js:** Web framework to build the RESTful API.
*   **MongoDB & Mongoose:** NoSQL database and ODM (Object Data Modeling) for interaction with MongoDB.
*   **Bcrypt:** Library for password hashing.
*   **JSON Web Tokens (JWT):** For user authentication and authorization.
*   **Multer:** Middleware for handling file uploads (audio and images).
*   **Helmet:** Helps secure the Express application against security vulnerabilities.
*   **Express-Rate-Limit:** Middleware to limit repeated requests to the same API, to prevent brute-force attacks.
*   **CORS:** Middleware to enable Cross-Origin Resource Sharing.
*   **Compression:** For HTTP response data compression.
*   **Morgan:** HTTP request logger.
*   **Dotenv:** To load environment variables.

### **Frontend (Vue.js):**
*   **Vue.js 3:** Progressive JavaScript framework for building the user interface.
*   **Vue Router:** Route management and SPA (Single Page Application) navigation.
*   **Tailwind CSS:** Utility-first CSS framework for fast and responsive styles.
*   **Axios:** HTTP client to make requests to the backend API.

## Environment Setup

Secrets are not tracked in git. Create your local files from the templates and fill in the values:

```bash
cp .env.example .env
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env
```

*   `MONGO_INITDB_ROOT_PASSWORD` is only applied when the MongoDB data volume is first created. To change it later, update the password inside MongoDB or recreate the volume.
*   With Docker Compose, use `database` as the MongoDB host in `MONGODB_URI`, since that is the service name on the compose network.

## Known Dev Dependency Advisories

`npm audit` still reports advisories in the frontend's Vue CLI 5 development toolchain (`@vue/cli-service`, `webpack-dev-server`, `@vue/cli-plugin-eslint`, and related packages). The only automatic fixes are major upgrades (webpack-dev-server 5, or a downgrade of `@vue/cli-plugin-eslint`), which require changes to the build setup, so they were deferred. The frontend Docker service runs this dev server, so run it only on trusted networks.

## Project Entities

The project is built around the following main entities:

*   **USER:**
    *   Represents the platform user. Can be a normal user or an **Author** (one who uploads songs).
    *   Stores information such as `name`, `email`, `password` (hashed), and `address` data (street, neighborhood, state, CEP).
*   **SONG (AUDIO):**
    *   Represents an audio track available on the platform.
    *   Has `name`, `artist`, `genre`, `filePath` (path to the audio file), `thumbnailPath` (path to the thumbnail), and `autorId` (linked to USER).
*   **PLAYLIST:**
    *   Collection of songs.
    *   Has `name`, `description`, `donoId` (linked to the USER who created the playlist), an array of `musicasIds` (linked to SONGS), `permission` (public/private), and `thumbnailPath`.

---

## API Endpoints

A Postman collection has been provided to facilitate testing the backend endpoints. Import the file `Rotas-Postman/Spotify - Collection.postman_collection.json` into your Postman.

The endpoints include CRUD operations for:

*   **Users:**
    *   `POST /create-user`
    *   `GET /get-users`
    *   `GET /get-user/:id`
    *   `PUT /edit-user/:id`
    *   `DELETE /delete-user/:id`
*   **Songs:**
    *   `POST /create-music` (supports `form-data` for files)
    *   `GET /get-musics`
    *   `GET /get-music/:id`
    *   `GET /get-musics-by-user/:autorId`
    *   `PUT /edit-music/:id` (supports `form-data` for files)
    *   `DELETE /delete-music/:id`
*   **Playlists:**
    *   `POST /create-playlist` (supports `form-data` for thumbnail and `musicasIdsArray` as JSON string)
    *   `GET /get-playlists`
    *   `GET /get-playlist/:id`
    *   `GET /get-playlists-by-user/:donoId`
    *   `PUT /edit-playlist/:id` (supports `form-data` for thumbnail)
    *   `DELETE /delete-playlist/:id`
*   **Authentication:**
    *   `POST /login` (to authenticate users)
    *   `POST /logout` (to end sessions)

<div id="pt"></div>

---

# MusicStream: Uma Réplica Baseada no Spotify \ ***7º Termo - LP 2***

Este projeto é uma aplicação web full-stack desenvolvida como uma réplica simplificada do Spotify, focada no gerenciamento de usuários, músicas e playlists. Ele é construído com um backend em Node.js (Express), um frontend em Vue.js e utiliza MongoDB como banco de dados, tudo orquestrado via Docker Compose para um ambiente de desenvolvimento consistente.

## Visão Geral

A aplicação permite que usuários façam login, gerenciem seus perfis, carreguem e organizem suas músicas, e criem playlists. A interface do usuário é inspirada no design do Spotify, oferecendo uma experiência intuitiva para navegação e interação com o conteúdo musical.

## Funcionalidades Principais


### **Gerenciamento de Usuários:**
*   **Criação, Leitura, Atualização e Exclusão (CRUD):** Total controle sobre os perfis de usuário.
*   **Autenticação:** Sistema de login seguro com hashing de senhas (`bcrypt`) e JSON Web Tokens (JWT) para sessões autenticadas.
*   **Preenchimento Automático de Endereço:** Integração com a API ViaCEP para preenchimento automático de logradouro, bairro e estado com base no CEP.

### **Gerenciamento de Músicas:**
*   **CRUD:** Capacidade de adicionar, visualizar, editar e remover músicas.
*   **Upload de Mídia:** Suporte para upload de arquivos de áudio e miniaturas (thumbnails) associadas às músicas.
*   **Organização por Autor:** Músicas são associadas a um `autorId`, permitindo a listagem de músicas por usuário.

### **Gerenciamento de Playlists:**
*   **CRUD:** Criação, visualização, edição e exclusão de playlists.
*   **Adição de Músicas:** Playlists podem incluir múltiplas músicas (por seus IDs).
*   **Permissões:** Playlists podem ser definidas como "Públicas" ou "Privadas".
*   **Upload de Thumbnail:** Suporte para upload de imagens de capa para as playlists.

  ---

## Tecnologias Utilizadas

### **Backend (Node.js/Express):**

*   **Docker:** Para empacotar e isolar os ambientes do backend, frontend e banco de dados.
*   **Docker Compose:** Para definir e executar aplicações Docker multi-contêineres com uma única linha de comando.
*   **Node.js:** Ambiente de execução JavaScript.
*   **Express.js:** Framework web para construir a API RESTful.
*   **MongoDB & Mongoose:** Banco de dados NoSQL e ODM (Object Data Modeling) para interação com o MongoDB.
*   **Bcrypt:** Biblioteca para hashing de senhas.
*   **JSON Web Tokens (JWT):** Para autenticação e autorização de usuários.
*   **Multer:** Middleware para tratamento de upload de arquivos (áudio e imagens).
*   **Helmet:** Ajuda a proteger a aplicação Express contra vulnerabilidades de segurança.
*   **Express-Rate-Limit:** Middleware para limitar requisições repetidas para a mesma API, para evitar ataques de força bruta.
*   **CORS:** Middleware para habilitar o Compartilhamento de Recursos de Origem Cruzada.
*   **Compression:** Para compressão de dados da resposta HTTP.
*   **Morgan:** Logger de requisições HTTP.
*   **Dotenv:** Para carregar variáveis de ambiente.

### **Frontend (Vue.js):**
*   **Vue.js 3:** Framework JavaScript progressivo para a construção da interface do usuário.
*   **Vue Router:** Gerenciamento de rotas e navegação da SPA (Single Page Application).
*   **Tailwind CSS:** Framework CSS utility-first para estilos rápidos e responsivos.
*   **Axios:** Cliente HTTP para fazer requisições à API do backend.

## Configuração do Ambiente

Os segredos não são versionados no git. Crie seus arquivos locais a partir dos modelos e preencha os valores:

```bash
cp .env.example .env
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env
```

*   `MONGO_INITDB_ROOT_PASSWORD` só é aplicada quando o volume de dados do MongoDB é criado pela primeira vez. Para alterá-la depois, troque a senha dentro do MongoDB ou recrie o volume.
*   Com o Docker Compose, use `database` como host do MongoDB em `MONGODB_URI`, pois é o nome do serviço na rede do compose.

## Avisos Conhecidos de Dependências de Desenvolvimento

O `npm audit` ainda aponta avisos na cadeia de desenvolvimento do Vue CLI 5 do frontend (`@vue/cli-service`, `webpack-dev-server`, `@vue/cli-plugin-eslint` e pacotes relacionados). As únicas correções automáticas são upgrades major (webpack-dev-server 5, ou downgrade do `@vue/cli-plugin-eslint`), que exigem mudanças na configuração de build; por isso foram adiadas. O serviço `application` do Docker roda esse servidor de desenvolvimento, então execute-o apenas em redes confiáveis.

## Entidades do Projeto

O projeto é construído em torno das seguintes entidades principais:

*   **USUÁRIO:**
    *   Representa o usuário da plataforma. Pode ser um usuário normal ou um **Autor** (aquele que envia músicas).
    *   Armazena informações como `nome`, `email`, `senha` (hashed), e dados de `endereço` (logradouro, bairro, estado, CEP).
*   **MÚSICA (ÁUDIO):**
    *   Representa uma faixa de áudio disponível na plataforma.
    *   Possui `nome`, `artist`, `genero`, `filePath` (caminho para o arquivo de áudio), `thumbnailPath` (caminho para a miniatura), e `autorId` (ligada ao USUÁRIO).
*   **PLAYLIST:**
    *   Coleção de músicas.
    *   Possui `nome`, `descricao`, `donoId` (ligada ao USUÁRIO que criou a playlist), um array de `musicasIds` (ligada a MÚSICAS), `permission` (pública/privada), e `thumbnailPath`.

---

## Endpoints da API

Uma coleção do Postman foi fornecida para facilitar o teste dos endpoints do backend. Importe o arquivo `Rotas-Postman/Spotify - Collection.postman_collection.json` para o seu Postman.

Os endpoints incluem operações CRUD para:

*   **Usuários:**
    *   `POST /create-user`
    *   `GET /get-users`
    *   `GET /get-user/:id`
    *   `PUT /edit-user/:id`
    *   `DELETE /delete-user/:id`
*   **Músicas:**
    *   `POST /create-music` (suporta `form-data` para arquivos)
    *   `GET /get-musics`
    *   `GET /get-music/:id`
    *   `GET /get-musics-by-user/:autorId`
    *   `PUT /edit-music/:id` (suporta `form-data` para arquivos)
    *   `DELETE /delete-music/:id`
*   **Playlists:**
    *   `POST /create-playlist` (suporta `form-data` para thumbnail e `musicasIdsArray` como JSON string)
    *   `GET /get-playlists`
    *   `GET /get-playlist/:id`
    *   `GET /get-playlists-by-user/:donoId`
    *   `PUT /edit-playlist/:id` (suporta `form-data` para thumbnail)
    *   `DELETE /delete-playlist/:id`
*   **Autenticação:**
    *   `POST /login` (para autenticar usuários)
    *   `POST /logout` (para encerrar sessões)

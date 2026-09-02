# 📝 Blog Pessoal — Front-End em React & TypeScript

![React](https://img.shields.io/badge/React-19.2-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-8.0-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4.2-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![React Router](https://img.shields.io/badge/React_Router-7.1-CA4245?style=for-the-badge&logo=reactrouter&logoColor=white)
![Axios](https://img.shields.io/badge/Axios-REST_Client-5A29E4?style=for-the-badge&logo=axios&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen?style=for-the-badge)
![Licença](https://img.shields.io/badge/Licença-MIT-yellow?style=for-the-badge)

---

## 🔗 Acesso e Rotas da Aplicação

* **Ambiente de Desenvolvimento:** `http://localhost:5173`
* **Rotas Principais:**
  * `/`: Página de Login e Autenticação
  * `/cadastro`: Cadastro de Novos Usuários
  * `/home`: Painel Principal com Feed e Criação Rápida
  * `/postagens`: Listagem e Gestão Completa de Postagens
  * `/temas`: Listagem e Gestão de Categorias/Temas
  * `/perfil`: Visualização dos Dados do Usuário Conectado

---

## 📖 Visão Geral

O **Blog Pessoal** é uma aplicação web Single Page Application (SPA) desenvolvida em **React 19**, **TypeScript** e **Tailwind CSS**, criada como interface cliente do ecossistema de aprendizado do bootcamp **Generation Brasil (Turma JS13)**.

A plataforma consome uma API RESTful (NestJS ou Spring Boot) para gerenciar o ciclo de vida completo de postagens e temas. O projeto implementa controle de acesso autenticado com tokens **JWT**, gerenciamento de estado global centralizado via **Context API (`AuthContext`)**, rotas protegidas que impedem acessos não autorizados e componentes modulares com feedback reativo via **React Toastify** e loaders visuais.

---

## ✨ Funcionalidades

* 🔐 **Autenticação e Sessão de Usuário:**
  * Login com e-mail e senha, armazenando token JWT e dados do perfil no estado global da aplicação.
  * Cadastro de novos usuários com suporte a avatar fotográfico via URL externa.
  * Logout com encerramento de sessão, limpeza de estado e redirecionamento automático.
  * Tratamento defensivo de expiração de token: requisições com status `HTTP 401` efetuam logout automático.
* 📚 **Gestão Completa de Temas (CRUD):**
  * Listagem em cards estilizados de todas as categorias cadastradas.
  * Formulário dinâmico reaproveitável para cadastro e edição (`/cadastrartema` e `/editartema/:id`).
  * Tela de confirmação de exclusão com alerta de integridade (`/deletartema/:id`).
* 📰 **Gestão de Postagens (CRUD Completo):**
  * Feed de postagens com paginação visual em cards responsivos contendo título, texto, tema associado, data formatada (`Intl.DateTimeFormat`) e dados do autor.
  * Modal interativo de criação rápida (`ModalPostagem` via `reactjs-popup`) integrado diretamente na Home.
  * Atualização e exclusão com diálogo de confirmação.
* 🔔 **Feedback Reativo ao Usuário:** Notificações toast estilizadas em tempo real para sucesso, informação e erro (`ToastAlerta`).
* ⏳ **Indicadores de Carregamento Assíncrono:** Spinners visuais (`SyncLoader` e `ClipLoader`) em botões e áreas de consulta durante chamadas de rede.

---

## 🎯 Diferenciais e Destaques Técnicos

1. **Estado Global Centralizado com Context API (`AuthContext`):** Desacoplamento da lógica de autenticação do componente visual, permitindo que componentes como `Navbar`, `Footer` e formulários acessem o token e disparem logout de forma uniforme.
2. **Renderização Condicional de Layout:** Componentes estruturais como `Navbar` e `Footer` monitoram a existência do token no contexto, ocultando menus de navegação nas telas públicas de login e cadastro.
3. **Mapeamento de Modelos TypeScript Estritos:** Contratos de interface tipados (`Usuario`, `UsuarioLogin`, `Tema`, `Postagem`) garantindo segurança de tipos de ponta a ponta nas chamadas da API.
4. **Camada de Serviço Centralizada (`Service.ts`):** Abstração de requisições HTTP (`buscar`, `cadastrar`, `atualizar`, `deletar`) sobre a instância do Axios, padronizando cabeçalhos `Authorization: Bearer <token>`.

---

## 🏗️ Arquitetura e Estrutura de Pastas

```text
src/
├── assets/                     # Recursos gráficos estáticos
├── components/                 # Componentes reutilizáveis
│   ├── footer/                 # Rodapé dinâmico com links sociais
│   ├── navbar/                 # Barra de navegação com controle de logout
│   ├── postagem/               # Componentes de Postagens
│   │   ├── cardpostagem/       # Card individual de exibição de post
│   │   ├── deletarpostagem/    # Diálogo de exclusão de postagem
│   │   ├── formpostagem/       # Formulário de criação e edição
│   │   ├── listapostagens/     # Feed em grid com loader assíncrono
│   │   └── modalpostagem/      # Modal popup de publicação rápida
│   └── tema/                   # Componentes de Temas
│       ├── cardtema/           # Card individual de tema
│       ├── deletartema/        # Confirmação de exclusão de tema
│       ├── formtema/           # Formulário de cadastro/edição de tema
│       └── listatemas/         # Listagem geral de temas
├── contexts/                   # Estado global
│   └── AuthContext.tsx         # Contexto e Provider de Autenticação
├── models/                     # Interfaces TypeScript (DTOs do Frontend)
│   ├── Postagem.ts
│   ├── Tema.ts
│   ├── Usuario.ts
│   └── UsuarioLogin.ts
├── pages/                      # Telas completas da aplicação
│   ├── cadastro/               # Tela de registro de novo usuário
│   ├── home/                   # Dashboard inicial
│   ├── login/                  # Tela de autenticação
│   └── perfil/                 # Página de perfil do usuário logado
├── services/                   # Integração com API REST
│   └── Service.ts              # Funções de requisição HTTP com Axios
├── utils/                      # Utilitários globais
│   └── ToastAlerta.ts          # Centralizador de alertas visuais (Toastify)
├── App.tsx                     # Roteador central e provedores de contexto
├── index.css                   # Configurações globais do Tailwind CSS
└── main.tsx                    # Inicialização do DOM React
```

---

## 🎨 UX e Fluxo de Navegação

```text
               +-----------------------+
               |  Tela de Login  (/)   |
               +-----------------------+
                 | (Login com sucesso)   \ (Sem conta?)
                 v                        v
+-----------------------------+     +--------------------------+
|  Home (/home) & Feed        |     |  Cadastro (/cadastro)    |
|  - Modal Nova Postagem      |     +--------------------------+
+-----------------------------+
   |            |            |
   v            v            v
[Temas]    [Postagens]   [Perfil]
Listagem    Listagem      Dados do
/temas      /postagens    Usuário
```

---

## 🧭 Passo a Passo de Uso da Aplicação

1. **Acesso e Cadastro:** Acesse a aplicação na rota inicial `/`. Se ainda não possuir credenciais, clique em *Cadastre-se* e preencha nome, e-mail, senha e URL de avatar.
2. **Autenticação:** Faça login para ser redirecionado ao painel principal (`/home`). A barra de navegação completa será habilitada automaticamente.
3. **Gerenciamento de Temas:** Antes de publicar, navegue até `/temas` e verifique os temas cadastrados ou acesse `/cadastrartema` para criar um novo assunto (ex: *Tecnologia*, *Carreira*, *Dicas*).
4. **Publicação de Postagem:** Clique no botão *Nova Postagem* na Home para abrir o modal suspenso, informe título, texto e selecione o tema desejado no dropdown.
5. **Feed e Moderação:** No menu *Postagens*, visualize todas as publicações da comunidade com opção de editar ou excluir suas próprias postagens.
6. **Encerramento:** Clique em *Sair* na Navbar para revogar a sessão local com segurança.

---

## ⚙️ Requisitos e Instalação

### Pré-requisitos
* **Node.js:** Versão 18 ou superior.
* **Gerenciador de Pacotes:** `npm` (ou `yarn`).
* **Back-End Ativo:** API do Blog Pessoal rodando localmente ou na nuvem (porta padrão: `8080` ou `3000`).

### 1. Clonar o Repositório
```bash
git clone https://github.com/erickystn/generation_JS13_blogpessoal_React.git
cd generation_JS13_blogpessoal_React
```

### 2. Instalar as Dependências
```bash
npm install
```

### 3. Configurar a URL da API
Abra o arquivo `src/services/Service.ts` e certifique-se de que a `baseURL` aponta para o endereço do seu backend:
```typescript
import axios from "axios";

export const api = axios.create({
    baseURL: import.meta.env.VITE_API_URL || "http://localhost:8080"
});
```
Ou crie um arquivo `.env` na raiz do projeto:
```env
VITE_API_URL=http://localhost:8080
```

---

## 🚀 Como Executar

### Ambiente de Desenvolvimento
```bash
npm run dev
```
O Vite iniciará o servidor local em `http://localhost:5173`.

### Compilação para Produção
```bash
npm run build
```

### Visualização do Build de Produção
```bash
npm run preview
```

---

## 💻 Exemplos de Código e Integração

### 1. Consumo do Contexto de Autenticação (`AuthContext`)
```typescript
import { useContext } from "react";
import { AuthContext } from "../../contexts/AuthContext";

function ExemploComponente() {
    const { usuario, handleLogout } = useContext(AuthContext);

    return (
        <div>
            <h2>Olá, {usuario.nome}!</h2>
            <button onClick={handleLogout}>Desconectar</button>
        </div>
    );
}
```

### 2. Requisições Autenticadas com Token JWT via Axios
```typescript
// Chamada padronizada passando o token de autorização
await buscar('/postagens', setPostagens, {
    headers: { 
        Authorization: usuario.token 
    }
});
```

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Versão | Finalidade |
| :--- | :--- | :--- |
| **React** | 19.2 | Biblioteca declarativa para construção de interfaces SPA |
| **TypeScript** | 5.9 | Tipagem estática, interfaces e robustez de código |
| **Vite** | 8.0 | Ferramenta de build ultra-rápida e Hot Module Replacement |
| **Tailwind CSS** | 4.2 | Framework CSS utilitário para estilização responsiva |
| **React Router DOM**| 7.13 | Roteamento declarativo no cliente e parâmetros de URL |
| **Axios** | 1.x | Cliente HTTP para consumo de endpoints REST |
| **React Toastify** | 11.0 | Sistema de notificações toast para feedback ao usuário |
| **Reactjs-popup** | 2.0 | Modais e popups acessíveis |
| **React Spinners** | 0.17 | Indicadores de carregamento para requisições assíncronas |
| **Phosphor Icons** | 2.1 | Biblioteca de ícones vetoriais modernos |

---

## 📈 Melhorias e Próximos Passos (Roadmap)

- [ ] Implementação de **Dark Mode** toggle com persistência no navegador.
- [ ] Criação de campo de busca textual em tempo real no feed de postagens.
- [ ] Sistema de comentários e curtidas por postagem.
- [ ] Suíte de testes unitários e de integração com **Vitest** e **React Testing Library**.
- [ ] Validação visual de formulários com **React Hook Form** e **Zod**.

---

## 🤝 Como Contribuir

1. Faça um **Fork** do projeto.
2. Crie uma branch para sua modificação:
   ```bash
   git checkout -b feature/sua-feature
   ```
3. Commit suas alterações:
   ```bash
   git commit -m 'feat: adiciona campo de busca de postagens'
   ```
4. Suba para a branch:
   ```bash
   git push origin feature/sua-feature
   ```
5. Abra um **Pull Request** detalhado.

---

## 👤 Autor & 📄 Licença

Desenvolvido por **[Ericky Sant'ana](https://github.com/erickystn)** durante as atividades de desenvolvimento web da **Generation Brasil**.

Distribuído sob a licença **MIT**.

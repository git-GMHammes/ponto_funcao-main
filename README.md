# 📊 Sistema de Pontos de Função

Sistema completo para cadastro, cálculo e gestão de Pontos de Função (PF) para estimativa de esforço em projetos de software.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![PHP Version](https://img.shields.io/badge/PHP-8.1%2B-purple.svg)
![React](https://img.shields.io/badge/React-18.x-blue.svg)
![CodeIgniter](https://img.shields.io/badge/CodeIgniter-4.x-orange.svg)

## 📋 Sobre o Projeto

O **Sistema de Pontos de Função** é uma aplicação web desenvolvida para auxiliar equipes de desenvolvimento e gerentes de projeto na estimativa de esforço através da metodologia de Análise de Pontos de Função (APF). O sistema permite o cadastro detalhado de funções de dados e transações, aplicando automaticamente os cálculos conforme as normas do IFPUG (International Function Point Users Group).

### 🎯 Objetivo

Facilitar e automatizar o processo de contagem de pontos de função, proporcionando:
- Cadastro organizado de funcionalidades do sistema
- Cálculo automático de pontos de função brutos e ajustados
- Histórico de projetos e suas estimativas
- Geração de relatórios para documentação

## ✨ Funcionalidades

- ✅ **Cadastro de Projetos**: Gerenciamento completo de projetos
- ✅ **Funções de Dados**:
  - ALI (Arquivo Lógico Interno)
  - AIE (Arquivo de Interface Externa)
- ✅ **Funções Transacionais**:
  - EE (Entrada Externa)
  - SE (Saída Externa)
  - CE (Consulta Externa)
- ✅ **Cálculo Automático**: PF Bruto e PF Ajustado
- ✅ **Fator de Ajuste**: Configuração das 14 características gerais do sistema
- ✅ **Relatórios**: Visualização detalhada dos cálculos
- ✅ **Dashboard**: Visão geral dos projetos e métricas
- ✅ **Exportação**: PDF e Excel dos resultados

## 🚀 Tecnologias Utilizadas

### Backend
- **PHP 8.1+**
- **CodeIgniter 4.x** - Framework PHP
- **MySQL 8.0+** - Banco de dados relacional
- **JWT** - Autenticação de API

### Frontend
- **React 18.x** - Biblioteca JavaScript
- **React Router DOM** - Gerenciamento de rotas
- **Axios** - Cliente HTTP
- **Material-UI / Tailwind CSS** - Estilização
- **React Hook Form** - Gerenciamento de formulários
- **Chart.js** - Gráficos e visualizações

### Ferramentas de Desenvolvimento
- **Docker** - Containerização
- **Composer** - Gerenciador de dependências PHP
- **NPM/Yarn** - Gerenciador de pacotes JavaScript
- **Git** - Controle de versão

## 📁 Estrutura do Projeto
```
ponto_funcao-main/
├── backend/
│   ├── app/
│   │   ├── Config/
│   │   ├── Controllers/
│   │   │   ├── ProjetoController.php
│   │   │   ├── PontoFuncaoController.php
│   │   │   └── RelatorioController.php
│   │   ├── Models/
│   │   │   ├── ProjetoModel.php
│   │   │   ├── FuncaoDadosModel.php
│   │   │   ├── FuncaoTransacionalModel.php
│   │   │   └── FatorAjusteModel.php
│   │   ├── Database/
│   │   │   └── Migrations/
│   │   └── Filters/
│   ├── public/
│   └── .env
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Projeto/
│   │   │   ├── FuncaoDados/
│   │   │   ├── FuncaoTransacional/
│   │   │   ├── FatorAjuste/
│   │   │   └── Relatorio/
│   │   ├── pages/
│   │   │   ├── Dashboard.jsx
│   │   │   ├── Projetos.jsx
│   │   │   ├── CadastroFuncoes.jsx
│   │   │   └── Resultado.jsx
│   │   ├── services/
│   │   │   └── api.js
│   │   ├── utils/
│   │   ├── App.jsx
│   │   └── main.jsx
│   └── package.json
│
├── database/
│   └── ponto_funcao.sql
│
├── docker-compose.yml
├── .gitignore
└── README.md
```

## 🔧 Requisitos

- PHP >= 8.1
- Composer
- Node.js >= 18.x
- NPM ou Yarn
- MySQL >= 8.0
- Docker (opcional)

## 📦 Instalação

### 1. Clone o Repositório
```bash
git clone https://github.com/seu-usuario/ponto_funcao-main.git
cd ponto_funcao-main
```

### 2. Configuração do Backend
```bash
cd backend
composer install
```

Copie o arquivo de ambiente:
```bash
cp .env.example .env
```

Configure as variáveis de ambiente no arquivo `.env`:
```env
CI_ENVIRONMENT = development

database.default.hostname = localhost
database.default.database = ponto_funcao_db
database.default.username = root
database.default.password = sua_senha
database.default.DBDriver = MySQLi

JWT_SECRET_KEY = sua_chave_secreta_aqui
JWT_TIME_TO_LIVE = 3600
```

Execute as migrations:
```bash
php spark migrate
```

Execute os seeders (opcional):
```bash
php spark db:seed DatabaseSeeder
```

Inicie o servidor:
```bash
php spark serve
```

O backend estará disponível em: `http://localhost:8080`

### 3. Configuração do Frontend
```bash
cd frontend
npm install
# ou
yarn install
```

Crie o arquivo `.env` na raiz do frontend:
```env
VITE_API_URL=http://localhost:8080/api
```

Inicie o servidor de desenvolvimento:
```bash
npm run dev
# ou
yarn dev
```

O frontend estará disponível em: `http://localhost:5173`

### 4. Usando Docker (Alternativa)
```bash
docker-compose up -d
```

Isso irá inicializar:
- Backend (PHP/CodeIgniter): `http://localhost:8080`
- Frontend (React): `http://localhost:3000`
- MySQL: `localhost:3306`

## 🗄️ Estrutura do Banco de Dados

### Principais Tabelas

**projetos**
- id (PK)
- nome
- descricao
- data_inicio
- data_fim
- status
- created_at
- updated_at

**funcoes_dados**
- id (PK)
- projeto_id (FK)
- tipo (ALI/AIE)
- nome
- complexidade (baixa/media/alta)
- der (Dados Elementares Referenciados)
- rlr (Registros Lógicos Referenciados)
- pontos
- created_at

**funcoes_transacionais**
- id (PK)
- projeto_id (FK)
- tipo (EE/SE/CE)
- nome
- complexidade (baixa/media/alta)
- der
- alr (Arquivos Lógicos Referenciados)
- pontos
- created_at

**fatores_ajuste**
- id (PK)
- projeto_id (FK)
- caracteristica (1-14)
- nivel (0-5)
- created_at

**resultados**
- id (PK)
- projeto_id (FK)
- pf_bruto
- fator_ajuste
- pf_ajustado
- created_at

## 🔌 API Endpoints

### Autenticação
```http
POST /api/auth/login
POST /api/auth/register
POST /api/auth/logout
```

### Projetos
```http
GET    /api/projetos
GET    /api/projetos/:id
POST   /api/projetos
PUT    /api/projetos/:id
DELETE /api/projetos/:id
```

### Funções de Dados
```http
GET    /api/projetos/:id/funcoes-dados
POST   /api/funcoes-dados
PUT    /api/funcoes-dados/:id
DELETE /api/funcoes-dados/:id
```

### Funções Transacionais
```http
GET    /api/projetos/:id/funcoes-transacionais
POST   /api/funcoes-transacionais
PUT    /api/funcoes-transacionais/:id
DELETE /api/funcoes-transacionais/:id
```

### Fatores de Ajuste
```http
GET    /api/projetos/:id/fatores-ajuste
POST   /api/fatores-ajuste
PUT    /api/fatores-ajuste/:id
```

### Cálculos e Resultados
```http
GET    /api/projetos/:id/calcular
GET    /api/projetos/:id/relatorio
GET    /api/projetos/:id/exportar/pdf
GET    /api/projetos/:id/exportar/excel
```

## 📊 Metodologia de Cálculo

### Pontos de Função Bruto (PFB)

**Funções de Dados**
| Tipo | Complexidade | Pontos |
|------|--------------|--------|
| ALI  | Baixa        | 7      |
| ALI  | Média        | 10     |
| ALI  | Alta         | 15     |
| AIE  | Baixa        | 5      |
| AIE  | Média        | 7      |
| AIE  | Alta         | 10     |

**Funções Transacionais**
| Tipo | Complexidade | Pontos |
|------|--------------|--------|
| EE   | Baixa        | 3      |
| EE   | Média        | 4      |
| EE   | Alta         | 6      |
| SE   | Baixa        | 4      |
| SE   | Média        | 5      |
| SE   | Alta         | 7      |
| CE   | Baixa        | 3      |
| CE   | Média        | 4      |
| CE   | Alta         | 6      |

### Fator de Ajuste (FA)
```
FA = 0.65 + (0.01 × Σ GSC)
```

Onde GSC = Soma das 14 Características Gerais do Sistema (cada uma variando de 0 a 5)

### Pontos de Função Ajustado (PFA)
```
PFA = PFB × FA
```

## 🎨 Interface do Usuário

### Tela de Cadastro de Funções
```
┌─────────────────────────────────────────┐
│  Cadastro de Pontos de Função          │
├─────────────────────────────────────────┤
│                                         │
│  Tipo: [ALI ▼]                         │
│  Nome: [____________________________]  │
│  DER:  [__] RLR: [__]                  │
│  Complexidade: ⦿ Baixa ○ Média ○ Alta │
│                                         │
│  Pontos Calculados: 10 PF              │
│                                         │
│  [Adicionar Função] [Cancelar]         │
└─────────────────────────────────────────┘
```

### Tela de Resultado
```
┌─────────────────────────────────────────┐
│  Resultado da Análise de PF            │
├─────────────────────────────────────────┤
│                                         │
│  Funções de Dados:           45 PF     │
│  Funções Transacionais:      38 PF     │
│  ─────────────────────────────────     │
│  PF Bruto:                   83 PF     │
│                                         │
│  Fator de Ajuste:            0.95      │
│  ─────────────────────────────────     │
│  PF Ajustado:               78.85 PF   │
│                                         │
│  [Exportar PDF] [Exportar Excel]       │
└─────────────────────────────────────────┘
```

## 🧪 Testes

### Backend
```bash
cd backend
vendor/bin/phpunit
```

### Frontend
```bash
cd frontend
npm test
# ou
yarn test
```

## 📝 Exemplos de Uso

### Criar um Novo Projeto
```javascript
// Frontend - Exemplo de requisição
const criarProjeto = async () => {
  const response = await api.post('/projetos', {
    nome: 'Sistema de Vendas',
    descricao: 'Sistema web para gestão de vendas',
    data_inicio: '2024-01-15'
  });
  return response.data;
};
```

### Cadastrar Função de Dados
```javascript
const cadastrarALI = async (projetoId) => {
  const response = await api.post('/funcoes-dados', {
    projeto_id: projetoId,
    tipo: 'ALI',
    nome: 'Cadastro de Clientes',
    der: 15,
    rlr: 2,
    complexidade: 'media'
  });
  return response.data;
};
```

## 🤝 Contribuindo

1. Faça um Fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/NovaFuncionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 👥 Autores

* **Seu Nome** - *Desenvolvimento Inicial*

## 📞 Contato

- Email: seu-email@exemplo.com
- LinkedIn: [seu-linkedin](https://linkedin.com/in/seu-perfil)

## 🙏 Agradecimentos

- IFPUG - International Function Point Users Group
- Comunidade CodeIgniter
- Comunidade React

---

⭐️ Se este projeto foi útil para você, considere dar uma estrela!
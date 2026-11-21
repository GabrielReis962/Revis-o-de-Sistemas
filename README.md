# ArenaXP — Sistema de Controle de Estoque & Equipamentos

Projeto prático desenvolvido para o **Preparatório SAEP 2026 (SENAI — Técnico em Desenvolvimento de Sistemas)**. O sistema realiza o gerenciamento completo de equipamentos de e-sports/eventos, controle de entradas e saídas, alertas de estoque mínimo e auditoria de movimentações por usuário autenticado.

---

## Tecnologias Utilizadas

* **Back-end:** Java 17+, Spring Boot, Spring Web, Spring Data JPA, Hibernate
* **Banco de Dados:** MySQL 8+ (`arenaxp_db`)
* **Front-end:** HTML5, CSS3, JavaScript (Fetch API com suporte a sessão/cookies)
* **Segurança:** Autenticação baseada em sessão HTTP (`AuthInterceptor`) e senhas armazenadas com hash criptográfico SHA-256

---

## Estrutura de Pastas do Projeto

```text
arenaxp-saep-2026/
├── backend/                  # API REST e regras de negócio (Spring Boot)
│   ├── src/
│   └── pom.xml
├── frontend/                 # Interface web responsiva
│   ├── index.html
│   ├── login.html
│   ├── style.css
│   └── script.js
├── database/                 # Modelagem e carga inicial do banco
│   ├── arenaxp_db.sql
│   └── DER_ArenaXP.png
├── docs/                     # Evidências e relatórios de teste
│   └── Relatorio_Testes_ArenaXP.pdf
└── README.md
```

---

## Credenciais de Acesso (Carga Inicial)

O banco de dados já é inicializado com **3 usuários** (1 administrador e 2 operadores), **5 equipamentos** e **4 movimentações** para testes imediatos:

| Perfil | Nome | E-mail | Senha |
| :--- | :--- | :--- | :--- |
| **Administrador** | Administrador ArenaXP | `admin@arenaxp.com` | `ArenaXP@2026#Admin` |
| **Operador 1** | Lucas Almeida (Operador) | `operador1@arenaxp.com` | `Operador@2026` |
| **Operador 2** | Mariana Costa (Operador) | `operador2@arenaxp.com` | `Operador@2026` |

---

## Como Executar o Projeto

### 1. Banco de Dados (MySQL)
1. Certifique-se de que o serviço do **MySQL 8+** está em execução na porta `3306`.
2. Execute o script `database/arenaxp_db.sql` no MySQL Workbench (ou cliente SQL de sua preferência) para criar o schema `arenaxp_db`, as tabelas e a carga inicial.
   * *Nota:* Caso prefira iniciar o banco vazio, o próprio Spring Boot cria o schema automaticamente (`createDatabaseIfNotExist=true`) e popula a carga inicial via `DataInitializer.java` sem duplicar registros ao reiniciar.

### 2. Back-end (Spring Boot)
1. Abra a pasta `backend/` no **IntelliJ IDEA** (ou IDE Java de sua preferência).
2. Verifique o arquivo `backend/src/main/resources/application.properties`:
   * A conexão padrão está configurada com usuário `root` e senha `root` (ou via variáveis de ambiente `DB_USERNAME` e `DB_PASSWORD`). Caso o seu MySQL local utilize outra senha, ajuste a propriedade `spring.datasource.password`.
3. Execute a classe principal `ArenaXpApplication.java`.
4. A API estará disponível em `http://localhost:8080`.

### 3. Front-end (Interface Web)
1. Abra a pasta `frontend/` no **VS Code**.
2. Inicie a aplicação utilizando a extensão **Live Server** (porta padrão `5500`) a partir do arquivo `login.html`.
3. Acesse no navegador usando **`http://localhost:5500/login.html`** (utilize `localhost` na URL para manter o cookie de sessão compatível com o back-end).

---

## Funcionalidades Implementadas

* **Autenticação e Controle de Sessão:** Login validado no banco de dados, bloqueio automático de rotas e endpoints sem sessão ativa, exibição do usuário logado no cabeçalho e logout seguro.
* **CRUD Completo de Equipamentos:** Cadastro, edição, listagem ordenada alfabeticamente (**A–Z**), busca por nome ou código de patrimônio e bloqueio de exclusão para itens com histórico de movimentações vinculado.
* **Gestão de Estoque e Validações:** Registro de entradas e saídas vinculado ao usuário autenticado, bloqueio de saída superior ao saldo disponível e alerta visual automático quando `quantidade_atual <= estoque_minimo`.

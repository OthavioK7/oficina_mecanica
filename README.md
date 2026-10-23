# 🔧 AutoMecânica Pro — Sistema de Gestão de Oficina

Sistema web para gerenciamento de uma oficina mecânica, desenvolvido como projeto acadêmico do **SAEP / SENAI**. A aplicação organiza clientes, veículos e agendamentos de serviços em um banco de dados MySQL, com autenticação de usuários.

## 📌 Funcionalidades

- **Login e logout:** autenticação de funcionários e controle de sessão.
- **Dashboard:** resumo de clientes, veículos e agendamentos, além dos próximos serviços.
- **Clientes:** cadastro, listagem, pesquisa, edição e exclusão.
- **Validação de CPF:** verifica se o CPF informado contém 11 dígitos numéricos.
- **Veículos:** cadastro, listagem, edição e exclusão, com vínculo obrigatório a um cliente.
- **Agendamentos:** cadastro e listagem em ordem cronológica, atualização de data e exclusão.
- **Mensagens do sistema:** feedback para operações e erros.
- **Banco de dados relacional:** relacionamentos entre clientes, veículos e agendamentos.

## 🧰 Tecnologias utilizadas

- Python 3
- Flask 3.0.3
- MySQL
- `mysql-connector-python` 8.4.0
- Bcrypt 4.1.3
- Werkzeug 3.0.3
- HTML5
- CSS3
- JavaScript puro

## 📁 Estrutura do projeto

```text
oficina_mecanica/
├── saep_db.sql
├── venv/
└── sistema/
    ├── app.py
    ├── autenticacao.py
    ├── banco.py
    ├── clientes.py
    ├── veiculos.py
    ├── agendamento.py
    ├── rotas.py
    ├── requirements.txt
    ├── templates/
    │   ├── base.html
    │   ├── login.html
    │   ├── dashboard.html
    │   ├── clientes.html
    │   ├── veiculos.html
    │   └── agendamentos.html
    └── static/
        ├── css/
        │   └── style.css
        └── js/
            └── main.js
```

> A estrutura acima representa a organização prevista para o projeto. Confira se todos os templates e arquivos estáticos estão presentes na sua pasta.

## ⚙️ Requisitos

Antes de executar, instale/configure:

- Python 3 instalado;
- MySQL Server em execução;
- um cliente MySQL, como MySQL Workbench ou terminal;
- Git, caso queira versionar o projeto.

## 🚀 Como instalar e executar

### 1. Abra a pasta do projeto

No terminal, entre na pasta `oficina_mecanica`.

### 2. Crie e ative o ambiente virtual

**Windows (CMD/PowerShell):**

```bash
python -m venv venv
venv\Scripts\activate
```

**Linux/macOS:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Instale as dependências

```bash
pip install -r sistema/requirements.txt
```

### 4. Crie o banco de dados

Execute o arquivo `saep_db.sql` no MySQL. Pelo terminal, você pode usar:

```bash
mysql -u root -p < saep_db.sql
```

Digite a senha do usuário MySQL quando solicitado. O script cria o banco `saep_db`, as tabelas e alguns registros de demonstração.

**Atenção:** o script contém comandos `DROP TABLE IF EXISTS`, que apagam as tabelas indicadas antes de recriá-las. Faça backup de dados importantes antes de executá-lo novamente.

### 5. Configure a conexão com o MySQL

Por padrão, o sistema usa:

- Host: `localhost`
- Porta: `3306`
- Usuário: `root`
- Banco: `saep_db`
- Senha: vazia, caso a variável de ambiente não seja configurada

Se necessário, defina as variáveis de ambiente antes de iniciar o sistema.

**Windows PowerShell:**

```powershell
$env:DB_HOST="localhost"
$env:DB_USER="root"
$env:DB_PASSWORD="sua_senha"
$env:DB_NAME="saep_db"
$env:DB_PORT="3306"
$env:SECRET_KEY="defina_uma_chave_segura"
```

Substitua os valores pelos dados do seu ambiente. Não compartilhe senhas nem envie chaves secretas para o GitHub.

### 6. Teste a conexão com o banco

```bash
python sistema/banco.py
```

Se a conexão estiver configurada corretamente, o terminal deverá informar que o banco foi conectado e listar as tabelas encontradas.

### 7. Inicie a aplicação

```bash
python sistema/app.py
```

Abra no navegador:

**http://127.0.0.1:5000**

Para encerrar o servidor, pressione `Ctrl + C` no terminal.

## 🔐 Usuários de demonstração

O banco de dados de exemplo inclui estes usuários:

| Usuário | Senha de demonstração | Cargo |
|---|---|---|
| `admin` | `admin123` | Administrador / Gerente |
| `mecanico` | `senha123` | Mecânico Chefe |
| `recepcao` | `rec123` | Recepcionista |

> Essas credenciais são apenas para demonstração acadêmica. Não as utilize em produção. Antes de publicar o projeto, troque as senhas de exemplo e configure uma `SECRET_KEY` segura.

## 🗃️ Banco de dados

O banco `saep_db` contém quatro tabelas principais:

- **`usuarios`** — dados de acesso e cargo dos funcionários;
- **`clientes`** — dados cadastrais e informações de contato;
- **`veiculos`** — veículos vinculados aos clientes;
- **`agendamentos`** — serviços agendados, status, data, valor estimado e observações.

Os relacionamentos utilizam chaves estrangeiras para associar veículos a clientes e agendamentos a clientes e veículos.

## ✅ Roteiro de testes

- [ ] Entrar com credenciais válidas.
- [ ] Verificar se o sistema bloqueia login inválido.
- [ ] Cadastrar, pesquisar, editar e excluir um cliente.
- [ ] Confirmar que CPF com quantidade diferente de 11 dígitos é rejeitado.
- [ ] Cadastrar e editar um veículo associado a um cliente existente.
- [ ] Cadastrar um agendamento e conferir a ordenação por data.
- [ ] Alterar a data de um agendamento.
- [ ] Conferir as informações exibidas no dashboard.
- [ ] Sair do sistema e confirmar que a sessão foi encerrada.

## 🔒 Observações de segurança

- O projeto é destinado a estudo e demonstração, não estando automaticamente pronto para uso em produção.
- Configure uma chave secreta forte e credenciais próprias para o banco.
- Evite armazenar ou exibir dados pessoais reais em ambientes de teste.
- O código de exemplo armazena o CPF formatado e também um hash Bcrypt; hash não é criptografia reversível. Revise as regras de acesso e o tratamento desses dados antes de usar informações reais.
- Em produção, use HTTPS, valide os dados recebidos, proteja operações de alteração/exclusão e desative o modo de depuração.

## 👥 Projeto acadêmico

Desenvolvido para fins educacionais no contexto do **SAEP / SENAI**, com foco em desenvolvimento web, integração Python–MySQL, organização modular e gerenciamento de dados de uma oficina mecânica.

---

**AutoMecânica Pro** — organização e praticidade na gestão da oficina. ⚙️

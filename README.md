# Django Project Template

Este é um template para iniciar projetos Django com configurações modernas, incluindo gerenciamento de dependências com Poetry, configurações via Pydantic Settings, e suporte a PostgreSQL.

## Pré-requisitos

- Python 3.13 ou superior
- Poetry (gerenciador de dependências)
- PostgreSQL (ou Docker para execução local)

## Instalação

1. Clone este repositório:

   ```bash
   git clone <url-do-repositorio> meu-projeto
   cd meu-projeto
   ```

2. Instale as dependências com Poetry:

   ```bash
   poetry install
   ```

3. Configure o ambiente:
   - Copie o arquivo `.envexample` para `.env`:

    ```bash
     cp .envexample .env
    ```

   - Edite o arquivo `.env` com suas configurações.

## Configuração

### Arquivo .env

O arquivo `.env` contém as variáveis de ambiente. Principais configurações:

- `DEBUG`: Defina como `True` para desenvolvimento, `False` para produção.
- `SECRET_KEY`: **IMPORTANTE**: Gere uma nova chave secreta para o seu projeto. Nunca use a chave do template em produção.
  - Para gerar uma nova SECRET_KEY, execute no terminal:

    ```bash
    python -c "import secrets; print(secrets.token_urlsafe(50))"
    ```

- `ALLOWED_HOSTS`: Lista de hosts permitidos, separados por vírgula (ex: `localhost,127.0.0.1`).
- Configurações do banco de dados PostgreSQL:
  - `DB_NAME`: Nome do banco de dados.
  - `DB_USER`: Usuário do banco.
  - `DB_PASSWORD`: Senha do usuário.
  - `DB_HOST`: Host do banco (ex: `localhost` ou `db` se usando Docker).
  - `DB_PORT`: Porta do banco (padrão: 5432).

**Atenção**: Sempre gere uma nova `SECRET_KEY` ao usar este template. A chave no `.envexample` é apenas um placeholder.

### Banco de Dados

Este template está configurado para usar PostgreSQL. Certifique-se de ter um banco PostgreSQL rodando ou use Docker Compose para subir um container.

## Executando o Projeto

### Desenvolvimento Local

1. Ative o ambiente virtual do Poetry:

   ```bash
   poetry shell
   ```

2. Execute as migrações do Django:

   ```bash
   python manage.py migrate
   ```

3. Inicie o servidor de desenvolvimento:

   ```bash
   python manage.py runserver
   ```

Acesse em: <http://localhost:8000>

### Com Docker

Se preferir usar Docker, há um `docker-compose.yml` configurado:

1. Construa e inicie os containers:

   ```bash
   docker-compose up --build
   ```

Isso iniciará o Django e o PostgreSQL em containers.

## Estrutura do Projeto

- `core/`: Configurações principais do Django (settings, URLs, WSGI, ASGI).
- `manage.py`: Script de gerenciamento do Django.
- `pyproject.toml`: Configurações do Poetry e dependências.
- `.env`: Variáveis de ambiente (não versionado).
- `.envexample`: Exemplo das variáveis de ambiente.
- `docker-compose.yml`: Configuração para execução com Docker.
- `Dockerfile`: Imagem Docker para o projeto.

## Comandos Úteis

- **Linting e formatação**: `poetry run task lint`, `poetry run task format`
- **Executar testes**: Adicione testes em um diretório `tests/` e execute `python manage.py test`
- **Criar superusuário**: `python manage.py createsuperuser`

## Segurança

- Nunca commite o arquivo `.env` no repositório (já está no `.gitignore`).
- Gere uma nova `SECRET_KEY` para cada projeto.
- Defina `DEBUG=False` em produção.
- Configure `ALLOWED_HOSTS` adequadamente para o ambiente de produção.

## Contribuição

Para contribuir, siga os padrões de código definidos no `pyproject.toml` (Ruff para linting e formatação).

## Licença

Este template é distribuído sob a licença MIT.

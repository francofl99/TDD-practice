# Symfony Application

A modern Symfony 6.4 application with Docker and PostgreSQL integration.

## Prerequisites

- Docker
- Docker Compose

## Getting Started

1. Clone the repository:
```bash
git clone <repository-url>
cd symfony-app
```

2. Start the application:
```bash
docker compose up -d
```

3. Install dependencies:
```bash
docker compose exec app composer install
```

4. Create database schema:
```bash
docker compose exec app php bin/console doctrine:schema:create
```

The application will be available at http://localhost

## Development

- The application code is in the `src` directory
- Database runs on PostgreSQL and is accessible at `localhost:5432`
- Database credentials (for development):
  - User: user
  - Password: password
  - Database: symfony

## Commands

- Start the application: `docker-compose up -d`
- Stop the application: `docker-compose down`
- Run tests: `docker-compose exec app php bin/phpunit`
- Create database: `docker-compose exec app php bin/console doctrine:database:create`
- Run migrations: `docker-compose exec app php bin/console doctrine:migrations:migrate`
- Create entity: `docker-compose exec app php bin/console make:entity`
- Create controller: `docker-compose exec app php bin/console make:controller`
- Clear cache: `docker-compose exec app php bin/console cache:clear`
- Access database CLI: `docker-compose exec db psql -U user -d symfony`

## Project Structure

```
.
├── config/         # Symfony configuration files
├── public/        # Web server files
├── src/           # Application source code
├── templates/     # Twig templates
├── tests/         # Test files
├── var/           # Generated files (cache, logs)
├── vendor/        # Dependencies
└── docker/        # Docker-related files
```

## License

MIT
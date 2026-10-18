# 🚀 Actix Web Postgres Diesel Boilerplate

[![Rust](https://img.shields.io/badge/Rust-%23DEA584.svg?style=flat&logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![Actix Web](https://img.shields.io/badge/Framework-Actix%20Web-blue?style=flat&logo=rust)](https://actix.rs/)
[![Database-PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-336791?style=flat&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Diesel](https://img.shields.io/badge/ORM-Diesel-4B8BBE?style=flat&logo=rust)](https://diesel.rs/)
[![Docker](https://img.shields.io/badge/Docker-ready-blue?style=flat&logo=docker&logoColor=white)](https://www.docker.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A clean and ready-to-use boilerplate for building high-performance asynchronous web services using **Actix Web** 🦀 and **PostgreSQL** 🐘. This template helps you quickly start developing Rust-based APIs with database integration and migrations powered by **Diesel**.

---

## ⚙️ Prerequisites

Before you begin, make sure you have the following installed:

- 🧰 **Rust & Cargo** → [Install Rust](https://www.rust-lang.org/tools/install)
- 🐋 **Docker** → [Install Docker](https://docs.docker.com/get-docker/)
- 🛠️ **Diesel CLI** → for managing database migrations

---

## 🧩 Install Diesel CLI

Install the Diesel command-line tool with PostgreSQL support:

```bash
# Install libpq-dev for Diesel Postgres
sudo apt-get update && sudo apt-get install -y libpq-dev
cargo install diesel_cli --no-default-features --features postgres
```

---

## 🐘 Run PostgreSQL Instance (via Docker)

Start a local PostgreSQL instance with Docker:

```bash
docker run -d \
  --name actix_postgres \
  -e POSTGRES_USER=darix \
  -e POSTGRES_PASSWORD=your_password \
  -e POSTGRES_DB=actix_postgres_diesel \
  -p 5432:5432 \
  postgres:latest
```

---

## 🔧 Run Database Migrations

Run all Diesel migrations to set up your database schema:

```bash
diesel migration run
```

> 💡 Diesel CLI reads `DATABASE_URL` from your environment or `.env` file, so complete the setup in the next section first.

---

## 🏎️ Run Application with Cargo

Before running the application locally, make sure your environment variables are correctly set.

Start by copying the example environment file:

```bash
cp .env.example .env
```

Next, update the `DATABASE_URL` inside `.env` to match your local PostgreSQL setup. For example:

```env
DATABASE_URL=postgres://darix:your_password@localhost:5432/actix_postgres_diesel
```

Once your environment is configured, start the server using Cargo:

```bash
cargo run
```

The application will compile and launch your Actix Web server, making it instantly available for local development and testing.

---

## 🐳 Run with Docker (without Docker Compose)

If you prefer running the application directly with Docker, pass the PostgreSQL connection URL as an environment variable.

> ⚠️ Inside a container, `localhost` refers to the container itself. Use `host.docker.internal` (Docker Desktop) or add `--add-host=host.docker.internal:host-gateway` (Linux) to reach Postgres running on your host.

```bash
docker build -t actix_postgres_app .

docker run -d -p 5800:5800 \
  --add-host=host.docker.internal:host-gateway \
  -e DATABASE_URL="postgres://darix:your_password@host.docker.internal:5432/actix_postgres_diesel" \
  --name actix_postgres_app \
  actix_postgres_app
```

---

## 🚢 Deploy with Docker Compose

Easily build and deploy your application using Docker Compose 🧱🐳:

```bash
docker compose up -d --build
```

---

### 🏃‍♂️ Run the tests sequentially 🧪📋

```bash
cargo test -- --test-threads=1
```

<!-- ---

### 🌐 Access the API Docs

Open the interactive OpenAPI docs (Swagger UI) at:

👉 [http://0.0.0.0:8080/docs/](http://0.0.0.0:8080/docs/)

---

### 🧩 Example Preview Docs

![IMAGE](./img/image.png) -->
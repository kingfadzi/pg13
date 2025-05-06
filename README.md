# PostgreSQL 13 Benchmarking on AlmaLinux 8 (Dockerized)

This project provides a containerized setup for running PostgreSQL 13 on AlmaLinux 8, tuned for performance on an 8-core, 32GB RAM Linux host. It includes a benchmarking setup using `pgbench`.

---

## 🚀 Features

* PostgreSQL 13 built on AlmaLinux 8
* Custom user and group ID support for volume compatibility
* Performance-tuned `postgresql.conf` (16GB RAM target)
* Bind-mounted config for flexibility
* `pgbench` benchmark-ready
* Clean entrypoint logic with auto-initialization

---

## 🐳 Getting Started

### 1. Build and Run the Database

```bash
docker-compose up --build
```

PostgreSQL will initialize and listen on `localhost:5432` with:

* Username: `postgres`
* Password: `postgres`
* Default DB: `postgres`

### 2. Initialize Benchmark Data

Install `pgbench` locally or run it via container:

```bash
pgbench -i -s 100 -h localhost -p 5432 -U postgres postgres
```

### 3. Run a Benchmark Test

```bash
pgbench -h localhost -p 5432 -U postgres -c 10 -j 2 -T 60 postgres
```

Adjust `-c` (clients), `-j` (threads), and `-T` (duration) to test different loads.

---

## 💠 Files

* `Dockerfile`: Builds PostgreSQL 13 on AlmaLinux 8
* `docker-compose.yaml`: Defines the container environment
* `docker-entrypoint.sh`: Initializes and starts PostgreSQL
* `postgresql.conf`: Tuning configuration for 8-core/32GB system

---

## 📈 Sample Result (pgbench @ scale 100, 10 clients)

```
TPS: ~1920
Avg Latency: ~5ms
```

---

## 📌 License

MIT

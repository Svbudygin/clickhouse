# 📦 ClickHouse Monitoring & Simulation Stack

This repository provides a complete monitoring and analytics setup using ClickHouse, Prometheus, Grafana, Consul, and a custom data simulation service. It is designed for benchmarking ClickHouse with realistic event data, visualizing metrics, and experimenting with distributed cluster setups.

## 🚀 Components

### 🐘 ClickHouse Cluster

* 4 ClickHouse nodes (2 shards x 2 replicas)
* Configured with ZooKeeper coordination and `keeper.xml`
* Data replication and sharding defined via `cluster.xml`

### 🧠 Consul

* Leader election for computing metrics
* Service discovery and registration

### 🦉 Prometheus

* Scrapes metrics from microservices
* Stores internal time-series data

### 📊 Grafana

* Preconfigured with ClickHouse as datasource
* Includes auto-provisioning of dashboards and datasources
* Default login: `admin` / `admin123`

### 🧪 Microservice

* Simulates realistic item upload/update/save events
* Emits Prometheus metrics (`SAVE`, `UPDATE`, `ERROR` counters)
* Inserts data into ClickHouse buffers
* Performs leader election via Consul to ensure metrics are computed only once

## ⚙️ How It Works

1. `microservice` starts and registers itself with Consul
2. Prometheus begins scraping internal metrics on port `:84`
3. Every 100ms, the microservice generates a synthetic event (SAVE, UPDATE, or ERROR)
4. Two ClickHouse buffer tables are filled with event and status data
5. Grafana dashboards visualize metrics in real-time

## 🧩 Useful Commands

```bash
docker compose up --build
```

Access:

* Prometheus: [http://localhost:9090](http://localhost:9090)
* Grafana: [http://localhost:3000](http://localhost:3000)  (`admin` / `admin123`)
* Consul UI: [http://localhost:8500](http://localhost:8500)

## 🔗 Related Projects

* [LLM-MTS/devops](https://github.com/LLM-MTS/devops): Production-grade LLM assistant with orchestration and RAG integration

## 🧠 Author

Sergei Budygin

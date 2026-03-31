# 📊 Docker Monitoring Lab (Prometheus + Grafana + NGINX)

Laboratorio de monitoreo utilizando Docker Desktop y Docker Compose.

Incluye:
- Prometheus (recolección de métricas)
- Grafana (visualización)
- Node Exporter (métricas del sistema)
- Blackbox Exporter (monitoreo HTTP)
- NGINX (servicio web a monitorear)

---

# 🧱 Arquitectura

```
Docker Desktop
 ├── prometheus
 ├── grafana
 ├── node-exporter
 ├── blackbox-exporter
 └── nginx
```

Todos los contenedores comparten la red:
```
monitoring_net
```

---

# 📁 Estructura del proyecto

```
monitoring/
├── docker-compose.yml
└── prometheus/
    └── prometheus.yml
```

---

# ⚙️ Configuración

## 🔹 Prometheus

Archivo:
```
prometheus/prometheus.yml
```

Incluye:

- Scrape de Prometheus
- Node Exporter
- Blackbox Exporter (NGINX)

---

# 🚀 Despliegue

## 1. Crear red (solo primera vez)

```
docker network create monitoring_net
```

---

## 2. Levantar servicios

Desde la carpeta del proyecto:

```
docker compose up -d
```

---

## 3. Verificar contenedores

```
docker ps
```

---

## 4. Logs (debug)

```
docker logs prometheus
docker logs blackbox
```

---

# 🌐 Accesos

- Prometheus → http://localhost:9090  
- Grafana → http://localhost:3000  
- NGINX → http://localhost:8080  

---

# 📊 Métricas utilizadas

## Disponibilidad
```
probe_success{job="nginx-http"}
```

## Latencia
```
probe_duration_seconds{job="nginx-http"}
```

## Código HTTP
```
probe_http_status_code{job="nginx-http"}
```

---

# 📈 Grafana

## Data Source

- Tipo: Prometheus
- URL:
```
http://prometheus:9090
```

---

## Panel básico

Query:
```
probe_success{job="nginx-http"}
```

---

# 🧪 Pruebas

Detener NGINX:

```
docker stop nginx
```

Resultado esperado:
- probe_success → 0
- Servicio DOWN en Grafana

Levantar nuevamente:

```
docker start nginx
```

---

# ⚠️ Problemas comunes

## ❌ no such host (blackbox)
- El contenedor no está en la red

## ❌ No data en Grafana
- Revisar rango de tiempo
- Validar query con labels

## ❌ probe_success no existe
- Blackbox no está funcionando
- Target no está en UP

---

# 🧠 Aprendizajes

- Monitoreo en entornos Docker
- Uso de Prometheus y exporters
- Consultas con PromQL
- Debug de redes Docker

---

# 🚀 Mejoras futuras

- Alertas (Alertmanager)
- Dashboards avanzados
- cAdvisor (métricas de contenedores)
- Integración con Kubernetes

---

# 👨‍💻 Autor

Laboratorio práctico de monitoreo con Docker.
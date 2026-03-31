# 📊 Docker Monitoring Lab (Prometheus + Grafana + NGINX)

Este proyecto corresponde a un laboratorio práctico de monitoreo usando Docker Desktop, donde se implementa una solución completa con:

- Prometheus (recolección de métricas)
- Grafana (visualización)
- Node Exporter (métricas del sistema)
- Blackbox Exporter (monitoreo HTTP)
- NGINX (servicio a monitorear)

---

## 🧱 Arquitectura

```
Docker Desktop
 ├── Prometheus
 ├── Grafana
 ├── Node Exporter
 ├── Blackbox Exporter
 └── NGINX (target HTTP)
```

---

## 🚀 Componentes

### 🔹 Prometheus
Recolecta métricas desde distintos exporters.

### 🔹 Grafana
Permite visualizar métricas mediante dashboards.

### 🔹 Node Exporter
Entrega métricas del sistema (CPU, RAM, disco).

### 🔹 Blackbox Exporter
Permite monitorear endpoints HTTP (como NGINX).

### 🔹 NGINX
Servidor web utilizado como target de monitoreo.

---

## 🌐 Accesos

- Prometheus: http://localhost:9090  
- Grafana: http://localhost:3000  
- NGINX: http://localhost:8080  

---

## 📊 Métricas utilizadas

### Disponibilidad
```
probe_success{job="nginx-http"}
```

### Latencia
```
probe_duration_seconds{job="nginx-http"}
```

### Código HTTP
```
probe_http_status_code{job="nginx-http"}
```

---

## 🧪 Pruebas

Puedes validar el monitoreo deteniendo el contenedor NGINX:

```
docker stop nginx
```

Y observar en Grafana cómo cambia el estado a DOWN.

---

## ⚠️ Problemas comunes

### ❌ No aparece probe_success
- Verificar que el target esté en estado UP en Prometheus

### ❌ Error "no such host"
- Asegurar que los contenedores estén en la misma red Docker

### ❌ No data en Grafana
- Revisar el rango de tiempo (últimos 5 minutos)

---

## 🧠 Aprendizajes

- Uso de Prometheus en entornos containerizados
- Monitoreo HTTP con Blackbox Exporter
- Visualización en Grafana con PromQL
- Resolución de problemas de red en Docker

---

## 📌 Mejoras futuras

- Alertas (email / Telegram)
- Dashboards avanzados
- Monitoreo de múltiples servicios
- Integración con Kubernetes

---

## 👨‍💻 Autor

Proyecto desarrollado como laboratorio práctico de monitoreo.
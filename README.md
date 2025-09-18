# Privacera Base Helm Chart

A comprehensive, production-ready base Helm chart for microservices with built-in observability, security, and scalability features.

## 🚀 Quick Start

### Add the Helm Repository

```bash
helm repo add my-base-chart https://evilgenius-jp.github.io/my-base-chart/
helm repo update
```

### Install the Chart

```bash
# Basic installation
helm install my-app my-base-chart/privacera-base-chart

# With custom values
helm install my-app my-base-chart/privacera-base-chart -f my-values.yaml

# With inline values
helm install my-app my-base-chart/privacera-base-chart \
  --set app.name=my-microservice \
  --set image.repository=my-company/my-app \
  --set image.tag=v1.0.0
```

## 📋 Features

### ✅ Core Capabilities
- **Deployment & StatefulSet Support** - Choose between stateless and stateful workloads
- **Auto-scaling** - Horizontal Pod Autoscaler (HPA) and KEDA support
- **Service Management** - Internal and external service configurations
- **Ingress Management** - Multiple ingress controllers support
- **Storage Management** - Persistent Volume Claims with multiple storage classes

### 🔒 Security & Compliance
- **Service Accounts** - Dedicated service accounts with RBAC
- **Network Policies** - Micro-segmentation and traffic control
- **Pod Security** - Security contexts and pod security standards
- **Secrets Management** - Secure handling of sensitive data

### 📊 Observability & Monitoring
- **Health Checks** - Liveness, readiness, and startup probes
- **Metrics Collection** - Prometheus metrics and custom collectors
- **Logging** - Structured logging with multiple outputs
- **Tracing** - Distributed tracing support

### ⚡ Performance & Reliability
- **Resource Management** - CPU/memory requests and limits
- **Pod Disruption Budgets** - Maintain availability during updates
- **Rolling Updates** - Zero-downtime deployments
- **Multi-zone Deployment** - High availability across zones

## 📖 Documentation

### Chart Structure
```
charts/privacera-base-chart/
├── Chart.yaml              # Chart metadata
├── values.yaml             # Default values for Deployment
├── values-statefulset.yaml # Values for StatefulSet workloads
├── templates/              # Kubernetes templates
│   ├── deployment.yaml     # Main application deployment
│   ├── statefulset.yaml    # StatefulSet for persistent workloads
│   ├── service.yaml        # Internal service
│   ├── service-external.yaml # External service (LoadBalancer/NodePort)
│   ├── ingress.yaml        # Ingress configuration
│   ├── configmap.yaml      # Configuration management
│   ├── secret.yaml         # Secrets management
│   ├── service-account.yaml # RBAC and service accounts
│   ├── pvc.yaml           # Persistent volume claims
│   ├── hpa.yaml           # Horizontal Pod Autoscaler
│   ├── scaled-object.yaml # KEDA ScaledObject
│   ├── pdb.yaml           # Pod Disruption Budget
│   ├── networkpolicy.yaml # Network policies
│   └── _helpers.tpl       # Template helpers
└── examples/              # Usage examples
    ├── basic-microservice.yaml
    ├── advanced-microservice.yaml
    ├── database-statefulset.yaml
    └── production-microservice.yaml
```

### Configuration Examples

#### Basic Microservice
```yaml
app:
  name: "user-service"
  namespace: "production"

image:
  repository: "my-company/user-service"
  tag: "v1.2.3"

service:
  enabled: true
  type: ClusterIP
  port: 8080

ingress:
  enabled: true
  hosts:
    - host: api.example.com
      paths:
        - path: /users
          pathType: Prefix
```

#### Database StatefulSet
```yaml
workload:
  type: StatefulSet

app:
  name: "postgres-db"

image:
  repository: "postgres"
  tag: "15-alpine"

persistence:
  enabled: true
  size: 10Gi
  storageClass: "fast-ssd"

env:
  - name: POSTGRES_DB
    value: "myapp"
  - name: POSTGRES_PASSWORD
    valueFrom:
      secretKeyRef:
        name: postgres-secret
        key: password
```

## 🛠️ Configuration

### High Priority Configuration
The most commonly modified values:

```yaml
# Application Identity
app:
  name: "my-app"           # Application name
  namespace: "default"     # Target namespace
  
# Container Image  
image:
  repository: "nginx"      # Image repository
  tag: "latest"           # Image tag
  pullPolicy: IfNotPresent

# Workload Type
workload:
  type: Deployment        # Deployment or StatefulSet
  
# Service Configuration
service:
  enabled: true
  type: ClusterIP         # ClusterIP, NodePort, LoadBalancer
  port: 80
```

### Complete Configuration Reference
For all available configuration options, see:
- [values.yaml](./charts/privacera-base-chart/values.yaml) - Deployment workloads
- [values-statefulset.yaml](./charts/privacera-base-chart/values-statefulset.yaml) - StatefulSet workloads
- [examples/](./charts/privacera-base-chart/examples/) - Real-world examples

## 📚 Examples

### Microservice with Database
```bash
# Install PostgreSQL StatefulSet
helm install postgres my-base-chart/privacera-base-chart \
  -f examples/database-statefulset.yaml

# Install API service
helm install api my-base-chart/privacera-base-chart \
  -f examples/advanced-microservice.yaml
```

### Production Deployment
```bash
helm install production-app my-base-chart/privacera-base-chart \
  -f examples/production-microservice.yaml \
  --namespace production \
  --create-namespace
```

## 🔄 Upgrading

```bash
# Update repository
helm repo update

# Upgrade release
helm upgrade my-app my-base-chart/privacera-base-chart -f my-values.yaml

# Check upgrade status
helm status my-app
```

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Issues**: [GitHub Issues](https://github.com/evilgenius-jp/my-base-chart/issues)
- **Discussions**: [GitHub Discussions](https://github.com/evilgenius-jp/my-base-chart/discussions)
- **Documentation**: [Wiki](https://github.com/evilgenius-jp/my-base-chart/wiki)

## 📊 Chart Information

- **Chart Version**: 1.0.0
- **App Version**: 1.0.0
- **Kubernetes Version**: `>=1.20.0`
- **Helm Version**: `>=3.0.0`

---

⭐ **Star this repository if you find it useful!**

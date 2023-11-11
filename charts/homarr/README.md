# homarr

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.14.0](https://img.shields.io/badge/AppVersion-0.14.0-informational?style=flat-square)


A Helm chart to deploy homarr for Kubernetes

## Installing the Chart

### Add repository:

```bash
helm repo add homarr https://oben01.github.io/dmz-charts/charts/homarr
```

### Update Repository

```bash
helm repo update
```

### Install the chart

```bash
helm install [RELEASE_NAME] [CHART] --namespace [NAMESPACE] --create-namespace
```

For these commands, you should replace the placeholders accordingly:
- [RELEASE_NAME] - The name of your release.
- [CHART] - The name of your chart.
- [NAMESPACE] - The namespace where you want to deploy the chart.

Example using override values :

```bash
helm install homarr homarr/homarr --namespace homarr --create-namespace --values=override.yaml
```

`override.yaml` :

```bash
image:
 # Overrides the image tag whose default is the chart appVersion.
 tag: "0.14.0"
ingress:
 enabled: true
 className: traefik
 hosts:
  - host: homarr.homelab.dev
    paths:
     - path: /
       pathType: Prefix
  - host: www.homarr.homelab.dev
    paths:
     - path: /
       pathType: Prefix
 tls:
  - hosts:
     - "homarr.homelab.dev"
     - "www.homarr.homelab.dev"
    secretName: homelab-tls
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Node affinity for pod scheduling |
| autoscaling | object | `{"enabled":false,"maxReplicas":100,"minReplicas":1,"targetCPUUtilizationPercentage":80}` | Autoscaling configuration |
| autoscaling.enabled | bool | `false` | Enable autoscaling |
| autoscaling.maxReplicas | int | `100` | Maximum replicas |
| autoscaling.minReplicas | int | `1` | Minimum replicas |
| autoscaling.targetCPUUtilizationPercentage | int | `80` | Target CPU utilization for autoscaling |
| fullnameOverride | string | `""` | Overrides chart's fullname |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"ghcr.io/ajnart/homarr"` | Image repository |
| image.tag | string | `"latest"` | Overrides the image tag whose default is the chart appVersion |
| imagePullSecrets | list | `[]` | Secrets for Docker registry |
| ingress | object | `{"annotations":{},"enabled":false,"hosts":[{"host":"chart-example.local","paths":[{"path":"/","pathType":"ImplementationSpecific"}]}],"ingressClassName":"","tls":[]}` | Ingress configuration |
| ingress.annotations | object | `{}` | Ingress annotations |
| ingress.enabled | bool | `false` | Enable ingress |
| ingress.hosts | list | `[{"host":"chart-example.local","paths":[{"path":"/","pathType":"ImplementationSpecific"}]}]` | Ingress hosts configuration |
| ingress.ingressClassName | string | `""` | Ingress class name |
| ingress.tls | list | `[]` | Ingress TLS configuration |
| nameOverride | string | `""` | Overrides chart's name |
| nodeSelector | object | `{}` | Node selectors for pod scheduling |
| persistence | list | `[{"accessMode":"ReadWriteOnce","enabled":true,"mountPath":"/app/data/configs","name":"homarr-config","size":"50Mi","storageClassName":"local-path"},{"accessMode":"ReadWriteOnce","enabled":true,"mountPath":"/app/database","name":"homarr-database","size":"50Mi","storageClassName":"local-path"},{"accessMode":"ReadWriteOnce","enabled":true,"mountPath":"/app/public/icons","name":"homarr-icons","size":"50Mi","storageClassName":"local-path"}]` | Persistent storage configuration |
| persistence[0].accessMode | string | `"ReadWriteOnce"` | Access mode |
| persistence[0].enabled | bool | `true` | Enable this persistent storage |
| persistence[0].mountPath | string | `"/app/data/configs"` | Mount path inside the pod |
| persistence[0].size | string | `"50Mi"` | Storage size |
| persistence[0].storageClassName | string | `"local-path"` | Storage class name |
| podAnnotations | object | `{}` | Pod annotations |
| podLabels | object | `{}` | Pod labels |
| podSecurityContext | object | `{}` | Pod security context |
| replicaCount | int | `1` | Number of replicas |
| resources | object | `{}` | Resource configuration |
| securityContext | object | `{}` | Security context |
| service | object | `{"port":7575,"targetPort":7575,"type":"ClusterIP"}` | Service configuration |
| service.port | int | `7575` | Service port |
| service.targetPort | int | `7575` | Service target port |
| service.type | string | `"ClusterIP"` | Service type |
| tolerations | list | `[]` | Node tolerations for pod scheduling |

----------------------------------------------

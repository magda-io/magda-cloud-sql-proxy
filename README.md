# magda-cloud-sql-proxy

![Version: 1.0.1](https://img.shields.io/badge/Version-1.0.1-informational?style=flat-square)

It's a replacement of Magda internal built-in Cloud SQL Proxy helm chart. Its 100% compitible with Magda's internal built-in [cloud-sql-proxy](https://github.com/magda-io/magda/tree/master/deploy/helm/internal-charts/cloud-sql-proxy) chart.

A user might want to disable Magda's internal built-in [cloud-sql-proxy](https://github.com/magda-io/magda/tree/master/deploy/helm/internal-charts/cloud-sql-proxy) chart and use this one as the dependency instead when he wants to use different version of google cloud sql proxy docker image but ealier versions of Magda that he uses doesn't allow specifying Google Cloud SQL Proxy docker image.

## How to use

Declare as a dependency in your chart.yaml:

```yaml
- name: magda-cloud-sql-proxy
    version: 1.0.1
    repository: https://charts.magda.io
```

Disable Magda's built-in Cloud SQL Proxy in your config file:

```yaml 
tags:
  all: false
  cloud-sql-proxy: false
```

Please note: you will still want to leave the global `useCloudSql` field to true to make all Magda conponents use cloud sql connections. e.g.:

```yaml
global:
  useCombinedDb: false
  useCloudSql: true
```

## Requirements

Kubernetes: `>= 1.14.0-0`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| autoscaler.enabled | bool | `false` |  |
| autoscaler.maxReplicas | int | `3` |  |
| autoscaler.minReplicas | int | `1` |  |
| autoscaler.targetCPUUtilizationPercentage | int | `80` |  |
| global | object | `{}` |  |
| image.name | string | `"cloudsql-docker"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"gcr.io"` |  |
| image.tag | float | `1.11` |  |
| replicas | string | `nil` | no. of replicas required for the deployment. If not set, k8s will assume `1` but allows HPA (autoscaler) alters it. @default 1 |
| resources.requests.cpu | string | `"50m"` |  |
| resources.requests.memory | string | `"50Mi"` |  |
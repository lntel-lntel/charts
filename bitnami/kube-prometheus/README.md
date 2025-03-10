<!--- app-name: Prometheus Operator -->

# Prometheus Operator packaged by Bitnami

Prometheus Operator provides easy monitoring definitions for Kubernetes services and deployment and management of Prometheus instances.

[Overview of Prometheus Operator](https://github.com/coreos/prometheus-operator)

Trademarks: This software listing is packaged by Bitnami. The respective trademarks mentioned in the offering are owned by the respective companies, and use of them does not imply any affiliation or endorsement.

## TL;DR

```console
helm repo add my-repo https://charts.bitnami.com/bitnami
helm install my-release my-repo/kube-prometheus
```

## Introduction

This chart bootstraps [Prometheus Operator](https://github.com/bitnami/containers/tree/main/bitnami/prometheus-operator) on [Kubernetes](https://kubernetes.io) using the [Helm](https://helm.sh) package manager.

In the default configuration the chart deploys the following components on the Kubernetes cluster:

- [Prometheus Operator](https://github.com/prometheus-operator/prometheus-operator)
- [Prometheus](https://github.com/prometheus/prometheus/)
- [Alertmanager](https://github.com/prometheus/alertmanager)

> **:warning: IMPORTANT**

Only one instance of the Prometheus Operator component should be running in the cluster. If you wish to deploy this chart to **manage multiple instances** of Prometheus in your Kubernetes cluster, you **have to disable** the installation of the Prometheus Operator component using the `operator.enabled=false` chart installation argument.

Bitnami charts can be used with [Kubeapps](https://kubeapps.dev/) for deployment and management of Helm Charts in clusters.

## Prerequisites

- Kubernetes 1.16+
- Helm 3.2.0+

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm repo add my-repo https://charts.bitnami.com/bitnami
helm install my-release my-repo/kube-prometheus
```

The command deploys kube-prometheus on the Kubernetes cluster in the default configuration. The [configuration](#configuration-and-installation-details) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` release:

```console
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release. Use the flag `--purge` to delete all history too.

## Parameters

### Global parameters

| Name                      | Description                                     | Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `global.imageRegistry`    | Global Docker image registry                    | `""`  |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]`  |
| `global.storageClass`     | Global StorageClass for Persistent Volume(s)    | `""`  |

### Common parameters

| Name                | Description                                                                                                | Value           |
| ------------------- | ---------------------------------------------------------------------------------------------------------- | --------------- |
| `kubeVersion`       | Force target Kubernetes version (using Helm capabilities if not set)                                       | `""`            |
| `nameOverride`      | String to partially override `kube-prometheus.name` template with a string (will prepend the release name) | `""`            |
| `fullnameOverride`  | String to fully override `kube-prometheus.fullname` template with a string                                 | `""`            |
| `namespaceOverride` | String to fully override common.names.namespace                                                            | `""`            |
| `commonAnnotations` | Annotations to add to all deployed objects                                                                 | `{}`            |
| `commonLabels`      | Labels to add to all deployed objects                                                                      | `{}`            |
| `extraDeploy`       | Array of extra objects to deploy with the release                                                          | `[]`            |
| `clusterDomain`     | Kubernetes cluster domain name                                                                             | `cluster.local` |

### Prometheus Operator Parameters

| Name                                                                                  | Description                                                                                                            | Value                         |
| ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| `operator.enabled`                                                                    | Deploy Prometheus Operator to the cluster                                                                              | `true`                        |
| `operator.image.registry`                                                             | Prometheus Operator image registry                                                                                     | `docker.io`                   |
| `operator.image.repository`                                                           | Prometheus Operator image repository                                                                                   | `bitnami/prometheus-operator` |
| `operator.image.tag`                                                                  | Prometheus Operator image tag (immutable tags are recommended)                                                         | `0.63.0-debian-11-r3`         |
| `operator.image.digest`                                                               | Prometheus Operator image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag    | `""`                          |
| `operator.image.pullPolicy`                                                           | Prometheus Operator image pull policy                                                                                  | `IfNotPresent`                |
| `operator.image.pullSecrets`                                                          | Specify docker-registry secret names as an array                                                                       | `[]`                          |
| `operator.extraArgs`                                                                  | Additional arguments passed to Prometheus Operator                                                                     | `[]`                          |
| `operator.command`                                                                    | Override default container command (useful when using custom images)                                                   | `[]`                          |
| `operator.args`                                                                       | Override default container args (useful when using custom images)                                                      | `[]`                          |
| `operator.lifecycleHooks`                                                             | for the Prometheus Operator container(s) to automate configuration before or after startup                             | `{}`                          |
| `operator.extraEnvVars`                                                               | Array with extra environment variables to add to Prometheus Operator nodes                                             | `[]`                          |
| `operator.extraEnvVarsCM`                                                             | Name of existing ConfigMap containing extra env vars for Prometheus Operator nodes                                     | `""`                          |
| `operator.extraEnvVarsSecret`                                                         | Name of existing Secret containing extra env vars for Prometheus Operator nodes                                        | `""`                          |
| `operator.extraVolumes`                                                               | Optionally specify extra list of additional volumes for the Prometheus Operator pod(s)                                 | `[]`                          |
| `operator.extraVolumeMounts`                                                          | Optionally specify extra list of additional volumeMounts for the Prometheus Operator container(s)                      | `[]`                          |
| `operator.sidecars`                                                                   | Add additional sidecar containers to the Prometheus Operator pod(s)                                                    | `[]`                          |
| `operator.initContainers`                                                             | Add additional init containers to the Prometheus Operator pod(s)                                                       | `[]`                          |
| `operator.hostAliases`                                                                | Add deployment host aliases                                                                                            | `[]`                          |
| `operator.serviceAccount.create`                                                      | Specify whether to create a ServiceAccount for Prometheus Operator                                                     | `true`                        |
| `operator.serviceAccount.name`                                                        | The name of the ServiceAccount to create                                                                               | `""`                          |
| `operator.serviceAccount.automountServiceAccountToken`                                | Automount service account token for the server service account                                                         | `true`                        |
| `operator.serviceAccount.annotations`                                                 | Annotations for service account. Evaluated as a template. Only used if `create` is `true`.                             | `{}`                          |
| `operator.schedulerName`                                                              | Name of the Kubernetess scheduler (other than default)                                                                 | `""`                          |
| `operator.terminationGracePeriodSeconds`                                              | In seconds, time the given to the Prometheus Operator pod needs to terminate gracefully                                | `""`                          |
| `operator.topologySpreadConstraints`                                                  | Topology Spread Constraints for pod assignment                                                                         | `[]`                          |
| `operator.podSecurityContext.enabled`                                                 | Enable pod security context                                                                                            | `true`                        |
| `operator.podSecurityContext.runAsUser`                                               | User ID for the container                                                                                              | `1001`                        |
| `operator.podSecurityContext.fsGroup`                                                 | Group ID for the container filesystem                                                                                  | `1001`                        |
| `operator.containerSecurityContext.enabled`                                           | Enable container security context                                                                                      | `true`                        |
| `operator.containerSecurityContext.capabilities.drop`                                 | Linux Kernel capabilities which should be dropped                                                                      | `[]`                          |
| `operator.containerSecurityContext.runAsNonRoot`                                      | Force the container to run as a non root user                                                                          | `true`                        |
| `operator.containerSecurityContext.allowPrivilegeEscalation`                          | Switch privilegeEscalation possibility on or off                                                                       | `false`                       |
| `operator.containerSecurityContext.readOnlyRootFilesystem`                            | Mount / (root) as a readonly filesystem                                                                                | `false`                       |
| `operator.service.type`                                                               | Kubernetes service type                                                                                                | `ClusterIP`                   |
| `operator.service.ports.http`                                                         | Prometheus Operator service port                                                                                       | `8080`                        |
| `operator.service.clusterIP`                                                          | Specific cluster IP when service type is cluster IP. Use `None` for headless service                                   | `""`                          |
| `operator.service.nodePorts.http`                                                     | Kubernetes Service nodePort                                                                                            | `""`                          |
| `operator.service.loadBalancerIP`                                                     | `loadBalancerIP` if service type is `LoadBalancer`                                                                     | `""`                          |
| `operator.service.loadBalancerSourceRanges`                                           | Address that are allowed when svc is `LoadBalancer`                                                                    | `[]`                          |
| `operator.service.externalTrafficPolicy`                                              | Enable client source IP preservation                                                                                   | `Cluster`                     |
| `operator.service.healthCheckNodePort`                                                | Specifies the health check node port (numeric port number) for the service if `externalTrafficPolicy` is set to Local. | `""`                          |
| `operator.service.annotations`                                                        | Additional annotations for Prometheus Operator service                                                                 | `{}`                          |
| `operator.service.extraPorts`                                                         | Extra ports to expose (normally used with the `sidecar` value)                                                         | `[]`                          |
| `operator.service.sessionAffinity`                                                    | Session Affinity for Kubernetes service, can be "None" or "ClientIP"                                                   | `None`                        |
| `operator.service.sessionAffinityConfig`                                              | Additional settings for the sessionAffinity                                                                            | `{}`                          |
| `operator.serviceMonitor.enabled`                                                     | Creates a ServiceMonitor to monitor Prometheus Operator                                                                | `true`                        |
| `operator.serviceMonitor.interval`                                                    | Scrape interval (use by default, falling back to Prometheus' default)                                                  | `""`                          |
| `operator.serviceMonitor.metricRelabelings`                                           | Metric relabeling                                                                                                      | `[]`                          |
| `operator.serviceMonitor.relabelings`                                                 | Relabel configs                                                                                                        | `[]`                          |
| `operator.serviceMonitor.scrapeTimeout`                                               | Timeout after which the scrape is ended                                                                                | `""`                          |
| `operator.serviceMonitor.labels`                                                      | Extra labels for the ServiceMonitor                                                                                    | `{}`                          |
| `operator.serviceMonitor.annotations`                                                 | Extra annotations for the ServiceMonitor                                                                               | `{}`                          |
| `operator.resources`                                                                  | Configure resource requests and limits                                                                                 | `{}`                          |
| `operator.podAffinityPreset`                                                          | Pod affinity preset                                                                                                    | `""`                          |
| `operator.podAntiAffinityPreset`                                                      | Prometheus Operator Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`           | `soft`                        |
| `operator.nodeAffinityPreset.type`                                                    | Prometheus Operator Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard`          | `""`                          |
| `operator.nodeAffinityPreset.key`                                                     | Prometheus Operator Node label key to match Ignored if `affinity` is set.                                              | `""`                          |
| `operator.nodeAffinityPreset.values`                                                  | Prometheus Operator Node label values to match. Ignored if `affinity` is set.                                          | `[]`                          |
| `operator.affinity`                                                                   | Prometheus Operator Affinity for pod assignment                                                                        | `{}`                          |
| `operator.nodeSelector`                                                               | Prometheus Operator Node labels for pod assignment                                                                     | `{}`                          |
| `operator.tolerations`                                                                | Prometheus Operator Tolerations for pod assignment                                                                     | `[]`                          |
| `operator.podAnnotations`                                                             | Annotations for Prometheus Operator pods                                                                               | `{}`                          |
| `operator.podLabels`                                                                  | Extra labels for Prometheus Operator pods                                                                              | `{}`                          |
| `operator.priorityClassName`                                                          | Priority class assigned to the Pods                                                                                    | `""`                          |
| `operator.livenessProbe.enabled`                                                      | Turn on and off liveness probe                                                                                         | `true`                        |
| `operator.livenessProbe.initialDelaySeconds`                                          | Delay before liveness probe is initiated                                                                               | `120`                         |
| `operator.livenessProbe.periodSeconds`                                                | How often to perform the probe                                                                                         | `10`                          |
| `operator.livenessProbe.timeoutSeconds`                                               | When the probe times out                                                                                               | `5`                           |
| `operator.livenessProbe.failureThreshold`                                             | Minimum consecutive failures for the probe                                                                             | `6`                           |
| `operator.livenessProbe.successThreshold`                                             | Minimum consecutive successes for the probe                                                                            | `1`                           |
| `operator.readinessProbe.enabled`                                                     | Turn on and off readiness probe                                                                                        | `true`                        |
| `operator.readinessProbe.initialDelaySeconds`                                         | Delay before readiness probe is initiated                                                                              | `30`                          |
| `operator.readinessProbe.periodSeconds`                                               | How often to perform the probe                                                                                         | `10`                          |
| `operator.readinessProbe.timeoutSeconds`                                              | When the probe times out                                                                                               | `5`                           |
| `operator.readinessProbe.failureThreshold`                                            | Minimum consecutive failures for the probe                                                                             | `6`                           |
| `operator.readinessProbe.successThreshold`                                            | Minimum consecutive successes for the probe                                                                            | `1`                           |
| `operator.startupProbe.enabled`                                                       | Turn on and off startup probe                                                                                          | `false`                       |
| `operator.startupProbe.initialDelaySeconds`                                           | Delay before startup probe is initiated                                                                                | `30`                          |
| `operator.startupProbe.periodSeconds`                                                 | How often to perform the probe                                                                                         | `10`                          |
| `operator.startupProbe.timeoutSeconds`                                                | When the probe times out                                                                                               | `5`                           |
| `operator.startupProbe.failureThreshold`                                              | Minimum consecutive failures for the probe                                                                             | `6`                           |
| `operator.startupProbe.successThreshold`                                              | Minimum consecutive successes for the probe                                                                            | `1`                           |
| `operator.customLivenessProbe`                                                        | Custom livenessProbe that overrides the default one                                                                    | `{}`                          |
| `operator.customReadinessProbe`                                                       | Custom readinessProbe that overrides the default one                                                                   | `{}`                          |
| `operator.customStartupProbe`                                                         | Custom startupProbe that overrides the default one                                                                     | `{}`                          |
| `operator.logLevel`                                                                   | Log level for Prometheus Operator                                                                                      | `info`                        |
| `operator.logFormat`                                                                  | Log format for Prometheus Operator                                                                                     | `logfmt`                      |
| `operator.configReloaderResources`                                                    | Set the prometheus config reloader side-car CPU and memory requests and limits.                                        | `{}`                          |
| `operator.kubeletService.enabled`                                                     | If true, the operator will create and maintain a service for scraping kubelets                                         | `true`                        |
| `operator.kubeletService.namespace`                                                   | Namespace to deploy the kubelet service                                                                                | `kube-system`                 |
| `operator.prometheusConfigReloader.image`                                             | Prometheus Config Reloader image. If not set, the same as `operator.image.registry`                                    | `{}`                          |
| `operator.prometheusConfigReloader.containerSecurityContext.enabled`                  | Enable container security context                                                                                      | `true`                        |
| `operator.prometheusConfigReloader.containerSecurityContext.readOnlyRootFilesystem`   | mount / (root) as a readonly filesystem                                                                                | `false`                       |
| `operator.prometheusConfigReloader.containerSecurityContext.allowPrivilegeEscalation` | Switch privilegeEscalation possibility on or off                                                                       | `false`                       |
| `operator.prometheusConfigReloader.containerSecurityContext.runAsNonRoot`             | Force the container to run as a non root user                                                                          | `true`                        |
| `operator.prometheusConfigReloader.containerSecurityContext.capabilities.drop`        | Linux Kernel capabilities which should be dropped                                                                      | `[]`                          |
| `operator.prometheusConfigReloader.livenessProbe.enabled`                             | Turn on and off liveness probe                                                                                         | `true`                        |
| `operator.prometheusConfigReloader.livenessProbe.initialDelaySeconds`                 | Delay before liveness probe is initiated                                                                               | `10`                          |
| `operator.prometheusConfigReloader.livenessProbe.periodSeconds`                       | How often to perform the probe                                                                                         | `10`                          |
| `operator.prometheusConfigReloader.livenessProbe.timeoutSeconds`                      | When the probe times out                                                                                               | `5`                           |
| `operator.prometheusConfigReloader.livenessProbe.failureThreshold`                    | Minimum consecutive failures for the probe                                                                             | `6`                           |
| `operator.prometheusConfigReloader.livenessProbe.successThreshold`                    | Minimum consecutive successes for the probe                                                                            | `1`                           |
| `operator.prometheusConfigReloader.readinessProbe.enabled`                            | Turn on and off readiness probe                                                                                        | `true`                        |
| `operator.prometheusConfigReloader.readinessProbe.initialDelaySeconds`                | Delay before readiness probe is initiated                                                                              | `15`                          |
| `operator.prometheusConfigReloader.readinessProbe.periodSeconds`                      | How often to perform the probe                                                                                         | `20`                          |
| `operator.prometheusConfigReloader.readinessProbe.timeoutSeconds`                     | When the probe times out                                                                                               | `5`                           |
| `operator.prometheusConfigReloader.readinessProbe.failureThreshold`                   | Minimum consecutive failures for the probe                                                                             | `6`                           |
| `operator.prometheusConfigReloader.readinessProbe.successThreshold`                   | Minimum consecutive successes for the probe                                                                            | `1`                           |
| `operator.namespaces`                                                                 | Optional comma-separated list of namespaces to watch (default=all).                                                    | `""`                          |

### Prometheus Parameters

| Name                                                                  | Description                                                                                                                      | Value                     |
| --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| `prometheus.enabled`                                                  | Deploy Prometheus to the cluster                                                                                                 | `true`                    |
| `prometheus.image.registry`                                           | Prometheus image registry                                                                                                        | `docker.io`               |
| `prometheus.image.repository`                                         | Prometheus image repository                                                                                                      | `bitnami/prometheus`      |
| `prometheus.image.tag`                                                | Prometheus image tag (immutable tags are recommended)                                                                            | `2.42.0-debian-11-r4`     |
| `prometheus.image.digest`                                             | Prometheus image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag                       | `""`                      |
| `prometheus.image.pullSecrets`                                        | Specify docker-registry secret names as an array                                                                                 | `[]`                      |
| `prometheus.serviceAccount.create`                                    | Specify whether to create a ServiceAccount for Prometheus                                                                        | `true`                    |
| `prometheus.serviceAccount.name`                                      | The name of the ServiceAccount to create                                                                                         | `""`                      |
| `prometheus.serviceAccount.annotations`                               | Additional annotations for created Prometheus ServiceAccount                                                                     | `{}`                      |
| `prometheus.serviceAccount.automountServiceAccountToken`              | Automount service account token for the server service account                                                                   | `true`                    |
| `prometheus.podSecurityContext.enabled`                               | Enable security context                                                                                                          | `true`                    |
| `prometheus.podSecurityContext.runAsUser`                             | User ID for the container                                                                                                        | `1001`                    |
| `prometheus.podSecurityContext.fsGroup`                               | Group ID for the container filesystem                                                                                            | `1001`                    |
| `prometheus.containerSecurityContext.enabled`                         | Enable container security context                                                                                                | `true`                    |
| `prometheus.containerSecurityContext.readOnlyRootFilesystem`          | Mount / (root) as a readonly filesystem                                                                                          | `false`                   |
| `prometheus.containerSecurityContext.allowPrivilegeEscalation`        | Switch privilegeEscalation possibility on or off                                                                                 | `false`                   |
| `prometheus.containerSecurityContext.runAsNonRoot`                    | Force the container to run as a non root user                                                                                    | `true`                    |
| `prometheus.containerSecurityContext.capabilities.drop`               | Linux Kernel capabilities which should be dropped                                                                                | `[]`                      |
| `prometheus.pdb.create`                                               | Create a pod disruption budget for Prometheus                                                                                    | `false`                   |
| `prometheus.pdb.minAvailable`                                         | Minimum number / percentage of pods that should remain scheduled                                                                 | `1`                       |
| `prometheus.pdb.maxUnavailable`                                       | Maximum number / percentage of pods that may be made unavailable                                                                 | `""`                      |
| `prometheus.service.type`                                             | Kubernetes service type                                                                                                          | `ClusterIP`               |
| `prometheus.service.ports.http`                                       | Prometheus service port                                                                                                          | `9090`                    |
| `prometheus.service.clusterIP`                                        | Specific cluster IP when service type is cluster IP. Use `None` for headless service                                             | `""`                      |
| `prometheus.service.nodePorts.http`                                   | Specify the nodePort value for the LoadBalancer and NodePort service types.                                                      | `""`                      |
| `prometheus.service.loadBalancerIP`                                   | `loadBalancerIP` if service type is `LoadBalancer`                                                                               | `""`                      |
| `prometheus.service.loadBalancerSourceRanges`                         | Address that are allowed when service is `LoadBalancer`                                                                          | `[]`                      |
| `prometheus.service.externalTrafficPolicy`                            | Enable client source IP preservation                                                                                             | `Cluster`                 |
| `prometheus.service.healthCheckNodePort`                              | Specifies the health check node port                                                                                             | `""`                      |
| `prometheus.service.annotations`                                      | Additional annotations for Prometheus service  (this value is evaluated as a template)                                           | `{}`                      |
| `prometheus.service.sessionAffinity`                                  | Session Affinity for Kubernetes service, can be "None" or "ClientIP"                                                             | `None`                    |
| `prometheus.service.sessionAffinityConfig`                            | Additional settings for the sessionAffinity                                                                                      | `{}`                      |
| `prometheus.serviceMonitor.enabled`                                   | Creates a ServiceMonitor to monitor Prometheus itself                                                                            | `true`                    |
| `prometheus.serviceMonitor.interval`                                  | Scrape interval (use by default, falling back to Prometheus' default)                                                            | `""`                      |
| `prometheus.serviceMonitor.metricRelabelings`                         | Metric relabeling                                                                                                                | `[]`                      |
| `prometheus.serviceMonitor.relabelings`                               | Relabel configs                                                                                                                  | `[]`                      |
| `prometheus.ingress.enabled`                                          | Enable ingress controller resource                                                                                               | `false`                   |
| `prometheus.ingress.pathType`                                         | Ingress Path type                                                                                                                | `ImplementationSpecific`  |
| `prometheus.ingress.apiVersion`                                       | Override API Version (automatically detected if not set)                                                                         | `""`                      |
| `prometheus.ingress.hostname`                                         | Default host for the ingress resource                                                                                            | `prometheus.local`        |
| `prometheus.ingress.path`                                             | The Path to Prometheus. You may need to set this to '/*' in order to use this with ALB ingress controllers                       | `/`                       |
| `prometheus.ingress.annotations`                                      | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations. | `{}`                      |
| `prometheus.ingress.ingressClassName`                                 | IngressClass that will be be used to implement the Ingress (Kubernetes 1.18+)                                                    | `""`                      |
| `prometheus.ingress.tls`                                              | Enable TLS configuration for the hostname defined at prometheus.ingress.hostname parameter                                       | `false`                   |
| `prometheus.ingress.selfSigned`                                       | Create a TLS secret for this ingress record using self-signed certificates generated by Helm                                     | `false`                   |
| `prometheus.ingress.extraHosts`                                       | The list of additional hostnames to be covered with this ingress record.                                                         | `[]`                      |
| `prometheus.ingress.extraPaths`                                       | Additional arbitrary path/backend objects                                                                                        | `[]`                      |
| `prometheus.ingress.extraTls`                                         | The tls configuration for additional hostnames to be covered with this ingress record.                                           | `[]`                      |
| `prometheus.ingress.secrets`                                          | If you're providing your own certificates, please use this to add the certificates as secrets                                    | `[]`                      |
| `prometheus.ingress.extraRules`                                       | Additional rules to be covered with this ingress record                                                                          | `[]`                      |
| `prometheus.externalUrl`                                              | External URL used to access Prometheus                                                                                           | `""`                      |
| `prometheus.resources`                                                | CPU/Memory resource requests/limits for node                                                                                     | `{}`                      |
| `prometheus.podAffinityPreset`                                        | Prometheus Pod affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                   | `""`                      |
| `prometheus.podAntiAffinityPreset`                                    | Prometheus Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                              | `soft`                    |
| `prometheus.nodeAffinityPreset.type`                                  | Prometheus Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                             | `""`                      |
| `prometheus.nodeAffinityPreset.key`                                   | Prometheus Node label key to match Ignored if `affinity` is set.                                                                 | `""`                      |
| `prometheus.nodeAffinityPreset.values`                                | Prometheus Node label values to match. Ignored if `affinity` is set.                                                             | `[]`                      |
| `prometheus.affinity`                                                 | Prometheus Affinity for pod assignment                                                                                           | `{}`                      |
| `prometheus.nodeSelector`                                             | Prometheus Node labels for pod assignment                                                                                        | `{}`                      |
| `prometheus.tolerations`                                              | Prometheus Tolerations for pod assignment                                                                                        | `[]`                      |
| `prometheus.scrapeInterval`                                           | Interval between consecutive scrapes                                                                                             | `""`                      |
| `prometheus.evaluationInterval`                                       | Interval between consecutive evaluations                                                                                         | `""`                      |
| `prometheus.listenLocal`                                              | ListenLocal makes the Prometheus server listen on loopback                                                                       | `false`                   |
| `prometheus.livenessProbe.enabled`                                    | Turn on and off liveness probe                                                                                                   | `true`                    |
| `prometheus.livenessProbe.path`                                       | Path of the HTTP service for checking the healthy state                                                                          | `/-/healthy`              |
| `prometheus.livenessProbe.initialDelaySeconds`                        | Delay before liveness probe is initiated                                                                                         | `0`                       |
| `prometheus.livenessProbe.periodSeconds`                              | How often to perform the probe                                                                                                   | `10`                      |
| `prometheus.livenessProbe.timeoutSeconds`                             | When the probe times out                                                                                                         | `3`                       |
| `prometheus.livenessProbe.failureThreshold`                           | Minimum consecutive failures for the probe                                                                                       | `10`                      |
| `prometheus.livenessProbe.successThreshold`                           | Minimum consecutive successes for the probe                                                                                      | `1`                       |
| `prometheus.readinessProbe.enabled`                                   | Turn on and off readiness probe                                                                                                  | `true`                    |
| `prometheus.readinessProbe.path`                                      | Path of the HTTP service for checking the ready state                                                                            | `/-/ready`                |
| `prometheus.readinessProbe.initialDelaySeconds`                       | Delay before readiness probe is initiated                                                                                        | `0`                       |
| `prometheus.readinessProbe.periodSeconds`                             | How often to perform the probe                                                                                                   | `10`                      |
| `prometheus.readinessProbe.timeoutSeconds`                            | When the probe times out                                                                                                         | `3`                       |
| `prometheus.readinessProbe.failureThreshold`                          | Minimum consecutive failures for the probe                                                                                       | `10`                      |
| `prometheus.readinessProbe.successThreshold`                          | Minimum consecutive successes for the probe                                                                                      | `1`                       |
| `prometheus.startupProbe.enabled`                                     | Turn on and off readiness probe                                                                                                  | `true`                    |
| `prometheus.startupProbe.path`                                        | Path of the HTTP service for checking the ready state                                                                            | `/-/ready`                |
| `prometheus.startupProbe.initialDelaySeconds`                         | Delay before readiness probe is initiated                                                                                        | `0`                       |
| `prometheus.startupProbe.periodSeconds`                               | How often to perform the probe                                                                                                   | `15`                      |
| `prometheus.startupProbe.timeoutSeconds`                              | When the probe times out                                                                                                         | `3`                       |
| `prometheus.startupProbe.failureThreshold`                            | Minimum consecutive failures for the probe                                                                                       | `60`                      |
| `prometheus.startupProbe.successThreshold`                            | Minimum consecutive successes for the probe                                                                                      | `1`                       |
| `prometheus.enableAdminAPI`                                           | Enable Prometheus adminitrative API                                                                                              | `false`                   |
| `prometheus.enableFeatures`                                           | Enable access to Prometheus disabled features.                                                                                   | `[]`                      |
| `prometheus.alertingEndpoints`                                        | Alertmanagers to which alerts will be sent                                                                                       | `[]`                      |
| `prometheus.externalLabels`                                           | External labels to add to any time series or alerts when communicating with external systems                                     | `{}`                      |
| `prometheus.replicaExternalLabelName`                                 | Name of the external label used to denote replica name                                                                           | `""`                      |
| `prometheus.replicaExternalLabelNameClear`                            | Clear external label used to denote replica name                                                                                 | `false`                   |
| `prometheus.routePrefix`                                              | Prefix used to register routes, overriding externalUrl route                                                                     | `/`                       |
| `prometheus.prometheusExternalLabelName`                              | Name of the external label used to denote Prometheus instance name                                                               | `""`                      |
| `prometheus.prometheusExternalLabelNameClear`                         | Clear external label used to denote Prometheus instance name                                                                     | `false`                   |
| `prometheus.secrets`                                                  | Secrets that should be mounted into the Prometheus Pods                                                                          | `[]`                      |
| `prometheus.configMaps`                                               | ConfigMaps that should be mounted into the Prometheus Pods                                                                       | `[]`                      |
| `prometheus.querySpec`                                                | The query command line flags when starting Prometheus                                                                            | `{}`                      |
| `prometheus.ruleNamespaceSelector`                                    | Namespaces to be selected for PrometheusRules discovery                                                                          | `{}`                      |
| `prometheus.ruleSelector`                                             | PrometheusRules to be selected for target discovery                                                                              | `{}`                      |
| `prometheus.serviceMonitorSelector`                                   | ServiceMonitors to be selected for target discovery                                                                              | `{}`                      |
| `prometheus.serviceMonitorNamespaceSelector`                          | Namespaces to be selected for ServiceMonitor discovery                                                                           | `{}`                      |
| `prometheus.podMonitorSelector`                                       | PodMonitors to be selected for target discovery.                                                                                 | `{}`                      |
| `prometheus.podMonitorNamespaceSelector`                              | Namespaces to be selected for PodMonitor discovery                                                                               | `{}`                      |
| `prometheus.probeSelector`                                            | Probes to be selected for target discovery.                                                                                      | `{}`                      |
| `prometheus.probeNamespaceSelector`                                   | Namespaces to be selected for Probe discovery                                                                                    | `{}`                      |
| `prometheus.retention`                                                | Metrics retention days                                                                                                           | `10d`                     |
| `prometheus.retentionSize`                                            | Maximum size of metrics                                                                                                          | `""`                      |
| `prometheus.disableCompaction`                                        | Disable the compaction of the Prometheus TSDB                                                                                    | `false`                   |
| `prometheus.walCompression`                                           | Enable compression of the write-ahead log using Snappy                                                                           | `false`                   |
| `prometheus.paused`                                                   | If true, the Operator won't process any Prometheus configuration changes                                                         | `false`                   |
| `prometheus.replicaCount`                                             | Number of Prometheus replicas desired                                                                                            | `1`                       |
| `prometheus.shards`                                                   | Number of Prometheus shards desired                                                                                              | `1`                       |
| `prometheus.logLevel`                                                 | Log level for Prometheus                                                                                                         | `info`                    |
| `prometheus.logFormat`                                                | Log format for Prometheus                                                                                                        | `logfmt`                  |
| `prometheus.podMetadata`                                              | Standard object's metadata                                                                                                       | `{}`                      |
| `prometheus.remoteRead`                                               | The remote_read spec configuration for Prometheus                                                                                | `[]`                      |
| `prometheus.remoteWrite`                                              | The remote_write spec configuration for Prometheus                                                                               | `[]`                      |
| `prometheus.enableRemoteWriteReceiver`                                | Enable Prometheus to be used as a receiver for the Prometheus remote write protocol.                                             | `false`                   |
| `prometheus.storageSpec`                                              | Prometheus StorageSpec for persistent data                                                                                       | `{}`                      |
| `prometheus.persistence.enabled`                                      | Use PVCs to persist data. If the storageSpec is provided this will not take effect.                                              | `false`                   |
| `prometheus.persistence.storageClass`                                 | Persistent Volume Storage Class                                                                                                  | `""`                      |
| `prometheus.persistence.accessModes`                                  | Persistent Volume Access Modes                                                                                                   | `["ReadWriteOnce"]`       |
| `prometheus.persistence.size`                                         | Persistent Volume Size                                                                                                           | `8Gi`                     |
| `prometheus.persistence.annotations`                                  | Persistent Volume Claim annotations                                                                                              | `{}`                      |
| `prometheus.priorityClassName`                                        | Priority class assigned to the Pods                                                                                              | `""`                      |
| `prometheus.containers`                                               | Containers allows injecting additional containers                                                                                | `[]`                      |
| `prometheus.initContainers`                                           | Add additional init containers to the prometheus pod(s)                                                                          | `[]`                      |
| `prometheus.volumes`                                                  | Volumes allows configuration of additional volumes                                                                               | `[]`                      |
| `prometheus.volumeMounts`                                             | VolumeMounts allows configuration of additional VolumeMounts. Evaluated as a template                                            | `[]`                      |
| `prometheus.additionalPrometheusRules`                                | PrometheusRule defines recording and alerting rules for a Prometheus instance.                                                   | `[]`                      |
| `prometheus.additionalScrapeConfigs.enabled`                          | Enable additional scrape configs                                                                                                 | `false`                   |
| `prometheus.additionalScrapeConfigs.type`                             | Indicates if the cart should use external additional scrape configs or internal configs                                          | `external`                |
| `prometheus.additionalScrapeConfigs.external.name`                    | Name of the secret that Prometheus should use for the additional external scrape configuration                                   | `""`                      |
| `prometheus.additionalScrapeConfigs.external.key`                     | Name of the key inside the secret to be used for the additional external scrape configuration                                    | `""`                      |
| `prometheus.additionalScrapeConfigs.internal.jobList`                 | A list of Prometheus scrape jobs                                                                                                 | `[]`                      |
| `prometheus.additionalScrapeConfigsExternal.enabled`                  | Deprecated: Enable additional scrape configs that are managed externally to this chart                                           | `false`                   |
| `prometheus.additionalScrapeConfigsExternal.name`                     | Deprecated: Name of the secret that Prometheus should use for the additional scrape configuration                                | `""`                      |
| `prometheus.additionalScrapeConfigsExternal.key`                      | Deprecated: Name of the key inside the secret to be used for the additional scrape configuration                                 | `""`                      |
| `prometheus.additionalAlertRelabelConfigsExternal.enabled`            | Enable additional Prometheus alert relabel configs that are managed externally to this chart                                     | `false`                   |
| `prometheus.additionalAlertRelabelConfigsExternal.name`               | Name of the secret that Prometheus should use for the additional Prometheus alert relabel configuration                          | `""`                      |
| `prometheus.additionalAlertRelabelConfigsExternal.key`                | Name of the key inside the secret to be used for the additional Prometheus alert relabel configuration                           | `""`                      |
| `prometheus.thanos.create`                                            | Create a Thanos sidecar container                                                                                                | `false`                   |
| `prometheus.thanos.image.registry`                                    | Thanos image registry                                                                                                            | `docker.io`               |
| `prometheus.thanos.image.repository`                                  | Thanos image name                                                                                                                | `bitnami/thanos`          |
| `prometheus.thanos.image.tag`                                         | Thanos image tag                                                                                                                 | `0.30.2-scratch-r1`       |
| `prometheus.thanos.image.digest`                                      | Thanos image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag                           | `""`                      |
| `prometheus.thanos.image.pullPolicy`                                  | Thanos image pull policy                                                                                                         | `IfNotPresent`            |
| `prometheus.thanos.image.pullSecrets`                                 | Specify docker-registry secret names as an array                                                                                 | `[]`                      |
| `prometheus.thanos.containerSecurityContext.enabled`                  | Enable container security context                                                                                                | `true`                    |
| `prometheus.thanos.containerSecurityContext.readOnlyRootFilesystem`   | mount / (root) as a readonly filesystem                                                                                          | `false`                   |
| `prometheus.thanos.containerSecurityContext.allowPrivilegeEscalation` | Switch privilegeEscalation possibility on or off                                                                                 | `false`                   |
| `prometheus.thanos.containerSecurityContext.runAsNonRoot`             | Force the container to run as a non root user                                                                                    | `true`                    |
| `prometheus.thanos.containerSecurityContext.capabilities.drop`        | Linux Kernel capabilities which should be dropped                                                                                | `[]`                      |
| `prometheus.thanos.prometheusUrl`                                     | Override default prometheus url `http://localhost:9090`                                                                          | `""`                      |
| `prometheus.thanos.extraArgs`                                         | Additional arguments passed to the thanos sidecar container                                                                      | `[]`                      |
| `prometheus.thanos.objectStorageConfig`                               | Support mounting a Secret for the objectStorageConfig of the sideCar container.                                                  | `{}`                      |
| `prometheus.thanos.extraVolumeMounts`                                 | Additional volumeMounts from `prometheus.volumes` for thanos sidecar container                                                   | `[]`                      |
| `prometheus.thanos.resources.limits`                                  | The resources limits for the Thanos sidecar container                                                                            | `{}`                      |
| `prometheus.thanos.resources.requests`                                | The resources requests for the Thanos sidecar container                                                                          | `{}`                      |
| `prometheus.thanos.livenessProbe.enabled`                             | Turn on and off liveness probe                                                                                                   | `true`                    |
| `prometheus.thanos.livenessProbe.path`                                | Path of the HTTP service for checking the healthy state                                                                          | `/-/healthy`              |
| `prometheus.thanos.livenessProbe.initialDelaySeconds`                 | Delay before liveness probe is initiated                                                                                         | `0`                       |
| `prometheus.thanos.livenessProbe.periodSeconds`                       | How often to perform the probe                                                                                                   | `5`                       |
| `prometheus.thanos.livenessProbe.timeoutSeconds`                      | When the probe times out                                                                                                         | `3`                       |
| `prometheus.thanos.livenessProbe.failureThreshold`                    | Minimum consecutive failures for the probe                                                                                       | `120`                     |
| `prometheus.thanos.livenessProbe.successThreshold`                    | Minimum consecutive successes for the probe                                                                                      | `1`                       |
| `prometheus.thanos.readinessProbe.enabled`                            | Turn on and off readiness probe                                                                                                  | `true`                    |
| `prometheus.thanos.readinessProbe.path`                               | Path of the HTTP service for checking the ready state                                                                            | `/-/ready`                |
| `prometheus.thanos.readinessProbe.initialDelaySeconds`                | Delay before readiness probe is initiated                                                                                        | `0`                       |
| `prometheus.thanos.readinessProbe.periodSeconds`                      | How often to perform the probe                                                                                                   | `5`                       |
| `prometheus.thanos.readinessProbe.timeoutSeconds`                     | When the probe times out                                                                                                         | `3`                       |
| `prometheus.thanos.readinessProbe.failureThreshold`                   | Minimum consecutive failures for the probe                                                                                       | `120`                     |
| `prometheus.thanos.readinessProbe.successThreshold`                   | Minimum consecutive successes for the probe                                                                                      | `1`                       |
| `prometheus.thanos.service.type`                                      | Kubernetes service type                                                                                                          | `ClusterIP`               |
| `prometheus.thanos.service.ports.grpc`                                | Thanos service port                                                                                                              | `10901`                   |
| `prometheus.thanos.service.clusterIP`                                 | Specific cluster IP when service type is cluster IP. Use `None` to create headless service by default.                           | `None`                    |
| `prometheus.thanos.service.nodePorts.grpc`                            | Specify the nodePort value for the LoadBalancer and NodePort service types.                                                      | `""`                      |
| `prometheus.thanos.service.loadBalancerIP`                            | `loadBalancerIP` if service type is `LoadBalancer`                                                                               | `""`                      |
| `prometheus.thanos.service.loadBalancerSourceRanges`                  | Address that are allowed when svc is `LoadBalancer`                                                                              | `[]`                      |
| `prometheus.thanos.service.annotations`                               | Additional annotations for Prometheus service                                                                                    | `{}`                      |
| `prometheus.thanos.service.extraPorts`                                | Additional ports to expose from the Thanos sidecar container                                                                     | `[]`                      |
| `prometheus.thanos.service.externalTrafficPolicy`                     | Prometheus service external traffic policy                                                                                       | `Cluster`                 |
| `prometheus.thanos.service.sessionAffinity`                           | Session Affinity for Kubernetes service, can be "None" or "ClientIP"                                                             | `None`                    |
| `prometheus.thanos.service.sessionAffinityConfig`                     | Additional settings for the sessionAffinity                                                                                      | `{}`                      |
| `prometheus.thanos.ingress.enabled`                                   | Enable ingress controller resource                                                                                               | `false`                   |
| `prometheus.thanos.ingress.pathType`                                  | Ingress path type                                                                                                                | `ImplementationSpecific`  |
| `prometheus.thanos.ingress.apiVersion`                                | Force Ingress API version (automatically detected if not set)                                                                    | `""`                      |
| `prometheus.thanos.ingress.hostname`                                  | Default host for the ingress record                                                                                              | `thanos.prometheus.local` |
| `prometheus.thanos.ingress.path`                                      | Default path for the ingress record                                                                                              | `/`                       |
| `prometheus.thanos.ingress.annotations`                               | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations. | `{}`                      |
| `prometheus.thanos.ingress.ingressClassName`                          | IngressClass that will be be used to implement the Ingress (Kubernetes 1.18+)                                                    | `""`                      |
| `prometheus.thanos.ingress.tls`                                       | Enable TLS configuration for the host defined at `ingress.hostname` parameter                                                    | `false`                   |
| `prometheus.thanos.ingress.selfSigned`                                | Create a TLS secret for this ingress record using self-signed certificates generated by Helm                                     | `false`                   |
| `prometheus.thanos.ingress.extraHosts`                                | An array with additional hostname(s) to be covered with the ingress record                                                       | `[]`                      |
| `prometheus.thanos.ingress.extraPaths`                                | An array with additional arbitrary paths that may need to be added to the ingress under the main host                            | `[]`                      |
| `prometheus.thanos.ingress.extraTls`                                  | TLS configuration for additional hostname(s) to be covered with this ingress record                                              | `[]`                      |
| `prometheus.thanos.ingress.secrets`                                   | Custom TLS certificates as secrets                                                                                               | `[]`                      |
| `prometheus.thanos.ingress.extraRules`                                | The list of additional rules to be added to this ingress record. Evaluated as a template                                         | `[]`                      |
| `prometheus.portName`                                                 | Port name used for the pods and governing service. This defaults to web                                                          | `web`                     |

### Alertmanager Parameters

| Name                                                             | Description                                                                                                                                                                                                                                                                                                | Value                    |
| ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `alertmanager.enabled`                                           | Deploy Alertmanager to the cluster                                                                                                                                                                                                                                                                         | `true`                   |
| `alertmanager.image.registry`                                    | Prometheus image registry                                                                                                                                                                                                                                                                                  | `docker.io`              |
| `alertmanager.image.repository`                                  | Prometheus image repository                                                                                                                                                                                                                                                                                | `bitnami/alertmanager`   |
| `alertmanager.image.tag`                                         | Prometheus image tag (immutable tags are recommended)                                                                                                                                                                                                                                                      | `0.25.0-debian-11-r20`   |
| `alertmanager.image.digest`                                      | Prometheus image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag                                                                                                                                                                                                 | `""`                     |
| `alertmanager.image.pullSecrets`                                 | Specify docker-registry secret names as an array                                                                                                                                                                                                                                                           | `[]`                     |
| `alertmanager.serviceAccount.create`                             | Specify whether to create a ServiceAccount for Alertmanager                                                                                                                                                                                                                                                | `true`                   |
| `alertmanager.serviceAccount.name`                               | The name of the ServiceAccount to create                                                                                                                                                                                                                                                                   | `""`                     |
| `alertmanager.serviceAccount.automountServiceAccountToken`       | Automount service account token for the server service account                                                                                                                                                                                                                                             | `true`                   |
| `alertmanager.serviceAccount.annotations`                        | Annotations for service account. Evaluated as a template. Only used if `create` is `true`.                                                                                                                                                                                                                 | `{}`                     |
| `alertmanager.podSecurityContext.enabled`                        | Enable security context                                                                                                                                                                                                                                                                                    | `true`                   |
| `alertmanager.podSecurityContext.runAsUser`                      | User ID for the container                                                                                                                                                                                                                                                                                  | `1001`                   |
| `alertmanager.podSecurityContext.fsGroup`                        | Group ID for the container filesystem                                                                                                                                                                                                                                                                      | `1001`                   |
| `alertmanager.containerSecurityContext.enabled`                  | Enable container security context                                                                                                                                                                                                                                                                          | `true`                   |
| `alertmanager.containerSecurityContext.readOnlyRootFilesystem`   | mount / (root) as a readonly filesystem                                                                                                                                                                                                                                                                    | `false`                  |
| `alertmanager.containerSecurityContext.allowPrivilegeEscalation` | Switch privilegeEscalation possibility on or off                                                                                                                                                                                                                                                           | `false`                  |
| `alertmanager.containerSecurityContext.runAsNonRoot`             | Force the container to run as a non root user                                                                                                                                                                                                                                                              | `true`                   |
| `alertmanager.containerSecurityContext.capabilities.drop`        | Linux Kernel capabilities which should be dropped                                                                                                                                                                                                                                                          | `[]`                     |
| `alertmanager.pdb.create`                                        | Create a pod disruption budget for Alertmanager                                                                                                                                                                                                                                                            | `false`                  |
| `alertmanager.pdb.minAvailable`                                  | Minimum number / percentage of pods that should remain scheduled                                                                                                                                                                                                                                           | `1`                      |
| `alertmanager.pdb.maxUnavailable`                                | Maximum number / percentage of pods that may be made unavailable                                                                                                                                                                                                                                           | `""`                     |
| `alertmanager.service.type`                                      | Kubernetes service type                                                                                                                                                                                                                                                                                    | `ClusterIP`              |
| `alertmanager.service.ports.http`                                | Alertmanager service port                                                                                                                                                                                                                                                                                  | `9093`                   |
| `alertmanager.service.clusterIP`                                 | Specific cluster IP when service type is cluster IP. Use `None` for headless service                                                                                                                                                                                                                       | `""`                     |
| `alertmanager.service.nodePorts.http`                            | Specify the nodePort value for the LoadBalancer and NodePort service types.                                                                                                                                                                                                                                | `""`                     |
| `alertmanager.service.loadBalancerIP`                            | `loadBalancerIP` if service type is `LoadBalancer`                                                                                                                                                                                                                                                         | `""`                     |
| `alertmanager.service.loadBalancerSourceRanges`                  | Address that are allowed when svc is `LoadBalancer`                                                                                                                                                                                                                                                        | `[]`                     |
| `alertmanager.service.externalTrafficPolicy`                     | Enable client source IP preservation                                                                                                                                                                                                                                                                       | `Cluster`                |
| `alertmanager.service.healthCheckNodePort`                       | Specifies the health check node port                                                                                                                                                                                                                                                                       | `""`                     |
| `alertmanager.service.extraPorts`                                | Extra ports to expose (normally used with the `sidecar` value)                                                                                                                                                                                                                                             | `[]`                     |
| `alertmanager.service.sessionAffinity`                           | Session Affinity for Kubernetes service, can be "None" or "ClientIP"                                                                                                                                                                                                                                       | `None`                   |
| `alertmanager.service.sessionAffinityConfig`                     | Additional settings for the sessionAffinity                                                                                                                                                                                                                                                                | `{}`                     |
| `alertmanager.service.annotations`                               | Additional annotations for Alertmanager service (this value is evaluated as a template)                                                                                                                                                                                                                    | `{}`                     |
| `alertmanager.serviceMonitor.enabled`                            | Creates a ServiceMonitor to monitor Alertmanager                                                                                                                                                                                                                                                           | `true`                   |
| `alertmanager.serviceMonitor.interval`                           | Scrape interval. If not set, the Prometheus default scrape interval is used.                                                                                                                                                                                                                               | `""`                     |
| `alertmanager.serviceMonitor.metricRelabelings`                  | Metric relabeling                                                                                                                                                                                                                                                                                          | `[]`                     |
| `alertmanager.serviceMonitor.relabelings`                        | Relabel configs                                                                                                                                                                                                                                                                                            | `[]`                     |
| `alertmanager.serviceMonitor.jobLabel`                           | The name of the label on the target service to use as the job name in prometheus.                                                                                                                                                                                                                          | `""`                     |
| `alertmanager.serviceMonitor.scrapeTimeout`                      | Timeout after which the scrape is ended                                                                                                                                                                                                                                                                    | `""`                     |
| `alertmanager.serviceMonitor.selector`                           | ServiceMonitor selector labels                                                                                                                                                                                                                                                                             | `{}`                     |
| `alertmanager.serviceMonitor.labels`                             | Extra labels for the ServiceMonitor                                                                                                                                                                                                                                                                        | `{}`                     |
| `alertmanager.serviceMonitor.annotations`                        | Extra annotations for the ServiceMonitor                                                                                                                                                                                                                                                                   | `{}`                     |
| `alertmanager.serviceMonitor.honorLabels`                        | honorLabels chooses the metric's labels on collisions with target labels                                                                                                                                                                                                                                   | `false`                  |
| `alertmanager.ingress.enabled`                                   | Enable ingress controller resource                                                                                                                                                                                                                                                                         | `false`                  |
| `alertmanager.ingress.pathType`                                  | Ingress Path type                                                                                                                                                                                                                                                                                          | `ImplementationSpecific` |
| `alertmanager.ingress.apiVersion`                                | Override API Version (automatically detected if not set)                                                                                                                                                                                                                                                   | `""`                     |
| `alertmanager.ingress.hostname`                                  | Default host for the ingress resource                                                                                                                                                                                                                                                                      | `alertmanager.local`     |
| `alertmanager.ingress.path`                                      | The Path to Alert Manager. You may need to set this to '/*' in order to use this with ALB ingress controllers.                                                                                                                                                                                             | `/`                      |
| `alertmanager.ingress.annotations`                               | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations.                                                                                                                                                                           | `{}`                     |
| `alertmanager.ingress.ingressClassName`                          | IngressClass that will be be used to implement the Ingress (Kubernetes 1.18+)                                                                                                                                                                                                                              | `""`                     |
| `alertmanager.ingress.tls`                                       | Enable TLS configuration for the hostname defined at alertmanager.ingress.hostname parameter                                                                                                                                                                                                               | `false`                  |
| `alertmanager.ingress.selfSigned`                                | Create a TLS secret for this ingress record using self-signed certificates generated by Helm                                                                                                                                                                                                               | `false`                  |
| `alertmanager.ingress.extraHosts`                                | The list of additional hostnames to be covered with this ingress record.                                                                                                                                                                                                                                   | `[]`                     |
| `alertmanager.ingress.extraPaths`                                | Additional arbitrary path/backend objects                                                                                                                                                                                                                                                                  | `[]`                     |
| `alertmanager.ingress.extraTls`                                  | The tls configuration for additional hostnames to be covered with this ingress record.                                                                                                                                                                                                                     | `[]`                     |
| `alertmanager.ingress.secrets`                                   | If you're providing your own certificates, please use this to add the certificates as secrets                                                                                                                                                                                                              | `[]`                     |
| `alertmanager.ingress.extraRules`                                | Additional rules to be covered with this ingress record                                                                                                                                                                                                                                                    | `[]`                     |
| `alertmanager.externalUrl`                                       | External URL used to access Alertmanager                                                                                                                                                                                                                                                                   | `""`                     |
| `alertmanager.resources`                                         | CPU/Memory resource requests/limits for node                                                                                                                                                                                                                                                               | `{}`                     |
| `alertmanager.podAffinityPreset`                                 | Alertmanager Pod affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                                                                                                                                                                                           | `""`                     |
| `alertmanager.podAntiAffinityPreset`                             | Alertmanager Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                                                                                                                                                                                      | `soft`                   |
| `alertmanager.nodeAffinityPreset.type`                           | Alertmanager Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                                                                                                                                                                                     | `""`                     |
| `alertmanager.nodeAffinityPreset.key`                            | Alertmanager Node label key to match Ignored if `affinity` is set.                                                                                                                                                                                                                                         | `""`                     |
| `alertmanager.nodeAffinityPreset.values`                         | Alertmanager Node label values to match. Ignored if `affinity` is set.                                                                                                                                                                                                                                     | `[]`                     |
| `alertmanager.affinity`                                          | Alertmanager Affinity for pod assignment                                                                                                                                                                                                                                                                   | `{}`                     |
| `alertmanager.nodeSelector`                                      | Alertmanager Node labels for pod assignment                                                                                                                                                                                                                                                                | `{}`                     |
| `alertmanager.tolerations`                                       | Alertmanager Tolerations for pod assignment                                                                                                                                                                                                                                                                | `[]`                     |
| `alertmanager.config`                                            | Alertmanager configuration directive                                                                                                                                                                                                                                                                       | `{}`                     |
| `alertmanager.templateFiles`                                     | Extra files to be added inside the `alertmanager-{{ template "kube-prometheus.alertmanager.fullname" . }}` secret.                                                                                                                                                                                         | `{}`                     |
| `alertmanager.externalConfig`                                    | Alertmanager configuration is created externally. If true, `alertmanager.config` is ignored, and a secret will not be created.                                                                                                                                                                             | `false`                  |
| `alertmanager.replicaCount`                                      | Number of Alertmanager replicas desired                                                                                                                                                                                                                                                                    | `1`                      |
| `alertmanager.livenessProbe.enabled`                             | Turn on and off liveness probe                                                                                                                                                                                                                                                                             | `true`                   |
| `alertmanager.livenessProbe.path`                                | Path of the HTTP service for checking the healthy state                                                                                                                                                                                                                                                    | `/-/healthy`             |
| `alertmanager.livenessProbe.initialDelaySeconds`                 | Delay before liveness probe is initiated                                                                                                                                                                                                                                                                   | `0`                      |
| `alertmanager.livenessProbe.periodSeconds`                       | How often to perform the probe                                                                                                                                                                                                                                                                             | `5`                      |
| `alertmanager.livenessProbe.timeoutSeconds`                      | When the probe times out                                                                                                                                                                                                                                                                                   | `3`                      |
| `alertmanager.livenessProbe.failureThreshold`                    | Minimum consecutive failures for the probe                                                                                                                                                                                                                                                                 | `120`                    |
| `alertmanager.livenessProbe.successThreshold`                    | Minimum consecutive successes for the probe                                                                                                                                                                                                                                                                | `1`                      |
| `alertmanager.readinessProbe.enabled`                            | Turn on and off readiness probe                                                                                                                                                                                                                                                                            | `true`                   |
| `alertmanager.readinessProbe.path`                               | Path of the HTTP service for checking the ready state                                                                                                                                                                                                                                                      | `/-/ready`               |
| `alertmanager.readinessProbe.initialDelaySeconds`                | Delay before readiness probe is initiated                                                                                                                                                                                                                                                                  | `0`                      |
| `alertmanager.readinessProbe.periodSeconds`                      | How often to perform the probe                                                                                                                                                                                                                                                                             | `5`                      |
| `alertmanager.readinessProbe.timeoutSeconds`                     | When the probe times out                                                                                                                                                                                                                                                                                   | `3`                      |
| `alertmanager.readinessProbe.failureThreshold`                   | Minimum consecutive failures for the probe                                                                                                                                                                                                                                                                 | `120`                    |
| `alertmanager.readinessProbe.successThreshold`                   | Minimum consecutive successes for the probe                                                                                                                                                                                                                                                                | `1`                      |
| `alertmanager.logLevel`                                          | Log level for Alertmanager                                                                                                                                                                                                                                                                                 | `info`                   |
| `alertmanager.logFormat`                                         | Log format for Alertmanager                                                                                                                                                                                                                                                                                | `logfmt`                 |
| `alertmanager.podMetadata`                                       | Standard object's metadata.                                                                                                                                                                                                                                                                                | `{}`                     |
| `alertmanager.secrets`                                           | Secrets that should be mounted into the Alertmanager Pods                                                                                                                                                                                                                                                  | `[]`                     |
| `alertmanager.configMaps`                                        | ConfigMaps that should be mounted into the Alertmanager Pods                                                                                                                                                                                                                                               | `[]`                     |
| `alertmanager.retention`                                         | Metrics retention days                                                                                                                                                                                                                                                                                     | `120h`                   |
| `alertmanager.storageSpec`                                       | Alertmanager StorageSpec for persistent data                                                                                                                                                                                                                                                               | `{}`                     |
| `alertmanager.persistence.enabled`                               | Use PVCs to persist data. If the storageSpec is provided this will not take effect.                                                                                                                                                                                                                        | `false`                  |
| `alertmanager.persistence.storageClass`                          | Persistent Volume Storage Class                                                                                                                                                                                                                                                                            | `""`                     |
| `alertmanager.persistence.accessModes`                           | Persistent Volume Access Modes                                                                                                                                                                                                                                                                             | `["ReadWriteOnce"]`      |
| `alertmanager.persistence.size`                                  | Persistent Volume Size                                                                                                                                                                                                                                                                                     | `8Gi`                    |
| `alertmanager.persistence.annotations`                           | Persistent Volume Claim annotations                                                                                                                                                                                                                                                                        | `{}`                     |
| `alertmanager.paused`                                            | If true, the Operator won't process any Alertmanager configuration changes                                                                                                                                                                                                                                 | `false`                  |
| `alertmanager.listenLocal`                                       | ListenLocal makes the Alertmanager server listen on loopback                                                                                                                                                                                                                                               | `false`                  |
| `alertmanager.containers`                                        | Containers allows injecting additional containers                                                                                                                                                                                                                                                          | `[]`                     |
| `alertmanager.volumes`                                           | Volumes allows configuration of additional volumes. Evaluated as a template                                                                                                                                                                                                                                | `[]`                     |
| `alertmanager.volumeMounts`                                      | VolumeMounts allows configuration of additional VolumeMounts. Evaluated as a template                                                                                                                                                                                                                      | `[]`                     |
| `alertmanager.priorityClassName`                                 | Priority class assigned to the Pods                                                                                                                                                                                                                                                                        | `""`                     |
| `alertmanager.additionalPeers`                                   | AdditionalPeers allows injecting a set of additional Alertmanagers to peer with to form a highly available cluster                                                                                                                                                                                         | `[]`                     |
| `alertmanager.routePrefix`                                       | Prefix used to register routes, overriding externalUrl route                                                                                                                                                                                                                                               | `/`                      |
| `alertmanager.portName`                                          | Port name used for the pods and governing service. This defaults to web                                                                                                                                                                                                                                    | `web`                    |
| `alertmanager.configNamespaceSelector`                           | AlertmanagerConfigs to be selected for to merge and configure Alertmanager with. This defaults to {}                                                                                                                                                                                                       | `{}`                     |
| `alertmanager.configSelector`                                    | Namespaces to be selected for AlertmanagerConfig discovery. If nil, only check own namespace. This defaults to {}                                                                                                                                                                                          | `{}`                     |
| `alertmanager.configuration`                                     | EXPERIMENTAL: alertmanagerConfiguration specifies the global Alertmanager configuration. If defined, it takes precedence over the `configSecret` field. This field may change in future releases. The specified global alertmanager config will not force add a namespace label in routes and inhibitRules | `{}`                     |

### Exporters

| Name                                               | Description                                                                                            | Value                        |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------- |
| `exporters.node-exporter.enabled`                  | Enable node-exporter                                                                                   | `true`                       |
| `exporters.kube-state-metrics.enabled`             | Enable kube-state-metrics                                                                              | `true`                       |
| `node-exporter`                                    | Node Exporter deployment configuration                                                                 | `{}`                         |
| `kube-state-metrics`                               | Kube State Metrics deployment configuration                                                            | `{}`                         |
| `kubelet.enabled`                                  | Create a ServiceMonitor to scrape kubelet service                                                      | `true`                       |
| `kubelet.namespace`                                | Namespace where kubelet service is deployed. Related configuration `operator.kubeletService.namespace` | `kube-system`                |
| `kubelet.serviceMonitor.https`                     | Enable scraping of the kubelet over HTTPS                                                              | `true`                       |
| `kubelet.serviceMonitor.interval`                  | Scrape interval (use by default, falling back to Prometheus' default)                                  | `""`                         |
| `kubelet.serviceMonitor.resource`                  | Enable scraping /metrics/resource from kubelet's service                                               | `false`                      |
| `kubelet.serviceMonitor.resourcePath`              | From kubernetes 1.18, /metrics/resource/v1alpha1 was renamed to /metrics/resource                      | `/metrics/resource/v1alpha1` |
| `kubelet.serviceMonitor.resourceRelabelings`       | Metric relabeling                                                                                      | `[]`                         |
| `kubelet.serviceMonitor.resourceMetricRelabelings` | Metric relabeling                                                                                      | `[]`                         |
| `kubelet.serviceMonitor.metricRelabelings`         | Metric relabeling                                                                                      | `[]`                         |
| `kubelet.serviceMonitor.relabelings`               | Relabel configs                                                                                        | `[]`                         |
| `kubelet.serviceMonitor.cAdvisor`                  | Enable scraping /metrics/cadvisor from kubelet's service                                               | `true`                       |
| `kubelet.serviceMonitor.cAdvisorMetricRelabelings` | Metric relabeling for scraping cAdvisor                                                                | `[]`                         |
| `kubelet.serviceMonitor.cAdvisorRelabelings`       | Relabel configs for scraping cAdvisor                                                                  | `[]`                         |
| `kubelet.serviceMonitor.labels`                    | Extra labels for the ServiceMonitor                                                                    | `{}`                         |
| `kubelet.serviceMonitor.annotations`               | Extra annotations for the ServiceMonitor                                                               | `{}`                         |

### Blackbox Exporter Deployment Parameters

| Name                                                           | Description                                                                                                       | Value                       |
| -------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | --------------------------- |
| `blackboxExporter.enabled`                                     | Enable Blackbox Exporter deployment                                                                               | `true`                      |
| `blackboxExporter.image.registry`                              | Blackbox Exporter image registry                                                                                  | `docker.io`                 |
| `blackboxExporter.image.repository`                            | Blackbox Exporter image repository                                                                                | `bitnami/blackbox-exporter` |
| `blackboxExporter.image.pullPolicy`                            | Blackbox Exporter image pull policy                                                                               | `IfNotPresent`              |
| `blackboxExporter.image.tag`                                   | Blackbox Exporter image tag (immutable tags are recommended)                                                      | `0.23.0-debian-11-r26`      |
| `blackboxExporter.image.digest`                                | Blackbox Exporter image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag | `""`                        |
| `blackboxExporter.image.pullSecrets`                           | Specify docker-registry secret names as an array                                                                  | `[]`                        |
| `blackboxExporter.extraEnvVars`                                | Array with extra environment variables to add to blackboxExporter nodes                                           | `[]`                        |
| `blackboxExporter.extraEnvVarsCM`                              | Name of existing ConfigMap containing extra env vars for blackboxExporter nodes                                   | `""`                        |
| `blackboxExporter.extraEnvVarsSecret`                          | Name of existing Secret containing extra env vars for blackboxExporter nodes                                      | `""`                        |
| `blackboxExporter.command`                                     | Override default container command (useful when using custom images)                                              | `[]`                        |
| `blackboxExporter.args`                                        | Override default container args (useful when using custom images)                                                 | `[]`                        |
| `blackboxExporter.replicaCount`                                | Number of Blackbox Exporter replicas to deploy                                                                    | `1`                         |
| `blackboxExporter.livenessProbe.enabled`                       | Enable livenessProbe on Blackbox Exporter nodes                                                                   | `true`                      |
| `blackboxExporter.livenessProbe.initialDelaySeconds`           | Initial delay seconds for livenessProbe                                                                           | `30`                        |
| `blackboxExporter.livenessProbe.periodSeconds`                 | Period seconds for livenessProbe                                                                                  | `10`                        |
| `blackboxExporter.livenessProbe.timeoutSeconds`                | Timeout seconds for livenessProbe                                                                                 | `1`                         |
| `blackboxExporter.livenessProbe.failureThreshold`              | Failure threshold for livenessProbe                                                                               | `3`                         |
| `blackboxExporter.livenessProbe.successThreshold`              | Success threshold for livenessProbe                                                                               | `1`                         |
| `blackboxExporter.readinessProbe.enabled`                      | Enable readinessProbe on Blackbox Exporter nodes                                                                  | `true`                      |
| `blackboxExporter.readinessProbe.initialDelaySeconds`          | Initial delay seconds for readinessProbe                                                                          | `60`                        |
| `blackboxExporter.readinessProbe.periodSeconds`                | Period seconds for readinessProbe                                                                                 | `10`                        |
| `blackboxExporter.readinessProbe.timeoutSeconds`               | Timeout seconds for readinessProbe                                                                                | `1`                         |
| `blackboxExporter.readinessProbe.failureThreshold`             | Failure threshold for readinessProbe                                                                              | `3`                         |
| `blackboxExporter.readinessProbe.successThreshold`             | Success threshold for readinessProbe                                                                              | `1`                         |
| `blackboxExporter.startupProbe.enabled`                        | Enable startupProbe on Blackbox Exporter containers                                                               | `false`                     |
| `blackboxExporter.startupProbe.initialDelaySeconds`            | Initial delay seconds for startupProbe                                                                            | `30`                        |
| `blackboxExporter.startupProbe.periodSeconds`                  | Period seconds for startupProbe                                                                                   | `10`                        |
| `blackboxExporter.startupProbe.timeoutSeconds`                 | Timeout seconds for startupProbe                                                                                  | `1`                         |
| `blackboxExporter.startupProbe.failureThreshold`               | Failure threshold for startupProbe                                                                                | `15`                        |
| `blackboxExporter.startupProbe.successThreshold`               | Success threshold for startupProbe                                                                                | `1`                         |
| `blackboxExporter.customLivenessProbe`                         | Custom livenessProbe that overrides the default one                                                               | `{}`                        |
| `blackboxExporter.customReadinessProbe`                        | Custom readinessProbe that overrides the default one                                                              | `{}`                        |
| `blackboxExporter.customStartupProbe`                          | Custom startupProbe that overrides the default one                                                                | `{}`                        |
| `blackboxExporter.configuration`                               | Blackbox Exporter configuration                                                                                   | `{}`                        |
| `blackboxExporter.existingConfigMap`                           | ConfigMap pointing to the Blackbox Exporter configuration                                                         | `""`                        |
| `blackboxExporter.containerPorts.http`                         | Blackbox Exporter HTTP container port                                                                             | `19115`                     |
| `blackboxExporter.serviceAccount.create`                       | Enable creation of ServiceAccount for WordPress pod                                                               | `true`                      |
| `blackboxExporter.serviceAccount.name`                         | The name of the ServiceAccount to use.                                                                            | `""`                        |
| `blackboxExporter.serviceAccount.automountServiceAccountToken` | Allows auto mount of ServiceAccountToken on the serviceAccount created                                            | `true`                      |
| `blackboxExporter.serviceAccount.annotations`                  | Additional custom annotations for the ServiceAccount                                                              | `{}`                        |
| `blackboxExporter.resources.limits`                            | The resources limits for the blackboxExporter containers                                                          | `{}`                        |
| `blackboxExporter.resources.requests`                          | The requested resources for the blackboxExporter containers                                                       | `{}`                        |
| `blackboxExporter.podSecurityContext.enabled`                  | Enabled Blackbox Exporter pods' Security Context                                                                  | `true`                      |
| `blackboxExporter.podSecurityContext.fsGroup`                  | Set Blackbox Exporter pod's Security Context fsGroup                                                              | `1001`                      |
| `blackboxExporter.containerSecurityContext.enabled`            | Enabled Blackbox Exporter containers' Security Context                                                            | `true`                      |
| `blackboxExporter.containerSecurityContext.runAsUser`          | Set Blackbox Exporter containers' Security Context runAsUser                                                      | `1001`                      |
| `blackboxExporter.containerSecurityContext.runAsNonRoot`       | Set Blackbox Exporter containers' Security Context runAsNonRoot                                                   | `true`                      |
| `blackboxExporter.lifecycleHooks`                              | for the blackboxExporter container(s) to automate configuration before or after startup                           | `{}`                        |
| `blackboxExporter.hostAliases`                                 | blackboxExporter pods host aliases                                                                                | `[]`                        |
| `blackboxExporter.podLabels`                                   | Extra labels for blackboxExporter pods                                                                            | `{}`                        |
| `blackboxExporter.podAnnotations`                              | Annotations for blackboxExporter pods                                                                             | `{}`                        |
| `blackboxExporter.podAffinityPreset`                           | Pod affinity preset. Ignored if `blackboxExporter.affinity` is set. Allowed values: `soft` or `hard`              | `""`                        |
| `blackboxExporter.podAntiAffinityPreset`                       | Pod anti-affinity preset. Ignored if `blackboxExporter.affinity` is set. Allowed values: `soft` or `hard`         | `soft`                      |
| `blackboxExporter.nodeAffinityPreset.type`                     | Node affinity preset type. Ignored if `blackboxExporter.affinity` is set. Allowed values: `soft` or `hard`        | `""`                        |
| `blackboxExporter.nodeAffinityPreset.key`                      | Node label key to match. Ignored if `blackboxExporter.affinity` is set                                            | `""`                        |
| `blackboxExporter.nodeAffinityPreset.values`                   | Node label values to match. Ignored if `blackboxExporter.affinity` is set                                         | `[]`                        |
| `blackboxExporter.affinity`                                    | Affinity for Blackbox Exporter pods assignment                                                                    | `{}`                        |
| `blackboxExporter.nodeSelector`                                | Node labels for Blackbox Exporter pods assignment                                                                 | `{}`                        |
| `blackboxExporter.tolerations`                                 | Tolerations for Blackbox Exporter pods assignment                                                                 | `[]`                        |
| `blackboxExporter.topologySpreadConstraints`                   | Topology Spread Constraints for pod assignment spread across your cluster among failure-domains                   | `[]`                        |
| `blackboxExporter.priorityClassName`                           | Blackbox Exporter pods' priorityClassName                                                                         | `""`                        |
| `blackboxExporter.schedulerName`                               | Kubernetes pod scheduler registry                                                                                 | `""`                        |
| `blackboxExporter.terminationGracePeriodSeconds`               | In seconds, time the given to the Blackbox Exporter pod needs to terminate gracefully                             | `""`                        |
| `blackboxExporter.updateStrategy.type`                         | Blackbox Exporter statefulset strategy type                                                                       | `RollingUpdate`             |
| `blackboxExporter.extraVolumes`                                | Optionally specify extra list of additional volumes for the Blackbox Exporter pod(s)                              | `[]`                        |
| `blackboxExporter.extraVolumeMounts`                           | Optionally specify extra list of additional volumeMounts for the Blackbox Exporter container(s)                   | `[]`                        |
| `blackboxExporter.sidecars`                                    | Add additional sidecar containers to the Blackbox Exporter pod(s)                                                 | `[]`                        |
| `blackboxExporter.initContainers`                              | Add additional init containers to the Blackbox Exporter pod(s)                                                    | `[]`                        |

### Blackbox Exporter Traffic Exposure Parameters

| Name                                                      | Description                                                                                                                     | Value         |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| `blackboxExporter.service.type`                           | Blackbox Exporter service type                                                                                                  | `ClusterIP`   |
| `blackboxExporter.service.ports.http`                     | Blackbox Exporter HTTP service port                                                                                             | `19115`       |
| `blackboxExporter.service.nodePorts.http`                 | Node port for HTTP                                                                                                              | `""`          |
| `blackboxExporter.service.sessionAffinity`                | Control where client requests go, to the same pod or round-robin                                                                | `None`        |
| `blackboxExporter.service.sessionAffinityConfig`          | Additional settings for the sessionAffinity                                                                                     | `{}`          |
| `blackboxExporter.service.clusterIP`                      | Blackbox Exporter service Cluster IP                                                                                            | `""`          |
| `blackboxExporter.service.loadBalancerIP`                 | Blackbox Exporter service Load Balancer IP                                                                                      | `""`          |
| `blackboxExporter.service.loadBalancerSourceRanges`       | Blackbox Exporter service Load Balancer sources                                                                                 | `[]`          |
| `blackboxExporter.service.externalTrafficPolicy`          | Blackbox Exporter service external traffic policy                                                                               | `Cluster`     |
| `blackboxExporter.service.annotations`                    | Additional custom annotations for Blackbox Exporter service                                                                     | `{}`          |
| `blackboxExporter.service.extraPorts`                     | Extra ports to expose in the Blackbox Exporter service                                                                          | `[]`          |
| `kubeApiServer.enabled`                                   | Create a ServiceMonitor to scrape kube-apiserver service                                                                        | `true`        |
| `kubeApiServer.serviceMonitor.interval`                   | Scrape interval. If not set, the Prometheus default scrape interval is used.                                                    | `""`          |
| `kubeApiServer.serviceMonitor.metricRelabelings`          | Metric relabeling                                                                                                               | `[]`          |
| `kubeApiServer.serviceMonitor.relabelings`                | Relabel configs                                                                                                                 | `[]`          |
| `kubeControllerManager.enabled`                           | Create a ServiceMonitor to scrape kube-controller-manager service                                                               | `true`        |
| `kubeControllerManager.endpoints`                         | If your kube controller manager is not deployed as a pod, specify IPs it can be found on                                        | `[]`          |
| `kubeControllerManager.namespace`                         | Namespace where kube-controller-manager service is deployed.                                                                    | `kube-system` |
| `kubeControllerManager.service.enabled`                   | Whether or not to create a Service object for kube-controller-manager                                                           | `true`        |
| `kubeControllerManager.service.ports.http`                | Listening port of the kube-controller-manager Service object                                                                    | `10252`       |
| `kubeControllerManager.service.targetPorts.http`          | Port to target on the kube-controller-manager Pods. This should be the port that kube-controller-manager is exposing metrics on | `10252`       |
| `kubeControllerManager.service.selector`                  | Optional PODs Label selector for the service                                                                                    | `{}`          |
| `kubeControllerManager.serviceMonitor.interval`           | Scrape interval (use by default, falling back to Prometheus' default)                                                           | `""`          |
| `kubeControllerManager.serviceMonitor.https`              | Enable scraping kube-controller-manager over https                                                                              | `false`       |
| `kubeControllerManager.serviceMonitor.insecureSkipVerify` | Skip TLS certificate validation when scraping                                                                                   | `""`          |
| `kubeControllerManager.serviceMonitor.serverName`         | Name of the server to use when validating TLS certificate                                                                       | `""`          |
| `kubeControllerManager.serviceMonitor.metricRelabelings`  | Metric relabeling                                                                                                               | `[]`          |
| `kubeControllerManager.serviceMonitor.relabelings`        | Relabel configs                                                                                                                 | `[]`          |
| `kubeScheduler.enabled`                                   | Create a ServiceMonitor to scrape kube-scheduler service                                                                        | `true`        |
| `kubeScheduler.endpoints`                                 | If your kube scheduler is not deployed as a pod, specify IPs it can be found on                                                 | `[]`          |
| `kubeScheduler.namespace`                                 | Namespace where kube-scheduler service is deployed.                                                                             | `kube-system` |
| `kubeScheduler.service.enabled`                           | Whether or not to create a Service object for kube-scheduler                                                                    | `true`        |
| `kubeScheduler.service.ports.http`                        | Listening port of the kube scheduler Service object                                                                             | `10251`       |
| `kubeScheduler.service.targetPorts.http`                  | Port to target on the kube scheduler Pods. This should be the port that kube scheduler is exposing metrics on                   | `10251`       |
| `kubeScheduler.service.selector`                          | Optional PODs Label selector for the service                                                                                    | `{}`          |
| `kubeScheduler.serviceMonitor.interval`                   | Scrape interval (use by default, falling back to Prometheus' default)                                                           | `""`          |
| `kubeScheduler.serviceMonitor.https`                      | Enable scraping kube-scheduler over https                                                                                       | `false`       |
| `kubeScheduler.serviceMonitor.insecureSkipVerify`         | Skip TLS certificate validation when scraping                                                                                   | `""`          |
| `kubeScheduler.serviceMonitor.serverName`                 | Name of the server to use when validating TLS certificate                                                                       | `""`          |
| `kubeScheduler.serviceMonitor.metricRelabelings`          | Metric relabeling                                                                                                               | `[]`          |
| `kubeScheduler.serviceMonitor.relabelings`                | Relabel configs                                                                                                                 | `[]`          |
| `kubeScheduler.serviceMonitor.labels`                     | Extra labels for the ServiceMonitor                                                                                             | `{}`          |
| `kubeScheduler.serviceMonitor.annotations`                | Extra annotations for the ServiceMonitor                                                                                        | `{}`          |
| `coreDns.enabled`                                         | Create a ServiceMonitor to scrape coredns service                                                                               | `true`        |
| `coreDns.namespace`                                       | Namespace where core dns service is deployed.                                                                                   | `kube-system` |
| `coreDns.service.enabled`                                 | Whether or not to create a Service object for coredns                                                                           | `true`        |
| `coreDns.service.ports.http`                              | Listening port of the coredns Service object                                                                                    | `9153`        |
| `coreDns.service.targetPorts.http`                        | Port to target on the coredns Pods. This should be the port that coredns is exposing metrics on                                 | `9153`        |
| `coreDns.service.selector`                                | Optional PODs Label selector for the service                                                                                    | `{}`          |
| `coreDns.serviceMonitor.interval`                         | Scrape interval. If not set, the Prometheus default scrape interval is used.                                                    | `""`          |
| `coreDns.serviceMonitor.metricRelabelings`                | Metric relabel configs to apply to samples before ingestion.                                                                    | `[]`          |
| `coreDns.serviceMonitor.relabelings`                      | Relabel configs to apply to samples before ingestion.                                                                           | `[]`          |
| `kubeProxy.enabled`                                       | Create a ServiceMonitor to scrape the kube-proxy Service                                                                        | `true`        |
| `kubeProxy.endpoints`                                     | If your kube-proxy is not deployed as a pod, specify IPs it can be found on                                                     | `[]`          |
| `kubeProxy.namespace`                                     | Namespace where kube-proxy service is deployed.                                                                                 | `kube-system` |
| `kubeProxy.service.enabled`                               | Whether or not to create a Service object for kube-proxy                                                                        | `true`        |
| `kubeProxy.service.ports.http`                            | Listening port of the kube-proxy Service object                                                                                 | `10249`       |
| `kubeProxy.service.targetPorts.http`                      | Port to target on the kube-proxy Pods. This should be the port that kube-proxy is exposing metrics on                           | `10249`       |
| `kubeProxy.service.selector`                              | Optional PODs Label selector for the service                                                                                    | `{}`          |
| `kubeProxy.serviceMonitor.https`                          | Enable scraping kube-proxy over https.                                                                                          | `false`       |
| `kubeProxy.serviceMonitor.interval`                       | Scrape interval (use by default, falling back to Prometheus' default)                                                           | `""`          |
| `kubeProxy.serviceMonitor.metricRelabelings`              | Metric relabeling                                                                                                               | `[]`          |
| `kubeProxy.serviceMonitor.relabelings`                    | Relabel configs                                                                                                                 | `[]`          |
| `kubeProxy.serviceMonitor.labels`                         | Extra labels for the ServiceMonitor                                                                                             | `{}`          |
| `kubeProxy.serviceMonitor.annotations`                    | Extra annotations for the ServiceMonitor                                                                                        | `{}`          |

### RBAC parameters

| Name              | Description                                                                                                                                                        | Value  |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------ |
| `rbac.create`     | Whether to create and use RBAC resources or not                                                                                                                    | `true` |
| `rbac.pspEnabled` | Whether to create a PodSecurityPolicy and bound it with RBAC. WARNING: PodSecurityPolicy is deprecated in Kubernetes v1.21 or later, unavailable in v1.25 or later | `true` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install my-release \
  --set operator.logLevel=debug \
  --set prometheus.replicaCount=5 \
    my-repo/kube-prometheus
```

The above command sets the Prometheus Operator `logLevel` to `debug`. Additionally it sets the `prometheus.replicaCount` to `5`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
helm install my-release -f values.yaml my-repo/kube-prometheus
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Configuration and installation details

### [Rolling vs Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

Bitnami will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.

### Additional scrape configurations

The following values have been deprecated. See [Upgrading](#upgrading) below.

```console
prometheus.additionalScrapeConfigsExternal.enabled
prometheus.additionalScrapeConfigsExternal.name
prometheus.additionalScrapeConfigsExternal.key
```

It is possible to inject externally managed scrape configurations via a Secret by setting `prometheus.additionalScrapeConfigs.enabled` to `true` and `prometheus.additionalScrapeConfigs.type` to `external`. The secret must exist in the same namespace as the chart deployment. Set the secret name using the parameter `prometheus.additionalScrapeConfigs.external.name`, and the key containing the additional scrape configuration using the `prometheus.additionalScrapeConfigs.external.key`.

It is also possible to define scrape configuratios to be managed by the Helm chart by setting `prometheus.additionalScrapeConfigs.enabled` to `true` and `prometheus.additionalScrapeConfigs.type` to `internal`. You can then use `prometheus.additionalScrapeConfigs.internal.jobList` to define a list of additional scrape jobs for Prometheus.

Refer to the [chart documentation on customizing scrape configurations](https://docs.bitnami.com/kubernetes/apps/prometheus-operator/configuration/customize-scrape-configurations) for an example.

### Additional alert relabel configurations

It is possible to inject externally managed Prometheus alert relabel configurations via a Secret by setting `prometheus.additionalAlertRelabelConfigsExternal.enabled` to `true`. The secret must exist in the same namespace as the chart deployment. Set the secret name using the parameter `prometheus.additionalAlertRelabelConfigsExternal.name`, and the key containing the additional alert relabel configuration using the `prometheus.additionalAlertRelabelConfigsExternal.key`.

Refer to the [chart documentation on customizing alert configurations](https://docs.bitnami.com/kubernetes/apps/prometheus-operator/configuration/customize-alert-configurations) for an example.

### Set Pod affinity

This chart allows setting custom Pod affinity using the `XXX.affinity` parameter(s). Find more information about Pod's affinity in the [Kubernetes documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity).

As an alternative, use one of the preset configurations for pod affinity, pod anti-affinity, and node affinity available at the [bitnami/common](https://github.com/bitnami/charts/tree/main/bitnami/common#affinities) chart. To do so, set the `XXX.podAffinityPreset`, `XXX.podAntiAffinityPreset`, or `XXX.nodeAffinityPreset` parameters.

## Troubleshooting

Find more information about how to deal with common errors related to Bitnami's Helm charts in [this troubleshooting guide](https://docs.bitnami.com/general/how-to/troubleshoot-helm-chart-issues).

## Upgrading

```console
helm upgrade my-release my-repo/kube-prometheus
```

### To 8.0.0

This major updates the kube-state-metrics subchart to its newest major, 3.0.0, and the node-exporter subchart to its newest major, 3.0.0. Both releases contains name changes to a few of its values. For more information, please refer to [kube-state-metrics upgrade notes](https://github.com/bitnami/charts/tree/main/bitnami/kube-state-metrics#to-300) and [node-exporter upgrade notes](https://github.com/bitnami/charts/tree/main/bitnami/node-exporter#to-300).

### To 7.0.0

This major release renames several values in this chart and adds missing features, in order to be aligned with the rest of the assets in the Bitnami charts repository.

Affected values:

- `global.labels` has been removed. Please use `commonLabels` instead.
- `prometheus.thanos.ingress` has been refactored.
- Changes to service ports:
  - `operator.service.port` was renamed as `operator.service.ports.http`.
  - `operator.service.nodePort` was renamed as `operator.service.nodePorts.http`.
  - `prometheus.service.port` was renamed as `prometheus.service.ports.http`.
  - `prometheus.service.nodePort` was renamed as `prometheus.service.nodePorts.http`.
  - `alertmanager.service.port` was renamed as `alertmanager.service.ports.http`.
  - `alertmanager.service.nodePort` was renamed as `alertmanager.service.nodePorts.http`.
  - `kubeControllerManager.service.port` was renamed as `kubeControllerManager.service.ports.http`.
  - `kubeControllerManager.service.targetPort` was renamed as `kubeControllerManager.service.targetPorts.http`.
  - `kubeScheduler.service.port` was renamed as `kubeScheduler.service.ports.http`.
  - `kubeScheduler.service.targetPort` was renamed as `kubeScheduler.service.targetPorts.http`.
  - `coreDns.service.port` was renamed as `coreDns.service.ports.http`.
  - `coreDns.service.targetPort` was renamed as `coreDns.service.targetPorts.http`.
  - `kubeProxy.service.port` was renamed as `kubeProxy.service.ports.http`.
  - `kubeProxy.service.targetPort` was renamed as `kubeProxy.service.targetPorts.http`.
  - `prometheus.thanos.service.port` was renamed as `prometheus.thanos.service.ports.grpc`.
  - `prometheus.thanos.service.nodePort` was renamed as `prometheus.thanos.service.nodePorts.grpc`.
- `alertmanager.service.stickySessions` has been replaced with the parameter `alertmanager.service.sessionAffinity`.
- `prometheus.service.stickySessions` has been replaced with the parameter `prometheus.service.sessionAffinity`.
- `operator.livenessProbe.path` have been removed, and livenessProbe is now interpreted as a template. To customize the probe, use customLivenessProbe.
- `operator.readinessProbe.path` have been removed, and readinessProbe is now interpreted as a template. To customize the probe, use customReadinessProbe.
- `prometheus.podDisruptionBudget.*` was renamed as `prometheus.pdb.*`.
- `prometheus.podDisruptionBudget.enabled` was renamed as `prometheus.pdb.create`.
- `alertmanager.podDisruptionBudget.*` was renamed as `alertmanager.pdb.*`.
- `alertmanager.podDisruptionBudget.enabled` was renamed as `alertmanager.pdb.create`.
- Unused value `prometheus.matchLabels` has been removed.
- Unused value `rbac.apiVersion` has been removed

### To 6.0.0

This major update changes the `securityContext` interface in the `values.yaml` file.

Please note if you have changes in the `securityContext` fields those need to be migrated to `podSecurityContext`.

```diff
# ...
- securityContext:
+ podSecurityContext:
# ...
```

Other than that a new `securityContext` interface for containers got introduced `containerSecurityContext`. It's default is enabled so if you do not need it you need to opt out of it.

If you use [Strategic Merge Patch](https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/user-guides/strategic-merge-patch.md) for any of the
`Alertmanager` or `Prometheus` kinds you need to actively disable all of those things below. For the resource you want to use Strategic Merge Patch for.

```yaml
<resource>:
  containerSecurityContext:
    enabled: false
  livenessProbe:
    enabled: false
  readinessProbe:
    enabled: false
```

### To 5.0.0

This major updates the kube-state-metrics subchart to it newest major, 2.0.0, which contains name changes to a few of its values. For more information on this subchart's major, please refer to [kube-state-metrics upgrade notes](https://github.com/bitnami/charts/tree/main/bitnami/kube-state-metrics#to-200).

### To 4.4.0

This version replaced the old `configReloaderCpu` and `configReloaderMemory` variables in favor of the new `configReloaderResources` map to define the requests and limits for the config-reloader sidecards. Users who made use of the old variables will need to migrate to the new ones.

### To 4.0.0

This version standardizes the way of defining Ingress rules.
When configuring a single hostname for the Prometheus Ingress rule, set the `prometheus.ingress.hostname` value. When defining more than one, set the `prometheus.ingress.extraHosts` array.
When configuring a single hostname for the Alertmanager Ingress rule, set the `alertmanager.ingress.hostname` value. When defining more than one, set the `alertmanager.ingress.extraHosts` array.

Apart from this case, no issues are expected to appear when upgrading.

### To 3.4.0

Some parameters disappeared in favor of new ones:

- `prometheus.additionalScrapeConfigsExternal.enabled` -> deprecated in favor of `prometheus.additionalScrapeConfigs.enabled` and `prometheus.additionalScrapeConfigs.type`.
- `prometheus.additionalScrapeConfigsExternal.name` -> deprecated in favor of `prometheus.additionalScrapeConfigs.external.name`.
- `prometheus.additionalScrapeConfigsExternal.key` -> deprecated in favor of `prometheus.additionalScrapeConfigs.external.key`.

Adapt you parameters accordingly if you are external scrape configs.

### To 3.1.0

Some parameters disappeared in favor of new ones:

- `*.podAffinity` -> deprecated in favor of `*.podAffinityPreset`.
- `*.podAntiAffinity` -> deprecated in favor of `*.podAntiAffinityPreset`.
- `*.nodeAffinity` -> deprecated in favor of `*.nodeAffinityPreset.type`, `*.nodeAffinityPreset.key` and `*.nodeAffinityPreset.values`.

Adapt parameters accordingly if you are setting custom affinity.

### To 3.0.0

[On November 13, 2020, Helm v2 support formally ended](https://github.com/helm/charts#status-of-the-project). This major version is the result of the required changes applied to the Helm Chart to be able to incorporate the different features added in Helm v3 and to be consistent with the Helm project itself regarding the Helm v2 EOL.

[Learn more about this change and related upgrade considerations](https://docs.bitnami.com/kubernetes/apps/prometheus-operator/administration/upgrade-helm3/).

### To 2.1.0

> Note: ignore these instructions if you did not enabled the Thanos sidecar on Prometheus pods.

The Thanos sidecar svc is transformed into a headless service by default so Thanos can discover every available sidecar. You can undo this change by setting the `prometheus.thanos.service.clusterIP` parameter to an empty string `""`.

To upgrade from version 2.0.0, previously remove the Thanos sidecar svc to avoid issues with immutable fields:

```console
kubectl delete svc my-relase-kube-prometheus-prometheus-thanos
helm upgrade my-release --set prometheus.thanos.create=true my-repo/kube-prometheus
```

### To 2.0.0

- CRDs were updated to the latest prometheus-operator v0.4.1 release artifacts
  - The apiVersion of CRDs was updated from `apiextensions.k8s.io/v1beta1` to `apiextensions.k8s.io/v1`
  - Kubernetes 1.16 is required

### To 1.0.0

- The chart was renamed to `kube-prometheus` to be more accurate with the actual capabilities of the chart: it does not just deploy the Prometheus operator, it deploys an entire cluster monitoring stack, that includes other components (e.g. NodeExporter or Kube State metrics). Find more information about the reasons behind this decision at [#3490](https://github.com/bitnami/charts/issues/3490).
- New CRDs were added and some existing ones were updated.
- This version also introduces `bitnami/common`, a [library chart](https://helm.sh/docs/topics/library_charts/#helm) as a dependency. More documentation about this new utility could be found [here](https://github.com/bitnami/charts/tree/main/bitnami/common#bitnami-common-library-chart). Please, make sure that you have updated the chart dependencies before executing any upgrade.

> Note: There is no backwards compatibility due to the above mentioned changes. It's necessary to install a new release of the chart, and migrate the existing TSDB data to the new Prometheus instances.

## License

Copyright &copy; 2023 Bitnami

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

<http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
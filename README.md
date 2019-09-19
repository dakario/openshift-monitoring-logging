# Malaw - Monitoring
* * *
This document shows the list of required metrics and alerts.

This document also details the different types of Prometheus integration according to SONATEL monitoring stack.

* Grafana to OpenShift Prometheus
* Prometheus to OpenShift Prometheus
* Centreon to OpenShift Prometheus

## Overview

OpenShift Container Platform ships with a pre-configured and self-updating monitoring stack that is based on the Prometheus open source project and its wider eco-system. It provides monitoring of cluster components and ships with a set of alerts to immediately notify the cluster administrator about any occurring problems and a set of Grafana dashboards.

At the heart of the monitoring stack sits the OpenShift Container Platform Cluster Monitoring Operator (CMO), which watches over the deployed monitoring components and resources, and ensures that they are always up to date.

The Prometheus Operator (PO) creates, configures, and manages Prometheus and Alertmanager instances. It also automatically generates monitoring target configurations based on familiar Kubernetes label queries.

In addition to Prometheus and Alertmanager, OpenShift Container Platform Monitoring also includes node-exporter and kube-state-metrics. Node-exporter is an agent deployed on every node to collect metrics about it. The kube-state-metrics exporter agent converts Kubernetes objects to metrics consumable by Prometheus.

The targets monitored as part of the cluster monitoring are:

* Prometheus itself

* Prometheus-Operator

* cluster-monitoring-operator

* Alertmanager cluster instances

* Kubernetes apiserver

* kubelets (the kubelet embeds cAdvisor for per container metrics)

* kube-controllers

* kube-state-metrics

* node-exporter

* **etcd (if etcd monitoring is enabled)**


## Metrics

### Cluster Usage

* KubeCPUOvercommit
* KubeCPUOvercommit
* KubeMemOvercommit
* KubeMemOvercommit
* KubeQuotaExceeded

### Clients
* KubeClientCertificateExpiration
* KubeClientCertificateExpiration
* KubeClientErrors
* KubeClientErrors

### Master

* KubeAPIDown
* KubeAPIErrorsHigh
* KubeAPIErrorsHigh
* KubeAPILatencyHigh
* KubeAPILatencyHigh
* KubeControllerManagerDown
* KubeSchedulerDown

### Kube core components

* KubeCronJobRunning
* KubeDaemonSetMisScheduled
* KubeDaemonSetNotScheduled
* KubeDaemonSetRolloutStuck
* KubeDeploymentGenerationMismatch
* KubeDeploymentReplicasMismatch
* KubeJobCompletion
* KubeJobFailed
* KubePersistentVolumeFullInFourDays
* KubePersistentVolumeUsageCritical
* KubePodCrashLooping
* KubePodNotReady
* KubeStatefulSetGenerationMismatch
* KubeStatefulSetReplicasMismatch


### Machines

* KubeletDown
* KubeletTooManyPods
* NodeDiskRunningFull
* NodeExporterDown
* KubeNodeNotReady

### Etcd

* etcd_server_has_leader
* etcd_server_leader_changes_seen_total
* etcd_server_proposals_applied_total
* etcd_server_proposals_committed_total
* etcd_server_proposals_pending
* etcd_server_proposals_failed_total
* etcd_debugging_mvcc_db_total_size_in_bytes
* etcd_disk_backend_commit_duration_seconds
* etcd_disk_wal_fsync_duration_seconds
* etcd_network_client_grpc_received_bytes_total
* etcd_network_client_grpc_sent_bytes_total

### Prometheus, Alertmanager, Operator  and Cluster Operator

* PrometheusConfigReloadFailed
* PrometheusDown
* PrometheusErrorSendingAlerts
* PrometheusErrorSendingAlerts
* PrometheusNotConnectedToAlertmanagers
* PrometheusNotIngestingSamples
* PrometheusNotificationQueueRunningFull
* PrometheusOperatorDown
* PrometheusTSDBCompactionsFailing
* PrometheusTSDBReloadsFailing
* PrometheusTSDBWALCorruptions
* PrometheusTargetScrapesDuplicate
* AlertmanagerConfigInconsistent
* AlertmanagerDown
* AlertmanagerDownOrMissing
* AlertmanagerFailedReload
* ClusterMonitoringOperatorDown
* ClusterMonitoringOperatorErrors
* TargetDown
* KubeStateMetricsDown


## Alerts

| Alert                                  | Severity | Description                                                                                                                                                                         |
|----------------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ClusterMonitoringOperatorErrors        | critical | Cluster Monitoring Operator is experiencing X% errors\.                                                                                                                             |
| AlertmanagerDown                       | critical | Alertmanager has disappeared from Prometheus target discovery\.                                                                                                                     |
| ClusterMonitoringOperatorDown          | critical | ClusterMonitoringOperator has disappeared from Prometheus target discovery\.                                                                                                        |
| KubeAPIDown                            | critical | KubeAPI has disappeared from Prometheus target discovery\.                                                                                                                          |
| KubeControllerManagerDown              | critical | KubeControllerManager has disappeared from Prometheus target discovery\.                                                                                                            |
| KubeSchedulerDown                      | critical | KubeScheduler has disappeared from Prometheus target discovery\.                                                                                                                    |
| KubeStateMetricsDown                   | critical | KubeStateMetrics has disappeared from Prometheus target discovery\.                                                                                                                 |
| KubeletDown                            | critical | Kubelet has disappeared from Prometheus target discovery\.                                                                                                                          |
| NodeExporterDown                       | critical | NodeExporter has disappeared from Prometheus target discovery\.                                                                                                                     |
| PrometheusDown                         | critical | Prometheus has disappeared from Prometheus target discovery\.                                                                                                                       |
| PrometheusOperatorDown                 | critical | PrometheusOperator has disappeared from Prometheus target discovery\.                                                                                                               |
| KubePodCrashLooping                    | critical | Namespace/Pod \(Container\) is restarting times / second                                                                                                                            |
| KubePodNotReady                        | critical | Namespace/Pod is not ready\.                                                                                                                                                        |
| KubeDeploymentGenerationMismatch       | critical | Deployment Namespace/Deploymentgeneration mismatch                                                                                                                                  |
| KubeDeploymentReplicasMismatch         | critical | Deployment Namespace/Deploymentreplica mismatch                                                                                                                                     |
| KubeStatefulSetReplicasMismatch        | critical | StatefulSet Namespace/StatefulSetreplica mismatch                                                                                                                                   |
| KubeStatefulSetGenerationMismatch      | critical | StatefulSet Namespace/StatefulSetgeneration mismatch                                                                                                                                |
| KubeDaemonSetRolloutStuck              | critical | Only X% of desired pods scheduled and ready for daemon set Namespace/DaemonSet                                                                                                      |
| KubeDaemonSetNotScheduled              | warning  | A number of pods of daemonset Namespace/DaemonSet are not scheduled\.                                                                                                               |
| KubeDaemonSetMisScheduled              | warning  | A number of pods of daemonset Namespace/DaemonSet are running where they are not supposed to run\.                                                                                  |
| KubeCronJobRunning                     | warning  | CronJob Namespace/CronJob is taking more than 1h to complete\.                                                                                                                      |
| KubeJobCompletion                      | warning  | Job Namespaces/Job is taking more than 1h to complete\.                                                                                                                             |
| KubeJobFailed                          | warning  | Job Namespaces/Job failed to complete\.                                                                                                                                             |
| KubeCPUOvercommit                      | warning  | Overcommited CPU resource requests on Pods, cannot tolerate node failure\.                                                                                                          |
| KubeMemOvercommit                      | warning  | Overcommited Memory resource requests on Pods, cannot tolerate node failure\.                                                                                                       |
| KubeCPUOvercommit                      | warning  | Overcommited CPU resource request quota on Namespaces\.                                                                                                                             |
| KubeMemOvercommit                      | warning  | Overcommited Memory resource request quota on Namespaces\.                                                                                                                          |
| alerKubeQuotaExceeded                  | warning  | X% usage of Resource in namespace Namespace\.                                                                                                                                       |
| KubePersistentVolumeUsageCritical      | critical | The persistent volume claimed by PersistentVolumeClaim in namespace Namespace has X% free\.                                                                                         |
| KubePersistentVolumeFullInFourDays     | critical | Based on recent sampling, the persistent volume claimed by PersistentVolumeClaim in namespace Namespace is expected to fill up within four days\. Currently X bytes are available\. |
| KubeNodeNotReady                       | warning  | Node has been unready for more than an hour                                                                                                                                         |
| KubeVersionMismatch                    | warning  | There are X different versions of Kubernetes components running\.                                                                                                                   |
| KubeClientErrors                       | warning  | Kubernetes API server client 'Job/Instance' is experiencing X% errors\.'                                                                                                            |
| KubeClientErrors                       | warning  | Kubernetes API server client 'Job/Instance' is experiencing X errors / sec\.'                                                                                                       |
| KubeletTooManyPods                     | warning  | Kubelet Instance is running X pods, close to the limit of 110\.                                                                                                                     |
| KubeAPILatencyHigh                     | warning  | The API server has a 99th percentile latency of X seconds for Verb Resource\.                                                                                                       |
| KubeAPILatencyHigh                     | critical | The API server has a 99th percentile latency of X seconds for Verb Resource\.                                                                                                       |
| KubeAPIErrorsHigh                      | critical | API server is erroring for X% of requests\.                                                                                                                                         |
| KubeAPIErrorsHigh                      | warning  | API server is erroring for X% of requests\.                                                                                                                                         |
| KubeClientCertificateExpiration        | warning  | Kubernetes API certificate is expiring in less than 7 days\.                                                                                                                        |
| KubeClientCertificateExpiration        | critical | Kubernetes API certificate is expiring in less than 1 day\.                                                                                                                         |
| AlertmanagerConfigInconsistent         | critical | Summary: Configuration out of sync\. Description: The configuration of the instances of the Alertmanager cluster Service are out of sync\.                                          |
| AlertmanagerFailedReload               | warning  | Summary: Alertmanager’s configuration reload failed\. Description: Reloading Alertmanager’s configuration has failed for Namespace/Pod\.                                            |
| TargetDown                             | warning  | Summary: Targets are down\. Description: X% of Job targets are down\.                                                                                                               |
| DeadMansSwitch                         | none     | Summary: Alerting DeadMansSwitch\. Description: This is a DeadMansSwitch meant to ensure that the entire Alerting pipeline is functional\.                                          |
| NodeDiskRunningFull                    | warning  | Device Device of node\-exporter Namespace/Pod is running full within the next 24 hours\.                                                                                            |
| NodeDiskRunningFull                    | critical | Device Device of node\-exporter Namespace/Pod is running full within the next 2 hours\.                                                                                             |
| PrometheusConfigReloadFailed           | warning  | Summary: Reloading Prometheus' configuration failed\. Description: Reloading Prometheus' configuration has failed for Namespace/Pod                                                 |
| PrometheusNotificationQueueRunningFull | warning  | Summary: Prometheus' alert notification queue is running full\. Description: Prometheus' alert notification queue is running full for Namespace/Pod                                 |
| PrometheusErrorSendingAlerts           | warning  | Summary: Errors while sending alert from Prometheus\. Description: Errors while sending alerts from Prometheus Namespace/Pod to Alertmanager Alertmanager                           |
| PrometheusErrorSendingAlerts           | critical | Summary: Errors while sending alerts from Prometheus\. Description: Errors while sending alerts from Prometheus Namespace/Pod to Alertmanager Alertmanager                          |
| PrometheusNotConnectedToAlertmanagers  | warning  | Summary: Prometheus is not connected to any Alertmanagers\. Description: Prometheus Namespace/Pod is not connected to any Alertmanagers                                             |
| PrometheusTSDBReloadsFailing           | warning  | Summary: Prometheus has issues reloading data blocks from disk\. Description: Job at Instance had X reload failures over the last four hours\.                                      |
| PrometheusTSDBCompactionsFailing       | warning  | Summary: Prometheus has issues compacting sample blocks\. Description: Job at Instance had X compaction failures over the last four hours\.                                         |
| PrometheusTSDBWALCorruptions           | warning  | Summary: Prometheus write\-ahead log is corrupted\. Description: Job at Instancehas a corrupted write\-ahead log \(WAL\)\.                                                          |
| PrometheusNotIngestingSamples          | warning  | Summary: Prometheus isn’t ingesting samples\. Description: Prometheus Namespace/Pod isn’t ingesting samples\.                                                                       |
| PrometheusTargetScrapesDuplicate       | warning  | Summary: Prometheus has many samples rejected\. Description: Namespace/Pod has many samples rejected due to duplicate timestamps but different values                               |
| EtcdInsufficientMembers                | critical | Etcd cluster "Job": insufficient members \(X\)\.                                                                                                                                    |
| EtcdNoLeader                           | critical | Etcd cluster "Job": member Instance has no leader\.                                                                                                                                 |
| EtcdHighNumberOfLeaderChanges          | warning  | Etcd cluster "Job": instance Instance has seen X leader changes within the last hour\.                                                                                              |
| EtcdHighNumberOfFailedGRPCRequests     | warning  | Etcd cluster "Job": X% of requests for GRPC\_Method failed on etcd instance Instance\.                                                                                              |
| EtcdHighNumberOfFailedGRPCRequests     | critical | Etcd cluster "Job": X% of requests for GRPC\_Method failed on etcd instance Instance\.                                                                                              |
| EtcdGRPCRequestsSlow                   | critical | Etcd cluster "Job": gRPC requests to GRPC\_Method are taking X\_s on etcd instance \_Instance\.                                                                                     |
| EtcdMemberCommunicationSlow            | warning  | Etcd cluster "Job": member communication with To is taking X\_s on etcd instance \_Instance\.                                                                                       |
| EtcdHighNumberOfFailedProposals        | warning  | Etcd cluster "Job": X proposal failures within the last hour on etcd instance Instance\.                                                                                            |
| EtcdHighFsyncDurations                 | warning  | Etcd cluster "Job": 99th percentile fync durations are X\_s on etcd instance \_Instance\.                                                                                           |
| EtcdHighCommitDurations                | warning  | Etcd cluster "Job": 99th percentile commit durations X\_s on etcd instance \_Instance\.                                                                                             |
| FdExhaustionClose                      | warning  | Job instance Instance will exhaust its file descriptors soon                                                                                                                        |
| FdExhaustionClose                      | critical | Job instance Instance will exhaust its file descriptors soon                                                                                                                        |



## Prometheus integration

A reverse proxy is used to perform authentication with OpenShift via OAuth and Kubernetes service accounts. But other standard tools e.g. Grafana and Pormetheus Federation - don't support this proxy authentication yet.

The following workaround is needed to make it work.

1. Generate a new user with htpasswd:

```
 htpasswd -s -c <file> <username>
```

2. Encode into base64

```
echo -n "new user created" | base64
```

3. Edit the secret by specifying the base64 encoded message

```
oc -n openshift-monitoring edit secret prometheus-k8s-htpasswd
```

4. Make sure that prometheus PODs use the new secret
5. Now you can login from your new Grafana to the default OpenShift Prometheus


### Grafana with username and password created with htpasswd

After creating a local user with htpasswd as shown above, now your new Grafana can fetch metrics from OpenShift prometheus.

* Create new Data source
* Choose Server Access Type
* Enable Basic Auth
* Specify username and password created with htpasswd
* Don't forget to skip TLS verify if certificates are not valid.
* Enjoy :)

### Grafana with username and password created with default credentials

#### Retrieve the POD ID

```
$ oc get po -n openshift-monitoring | grep grafana-
grafana-6bb5686b49-6hcjc                       2/2       Running   0          2d
```

#### Connect to the grafana POD

```
$ oc exec -it <POD ID> -n openshift-monitoring bash
```

#### Read credentials in /etc/grafana/provisioning/datasources/prometheus.yaml file

```
$ cat /etc/grafana/provisioning/datasources/prometheus.yaml

{
    "apiVersion": 1,
    "datasources": [
        {
            "access": "proxy",
            "basicAuth": true,
            "basicAuthPassword": "8XM3JFOK5ZEiXiyXfxw83ynj+iZ5+uDOPf7fE9NnBDnwkgtqu+6EOdddlxLLGx0LLIwxZdtUFtNBGXsssdZ+XdwzNvHyaWANayw8dfwwUc2lbSDUwFooaAnphiwQiJ1AdCE86qxOAMhnERzg4OqpQRGJQiCRm5BdQaHPFUaxRcJyW4A+XYNuddyQVEZM5LGZIxIyAjZ/rL0SFJCuRRwX7",
            "basicAuthUser": "internal",
            "editable": false,
            "jsonData": {
                "tlsSkipVerify": true
            },
            "name": "prometheus",
            "orgId": 1,
            "type": "prometheus",
            "url": "https://prometheus-k8s.openshift-monitoring.svc:9091",
            "version": 1
        }
    ]
```

* Create new Data source
* Choose Server Access Type
* Enable Basic Auth
* Specify username and password created with credentials (basicAuthUser and basicAuthPassword) within /etc/grafana/provisioning/datasources/prometheus.yaml file
* Don't forget to skip TLS verify if certificates are not valid.
* Enjoy :)

### Pull new metrics

As the Prometheus Operator was used to deploy Prometehus-Alermanager Stack,  we have to rely on ServiceMonitor CRD to new metrics target. See how to create a [ServiceMonitor](https://github.com/coreos/prometheus-operator/blob/master/Documentation/api.md#servicemonitorspec) 

### Exemple of routes and receivers implementation

#### 1. Download the existing Alermanger config file

```
kubectl -n openshift-monitoring get secret alertmanager-main -ojson | jq -r '.data["alertmanager.yaml"]' | base64 --decode > alertmanagerOLD.yaml
cp alertmanagerOLD.yaml alertmanager.yaml
```

The default file looks like this:

```
$ cat alertmanager.yaml

global:
  resolve_timeout: 5m
route:
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 12h
  receiver: default
  routes:
  - match:
      alertname: DeadMansSwitch
    repeat_interval: 5m
    receiver: deadmansswitch
receivers:
- name: default
- name: deadmansswitch
```

#### 2. Edit the Alermanger config file

##### A a new smtp receiver

```
receivers:
- name: beopenitmailadmin
  email_configs:
  - to: 'admin@beopenit.com'
    from: 'fake@gmail.com'
    smarthost: 'smtp.gmail.com:587'
    auth_username: 'fakeuser'
    auth_password: 'fakepassword'
- name: beopenitmailappli
  email_configs:
  - to: 'dev@beopenit.com'
    from: 'fake@gmail.com'
    smarthost: 'smtp.gmail.com:587'
    auth_username: 'fakeuser'
    auth_password: 'fakepassword'
```

##### Dispatch alerts

```
  routes:
  - match:
      alertname: EtcdInsufficientMembers
    repeat_interval: 5m
    receiver: beopenitmailadmin
  - match:
      alertname: KubePodCrashLooping
    repeat_interval: 5m
    receiver: beopenitmailadmin
```

#### 3. Update Alermanger config

```
kubectl -n openshift-monitoring create secret generic alertmanager-main --from-literal=alertmanager.yaml="$(< alertmanager.yaml)" --dry-run -oyaml | kubectl -n openshift-monitoring replace secret --filename=-
```


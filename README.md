This repository contains the files to deploy Hosted Cluster in Openshift Hosted Control Plane setup
## 📂 Project Structure
```bash
.
├── argo
│   ├── argoapp.yaml
│   ├── management-gitops-hypershift-rhacm_rolebinding.yaml
│   └── management-gitops-hypershift-rhacm.yaml
├── helmguest
│   └── my-guest-cluster-chart
│       ├── Chart.yaml
│       ├── templates
│       │   ├── clusters.yaml
│       │   ├── hosted-cluster.yaml
│       │   ├── node-pool.yaml
│       │   ├── pullsecret.yaml
│       │   └── sshkey.yaml
│       └── values.yaml
└── README.md
```
### values.yaml
```bash
dockerconfigjson: # Add your base64 encoded pull secret
idRsaPub: # Add your ssh public key
availabilityPolicy: # Change this to 'SingleReplica' for SNO and 'HighlyAvailable' for cluster
guestStorageClassName: # Hosted Cluster storage class name 
infraStorageClassName: # Management Cluster storage class name (support RWX)
guestVolumeSnapshotClassName: # Hosted Cluster storage snapshot class name
infraVolumeSnapshotClassName: # Management Cluster storage snapshot class name
```
### hosted-cluster.yaml
Uncomment following section when ACM is installed in Management Cluster
```bash
#---
#apiVersion: agent.open-cluster-management.io/v1
#kind: KlusterletAddonConfig
#metadata:
#  name: {{ .Values.guestClustername }}
#  namespace: {{ .Values.guestClustername }}
#spec:
#  applicationManager:
#    enabled: true
#  certPolicyController:
#    enabled: true
#  clusterLabels:
#    cloud: BareMetal
#    vendor: OpenShift
#  clusterName: {{ .Values.guestClustername }}
#  clusterNamespace: {{ .Values.guestClustername }}
#  policyController:
#    enabled: true
#  searchCollector:
#    enabled: true

```

# CKA Bookmarks
## Kubernetes Documentation
[k8s Main Documentation](https://kubernetes.io/docs/home/)\
[kubeadm Upgrade](https://v1-25.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)\
## Kubernetes Networking
[k8s Networking Service v1.25](https://v1-25.docs.kubernetes.io/docs/concepts/services-networking/service/)\
[k8s Networking Service](https://kubernetes.io/docs/concepts/services-networking/service/)\
## Kubernetes Configs
[k8s Persistent Volumes PVs](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)\
[k8s Config Maps](https://kubernetes.io/docs/concepts/configuration/configmap/)\
[k8s Config Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)\
## Kubernetes Controller Management
[k8s Controller Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)\
[k8s Controller Replica Set](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)\
[k8s Controller Stateful Sets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)\
[k8s Controller Daemon Sets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)\
[k8s Controllers Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/)\
## Kubernetes Cluster
[k8s Cluster Configure etcd](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)\
[k8s Authz Cert Signing Requests](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#create-certificatesigningrequest)\
https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-example - create role
https://kubernetes.io/docs/reference/access-authn-authz/rbac/#kubectl-create-rolebinding - create rolebinding
https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-pod
## Kubernetes Config Examples
https://kubernetes.io/docs/concepts/storage/volumes/#hostpath-configuration-example - Create pod with volume
https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolume - create PV with hostPath
https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolumeclaim
https://kubernetes.io/docs/concepts/storage/persistent-volumes/#claims-as-volumes - Pod with PVC
https://kubernetes.io/docs/concepts/storage/storage-classes/#local - StorageClass Local
https://github.com/kodekloudhub/certified-kubernetes-administrator-course - CKA github


# CKA Aliases
```
alias ll='ls -l'
alias kcr='kubectl create'
alias ka='kubectl apply -f'
alias k=kubectl
alias kg='kubectl get'
alias ke='kubectl edit'
alias kd='kubectl describe'
alias kdd='kubectl delete'
alias kgp='kubectl get pods'
alias kgd='kubectl get deployments'
alias kgpvc='kubectl get pvc'
alias kgpv='kubectl get pv'
export alias fg='--force --grace-period=0'
export alias do='--dry-run=client -o yaml'
export alias oy='-o yaml'
echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -o default -F __start_kubectl k' >>~/.bashrc
```

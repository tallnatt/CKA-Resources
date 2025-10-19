# CKA Bookmarks
## Kubernetes Documentation
[k8s Main Documentation](https://kubernetes.io/docs/home/)\
[kubeadm Upgrade](https://v1-25.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)
## Kubernetes Networking
[k8s Networking Service v1.25](https://v1-25.docs.kubernetes.io/docs/concepts/services-networking/service/)\
[k8s Networking Service](https://kubernetes.io/docs/concepts/services-networking/service/)
## Kubernetes Configs
[k8s Persistent Volumes PVs](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)\
[k8s Config Maps](https://kubernetes.io/docs/concepts/configuration/configmap/)\
[k8s Config Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)
## Kubernetes Controller Management
[k8s Controller Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)\
[k8s Controller Replica Set](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)\
[k8s Controller Stateful Sets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)\
[k8s Controller Daemon Sets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)\
[k8s Controllers Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/)
## Kubernetes Cluster
[k8s Cluster Configure etcd](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)\
[k8s Authz Cert Signing Requests](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#create-certificatesigningrequest)\
[k8s Authz Create Role Binding](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#kubectl-create-rolebinding)\
[k8s Authz Set Security Context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-pod)
## Kubernetes Config Examples
[k8s Create Pod with Volume](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath-configuration-example)\
[k8s Create a Persistant Volume with Host Path](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolume)\
[k8s Create Persistent Volume Claim](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolumeclaim)\
[k8s Create Pod with Persistent Volume Claim (PVC)](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#claims-as-volumes)\
[k8s Create Local Storage Class](https://kubernetes.io/docs/concepts/storage/storage-classes/#local)\
[k8s Authz Role Creation](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-example)\


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
alias fg='--force --grace-period=0'
alias do='--dry-run=client -o yaml'
alias oy='-o yaml'
echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -o default -F __start_kubectl k' >>~/.bashrc
```

# Command Examples
## POD Management
```
kubectl replace --force -f /tmp/kubectl-31523123.yaml ## Apply yaml config to a pod if values are not changed directly
kubectl run test --image=nginx
kubectl run redis --image=redis -n finance
kubectl run redis --image=redis:alpine -l='tier=db' ## Run a pod with a label
kubectl run custom-nginx --image=nginx --port=8080 ## Run a pod named nginx with port 8080
kubectl explain replicaset | grep VERSION
kubectl scale rs new-replica-set --replicas=5
kubectl scale --replicas -f replicaset-definition.yml
kubectl run webapp-color --image=kodekloud/webapp-color -l=name=webapp-color --env="APP_COLOR=green" ## Run a pod with label webapp-color and with env APP_COLOR=green
kubectl run pvviewer --image=redis --serviceaccount=pvviewer
kubectl get pods -A --sort-by='metadata.uid' > /root/pods.txt
kubectl get pods -A --sort-by='metadata.creationTimestamp' > /root/creation.txt
```

## Yaml File Generation
```
kubectl run nginx --image=nginx --dry-run=client -o yaml
kubectl create deployment nginx --image=nginx
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml
kubectl create deployment nginx --image=nginx --dry-run=test -o yaml > test-deploy.yaml ## Save deployment config to yaml file
kubectl create deployment nginx --image=nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml
kubectl run webapp-green --image=kodekloud/webapp-color --dry-run=client -o yaml --command --color=green > asd.yaml ## create a yaml file with a command
kubectl run webapp-green --image=kodekloud/webapp-color -- --color green
```

## Deployments
```
kubectl create deployment httpd-frontend --image=httpd:2.4-alpine --replicas=3
kubectl create deploy redis-deploy --image=redis --replicas=2 -n dev-ns
kubectl set image deployment nginx nginx=nginx:1.15
kubectl scale deployment nginx --replicas=5
kubectl expose deployment nginx --port 80
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
kubectl rollout status deployment/myapp-deployment
kubectl rollout history deployment/myapp-deployment
kubectl create –f deployment-definition.yml
kubectl rollout status deployment/myapp-deployment
kubectl rollout history deployment/myapp-deployment
kubectl get deployments
kubectl apply –f deployment-definition.yml
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
kubectl rollout undo deployment/myapp-deployment
kubectl -n admin2406 get deployment -o custom-columns=DEPLOYMENT:.metadata.name,CONTAINER_IMAGE:.spec.template.spec.containers[].image,READY_REPLICAS:.status.readyReplicas,NAMESPACE:.metadata.namespace --sort-by=.metadata.name > /opt/admin2406_data
```

## Services
```
kubectl expose deploy minio --type=NodePort --port=9001 --target-port=9001 --dry-run=client -o yaml > minio-svc.yaml
kubectl expose pod redis --port=6379 --name redis-service
kubectl run httpd --image=httpd:alpine --port=80 --expose
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml ## create service named redis-service of type ClusterIP to expose pod redis on port 6379 OR you can use
kubectl create service clusterip redis --tcp=6379:6378 --dry-run=client -o yaml
kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml ## Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes OR
kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml
```

## Scheduler
```
kubectl get pods --namespace kube-system ##Views any schedulers running
```

## Labels and Selectors
```
kubectl get pods --selector env=dev --no-headers | wc -l ##  Counts pods with label dev
kubectl get pods --selector='bu=finance' | wc -l ## Counts pods with labels bu=finance
kubectl get all --selector='env=prod' | wc -l
kubectl get all --selector env=prod,bu=finance,tier=frontend ## find under which launched with several labels.
kubectl label node node01.test.kz size=Super
```

## Taints and Tolerations
```
kubectl taint nodes node01.test.kz spray=mortein:NoSchedule     ## apply taint
kubectl taint nodes node01.test.kz spray=mortein:NoSchedule-    ## remove taint
```

## Daemon Sets
```
ls -l /etc/kubernetes/manifests/
ps -aux | grep /usr/bin/kubelet ## find the running kubelet, then find the line --config=/var/lib/kubelet/config.yaml
grep -i staticpod /var/lib/kubelet/config.yaml
kubectl run static-busybox --image=busybox --dry-run=client -o yaml --command -- sleep 1000 ## generate pod yaml file with command sleep 1000
kubectl run --restart=Never --image=busybox:1.28.4 static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```

## Schedulers
```
kubectl get events -o wide
```
## Logging and Monitoring
```
kubectl logs -p -c nginx web
kubectl top node
kubectl top pod
kubectl top pods --containers=true
```

## Config Maps
```
kubectl describe cm db-config
kubectl create configmap webapp-config-map --from-literal=APP_COLOR=darkblue
```

## initContainers
```
kubectl logs orange -c init-myservice ## Check initContainer logs
```

## Cluster Maintenance
```
kubectl drain node-1 ## Remove pods from node
kubectl cordon node-2 ## No new pods will be launched on the existing node, the pods running on the node will continue to operate.
kubectl uncordon node-1
kubectl upgrade plan
kubectl upgrade apply
kubectl drain node01 --ignore-daemonsets --force ## Force deletes nodes even they even if they have aJob, ReplicaSet, ReplicationController
```

## ETCD
```
kubectl describe pod etcd-controlplane -n kube-system
etcdctl version
```
### Backup etcd
```
ETCDCTL_API=3 etcdctl --endpoints=https://[127.0.0.1]:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save /opt/snapshot-pre-boot.db
```
### Restore etcd
```
ETCDCTL_API=3 etcdctl snapshot restore /opt/snapshot-pre-boot.db --data-dir /var/lib/etcd-from-backup
```

## TLS and Certificates
### Cert Signing Requests
```
cat akshay.csr | base64 -w 0
kubectl certificate approve akshay
kubectl get csr agent-smith -o yaml
kubectl delete csr agent-smith
```
### Validate Cert Location and Expiration
```
kubeadm certs check-expiration ## Locally signed certs
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -noout -enddate ## Externally signed Certs
```

## kubeconfig and Contexts
```
kubectl config get-contexts
kubectl config current-context
kubectl config view
kubectl config --kubeconfig=/root/my-kube-config use-context research ## switch to context research
```

## Role Based Access Control (RBAC)
```
kubectl get roles
kubectl get rolebindings
kubect describe role developer
kubectl describe rolebinding devuser-developer-binding
kubectl auth can-i create deployments
kubectl auth can-i delete node
kubectl auth can-i create deployments --as dev-user
kubectl auth can-i create pods --as dev-user
```

## Roles and Role Binding
```
kubectl create role developer --namespace=default --verb=list,create,delete --resource=pods
kubectl create rolebinding dev-user-binding --namespace=default --role=developer --user=dev-user
kubectl create role developer --verb=create --verb=get --verb=delete --verb=list --resource=pods --verb=create --verb=list --verb=delete --verb=get --resource=deployments --namespace=blue
```

## Cluster Roles
```
kubectl get clusterrolebindings --no-headers | wc -l
kubectl create clusterrole nodes --verb=create --verb=list --verb=delete --verb=watch --resource=nodes
kubectl create clusterrolebinding nodes-admin --clusterrole=nodes --user=michelle
kubectl create clusterrole storage-admin --verb=list,create,watch,list --resource=persistentvolumes,storageclasses
kubectl create clusterrolebinding michelle-storage-admin --clusterrole=storage-admin --user=someuser
```


## Service Accounts
```
kubectl create sa dashboard-sa
kubectl create token dashboard-sa
```

## helmsman Service Account
```
kubectl create clusterrole deployment-change --verb=get --verb=delete --verb=create --verb=list --verb=patch --verb=watch --resource=rs,deployment,secrets,services -n altyn-le-dev
kubectl create clusterrolebinding cr-deployment-change --clusterrole=deployment-change --serviceaccount=altyn-le-dev:deployer -n altyn-le-dev
```

## Security Contexts
```
kubectl exec ubuntu-sleeper -- whoami
```

## PV/PVC
```
kubectl describe pvc local-pvc
```

## DNS
```
kubectl exec -it hr -- nslookup mysql.payroll > /root/CKA/nslookup.out
```

## Data Ingress
```
kubectl create ingress minio-dev --dry-run=client -o yaml --rule="minio-dev.halykmarket.com/=minio:9000,tls=wildcard.halykmarket.com" -n minio-dev
kubectl create ingress ingress-test --rule="wear.my-online-store.com/wear*=wear-service:80"
kubectl create ingress pay-ingress --rule="/pay=pay-service:8282" --dry-run=client -o yaml -n critical-space > pay-ing.yaml
kubectl create ingress shop --rule='/wear=wear-service:8080' --rule='/watch=video-service:8080' -n app-space
```

## Troubleshooting
```
kubectl get nodes
service kube-apiserver status
service kube-controller-manager status
service kube-scheduler status
service kubelet status
service kube-proxy status
kubectl logs kube-apiserver-master -n kube-system
sudo journalctl -u kube-apiserver
kubectl describe node worker-1
sudo journalctl –u kubelet
openssl x509 -in /var/lib/kubelet/worker-1.crt -text
openssl x509 -noout -text -in /etc/kubernetes/pki/apiserver.crt
 openssl x509 -enddate -noout -text -in /etc/kubernetes/pki/apiserver.crt
/var/lib/kubelet/config.yaml ## Default kubelet config file
vi /etc/kubernetes/kubelet.conf ## Check for this file on the workers if there is a "node not found" errror
```

## Pod Execution
```
k run dns-resolver1 --image=busybox:1.28 --restart=Never --rm -it --command -- nslookup nginx-resolver-service > /root/CKA/nginx.svc
k run dns-resolver2 --image=busybox:1.28 --restart=Never --rm -it --command -- nslookup 10.244.192.4 > /root/CKA/nginx.pod
k run --rm -ti tshoot --image=redis --command -- nc -z -v -w -2 10.244.192.1 80
```

## JSON Path
```
kubectl get nodes -o json | jq -c 'paths'
kubectl get nodes -o json | jq -c 'paths' | grep type | grep -v "metadata" | grep address
```

## crictl
```
crictl logs 2354z34edhyd43 >& /opt/log/container.log  ## Write logs to file
```

## kubeadm join
```
kubeadm token list ## List tokens on the master node
kubeadm token delete <token value>  ## Delete a node token
kubeadm token create --print-join-command
kubeadm certs check-expiration ## check certificates
```
## kubectl Patching
```
kubectl patch daemonsets -n monitoring node-exporter --patch '{"spec": {"template": {"spec": {"hostNetwork": false}}}}' ## disable node exporter from external
```

## Misc Commands & Paths
```
ps -aux | grep kubelet | grep --color container-runtime-endpoint ## Find kubelet Socket 
/opt/cni/bin ## The CNI binaries path
ls /etc/cni/net.d/ ## Show the default CNI plugin
cat /etc/cni/net.d/10-flannel.conflist ## Check the CNI type

ip route
default via 172.25.1.1 dev eth1 
10.57.230.0/24 dev eth0 proto kernel scope link src 10.57.230.6 
10.244.0.0/16 dev weave proto kernel scope link src 10.244.192.0 
172.25.1.0/24 dev eth1 proto kernel scope link src 172.25.1.11
```


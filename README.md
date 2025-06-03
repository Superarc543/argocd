# argocd  
K8s 架構安裝 ArgoCD 紀錄  

官方網站:https://argocd.devops.gold/operator-manual/installation/#_3  

## HA版-正式環境  
https://github.com/argoproj/argo-cd/blob/master/manifests/ha/install.yaml  
## 非HA-評估版  
https://github.com/argoproj/argo-cd/blob/master/manifests/install.yaml  
## Helm版(社群維護)  
https://github.com/argoproj/argo-helm/tree/main/charts/argo-cd  

#####################################  
GitHub內的argocd Helm版本，內包SVC 搭配MetalLB 符合內網曝露專用  
修改values.yaml裡的  1003跟1004行 (1004添加MetalLB的IP Ranger即可，預設曝露80 Port-在1013行)  
#####################################  
※安装配置清单中包含的 ClusterRoleBinding 資源引用 argocd 名稱空間， 如果 Argo CD 安装到不同的名稱空間，要另外修改引用資源的名稱空間  

1. kubectl create namespace argocd  
2. kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml  
3. kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}' 或是 -p '{"spec": {"type": "NodePort"}}'  
※Default Cluster IP 看環境改  
4. kubectl get secrets -n argocd argocd-initial-admin-secret -o yaml  
5. echo "密碼" | base 64 -d  
6. 登入web console，預設帳號admin  

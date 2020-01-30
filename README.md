# Cheet-sheet
The correct command for SA is:
kubectl auth can-i <verb> <resource> --as=system:serviceaccount:<namespace>:<serviceaccountname> [-n <namespace>]

Command for users:
k auth can-i update pods --as=ltt-dev-deployer

# K8S-GOLDEN

Helm installation:
# To install helm fomr bash script:
$ curl https://raw.githubusercontent.com/helm/helm/master/scripts/get > get_helm.sh
$ chmod 700 get_helm.sh
$ ./get_helm.sh

# To install helm from  the wget path:
#!/bin/bash
wget https://storage.googleapis.com/kubernetes-helm/helm-v2.12.2-linux-amd64.tar.gz
tar -zxvf helm-v2.12.2-linux-amd64.tar.gz
mv linux-amd64/helm /usr/local/bin/helm
kubectl -n kube-system create sa tiller
kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller
kubectl create namespace kubeapps

# Run this command to install dashboard
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml

# Metrix related papckage:
Run
helm upgrade --install metrics stable/metrics-server --namespace kube-system
Or
kubectl create -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/monitoring-standalone/v1.7.0.yaml

# Authenticate your machine to the private registery:
docker login -u admin -p admin123 your-repo:8082
docker login -u admin -p admin123 your-repo:8083
This will create an entry in ~/.docker/config.json:

# To create splunk-connect-for-kubernetes
 helm install --name my-release -f values.yaml https://github.com/splunk/splunk-connect-for-kubernetes/releases/download/1.2.0/splunk-connect-for-kubernetes-1.2.0.tgz

example: kubectl auth can-i get pods --as=system:serviceaccount:kube-system:tiller -n kube-system


The correct command is:
kubectl auth can-i <verb> <resource> --as=system:serviceaccount:<namespace>:<serviceaccountname> [-n <namespace>]

To check whether the tiller account has the right to create a ServiceMonitor object:
kubectl auth can-i create servicemonitor --as=system:serviceaccount:staging:tiller -n staging

Note: to solve my issue with the tiller account, I had to add rights to the servicemonitors resource in the monitoring.coreos.com apiGroup. After that change, the above command returned yes (finally) and the installation of our Helm Chart succeeded.

Updated tiller-manager role:

kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: tiller-manager
  labels:
    org: ipos
    app: tiller
  annotations:
    description: "Role to give Tiller appropriate access in namespace"
    ref: "https://docs.helm.sh/using_helm/#example-deploy-tiller-in-a-namespace-restricted-to-deploying-resources-only-in-that-namespace"
rules:
- apiGroups: ["", "batch", "extensions", "apps"]
  resources: ["*"]
  verbs: ["*"]
- apiGroups:
    - monitoring.coreos.com
  resources:
    - servicemonitors
  verbs:
    - '*'


example: kubectl auth can-i get pods --as=system:serviceaccount:kube-system:tiller -n kube-system

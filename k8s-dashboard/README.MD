# K8S-GOLDEN
 To install k8s-dasboard follow instrucitons:
1. Run command: bash script.bashrc
2. Create your own cluster role (you can define you own resources and verbs inside the yaml maifest) 
   run command: k create -f clusterrole.yaml
3. Create a service account (you can define the name and the namespace inside the yaml manifest)
   run command: k create -f sa.yaml
4. Create clusterrolebinding to bind your role and serviceaccount
   run command:  k create -f cclusterrolebinding.yaml
NOTE you might wanna expose your deployment with LB or ingress service type to make it accessible externally (if you dont have control of infrastructure request network guy to attach LB to your server, you can also use NodePort service to xpose and access it)
5. If you use NodePort service take the public IP address of your node on which rus dashboard pod with NodePort and paste it in browser.
6. Describe your serviceaccount which you created for dashboard and take the token which it use.
7. Do kubectl describe secret (the name of the token) and use the token to access your dashboard.

DONE (enjoy your dashboard) ;)

# argocd-test

PoC for testing argocd

## Installation

Can be installed on any kubernetes cluster. I tested it on a kind cluster, so i can test it locally. The steps for kind cluster setup is as follows. For normal k8s cluster, it will be fairly simple.

- Create a namespace `argocd` first in the cluster and set the namespace context to this `argocd` namespace
- Install first `argocd/install.yaml`
- After installation, wait for a few mins and ensure all pods are running.
- Since on my mac, there is issues with kind cluster, I do port forward on the `argocd-server` service. For ex: `kubectl port-forward svc/argocd-server 8080:80`
- Once port forwarding is working, go to `https://localhost:8080`
- Login as user `admin` and for the password on a new terminal, run the command `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d` and paste the output as password
- Once logged in, you will see empty dashboard
- run the command `kubectl apply -f simple/sample-app-application.yaml` to see working of simple app deployment 
- run the command `kubectl apply -f app-of-apps/app-of-apps.yaml` to see app-of-apps deployment with multi-app concept / app-of-apps pattern

## Things to do after PoC

- Ensure every argo apps have separate projects based on the type of apps created
- Add ingress for argocd
- setup ssh keys or passwords for SCM integration with repos which need authentication.



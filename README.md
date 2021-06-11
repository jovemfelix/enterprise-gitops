## Steps



### Create Project using HELM cli

```shell
$ helm create fuseapp
```



```
$ helm template . --name-template my-fuse01-dev --namespace test-dev | oc apply --dry-run='client' -f - 
```



### Create ArgoCD Application

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-fuse01-dev
  namespace: openshift-gitops
spec:
  destination:
    name: ''
    namespace: test-dev
    server: 'https://kubernetes.default.svc'
  source:
    path: fuseapp/
    repoURL: 'https://github.com/jovemfelix/enterprise-gitops'
    targetRevision: master
  project: argocd-project-dev
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - CreateNamespace=true
```






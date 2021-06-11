## Steps



### Create Project using HELM cli

```shell
$ helm create fuseapp
```



### Create ArgoCD Application

```yaml
---
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-fuse-dev
  namespace: openshift-gitops
spec:
  project: default
  source:
    path: fuseapp/
    repoURL: https://github.com/jovemfelix/enterprise-gitops
    targetRevision: master
  destination:
    namespace: test-dev
    server: https://kubernetes.default.svc
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
    - CreateNamespace=true
```






# argocd

# Creating a Project with Allowing Any Destinations

apiVersion: argoproj.io/v1alpha1
kind: AppProject
metadata:
  name: demo-project
  namespace: argocd
spec:
  description: Demo Project
  sourceRepos:
  - '*'

  destinations:
  - namespace: '*'
    server: '*'

  clusterResourceWhitelist:
  - group: '*'
    kind: '*'

  namespaceResourceWhitelist:
  - group: '*'
    kind: '*'

# Creating a Project with Allowing Specific Destinations
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: 
  name: guestbook-demo-project
  namespace: argocd
spec: 
  destination: 
    namespace: guestbook-demo-project
    server: "https://kubernetes.default.svc"
  project: demo-project
  source: 
    path: guestbook
    repoURL: "https://github.com/mabusaa/argocd-example-apps.git"
    targetRevision: master
  syncPolicy:
    syncOptions:
      - CreateNamespace=true

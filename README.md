# 1. Install the gitops operator
oc apply -f operators/gitops.yaml

oc label ns/openshift-authentication argocd.argoproj.io/managed-by=openshift-gitops
oc label ns/openshift-config argocd.argoproj.io/managed-by=openshift-gitops

# 2. Install the other operators as gitops apps

oc apply -f 1.gitopsapps/operator-devspaces.yaml
oc apply -f 1.gitopsapps/operator-rhsso.yaml
oc apply -f 1.gitopsapps/operator-servicemesh.yaml
oc apply -f 1.gitopsapps/operator-web-terminal.yaml

# 3. Install the CRD required by the installed operators as gitops apps

oc apply -f 1.gitopsapps/crd-checluster.yaml
oc apply -f 1.gitopsapps/rhsso.yaml
oc apply -f 1.gitopsapps/servicemesh.yaml

# 4. Install the user applications/demos as gitops apps
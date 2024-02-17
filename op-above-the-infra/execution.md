# Install operators

oc new-project istio-system
oc new-project devspaces-operator
oc apply -f operator-gitops.yaml
oc apply -f operator-service-mesh.yaml
oc apply -f operator-devspaces.yaml

--manual approval for DevSpaces operator

oc apply -f checluster.yaml


https://devspaces.apps.rosa.dpenagos-hcp.pkig.p3.openshiftapps.com/api/user/id

if needed, from the devspace we can push to the github repo. But we must place the credentials to do that. 

kind: Secret
apiVersion: v1
metadata:
  name: personal-access-token-<your_choice_of_name_for_this_token>
  labels:
    app.kubernetes.io/component: scm-personal-access-token
    app.kubernetes.io/part-of: che.eclipse.org
  annotations:
    che.eclipse.org/che-userid: <che_user_id>
    che.eclipse.org/scm-personal-access-token-name: <git_provider_name>
    che.eclipse.org/scm-url: <git_provider_endpoint>
    che.eclipse.org/scm-organization: <git_provider_organization>
stringData:
  token: <Content_of_access_token>
type: Opaque

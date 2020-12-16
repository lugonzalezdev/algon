# algon helmfile example

## Prerequisites

- Kubernetes cluster accessible https://birthday.play-with-docker.com/kubernetes-docker-desktop/
- kubectl https://kubernetes.io/docs/tasks/tools/install-kubectl/
- helm https://helm.sh/docs/intro/install/
- helmfile https://github.com/roboll/helmfile
 
## Run algon with Loki and Grafana

```
helmfile -f helmfile.yml apply
```

## Portforward Grafana

```
kubectl get secret --namespace loki loki-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
kubectl port-forward --namespace loki service/loki-grafana 3000:80
```

Open Grafana http://localhost:3000 and use Loki's log view to run LogQL queries https://grafana.com/docs/loki/latest/logql/

## Delete chart

```
helmfile -f helmfile.yml delete
```
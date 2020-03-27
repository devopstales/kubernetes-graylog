# kubernetes-graylog
Kubernetes/Openshift central logging to Graylog


### Kubernets
```
kubectl apply -f filebeat.permission.yml
kubectl apply -f filebeat.settings.configmap.yml
kubectl apply -f filebeat.daemonset.yml
```

### Opeshift
If you are using Red Hat OpenShift, you need to specify additional settings in the manifest file

Modify the DaemonSet container spec in the manifest file:
```
  securityContext:
    runAsUser: 0
    privileged: true
```

Grant the filebeat service account access to the privileged SCC:
```
oc adm policy add-scc-to-user privileged system:serviceaccount:kube-system:filebeat
```

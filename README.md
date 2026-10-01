# ConfigMap and Secret Volumes
Reference project: https://gitlab.com/twn-devops-bootcamp/latest/10-kubernetes/configmap-and-secret-volume-types/-/tree/starting-code?ref_type=heads

For an example of using ConfigMap and Secret as `key:value` pairs for setting environment variables, see the repo [TWN-K8-Minukube-Mongo](https://github.com/JonathanBaqDev/TWN-K8-Minukube-Mongo).

This project demonstrates how to mount ConfigMap and Secret data as volumes inside a pod, exposing each item as a file that the application can read at runtime.

## Mosquitto message broker without a data volume

```bash
kubectl apply -f mosquitto-without-volumes.yaml
kubectl get pod
kubectl exec -it <pod_name> -- /bin/sh

cd mosquitto
cd config
cat mosquitto.conf # Inspect the default configuration file

kubectl delete -f mosquitto-without-volumes.yaml
```

## Overwrite the Mosquitto configuration file

- Create the ConfigMap and Secret before deploying the application.
- Define the volumes and mount them in the deployment file; see [mosquitto.yaml](mosquitto.yaml).

```bash
kubectl apply -f config-file.yaml
kubectl apply -f secret-file.yaml
kubectl get secret
kubectl get configmap

kubectl apply -f mosquitto.yaml
kubectl get pod
kubectl exec -it <pod_name> -- /bin/sh
```
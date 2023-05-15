# Setting up MongoDB on Kubernetes On Raspberry Pi 4

This repository contains YAML files and instructions to deploy MongoDB on Kubernetes using a deployment.


## Prerequisites

Make sure you have the following prerequisites installed and configured in your environment:

- Configured and accessible Kubernetes cluster (can be local or cloud-based)
- Installed and configured Kubernetes command-line tool (kubectl) to access the cluster

## Instructions

Follow the steps below to deploy MongoDB on Kubernetes:

1. Clone this repository to your local machine:

```shell
git clone <REPOSITORY_URL>
cd <REPOSITORY_NAME>
```

2. Verify that your Kubernetes context is correctly configured for the target cluster. You can use the following command to check:

```shell
kubectl config current-context
```

3. Create a namespace for MongoDB:

```shell
kubectl create namespace mongodb
```

4. Create a PersistentVolumeClaim (PVC) to store the MongoDB persistent data.

Check this before https://microk8s.io/docs/nfs#heading--common-issues

```shell
kubectl apply -f pvc.yaml
```
5. Create a ConfigMap to store the configuration data for the MongoDB deployment such as ports, replica set, and other configuration parameters.

```shell
kubectl apply -f configmap.yaml
```

6. Create a Secret to store sensitive information such as passwords and encryption keys.

```shell
kubectl apply -f secret.yaml
```

7. Deploy the MongoDB deployment by running the following command:
```shell
kubectl apply -f deployment.yaml
```

8. Deploy the MongoDB service by running the following command:
```shell
kubectl apply -f service.yaml
```

9. Check the status of the MongoDB deployment and pods:
```shell
kubectl get deployment -n mongodb
kubectl get pods -n mongodb
```

10. Wait until the MongoDB pods are in "Running" and "Ready" state.

## Customization

You can customize the MongoDB resources in the mongodb-deployment.yaml file to suit your needs. For example, you can adjust the number of replicas, resource configuration (CPU, memory), and other MongoDB-specific parameters.

Make sure to review and adjust the provided YAML files according to your specific configuration and requirements before deploying MongoDB on Kubernetes.

##  Issues

WARNING: MongoDB requires ARMv8.2-A or higher, and your current system does not appear to implement any of the common features for that!
  applies to all versions ≥5.0, any of 4.4 ≥4.4.19, and any of 4.2 ≥4.2.19
  see https://jira.mongodb.org/browse/SERVER-71772
  see https://jira.mongodb.org/browse/SERVER-55178
  see also https://en.wikichip.org/wiki/arm/armv8#ARMv8_Extensions_and_Processor_Features
  see also https://github.com/docker-library/mongo/issues/485#issuecomment-970864306

Mongodb only works up to version 4.0 on Raspberry 4

## Conclusion

Congratulations! You have successfully deployed MongoDB on Kubernetes using a deployment. You can now use MongoDB to store and retrieve data in your Kubernetes cluster.

Please note that this README provides only a basic overview, and you may need to adjust the steps and provided YAML files to fit your specific Kubernetes setup.

Enjoy exploring MongoDB on Kubernetes!

Generated from ChatGPT
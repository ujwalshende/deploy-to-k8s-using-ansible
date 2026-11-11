# Project: Automate Kubernetes Deployment Using Ansible
This project contains terraform code that creates an EKS cluster using the offical eks module from AWS, and an ansible playbook that creates a namespace in the EKS cluster and deploys an nginx application using `nginx.yaml` to it.

The ansible playbook (`deploy-to-k8s.yaml`) containes only one play. This play uses the kubeconfig file present in the default location for simplicity. It can be configured to use the kubeconfig file present in another location. One simple way to do it is by setting the K8S_AUTH_KUBECONFIG environment variable to the location/path of the kubeconfig file

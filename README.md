# Project: Automate Kubernetes Deployment Using Ansible
This project contains terraform code in terraform-eks-config folder that creates an EKS cluster using the offical eks module from AWS, and an ansible playbook that creates a namespace in the EKS cluster and deploys an nginx application using `nginx.yaml` to it.

The ansible playbook (`deploy-to-k8s.yaml`) containes only one play. This play uses the kubeconfig file present in `~/terraform/kubeconfig_myapp-eks-cluster`. It can be configured to use the kubeconfig file present in another location. One simple way to do it is by setting the K8S_AUTH_KUBECONFIG environment variable to the location/path of the kubeconfig file

After running the `terraform apply`, the output should look something like the following
```
Plan: 62 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

module.eks.aws_cloudwatch_log_group.this[0]: Creating...
module.eks.aws_iam_role.this[0]: Creating...
module.myapp-vpc.aws_vpc.this[0]: Creating...
module.eks.module.eks_managed_node_group["dev"].aws_iam_role.this[0]: Creating...
module.eks.aws_cloudwatch_log_group.this[0]: Creation complete after 0s [id=/aws/eks/myapp-eks-cluster/cluster]
module.eks.aws_iam_role.this[0]: Creation complete after 1s [id=myapp-eks-cluster-cluster-18ed83c6c22bca389dae02ef33]
module.eks.module.eks_managed_node_group["dev"].aws_iam_role.this[0]: Creation complete after 1s [id=dev-eks-node-group-503188ff882f31f03e9aebd75f]
module.eks.aws_iam_role_policy_attachment.this["AmazonEKSClusterPolicy"]: Creating...
module.eks.module.kms.data.aws_iam_policy_document.this[0]: Reading...
module.eks.module.eks_managed_node_group["dev"].aws_iam_role_policy_attachment.this["AmazonEKS_CNI_Policy"]: Creating...
module.eks.module.eks_managed_node_group["dev"].aws_iam_role_policy_attachment.this["AmazonEC2ContainerRegistryReadOnly"]: Creating...
module.eks.module.eks_managed_node_group["dev"].aws_iam_role_policy_attachment.this["AmazonEKSWorkerNodePolicy"]: Creating...
module.eks.module.kms.data.aws_iam_policy_document.this[0]: Read complete after 0s [id=2304895399]
module.eks.module.kms.aws_kms_key.this[0]: Creating...
module.eks.aws_iam_role_policy_attachment.this["AmazonEKSClusterPolicy"]: Creation complete after 0s [id=myapp-eks-cluster-cluster-18ed83c6c22bca389dae02ef33/arn:aws:iam::aws:policy/AmazonEKSClusterPolicy]
module.eks.module.eks_managed_node_group["dev"].aws_iam_role_policy_attachment.this["AmazonEC2ContainerRegistryReadOnly"]: Creation complete after 0s [id=dev-eks-node-group-503188ff882f31f03e9aebd75f/arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly]
module.eks.module.eks_managed_node_group["dev"].aws_iam_role_policy_attachment.this["AmazonEKS_CNI_Policy"]: Creation complete after 0s [id=dev-eks-node-group-503188ff882f31f03e9aebd75f/arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy]
module.eks.module.eks_managed_node_group["dev"].aws_iam_role_policy_attachment.this["AmazonEKSWorkerNodePolicy"]: Creation complete after 0s [id=dev-eks-node-group-503188ff882f31f03e9aebd75f/arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy]
module.myapp-vpc.aws_vpc.this[0]: Creation complete after 2s [id=vpc-01b301abc8fff109a]
module.myapp-vpc.aws_default_security_group.this[0]: Creating...
module.myapp-vpc.aws_subnet.private[1]: Creating...
module.myapp-vpc.aws_subnet.private[0]: Creating...
module.myapp-vpc.aws_route_table.public[0]: Creating...
module.myapp-vpc.aws_route_table.private[0]: Creating...
module.myapp-vpc.aws_default_route_table.default[0]: Creating...
module.eks.aws_security_group.cluster[0]: Creating...
module.myapp-vpc.aws_default_network_acl.this[0]: Creating...
module.myapp-vpc.aws_subnet.private[2]: Creating...
module.myapp-vpc.aws_default_route_table.default[0]: Creation complete after 0s [id=rtb-0dff1acd97d13dc67]
module.myapp-vpc.aws_subnet.public[0]: Creating...
module.myapp-vpc.aws_route_table.private[0]: Creation complete after 0s [id=rtb-00f70f4f67b6d2ab3]
module.myapp-vpc.aws_subnet.public[2]: Creating...
module.myapp-vpc.aws_route_table.public[0]: Creation complete after 0s [id=rtb-0df4284c116d66933]
module.myapp-vpc.aws_subnet.public[1]: Creating...
module.myapp-vpc.aws_subnet.private[2]: Creation complete after 0s [id=subnet-0e42b1a2129308b73]
module.myapp-vpc.aws_internet_gateway.this[0]: Creating...
module.myapp-vpc.aws_subnet.private[0]: Creation complete after 1s [id=subnet-0384ce1d7ec638da4]
module.eks.aws_security_group.node[0]: Creating...
module.myapp-vpc.aws_default_network_acl.this[0]: Creation complete after 1s [id=acl-041ba7ff9360c1193]
module.myapp-vpc.aws_subnet.public[0]: Creation complete after 1s [id=subnet-07634e2f9d5e47720]
module.myapp-vpc.aws_internet_gateway.this[0]: Creation complete after 1s [id=igw-0d7165dd7e29a233a]
module.myapp-vpc.aws_route.public_internet_gateway[0]: Creating...
module.myapp-vpc.aws_eip.nat[0]: Creating...
module.myapp-vpc.aws_default_security_group.this[0]: Creation complete after 1s [id=sg-0a3cfcab2c3de8083]
module.myapp-vpc.aws_subnet.public[2]: Creation complete after 1s [id=subnet-0d11c64546ea53d62]
module.myapp-vpc.aws_subnet.public[1]: Creation complete after 1s [id=subnet-09a8a1c7cae90952c]
module.myapp-vpc.aws_route_table_association.public[0]: Creating...
module.myapp-vpc.aws_route_table_association.public[1]: Creating...
module.myapp-vpc.aws_route_table_association.public[2]: Creating...
module.myapp-vpc.aws_route_table_association.public[0]: Creation complete after 0s [id=rtbassoc-060a44865559edb2e]
module.myapp-vpc.aws_route_table_association.public[1]: Creation complete after 0s [id=rtbassoc-0916dcd8da798065e]
module.myapp-vpc.aws_route_table_association.public[2]: Creation complete after 0s [id=rtbassoc-0b8b3c24cf3115a08]
module.myapp-vpc.aws_route.public_internet_gateway[0]: Creation complete after 0s [id=r-rtb-0df4284c116d669331080289494]
module.eks.aws_security_group.cluster[0]: Creation complete after 2s [id=sg-0e95f6e0d43fccfd2]
module.myapp-vpc.aws_eip.nat[0]: Creation complete after 1s [id=eipalloc-015eeea5b60fddfe6]
module.myapp-vpc.aws_nat_gateway.this[0]: Creating...
module.eks.aws_security_group.node[0]: Creation complete after 1s [id=sg-05f256badbce12f8f]
module.eks.aws_security_group_rule.node["ingress_nodes_ephemeral"]: Creating...
module.eks.aws_security_group_rule.node["ingress_cluster_9443_webhook"]: Creating...
module.eks.aws_security_group_rule.cluster["ingress_nodes_443"]: Creating...
module.eks.aws_security_group_rule.node["egress_all"]: Creating...
module.eks.aws_security_group_rule.node["ingress_self_coredns_tcp"]: Creating...
module.eks.aws_security_group_rule.node["ingress_cluster_10251_webhook"]: Creating...
module.eks.aws_security_group_rule.node["ingress_self_coredns_udp"]: Creating...
module.eks.aws_security_group_rule.cluster["ingress_nodes_443"]: Creation complete after 1s [id=sgrule-4092108172]
module.eks.aws_security_group_rule.node["egress_all"]: Creation complete after 1s [id=sgrule-3319766922]
module.eks.aws_security_group_rule.node["ingress_cluster_443"]: Creating...
module.eks.aws_security_group_rule.node["ingress_cluster_6443_webhook"]: Creating...
module.myapp-vpc.aws_subnet.private[1]: Creation complete after 3s [id=subnet-00b366ada04937f8a]
module.eks.aws_security_group_rule.node["ingress_cluster_8443_webhook"]: Creating...
module.eks.aws_security_group_rule.node["ingress_self_coredns_tcp"]: Creation complete after 2s [id=sgrule-2508855046]
module.eks.aws_security_group_rule.node["ingress_cluster_4443_webhook"]: Creating...
module.eks.aws_security_group_rule.node["ingress_nodes_ephemeral"]: Creation complete after 2s [id=sgrule-1993489618]
module.eks.aws_security_group_rule.node["ingress_cluster_kubelet"]: Creating...
module.eks.aws_security_group_rule.node["ingress_cluster_10251_webhook"]: Creation complete after 3s [id=sgrule-529476024]
module.myapp-vpc.aws_route_table_association.private[0]: Creating...
module.myapp-vpc.aws_route_table_association.private[0]: Creation complete after 0s [id=rtbassoc-034f80846f4d9aeba]
module.myapp-vpc.aws_route_table_association.private[2]: Creating...
module.eks.aws_security_group_rule.node["ingress_cluster_9443_webhook"]: Creation complete after 3s [id=sgrule-996563481]
module.myapp-vpc.aws_route_table_association.private[1]: Creating...
module.myapp-vpc.aws_route_table_association.private[2]: Creation complete after 0s [id=rtbassoc-088de80a37f1c9a2d]
module.myapp-vpc.aws_route_table_association.private[1]: Creation complete after 1s [id=rtbassoc-08ac917ce4abc9dee]
module.eks.aws_security_group_rule.node["ingress_self_coredns_udp"]: Creation complete after 4s [id=sgrule-836089065]
module.eks.aws_security_group_rule.node["ingress_cluster_6443_webhook"]: Creation complete after 3s [id=sgrule-1285248499]
module.eks.aws_security_group_rule.node["ingress_cluster_443"]: Creation complete after 4s [id=sgrule-2293766919]
module.eks.aws_security_group_rule.node["ingress_cluster_8443_webhook"]: Creation complete after 4s [id=sgrule-1606904274]
module.eks.aws_security_group_rule.node["ingress_cluster_4443_webhook"]: Creation complete after 4s [id=sgrule-2245603941]
module.eks.aws_security_group_rule.node["ingress_cluster_kubelet"]: Creation complete after 5s [id=sgrule-734427587]
module.eks.module.kms.aws_kms_key.this[0]: Still creating... [00m10s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [00m10s elapsed]
module.eks.module.kms.aws_kms_key.this[0]: Still creating... [00m20s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [00m20s elapsed]
module.eks.module.kms.aws_kms_key.this[0]: Creation complete after 28s [id=4f0074a5-d24e-4bb3-9152-9e032afa5598]
module.eks.module.kms.aws_kms_alias.this["cluster"]: Creating...
module.eks.aws_iam_policy.cluster_encryption[0]: Creating...
module.eks.aws_eks_cluster.this[0]: Creating...
module.eks.module.kms.aws_kms_alias.this["cluster"]: Creation complete after 0s [id=alias/eks/myapp-eks-cluster]
module.eks.aws_iam_policy.cluster_encryption[0]: Creation complete after 1s [id=arn:aws:iam::832348493841:policy/myapp-eks-cluster-cluster-ClusterEncryptionf0163762a83c75b1691ed43ab1]
module.eks.aws_iam_role_policy_attachment.cluster_encryption[0]: Creating...
module.eks.aws_iam_role_policy_attachment.cluster_encryption[0]: Creation complete after 0s [id=myapp-eks-cluster-cluster-18ed83c6c22bca389dae02ef33/arn:aws:iam::832348493841:policy/myapp-eks-cluster-cluster-ClusterEncryptionf0163762a83c75b1691ed43ab1]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [00m30s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [00m10s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [00m40s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [00m20s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [00m50s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [00m30s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [01m00s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [00m40s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [01m10s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [00m50s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [01m20s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [01m00s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [01m30s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [01m10s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [01m40s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [01m20s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [01m50s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [01m30s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Still creating... [02m00s elapsed]
module.myapp-vpc.aws_nat_gateway.this[0]: Creation complete after 2m3s [id=nat-041e47b54aacd3371]
module.myapp-vpc.aws_route.private_nat_gateway[0]: Creating...
module.myapp-vpc.aws_route.private_nat_gateway[0]: Creation complete after 0s [id=r-rtb-00f70f4f67b6d2ab31080289494]
module.eks.aws_eks_cluster.this[0]: Still creating... [01m40s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [01m50s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [02m00s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [02m10s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [02m20s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [02m30s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [02m40s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [02m50s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [03m00s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [03m10s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [03m20s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [03m30s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [03m40s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [03m50s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [04m00s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [04m10s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [04m20s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [04m30s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [04m40s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [04m50s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [05m00s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [05m10s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [05m20s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [05m30s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [05m40s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [05m50s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [06m00s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [06m10s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [06m20s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [06m30s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [06m40s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [06m50s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [07m00s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [07m10s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [07m20s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [07m30s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [07m40s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [07m50s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [08m00s elapsed]
module.eks.aws_eks_cluster.this[0]: Still creating... [08m10s elapsed]
module.eks.aws_eks_cluster.this[0]: Creation complete after 8m12s [id=myapp-eks-cluster]
module.eks.data.aws_eks_addon_version.this["eks-pod-identity-agent"]: Reading...
module.eks.data.aws_eks_addon_version.this["vpc-cni"]: Reading...
module.eks.data.aws_eks_addon_version.this["coredns"]: Reading...
module.eks.data.aws_eks_addon_version.this["kube-proxy"]: Reading...
module.eks.aws_ec2_tag.cluster_primary_security_group["application"]: Creating...
module.eks.aws_ec2_tag.cluster_primary_security_group["environment"]: Creating...
module.eks.aws_eks_access_entry.this["cluster_creator"]: Creating...
module.eks.time_sleep.this[0]: Creating...
module.eks.data.tls_certificate.this[0]: Reading...
module.eks.data.aws_eks_addon_version.this["vpc-cni"]: Read complete after 1s [id=vpc-cni]
module.eks.data.aws_eks_addon_version.this["kube-proxy"]: Read complete after 1s [id=kube-proxy]
module.eks.data.aws_eks_addon_version.this["coredns"]: Read complete after 1s [id=coredns]
module.eks.data.aws_eks_addon_version.this["eks-pod-identity-agent"]: Read complete after 1s [id=eks-pod-identity-agent]
module.eks.aws_eks_addon.before_compute["vpc-cni"]: Creating...
module.eks.aws_eks_addon.before_compute["eks-pod-identity-agent"]: Creating...
module.eks.aws_ec2_tag.cluster_primary_security_group["application"]: Creation complete after 1s [id=sg-03ef3d30f7d73067d,application]
module.eks.aws_ec2_tag.cluster_primary_security_group["environment"]: Creation complete after 1s [id=sg-03ef3d30f7d73067d,environment]
module.eks.aws_eks_access_entry.this["cluster_creator"]: Creation complete after 1s [id=myapp-eks-cluster:arn:aws:iam::832348493841:user/admin]
module.eks.aws_eks_access_policy_association.this["cluster_creator_admin"]: Creating...
module.eks.aws_eks_access_policy_association.this["cluster_creator_admin"]: Creation complete after 1s [id=myapp-eks-cluster#arn:aws:iam::832348493841:user/admin#arn:aws:eks::aws:cluster-access-policy/AmazonEKSClusterAdminPolicy]
module.eks.data.tls_certificate.this[0]: Read complete after 2s [id=38b12f081caa262d3c3b1b0f23fda4734317a14d]
module.eks.aws_iam_openid_connect_provider.oidc_provider[0]: Creating...
module.eks.aws_iam_openid_connect_provider.oidc_provider[0]: Creation complete after 0s [id=arn:aws:iam::832348493841:oidc-provider/oidc.eks.eu-central-1.amazonaws.com/id/B174AD6AEAD7491B27F895DA911A1663]
module.eks.time_sleep.this[0]: Still creating... [00m10s elapsed]
module.eks.aws_eks_addon.before_compute["eks-pod-identity-agent"]: Still creating... [00m10s elapsed]
module.eks.aws_eks_addon.before_compute["vpc-cni"]: Still creating... [00m10s elapsed]
module.eks.aws_eks_addon.before_compute["vpc-cni"]: Creation complete after 14s [id=myapp-eks-cluster:vpc-cni]
module.eks.time_sleep.this[0]: Still creating... [00m20s elapsed]
module.eks.aws_eks_addon.before_compute["eks-pod-identity-agent"]: Still creating... [00m20s elapsed]
module.eks.aws_eks_addon.before_compute["eks-pod-identity-agent"]: Creation complete after 24s [id=myapp-eks-cluster:eks-pod-identity-agent]
module.eks.time_sleep.this[0]: Still creating... [00m30s elapsed]
module.eks.time_sleep.this[0]: Creation complete after 30s [id=2026-11-15T11:03:57Z]
module.eks.module.eks_managed_node_group["dev"].module.user_data.null_resource.validate_cluster_service_cidr: Creating...
module.eks.module.eks_managed_node_group["dev"].module.user_data.null_resource.validate_cluster_service_cidr: Creation complete after 0s [id=3153705900604443889]
module.eks.module.eks_managed_node_group["dev"].aws_launch_template.this[0]: Creating...
module.eks.module.eks_managed_node_group["dev"].aws_launch_template.this[0]: Creation complete after 6s [id=lt-043d202471959e51b]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Creating...
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Still creating... [00m10s elapsed]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Still creating... [00m20s elapsed]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Still creating... [00m30s elapsed]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Still creating... [00m40s elapsed]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Still creating... [00m50s elapsed]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Still creating... [01m00s elapsed]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Still creating... [01m10s elapsed]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Still creating... [01m20s elapsed]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Still creating... [01m30s elapsed]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Still creating... [01m40s elapsed]
module.eks.module.eks_managed_node_group["dev"].aws_eks_node_group.this[0]: Creation complete after 1m48s [id=myapp-eks-cluster:dev-cd220757bf2885e1fa86dbb3ae]
module.eks.aws_eks_addon.this["kube-proxy"]: Creating...
module.eks.aws_eks_addon.this["coredns"]: Creating...
module.eks.aws_eks_addon.this["coredns"]: Still creating... [00m10s elapsed]
module.eks.aws_eks_addon.this["kube-proxy"]: Still creating... [00m10s elapsed]
module.eks.aws_eks_addon.this["kube-proxy"]: Still creating... [00m20s elapsed]
module.eks.aws_eks_addon.this["coredns"]: Still creating... [00m20s elapsed]
module.eks.aws_eks_addon.this["kube-proxy"]: Creation complete after 24s [id=myapp-eks-cluster:kube-proxy]
module.eks.aws_eks_addon.this["coredns"]: Still creating... [00m30s elapsed]
module.eks.aws_eks_addon.this["coredns"]: Still creating... [00m40s elapsed]
module.eks.aws_eks_addon.this["coredns"]: Creation complete after 44s [id=myapp-eks-cluster:coredns]

Apply complete! Resources: 62 added, 0 changed, 0 destroyed
```
After executing `ansible-playbook deploy-to-k8s.yaml`, the output should look like the following
<img width="942" height="267" alt="image" src="https://github.com/user-attachments/assets/d8d8038c-b5f5-4493-86e5-b4049ca17a93" />


# k8s-devops
Common charts for DevOps

* [aws-alb-ingress-controller](#aws-alb-ingress-controller): Kubernetes ingress resources by provisioning Application Load Balancers
* [cluster-autoscaler](#cluster-autoscaler): scales worker nodes within an AWS autoscaling group (ASG) or Spotinst Elastigroup.

# aws-alb-ingress-controller

* [src](https://github.com/helm/charts/tree/master/incubator/aws-alb-ingress-controller)

* modify `clusterName` in `aws-alb-ingress-controller.yaml`
* Add permissions to `NodeInstanceRole`
    ```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Action": [
                    "acm:DescribeCertificate",
                    "acm:ListCertificates",
                    "acm:GetCertificate",
                    "ec2:AuthorizeSecurityGroupIngress",
                    "ec2:CreateSecurityGroup",
                    "ec2:CreateTags",
                    "ec2:DeleteTags",
                    "ec2:DeleteSecurityGroup",
                    "ec2:DescribeAccountAttributes",
                    "ec2:DescribeAddresses",
                    "ec2:DescribeInstances",
                    "ec2:DescribeInstanceStatus",
                    "ec2:DescribeInternetGateways",
                    "ec2:DescribeNetworkInterfaces",
                    "ec2:DescribeSecurityGroups",
                    "ec2:DescribeSubnets",
                    "ec2:DescribeTags",
                    "ec2:DescribeVpcs",
                    "ec2:ModifyInstanceAttribute",
                    "ec2:ModifyNetworkInterfaceAttribute",
                    "ec2:RevokeSecurityGroupIngress",
                    "elasticloadbalancing:AddListenerCertificates",
                    "elasticloadbalancing:AddTags",
                    "elasticloadbalancing:CreateListener",
                    "elasticloadbalancing:CreateLoadBalancer",
                    "elasticloadbalancing:CreateRule",
                    "elasticloadbalancing:CreateTargetGroup",
                    "elasticloadbalancing:DeleteListener",
                    "elasticloadbalancing:DeleteLoadBalancer",
                    "elasticloadbalancing:DeleteRule",
                    "elasticloadbalancing:DeleteTargetGroup",
                    "elasticloadbalancing:DeregisterTargets",
                    "elasticloadbalancing:DescribeListenerCertificates",
                    "elasticloadbalancing:DescribeListeners",
                    "elasticloadbalancing:DescribeLoadBalancers",
                    "elasticloadbalancing:DescribeLoadBalancerAttributes",
                    "elasticloadbalancing:DescribeRules",
                    "elasticloadbalancing:DescribeSSLPolicies",
                    "elasticloadbalancing:DescribeTags",
                    "elasticloadbalancing:DescribeTargetGroups",
                    "elasticloadbalancing:DescribeTargetGroupAttributes",
                    "elasticloadbalancing:DescribeTargetHealth",
                    "elasticloadbalancing:ModifyListener",
                    "elasticloadbalancing:ModifyLoadBalancerAttributes",
                    "elasticloadbalancing:ModifyRule",
                    "elasticloadbalancing:ModifyTargetGroup",
                    "elasticloadbalancing:ModifyTargetGroupAttributes",
                    "elasticloadbalancing:RegisterTargets",
                    "elasticloadbalancing:RemoveListenerCertificates",
                    "elasticloadbalancing:RemoveTags",
                    "elasticloadbalancing:SetIpAddressType",
                    "elasticloadbalancing:SetSecurityGroups",
                    "elasticloadbalancing:SetSubnets",
                    "elasticloadbalancing:SetWebACL",
                    "iam:CreateServiceLinkedRole",
                    "iam:GetServerCertificate",
                    "iam:ListServerCertificates",
                    "waf-regional:GetWebACLForResource",
                    "waf-regional:GetWebACL",
                    "waf-regional:AssociateWebACL",
                    "waf-regional:DisassociateWebACL",
                    "tag:GetResources",
                    "tag:TagResources",
                    "waf:GetWebACL"
                ],
                "Resource": "*",
                "Effect": "Allow"
            }
        ]
    }
    ```
* install chart
   ```
   helm install incubator/aws-alb-ingress-controller \
     --file aws-alb-ingress-controller.yaml \
     --name aws-alb-ingress-controller \
     --namespace kube-system
   ```

# cluster-autoscaler

* [src](https://github.com/helm/charts/tree/master/stable/cluster-autoscaler)

* AWS

   * modify values in `cluster-autoscaler.yaml`

      * `autoDiscovery.clusterName`
      * `awsRegion`

   * Add permissions to `NodeInstanceRole`
        ```
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Action": [
                        "autoscaling:DescribeAutoScalingGroups",
                        "autoscaling:DescribeAutoScalingInstances",
                        "autoscaling:DescribeLaunchConfigurations",
                        "autoscaling:DescribeTags",
                        "autoscaling:SetDesiredCapacity",
                        "autoscaling:TerminateInstanceInAutoScalingGroup",
                        "ec2:DescribeLaunchTemplateVersions"
                    ],
                    "Resource": "*",
                    "Effect": "Allow"
                }
            ]
        }
        ```
   * install chart
        ```
        helm install incubator/cluster-autoscaler \
            --file cluster-autoscaler.yaml \
            --name cluster-autoscaler \
            --namespace kube-system
        ```

* GCP *TODO*

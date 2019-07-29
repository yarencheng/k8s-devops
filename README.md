# k8s-devops
Common charts for DevOps

* [aws-alb-ingress-controller](#aws-alb-ingress-controller): Kubernetes ingress resources by provisioning Application Load Balancers

# aws-alb-ingress-controller

1. modify `clusterName` in `aws-alb-ingress-controller.yaml`
2. install chart

   ```
   helm install incubator/aws-alb-ingress-controller --file aws-alb-ingress-controller.yaml
   ```

# Lab 04 - Cleanup

Duration: 15 mins

We deployed a lot of resources in these labs.  Clearly, you want to make sure they don't run up a bill from unused AWS resources.  This lab will help you clean up the resources you provisioned.



# The Nuclear Option
If you really want to stop AWS billing, close your AWS account.  If you've already stopped your active VMs and other cloud resources, you could still close your account to make very sure no additional charges are incurred.  Alternatively, in the rest of the lab, we'll walk through options that will allow you to continue to experiment and play with AWS.  But, if you prefer the nuclear approach, follow the instructions [here](https://aws.amazon.com/premiumsupport/knowledge-center/close-aws-account/).



# Cleaning up the resources

1. Delete K8s resources - Deployments

```
kubectl delete deploy redisbank-am-deployment redisbank-dg-deployment redisbank-pfm-deployment redisbank-tr-deployment redisbank-ui-deployment
```


2. Delete K8s resources - Ingress

```
kubectl delete ing redisbank-am-ingress redisbank-pfm-ingress redisbank-tr-ingress redisbank-ui-ingress
```


3. Delete K8s resources - Services

```
kubectl delete svc redisbank-am redisbank-pfm redisbank-tr redisbank-ui
```

4. Delete your EKS cluster.  Enter your student number.
This step may take up to 10 minutes.  This will also delete OIDC provider.

```
eksctl delete cluster <studentX>
```

The IAM service account and the policy can be deleted using the below commands. Please use your cluster name and your ploicy ARN.

```
eksctl delete iamserviceaccount --name aws-load-balancer-controller --cluster <CLUSTER-NAME> --namespace kube-system

aws iam delete-policy --policy-arn <AWSLoadBalancerControllerIAMPolicy-ARN>

```

5. Validate from AWS console by going to EKS and making sure the cluster is deleted.
Also check the nodes of the cluster are terminated. CloudFormation Template screen should have all resources deleted for the stacks that were used in the lab.
![](images/04-cleanup.png)

![](images/05-cleanup.png)

![](images/06-cleanup.png)

6. `Stack Info` tab indicates the status. In this case, its `DELETE_IN_PROGRESS`

![](images/06-cleanup.png)

7. Lets also delete the EC2 machine. Go to Ec2.

![](images/01-cleanup.png)

8. Terminate the instance.

![](images/02-cleanup.png)

![](images/03-cleanup.png)


You are pretty much done  [Go back](..)

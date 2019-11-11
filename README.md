Jupyter Notebooks with Docker on Windows 7  
==========================================
Abstract:
```
Although AWS EKS has been in GA for quite a while, and AWS EKS Fargate on the roadmap but not available yet,
it still requires a fair amount of manual effort to create the worker nodes and configure kubectl to talk to
the cluster.  In this QuickStart will build on CloudFormation scripts AWS has already provided to fully
automate the creation of the EKS Cluster.  We'll also use cloud-init and some basic shell scripts to configure
an EC2 instance with kubectl and configure it to talk to the cluster.  
```
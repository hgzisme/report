---
title: "Blog 1"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Streamline Machine Learning Workflows with SkyPilot on Amazon SageMaker HyperPod

by Roy Allela, Ankit Anand, and Zhanghao Wu | on July 11, 2025 | in [Amazon SageMaker HyperPod](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-hyperpod/), [Announcements](https://aws.amazon.com/blogs/machine-learning/category/post-types/announcements/) | [Permalink](https://aws.amazon.com/blogs/machine-learning/streamline-machine-learning-workflows-with-skypilot-on-amazon-sagemaker-hyperpod/) | [Comments](https://aws.amazon.com/blogs/machine-learning/streamline-machine-learning-workflows-with-skypilot-on-amazon-sagemaker-hyperpod/#Comments) | [Share](https://aws.amazon.com/blogs/machine-learning/streamline-machine-learning-workflows-with-skypilot-on-amazon-sagemaker-hyperpod/#)

This post is co-authored by Zhanghao Wu, co-creator of SkyPilot.

The rapid growth of generative AI and foundation models (FMs) has significantly increased the demand for compute resources for machine learning (ML) workloads. Modern ML workflows require efficient systems to distribute workloads across accelerated compute resources while keeping developer productivity high. Organizations need infrastructure solutions that are not only powerful but also flexible, resilient, and easy to manage.

[SkyPilot](https://docs.skypilot.co/en/latest/docs/index.html) is an *open-source* framework that simplifies running ML workloads by providing a unified abstraction layer, helping ML engineers run their workloads on various compute resources without managing the complexity of the underlying infrastructure. It provides a simple, high-level interface for provisioning resources, scheduling jobs, and managing distributed training across multiple nodes.

[Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker-ai/hyperpod/) is purpose-built infrastructure for developing and deploying large-scale FMs. SageMaker HyperPod not only provides the flexibility to create and use your own software stack but also delivers optimal performance through placing instances on the same spine, as well as built-in resiliency. Combining the resiliency of SageMaker HyperPod and the efficiency of SkyPilot provides a robust framework for scaling your generative AI workloads.

In this post, we share how SageMaker HyperPod, in collaboration with SkyPilot, is streamlining AI development workflows. This integration makes our advanced GPU infrastructure more accessible to ML engineers, thereby improving productivity and resource efficiency.

## Challenges in orchestrating machine learning workloads

[Kubernetes](https://kubernetes.io/) has become popular for ML workloads due to its scalability and rich ecosystem of *open-source* tools. SageMaker HyperPod orchestrated on [Amazon Elastic Kubernetes Service](https://aws.amazon.com/eks/) (Amazon EKS) combines the power of Kubernetes with the resilient environment of SageMaker HyperPod designed for training large models. Amazon EKS support in SageMaker HyperPod reinforces resiliency through deep health checks, automatic node recovery, and job auto-resume capabilities, providing uninterrupted training for large-scale, long-running jobs.

ML engineers transitioning from traditional VM environments or on-premises often face a steep learning curve. The complexity of Kubernetes manifest files and cluster management can pose significant challenges, potentially slowing down development cycles and resource utilization.

Furthermore, AI infrastructure teams face the challenge of balancing the need for advanced management tools with the desire to provide a user-friendly experience for their ML engineers. They require a solution that can offer both high-level control and ease of use for day-to-day operations.

## SageMaker HyperPod with SkyPilot

To address these challenges, we collaborated with SkyPilot to introduce a solution that leverages the strengths of both platforms. SageMaker HyperPod excels at managing the underlying compute resources and instances, providing the robust infrastructure needed for demanding AI workloads. SkyPilot complements this by offering an intuitive layer for job management, interactive development, and team orchestration.

Through this collaboration, we can offer our customers the best of both worlds: the robust, scalable infrastructure of SageMaker HyperPod, combined with a user-friendly interface that significantly reduces the learning curve for ML engineers. For AI infrastructure teams, this integration provides advanced management capabilities while simplifying the experience for their ML engineers, creating a win-win situation for all stakeholders.

SkyPilot helps AI teams run their workloads on different infrastructures with a unified high-level interface and powerful resource and job management capabilities. An AI engineer can bring their AI framework and specify the resource requirements for the job; SkyPilot intelligently schedules the workloads on the best infrastructure: finding available GPUs, provisioning GPUs, running the job, and managing its lifecycle.
![SkyPilot](/images/3-BlogsTranslated/3.1-Blog1/figure1.png)

## Solution overview

Deploying this solution is straightforward, whether you are working with existing SageMaker HyperPod clusters or setting up a new deployment. For existing clusters, you can connect using [AWS Command Line Interface](https://aws.amazon.com/cli/) (AWS CLI) commands to update the `kubeconfig` file and verify the setup. For new deployments, we will guide you through setting up the API server, creating clusters, and configuring high-performance networking options like Elastic Fabric Adapter (EFA).

The following diagram illustrates the solution architecture.
![SageMaker HyperPod](/images/3-BlogsTranslated/3.1-Blog1/figure2.png)

In the following sections, we will show you how to run SkyPilot jobs for multi-node distributed training on SageMaker HyperPod. We will walk through the process of creating a SageMaker HyperPod cluster, installing SkyPilot, creating a SkyPilot cluster, and deploying a SkyPilot training job.

### Prerequisites

You must have the following prerequisites:

  - An existing SageMaker HyperPod cluster with Amazon EKS (to create a new one, refer to [Deploy your HyperPod Cluster](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-hyperpod-gs-create-cluster.html)). You must provision a single `ml.p5.48xlarge` instance for the code snippets in the following sections.
  - Access to AWS CLI and `kubectl` command line tools.
  - A Python environment to install SkyPilot.

## Create a SageMaker HyperPod cluster

You can create an EKS cluster using a single [AWS CloudFormation](http://aws.amazon.com/cloudformation) stack as instructed in [using CloudFormation](https://catalog.us-east-1.prod.workshops.aws/workshops/2433d39e-ccfe-4c00-9d3d-9917b729258e), configured with a virtual private cloud (VPC) and storage resources.

To create and manage SageMaker HyperPod clusters, you can use the AWS Management Console or the AWS CLI. If you use the AWS CLI, specify the cluster configuration in a JSON file and select the EKS cluster created from the CloudFormation stack as the orchestrator for the SageMaker HyperPod cluster. Then, create the cluster's worker nodes with `NodeRecovery` set to `Automatic` to trigger automatic node recovery, and for `OnStartDeepHealthChecks`, include `InstanceStress` and `InstanceConnectivity` to enable deep health checks. See the following code:

```bash
cat > cluster-config.json <<EOL
{
    "ClusterName": "hp-cluster",
    "Orchestrator": {
        "Eks": {
            "ClusterArn": "${EKS_CLUSTER_ARN}"
        }
    },
    "InstanceGroups": [
        {
            "InstanceGroupName": "worker-group-1",
            "InstanceType": "ml.p5.48xlarge",
            "InstanceCount": 2,
            "LifeCycleConfig": {
                "SourceS3Uri": "s3://${BUCKET_NAME}",
                "OnCreate": "on_create.sh"
            },
            "ExecutionRole": "${EXECUTION_ROLE}",
            "ThreadsPerCore": 1,
            "OnStartDeepHealthChecks": [
                "InstanceStress",
                "InstanceConnectivity"
            ]
        }
    ],
    "VpcConfig": {
        "SecurityGroupIds": [
            "$SECURITY_GROUP"
        ],
        "Subnets": [
            "$SUBNET_ID"
        ]
    },
    "ResilienceConfig": {
        "NodeRecovery": "Automatic"
    }
}
EOL
```

You can add [InstanceStorageConfigs](https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_ClusterInstanceGroupSpecification.html#sagemaker-Type-ClusterInstanceGroupSpecification-InstanceStorageConfigs) to provision and attach additional [Amazon Elastic Block Store](http://aws.amazon.com/ebs) (Amazon EBS) volumes to the SageMaker HyperPod nodes.

To create the cluster using the [SageMaker HyperPod APIs](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-hyperpod-ref.html#sagemaker-hyperpod-ref-api), run the following AWS CLI command:

```bash
aws sagemaker create-cluster \
--cli-input-json file://cluster-config.json
```

You are now ready to set up SkyPilot on your SageMaker HyperPod cluster.

## Connect to the SageMaker HyperPod EKS cluster

From your AWS CLI environment, run the [aws eks update-kubeconfig](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/eks/update-kubeconfig.html) command to update your local `kube config` file (located at `~/.kube/config`) with the credentials and configuration required to connect to your EKS cluster using the `kubectl` command (provide your specific EKS cluster name):

```bash
aws eks update-kubeconfig --name $EKS_CLUSTER_NAME
```

You can verify that you are connected to the EKS cluster by running the following command:

```bash
kubectl config current-context
```

## Install SkyPilot with Kubernetes support

Use the following code to install SkyPilot with Kubernetes support using `pip`:

```bash
pip install skypilot[kubernetes]
```

This command installs the latest build of SkyPilot, including the necessary Kubernetes integrations.

## Verify SkyPilot connection to the EKS cluster

Check if SkyPilot can connect to your Kubernetes cluster:

```bash
sky check k8s
```

The output should look similar to the following code:

```
Checking credentials to enable clouds for SkyPilot.
Kubernetes: enabled [compute]

To enable a cloud, follow the hints above and rerun: sky check
If any problems remain, refer to detailed docs at: https://docs.skypilot.co/en/latest/getting-started/installation.html

🎉 Enabled clouds 🎉
Kubernetes [compute]
Active context: arn:aws:eks:us-east-2:XXXXXXXXXXXXX:cluster/sagemaker-hyperpod-eks-cluster

Using SkyPilot API server: http://127.0.0.1:46580
```

If this is your first time using SkyPilot with this Kubernetes cluster, you might see a prompt to create GPU labels for your nodes. Follow the instructions by running the following code:

```bash
python -m sky.utils.kubernetes.gpu_labeler --context <your-eks-context>
```

This script helps SkyPilot identify which GPU resources are available on each node in your cluster. The [GPU labeling task](https://docs.skypilot.co/en/latest/reference/kubernetes/kubernetes-setup.html#automatically-labelling-nodes) can take a few minutes depending on the number of GPU resources in your cluster.

## Discover available GPUs in the cluster

To view which GPU resources are available in your SageMaker HyperPod cluster, use the following code:

```bash
sky show-gpus --cloud k8s
```

This command lists the available GPU types and their counts. We have two `p5.48xlarge` instances, each equipped with 8 NVIDIA H100 GPUs:

```
Kubernetes GPUs
GPU REQUESTABLE_QTY_PER_NODE TOTAL_GPUS TOTAL_FREE_GPUS
H100 1, 2, 4, 8 16 16

Kubernetes per node accelerator availability
NODE_NAME GPU_NAME TOTAL_GPUS FREE_GPUS
hyperpod-i-00baa178bc31afde3 H100 8 8
hyperpod-i-038beefa954efab84 H100 8 8
```

## Launch an interactive development environment

With SkyPilot, you can launch a SkyPilot cluster for interactive development:

```bash
sky launch -c dev --gpus H100
```

This command creates an interactive development environment (IDE) with a single H100 GPU and syncs the local working directory to the cluster. SkyPilot handles pod creation, resource allocation, and IDE setup.

```
Considered resources (1 node):
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
 CLOUD        INSTANCE            vCPUs   Mem(GB)   ACCELERATORS   REGION/ZONE                                                            COST ($)   CHOSEN   
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Kubernetes   2CPU--8GB--H100:1   2       8         H100:1         arn:aws:eks:us-east-2:XXXXXXXXXX:cluster/sagemaker-hyperpod-eks-cluster   0.00           ✔     
------------------------------------------------------------------------------------------------------------------------------------------------------------------
Launching a new cluster 'dev'. Proceed? [Y/n]: Y
• Launching on Kubernetes.
Pod is up.
✔ Cluster launched: dev. View logs: sky api logs -1 sky-2025-05-05-15-28-47-523797/provision. log
• Syncing files.
Run commands not specified or empty.
Useful Commands
Cluster name: dey
To log into the head VM:   ssh dev
To submit a job:           sky exec dev yaml_file
To stop the cluster:       sky stop dev
To teardown the cluster:   sky down dev
```

After the launch is complete, you can connect to your IDE:

```bash
ssh dev
```

This command gives you an interactive shell inside the IDE, where you can run code, install packages, and perform ML experiments.

## Run training jobs

With SkyPilot, you can run distributed training jobs on your SageMaker HyperPod cluster. Here is an example of launching a distributed training job using a YAML configuration file.

First, create a file named `train.yaml` with your training job configuration:

```yaml
resources:
    accelerators: H100

num_nodes: 1

setup: |
    git clone --depth 1 https://github.com/pytorch/examples || true
    cd examples
    git filter-branch --prune-empty --subdirectory-filter distributed/minGPT-ddp
    # SkyPilot's default image on AWS/GCP has CUDA 11.6 (Azure 11.5).
    uv venv --python 3.10
    source .venv/bin/activate
    uv pip install -r requirements.txt "numpy<2" "torch"

run: |
    cd examples
    source .venv/bin/activate
    cd mingpt
    export LOGLEVEL=INFO

    MASTER_ADDR=$(echo "$SKYPILOT_NODE_IPS" | head -n1)
    echo "Starting distributed training, head node: $MASTER_ADDR"

    torchrun \
    --nnodes=$SKYPILOT_NUM_NODES \
    --nproc_per_node=$SKYPILOT_NUM_GPUS_PER_NODE \
    --master_addr=$MASTER_ADDR \
    --master_port=8008 \
    --node_rank=${SKYPILOT_NODE_RANK} \
    main.py
```

Then, launch your training job:

```bash
sky launch -c train train.yaml
```

This command creates a training job on a single `p5.48xlarge` node, equipped with 8 NVIDIA H100 GPUs. You can monitor the output using the following command:

```bash
sky logs train
```

## Run multi-node training jobs with EFA

Elastic Fabric Adapter (EFA) is a network interface for [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2/) (Amazon EC2) instances that enables you to run applications requiring high levels of inter-node communication at scale on AWS through a custom-built operating system bypass hardware interface. This allows applications to communicate directly with the network hardware while bypassing the operating system kernel, significantly reducing latency and CPU overhead. This direct hardware access is particularly beneficial for distributed ML workloads, where frequent inter-node communication during gradient synchronization can become a bottleneck. By using EFA-enabled instances like `p5.48xlarge` or `p6-b200.48xlarge`, data scientists can scale their training jobs across multiple nodes while maintaining the low-latency, high-bandwidth communication required for efficient distributed training, ultimately reducing training time and improving resource utilization for large-scale AI workloads.

The following code shows how to integrate this into your SkyPilot job:

```yaml
name: nccl-test-efa

resources:
  cloud: kubernetes
  accelerators: H100:8
  image_id: docker:public.ecr.aws/hpc-cloud/nccl-tests:latest

num_nodes: 2

envs:
  USE_EFA: "true"

run: |
  if [ "${SKYPILOT_NODE_RANK}" == "0" ]; then
    echo "Head node"

    # Total number of processes, NP should be the total number of GPUs in the cluster
    NP=$(($SKYPILOT_NUM_GPUS_PER_NODE * $SKYPILOT_NUM_NODES))

    # Append :${SKYPILOT_NUM_GPUS_PER_NODE} to each IP as slots
    nodes=""
    for ip in $SKYPILOT_NODE_IPS; do
      nodes="${nodes}${ip}:${SKYPILOT_NUM_GPUS_PER_NODE},"
    done
    nodes=${nodes::-1}
    echo "All nodes: ${nodes}"

    # Set environment variables
    export PATH=$PATH:/usr/local/cuda-12.2/bin:/opt/amazon/efa/bin:/usr/bin
    export LD_LIBRARY_PATH=/usr/local/cuda-12.2/lib64:/opt/amazon/openmpi/lib:/opt/nccl/build/lib:/opt/amazon/efa/lib:/opt/aws-ofi-nccl/install/lib:/usr/local/nvidia/lib:$LD_LIBRARY_PATH
    export NCCL_HOME=/opt/nccl
    export CUDA_HOME=/usr/local/cuda-12.2
    export NCCL_DEBUG=INFO
    export NCCL_BUFFSIZE=8388608
    export NCCL_P2P_NET_CHUNKSIZE=524288
    export NCCL_TUNER_PLUGIN=/opt/aws-ofi-nccl/install/lib/libnccl-ofi-tuner.so

    if [ "${USE_EFA}" == "true" ]; then
      export FI_PROVIDER="efa"
    else
      export FI_PROVIDER=""
    fi

    /opt/amazon/openmpi/bin/mpirun \
      --allow-run-as-root \
      --tag-output \
      -H $nodes \
      -np $NP \
      -N $SKYPILOT_NUM_GPUS_PER_NODE \
      --bind-to none \
      -x FI_PROVIDER \
      -x PATH \
      -x LD_LIBRARY_PATH \
      -x NCCL_DEBUG=INFO \
      -x NCCL_BUFFSIZE \
      -x NCCL_P2P_NET_CHUNKSIZE \
      -x NCCL_TUNER_PLUGIN \
      --mca pml ^cm,ucx \
      --mca btl tcp,self \
      --mca btl_tcp_if_exclude lo,docker0,veth_def_agent \
      /opt/nccl-tests/build/all_reduce_perf \
      -b 8 \
      -e 2G \
      -f 2 \
      -g 1 \
      -c 5 \
      -w 5 \
      -n 100
  else
    echo "Worker nodes"
  fi

config:
  kubernetes:
    pod_config:
      spec:
        containers:
        - resources:
            limits:
              vpc.amazonaws.com/efa: 32
            requests:
              vpc.amazonaws.com/efa: 32
```

## Clean up

To remove your SkyPilot cluster, run the following command:

```bash
sky down <cluster_name>
```

To delete the SageMaker HyperPod cluster created in this post, you can use the SageMaker AI console or the following AWS CLI command:

```bash
aws sagemaker delete-cluster --cluster-name <cluster_name>
```

Deleting the cluster will take a few minutes. You can confirm successful deletion when you no longer see the cluster on the SageMaker AI console.

If you used the CloudFormation stack to create resources, you can delete it with the following command:

```bash
aws cloudformation delete-stack --stack-name <stack_name>
```

## Conclusion

By combining the robust infrastructure capabilities of SageMaker HyperPod with the user-friendly interface of SkyPilot, we have introduced a solution that helps teams focus on innovation rather than infrastructure complexity. This approach not only simplifies operations but also enhances productivity and resource efficiency for organizations of all sizes. To get started, refer to [SkyPilot](https://catalog.us-east-1.prod.workshops.aws/workshops/2433d39e-ccfe-4c00-9d3d-9917b729258e/en-US/12-skypilot) in the [Amazon EKS Support on Amazon SageMaker HyperPod workshop](https://catalog.us-east-1.prod.workshops.aws/workshops/2433d39e-ccfe-4c00-9d3d-9917b729258e/en-US/12-skypilot).

## About the authors

**Roy Allela** is a Senior Solutions Architect specializing in AI/ML at AWS. He helps AWS customers—from small startups to large enterprises—train and deploy foundation models efficiently on AWS. He is passionate about computational optimization problems and improving the performance of AI workloads.

**Zhanghao Wu** is the co-creator of the *open-source* SkyPilot project and holds a PhD in computer science from UC Berkeley. He works on the SkyPilot core, client-server architecture, managed jobs, and generally improving the AI experience across diverse cloud infrastructures.

**Ankit Anand** is a Senior Product Marketing Manager (GTM) for Foundation Models at AWS. He collaborates with top generative AI model builders, strategic customers, and AWS service teams to support the deployment of the next generation of AI/ML workloads on AWS. Ankit's experience includes product management expertise in the financial services industry for high-frequency and low-latency trading, as well as business development for Amazon Alexa.

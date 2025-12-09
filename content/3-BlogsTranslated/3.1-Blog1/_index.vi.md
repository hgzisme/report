---
title: "Blog 1"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Tối ưu hóa quy trình học máy với SkyPilot trên Amazon SageMaker HyperPod

bởi Roy Allela, Ankit Anand, và Zhanghao Wu | vào ngày 11 tháng 7 năm 2025 | trong [Amazon SageMaker HyperPod](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-hyperpod/), [Thông báo](https://aws.amazon.com/blogs/machine-learning/category/post-types/announcements/) | [Liên kết cố định](https://aws.amazon.com/blogs/machine-learning/streamline-machine-learning-workflows-with-skypilot-on-amazon-sagemaker-hyperpod/) | [Bình luận](https://aws.amazon.com/blogs/machine-learning/streamline-machine-learning-workflows-with-skypilot-on-amazon-sagemaker-hyperpod/#Comments) | [Chia sẻ](https://aws.amazon.com/blogs/machine-learning/streamline-machine-learning-workflows-with-skypilot-on-amazon-sagemaker-hyperpod/#)

Bài viết này được đồng tác giả bởi Zhanghao Wu, người đồng sáng tạo SkyPilot.

Sự phát triển nhanh chóng của AI tạo sinh và các mô hình nền tảng (FMs) đã làm tăng đáng kể yêu cầu về tài nguyên tính toán cho các tác vụ máy học (ML). Các quy trình ML hiện đại đòi hỏi các hệ thống hiệu quả để phân phối tác vụ trên các tài nguyên tính toán tăng tốc, đồng thời đảm bảo năng suất của nhà phát triển luôn ở mức cao. Các tổ chức cần những giải pháp cơ sở hạ tầng không chỉ mạnh mẽ mà còn linh hoạt, bền bỉ và dễ dàng quản lý.

[SkyPilot](https://docs.skypilot.co/en/latest/docs/index.html) là một framework *mã nguồn mở* giúp đơn giản hóa việc chạy các tác vụ ML bằng cách cung cấp một lớp trừu tượng hóa hợp nhất, giúp các kỹ sư ML chạy tác vụ của họ trên các tài nguyên tính toán khác nhau mà không cần quản lý sự phức tạp của cơ sở hạ tầng bên dưới. Nó cung cấp một giao diện cấp cao, đơn giản để cấp phát tài nguyên, lên lịch cho các công việc và quản lý việc huấn luyện phân tán trên nhiều nodes.

[Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker-ai/hyperpod/) là một cơ sở hạ tầng được xây dựng chuyên dụng để phát triển và triển khai các FM quy mô lớn. SageMaker HyperPod không chỉ cung cấp sự linh hoạt để tạo và sử dụng ngăn xếp phần mềm của riêng bạn, mà còn mang lại hiệu suất tối ưu thông qua việc đặt các instance trên cùng một spine, cũng như khả năng phục hồi tích hợp sẵn. Việc kết hợp khả năng phục hồi của SageMaker HyperPod và hiệu quả của SkyPilot cung cấp một framework mạnh mẽ để mở rộng quy mô các tác vụ AI tạo sinh của bạn.

Trong bài viết này, chúng tôi chia sẻ cách SageMaker HyperPod, hợp tác cùng SkyPilot, đang tối ưu hóa các quy trình phát triển AI. Sự tích hợp này giúp cơ sở hạ tầng GPU tiên tiến của chúng tôi dễ tiếp cận hơn đối với các kỹ sư ML, qua đó nâng cao năng suất và hiệu quả sử dụng tài nguyên.

## Thách thức trong việc điều phối các tác vụ máy học

[Kubernetes](https://kubernetes.io/) đã trở nên phổ biến cho các tác vụ ML nhờ khả năng mở rộng và bộ công cụ *mã nguồn mở* phong phú. SageMaker HyperPod được điều phối trên [Amazon Elastic Kubernetes Service](https://aws.amazon.com/eks/) (Amazon EKS) kết hợp sức mạnh của Kubernetes với môi trường bền bỉ của SageMaker HyperPod được thiết kế để huấn luyện các mô hình lớn. Hỗ trợ Amazon EKS trong SageMaker HyperPod củng cố khả năng phục hồi thông qua việc kiểm tra sức khỏe sâu, phục hồi nodes tự động và khả năng tự động tiếp tục job, cung cấp quá trình huấn luyện không bị gián đoạn cho các job quy mô lớn và chạy trong thời gian dài.

Các kỹ sư ML chuyển đổi từ môi trường VM truyền thống hoặc tại chỗ thường phải đối mặt với một quá trình học hỏi khó khăn. Sự phức tạp của các tệp manifest và việc quản lý cụm của Kubernetes có thể đặt ra những thách thức đáng kể, có khả năng làm chậm chu kỳ phát triển và việc sử dụng tài nguyên.

Hơn nữa, các đội ngũ cơ sở hạ tầng AI phải đối mặt với thách thức trong việc cân bằng giữa nhu cầu về các công cụ quản lý tiên tiến với mong muốn cung cấp trải nghiệm thân thiện với người dùng cho các kỹ sư ML của họ. Họ yêu cầu một giải pháp có thể cung cấp cả khả năng kiểm soát ở cấp độ cao và sự dễ sử dụng cho các hoạt động hàng ngày.

## SageMaker HyperPod với SkyPilot

Để giải quyết những thách thức này, chúng tôi đã hợp tác với SkyPilot để giới thiệu một giải pháp tận dụng thế mạnh của cả hai nền tảng. SageMaker HyperPod vượt trội trong việc quản lý các tài nguyên tính toán và instance cơ bản, cung cấp cơ sở hạ tầng mạnh mẽ cần thiết cho các tác vụ AI đòi hỏi cao. SkyPilot bổ sung cho điều này bằng cách cung cấp một lớp trực quan để quản lý job, phát triển tương tác và điều phối nhóm.

Thông qua sự hợp tác này, chúng tôi có thể mang đến cho khách hàng của mình những ưu điểm tốt nhất của cả hai thế giới: cơ sở hạ tầng mạnh mẽ, có khả năng mở rộng của SageMaker HyperPod, kết hợp với giao diện thân thiện với người dùng giúp giảm đáng kể quá trình học hỏi cho các kỹ sư ML. Đối với các đội ngũ cơ sở hạ tầng AI, sự tích hợp này cung cấp khả năng quản lý tiên tiến đồng thời đơn giản hóa trải nghiệm cho các kỹ sư ML của họ, tạo ra một tình huống đôi bên cùng có lợi cho tất cả các bên liên quan.

SkyPilot giúp các đội ngũ AI chạy tác vụ của họ trên các cơ sở hạ tầng khác nhau với một giao diện cấp cao hợp nhất và khả năng quản lý tài nguyên và job mạnh mẽ. Một kỹ sư AI có thể mang framework AI của họ vào và chỉ định các yêu cầu tài nguyên cho job; SkyPilot sẽ lên lịch một cách thông minh cho các tác vụ trên cơ sở hạ tầng tốt nhất: tìm các GPU có sẵn, cấp phát GPU, chạy job và quản lý vòng đời của nó.
![SkyPilot](/images/3-BlogsTranslated/3.1-Blog1/figure1.png)

## Tổng quan về giải pháp

Việc triển khai giải pháp này rất đơn giản, cho dù bạn đang làm việc với các cụm SageMaker HyperPod hiện có hay thiết lập một triển khai mới. Đối với các cụm hiện có, bạn có thể kết nối bằng các lệnh của [Giao diện Dòng lệnh AWS](https://aws.amazon.com/cli/) (AWS CLI) để cập nhật tệp `kubeconfig` và xác minh thiết lập. Đối với các triển khai mới, chúng tôi sẽ hướng dẫn bạn cách thiết lập máy chủ API, tạo các cụm, và cấu hình các tùy chọn mạng hiệu suất cao như Elastic Fabric Adapter (EFA).

Sơ đồ sau đây minh họa kiến trúc của giải pháp.
![SageMaker HyperPod](/images/3-BlogsTranslated/3.1-Blog1/figure2.png)

Trong các phần tiếp theo, chúng tôi sẽ chỉ cho bạn cách chạy các job của SkyPilot cho việc huấn luyện phân tán nhiều nodes trên SageMaker HyperPod. Chúng ta sẽ đi qua quy trình tạo một cụm SageMaker HyperPod, cài đặt SkyPilot, tạo một cụm SkyPilot, và triển khai một job huấn luyện của SkyPilot.

### Yêu cầu tiên quyết

Bạn phải có các yêu cầu tiên quyết sau:

-   Một cụm SageMaker HyperPod hiện có với Amazon EKS (để tạo mới, hãy tham khảo [Triển khai Cụm HyperPod của bạn](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-hyperpod-gs-create-cluster.html)). Bạn phải cấp phát một instance `ml.p5.48xlarge` duy nhất cho các đoạn mã mẫu trong các phần sau.
-   Quyền truy cập vào các công cụ dòng lệnh AWS CLI và `kubectl`.
-   Một môi trường Python để cài đặt SkyPilot.

## Tạo một cụm SageMaker HyperPod

Bạn có thể tạo một cụm EKS bằng một stack [AWS CloudFormation](http://aws.amazon.com/cloudformation) duy nhất theo hướng dẫn trong [sử dụng CloudFormation](https://catalog.us-east-1.prod.workshops.aws/workshops/2433d39e-ccfe-4c00-9d3d-9917b729258e), được cấu hình với một đám mây riêng ảo (VPC) và các tài nguyên lưu trữ.

Để tạo và quản lý các cụm SageMaker HyperPod, bạn có thể sử dụng AWS Management Console hoặc AWS CLI. Nếu bạn sử dụng AWS CLI, hãy chỉ định cấu hình cụm trong một tệp JSON và chọn cụm EKS được tạo từ stack CloudFormation làm trình điều phối (orchestrator) cho cụm SageMaker HyperPod. Sau đó, bạn tạo các nodes worker của cụm với `NodeRecovery` được đặt thành `Automatic` để kích hoạt tính năng phục hồi nodes tự động, và đối với `OnStartDeepHealthChecks`, hãy thêm `InstanceStress` và `InstanceConnectivity` để bật tính năng kiểm tra sức khỏe sâu. Xem đoạn mã sau:

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

Bạn có thể thêm [InstanceStorageConfigs](https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_ClusterInstanceGroupSpecification.html#sagemaker-Type-ClusterInstanceGroupSpecification-InstanceStorageConfigs) để cấp phát và gắn các volume [Amazon Elastic Block Store](http://aws.amazon.com/ebs) (Amazon EBS) bổ sung vào các nodes của SageMaker HyperPod.

Để tạo cụm bằng cách sử dụng các [SageMaker HyperPod APIs](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-hyperpod-ref.html#sagemaker-hyperpod-ref-api), hãy chạy lệnh AWS CLI sau đây:

```bash
aws sagemaker create-cluster \
--cli-input-json file://cluster-config.json
```

Bây giờ bạn đã sẵn sàng để thiết lập SkyPilot trên cụm SageMaker HyperPod của mình.

## Kết nối đến cụm EKS của SageMaker HyperPod

Từ môi trường AWS CLI của bạn, hãy chạy lệnh [aws eks update-kubeconfig](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/eks/update-kubeconfig.html) để cập nhật tệp `kube config` cục bộ của bạn (nằm tại `~/.kube/config`) với thông tin xác thực và cấu hình cần thiết để kết nối đến cụm EKS của bạn bằng lệnh `kubectl` (hãy cung cấp tên cụm EKS cụ thể của bạn):

```bash
aws eks update-kubeconfig --name $EKS_CLUSTER_NAME
```

Bạn có thể xác minh rằng mình đã kết nối với cụm EKS bằng cách chạy lệnh sau:

```bash
kubectl config current-context
```

## Cài đặt SkyPilot với hỗ trợ Kubernetes

Sử dụng đoạn mã sau để cài đặt SkyPilot với hỗ trợ Kubernetes bằng `pip`:

```bash
pip install skypilot[kubernetes]
```

Lệnh này sẽ cài đặt bản dựng mới nhất của SkyPilot, bao gồm các tích hợp Kubernetes cần thiết.

## Xác minh kết nối của SkyPilot đến cụm EKS

Kiểm tra xem SkyPilot có thể kết nối đến cụm Kubernetes của bạn hay không:

```bash
sky check k8s
```

Đầu ra sẽ trông tương tự như đoạn mã sau:

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

Nếu đây là lần đầu tiên bạn sử dụng SkyPilot với cụm Kubernetes này, bạn có thể thấy một lời nhắc yêu cầu tạo nhãn GPU (GPU labels) cho các nodes của bạn. Hãy làm theo hướng dẫn bằng cách chạy đoạn mã sau:

```bash
python -m sky.utils.kubernetes.gpu_labeler --context <your-eks-context>
```

Script này giúp SkyPilot xác định những tài nguyên GPU nào đang có sẵn trên mỗi nodes trong cụm của bạn. [Tác vụ gán nhãn GPU](https://docs.skypilot.co/en/latest/reference/kubernetes/kubernetes-setup.html#automatically-labelling-nodes) có thể mất vài phút tùy thuộc vào số lượng tài nguyên GPU trong cụm của bạn.

## Khám phá các GPU có sẵn trong cụm

Để xem những tài nguyên GPU nào có sẵn trong cụm SageMaker HyperPod của bạn, hãy sử dụng đoạn mã sau:

```bash
sky show-gpus --cloud k8s
```

Lệnh này sẽ liệt kê các loại GPU có sẵn và số lượng của chúng. Chúng ta có hai instance `p5.48xlarge`, mỗi instance được trang bị 8 GPU NVIDIA H100:

```
Kubernetes GPUs
GPU REQUESTABLE_QTY_PER_NODE TOTAL_GPUS TOTAL_FREE_GPUS
H100 1, 2, 4, 8 16 16

Kubernetes per node accelerator availability
NODE_NAME GPU_NAME TOTAL_GPUS FREE_GPUS
hyperpod-i-00baa178bc31afde3 H100 8 8
hyperpod-i-038beefa954efab84 H100 8 8
```

## Khởi chạy một môi trường phát triển tương tác

Với SkyPilot, bạn có thể khởi chạy một cụm SkyPilot cho việc phát triển tương tác:

```bash
sky launch -c dev --gpus H100
```

Lệnh này tạo ra một môi trường phát triển tương tác (IDE) với một GPU H100 duy nhất và sẽ đồng bộ hóa thư mục làm việc cục bộ với cụm. SkyPilot xử lý việc tạo pod, phân bổ tài nguyên, và thiết lập IDE.

```
Considered resources (1 node):
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
 CLOUD        INSTANCE            vCPUs   Mem(GB)   ACCELERATORS   REGION/ZONE                                                                 COST ($)   CHOSEN   
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Kubernetes   2CPU--8GB--H100:1   2       8         H100:1         arn:aws:eks:us-east-2:XXXXXXXXXX:cluster/sagemaker-hyperpod-eks-cluster   0.00          ✔     
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

Sau khi khởi chạy xong, bạn có thể kết nối đến IDE của mình:

```bash
ssh dev
```

Lệnh này cung cấp cho bạn một trình bao tương tác (*interactive shell*) trong IDE, nơi bạn có thể chạy mã, cài đặt các gói, và thực hiện các thí nghiệm ML.

## Chạy các job huấn luyện

Với SkyPilot, bạn có thể chạy các job huấn luyện phân tán trên cụm SageMaker HyperPod của mình. Sau đây là một ví dụ về việc khởi chạy một job huấn luyện phân tán bằng tệp cấu hình YAML.

Đầu tiên, tạo một tệp có tên là `train.yaml` với cấu hình job huấn luyện của bạn:

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

Sau đó, khởi chạy job huấn luyện của bạn:

```bash
sky launch -c train train.yaml
```

Lệnh này tạo ra một job huấn luyện trên một nodes `p5.48xlarge` duy nhất, được trang bị 8 GPU NVIDIA H100. Bạn có thể theo dõi đầu ra bằng lệnh sau:

```bash
sky logs train
```

## Chạy các job huấn luyện đa nodes với EFA

Elastic Fabric Adapter (EFA) là một giao diện mạng cho các instance [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2/) (Amazon EC2) cho phép bạn chạy các ứng dụng đòi hỏi mức độ giao tiếp liên nodes (*inter-node communication*) cao ở quy mô lớn trên AWS thông qua giao diện phần cứng bỏ qua hệ điều hành (*operating system bypass*) được xây dựng riêng. Điều này cho phép các ứng dụng giao tiếp trực tiếp với phần cứng mạng trong khi bỏ qua nhân hệ điều hành, giúp giảm đáng kể độ trễ và chi phí CPU. Việc truy cập phần cứng trực tiếp này đặc biệt có lợi cho các tác vụ ML phân tán, nơi mà việc giao tiếp liên nodes thường xuyên trong quá trình đồng bộ hóa gradient có thể trở thành một điểm nghẽn. Bằng cách sử dụng các instance hỗ trợ EFA như `p5.48xlarge` hoặc `p6-b200.48xlarge`, các nhà khoa học dữ liệu có thể mở rộng quy mô các job huấn luyện của họ trên nhiều nodes trong khi vẫn duy trì giao tiếp có độ trễ thấp, băng thông cao cần thiết cho việc huấn luyện phân tán hiệu quả, và cuối cùng là giảm thời gian huấn luyện và cải thiện việc sử dụng tài nguyên cho các tác vụ AI quy mô lớn.

Đoạn mã sau đây cho thấy cách tích hợp điều này vào job SkyPilot của bạn:

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

## Dọn dẹp

Để xóa cụm SkyPilot của bạn, hãy chạy lệnh sau:

```bash
sky down <cluster_name>
```

Để xóa cụm SageMaker HyperPod đã tạo trong bài viết này, bạn có thể sử dụng SageMaker AI console hoặc lệnh AWS CLI sau:

```bash
aws sagemaker delete-cluster --cluster-name <cluster_name>
```

Việc xóa cụm sẽ mất vài phút. Bạn có thể xác nhận việc xóa thành công sau khi không còn thấy cụm nào trên SageMaker AI console.

Nếu bạn đã sử dụng stack CloudFormation để tạo tài nguyên, bạn có thể xóa nó bằng lệnh sau:

```bash
aws cloudformation delete-stack --stack-name <stack_name>
```

## Kết luận

Bằng cách kết hợp khả năng cơ sở hạ tầng mạnh mẽ của SageMaker HyperPod với giao diện thân thiện với người dùng của SkyPilot, chúng tôi đã giới thiệu một giải pháp giúp các đội ngũ tập trung vào sự đổi mới thay vì sự phức tạp của cơ sở hạ tầng. Cách tiếp cận này không chỉ đơn giản hóa các hoạt động mà còn nâng cao năng suất và hiệu quả sử dụng tài nguyên cho các tổ chức ở mọi quy mô. Để bắt đầu, hãy tham khảo [SkyPilot](https://catalog.us-east-1.prod.workshops.aws/workshops/2433d39e-ccfe-4c00-9d3d-9917b729258e/en-US/12-skypilot) trong [workshop Hỗ trợ Amazon EKS trên Amazon SageMaker HyperPod](https://catalog.us-east-1.prod.workshops.aws/workshops/2433d39e-ccfe-4c00-9d3d-9917b729258e/en-US/12-skypilot).

## Về các tác giả
**Roy Allela** là Kiến trúc sư giải pháp cao cấp chuyên về AI/ML tại AWS. Anh giúp đỡ các khách hàng của AWS—từ các công ty khởi nghiệp nhỏ đến các doanh nghiệp lớn—huấn luyện và triển khai các mô hình nền tảng một cách hiệu quả trên AWS. Anh có đam mê về các bài toán tối ưu hóa tính toán và cải thiện hiệu suất của các tác vụ AI.

**Zhanghao Wu** là người đồng sáng tạo dự án *mã nguồn mở* SkyPilot và có bằng Tiến sĩ ngành khoa học máy tính từ UC Berkeley. Anh làm việc trên lõi SkyPilot, kiến trúc client-server, các job được quản lý, và nhìn chung là cải thiện trải nghiệm AI trên các cơ sở hạ tầng đám mây đa dạng.

**Ankit Anand** là Chuyên gia Cao cấp về Tiếp thị sản phẩm (GTM) cho các Mô hình Nền tảng tại AWS. Anh hợp tác với các nhà xây dựng mô hình AI tạo sinh hàng đầu, các khách hàng chiến lược, và các đội ngũ dịch vụ của AWS để hỗ trợ triển khai thế hệ tiếp theo của các tác vụ AI/ML trên AWS. Kinh nghiệm của Ankit bao gồm chuyên môn quản lý sản phẩm trong ngành dịch vụ tài chính cho mảng giao dịch tần suất cao và độ trễ thấp, cũng như phát triển kinh doanh cho Amazon Alexa.
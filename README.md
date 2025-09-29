### What is Apache Spark?
Apache Spark is an open-source, distributed processing system designed for fast and general-purpose big data workloads. It is a unified analytics engine that can handle various types of data processing, including batch processing, real-time analytics, machine learning, and graph processing, within a single framework. 
Key characteristics and features of Apache Spark:

- **Speed**: Spark utilizes in-memory caching and optimized query execution, allowing it to process data significantly faster than older, disk-based systems like Hadoop MapReduce.
- **Ease of Use**: It provides user-friendly APIs in multiple programming languages, including Java, Scala, Python, and R, making it accessible to a wide range of developers.
- **Unified Engine**: Spark's core engine is complemented by several higher-level libraries, such as Spark SQL for structured data, MLlib for machine learning, Spark Streaming for real-time data streams, and GraphX for graph processing. These libraries can be combined to build complex data workflows. 
- **Distributed Processing**: Spark distributes massive computing tasks across a cluster of machines, breaking them down into smaller, parallelizable tasks for efficient processing.
- **Fault Tolerance**: It employs a resilient distributed dataset (RDD) model and a Directed Acyclic Graph (DAG) scheduler to ensure fault tolerance and efficient task execution across the cluster.
- **Flexibility**: Spark can run on various cluster managers, including Apache Hadoop YARN, Apache Mesos, Kubernetes, or in standalone mode, and can process data from diverse sources.

In essence, Apache Spark provides a powerful and flexible platform for handling large-scale data analytics and machine learning tasks with high performance and ease of development.


### What is the purpose of  this Ansible Playbook?
It is Ansible Playbook to deploy Apache Spark conveniently on Baremetal, Virtual Machines and Cloud Infrastructure.
The main purpose of this project is actually very simple. Because i have many jobs to install different kind of Apache Spark versions and reproduce issues & test features as a support
engineer. I just want to spend less time for it.

### The Architecture of Apache Spark
<p align="center">
<img src="https://github.com/rokmc756/Apache-Spark/blob/main/roles/spark/images/spark-cluster-overview.webp" width="80%" height="80%">
</p>


### Configure Varialbes such as Download Location, Versions, Install/Config Path, Informations
$ vi group_vars/all.yml
```yaml
~~ snip
_spark:
  worker:
    core: 6
    memory: "6G"
    default_core: 4
  download: false
  firewall: false
  user: "{{ _hadoop.user }}"
  group: "{{ _hadoop.group }}"
  major_version: 3
  minor_version: 5
  patch_version: 4
  bin_type: tgz
  download_url: "https://archive.apache.org/dist/spark"
  base_path: "{{ _hadoop.base_path }}"
  master_work_port: 7077
  worker_work_port: 7078
  master_ui_port: 8080
  worker_ui_port: 8081
  net:
    type: "virtual"                # Or Physical
    gateway: "192.168.0.1"
    ipaddr0: "192.168.0.19"
    ipaddr1: "192.168.1.19"
    ipaddr2: "192.168.2.19"
~~ snip
```

### Install or Deploy Spark
```yaml
$ make spark r=setup   s=bin
$ make spark r=config  s=cluster
$ make spark r=start   s=cluster

or
$ make spark r=install s=all
```

### Uninstall or Destroy Spark
```yaml
$ make spark r=stop   s=cluster
$ make spark r=delete s=bin

or
$ make spark r=uninstall s=all
```


## References
https://sparkbyexamples.com/



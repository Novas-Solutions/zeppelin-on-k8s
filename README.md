Introduction: 

    The Zeppelin, Spark and  Kubernetes importance and use cases are available briefly on the official website. Please refer to the below URL for the same.

    https://zeppelin.apache.org/docs/0.10.0/quickstart/kubernetes.html

 Flow Diagram: 

    https://lucid.app/lucidchart/74cdd090-afdc-4ca8-a5f8-63bdc89d2079/edit?viewport_loc=-149%2C37%2C1365%2C687%2C0_0&invitationId=inv_df25a0f9-9cd4-441a-9d86-5da36590e078


Key benefits of Spark + Zeppelin + Kubernetes are
    Horizontally scalable. (both Spark executors and Zeppelin interpreters)
    On-demand Spark cluster creation by running a notebook
    Super easy maintenance.
    Pre-requisite: 
    
        1. Kubernetes Cluster (on-premise, Cloud, Hybrid)

        2. Container runtime executor (docker)

        3. container registry

Steps

    1. Create the Kubernetes cluster on-premise or you can continue to Kubernetes as a Service. 

    2. Download OR clone the zeppelin source code repo. 
    # git clone https://github.com/Ntech-labs/zeppelin-on-k8s.git

    3. Create container image using docker for spark-application and zeppelin. The official docker image isn't compactible with the k8s cluster.

    # docker build -t zeppelin-server:0.10.0 -f /scripts/docker/zeppelin-server/Dockerfile
    # docker tag zeppelin-server:0.10.0 container-registry.com/zeppelin-server:0.10.0 && docker push container-registry.com/zeppelin-server:0.10.0

    # docker build -t zeppelin-interpreter:0.10.0 -f /scripts/docker/zeppelin-interpreter/Dockerfile
    # docker tag zeppelin-interpreter:0.10.0 container-registry.com/zeppelin-server:0.10.0 && docker push container-registry.com/zeppelin-interpreter:0.10.0

    # docker build -t spark-app:3.2.0 -f spark.Dockerfile
    # docker tag spark-app:3.2.0 container-registry.com/spark-app:3.2.0 && docker push container-registry.com/spark-app:3.2.0 

    4. Deploy the zeppelin on Kubernetes. 

    Before deploying kindly change the below content of the deployment file.
    A. Container-Images enpoints 
    B. Storage-class Name
    C. Remove the PVC section (If you are using static storage provisioning).
    D. Change the SERVICE_DOMAIN value: respective of the your ingress domain configuration

    # kubectl create -f k8s/zeppelin-server.yaml 




#### README from the OFFICIAL source.

# Apache Zeppelin

**Documentation:** [User Guide](https://zeppelin.apache.org/docs/latest/index.html)<br/>
**Mailing Lists:** [User and Dev mailing list](https://zeppelin.apache.org/community.html)<br/>
**Continuous Integration:** ![core](https://github.com/apache/zeppelin/workflows/core/badge.svg) ![frontend](https://github.com/apache/zeppelin/workflows/frontend/badge.svg) ![rat](https://github.com/apache/zeppelin/workflows/rat/badge.svg) <br/>
**Contributing:** [Contribution Guide](https://zeppelin.apache.org/contribution/contributions.html)<br/>
**Issue Tracker:** [Jira](https://issues.apache.org/jira/browse/ZEPPELIN)<br/>
**License:** [Apache 2.0](https://github.com/apache/zeppelin/blob/master/LICENSE)


**Zeppelin**, a web-based notebook that enables interactive data analytics. You can make beautiful data-driven, interactive and collaborative documents with SQL, Scala and more.

Core features:
   * Web based notebook style editor.
   * Built-in Apache Spark support


To know more about Zeppelin, visit our web site [https://zeppelin.apache.org](https://zeppelin.apache.org)


## Getting Started

### Install binary package
Please go to [install](https://zeppelin.apache.org/docs/latest/quickstart/install.html) to install Apache Zeppelin from binary package.

### Build from source
Please check [Build from source](https://zeppelin.apache.org/docs/latest/setup/basics/how_to_build.html) to build Zeppelin from source.

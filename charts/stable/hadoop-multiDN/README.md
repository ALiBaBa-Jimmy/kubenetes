# Hadoop Chart

[Hadoop](https://hadoop.apache.org/) is a framework for running large scale distributed applications.

This chart is primarily intended to be used for YARN and MapReduce job execution where HDFS is just used as a means to transport small artifacts within the framework and not for a distributed filesystem. Data should be read from cloud based datastores such as Google Cloud Storage, S3 or Swift.

## Chart Details

## Installing the Chart

Usage:

```
$ helm install --name hadoop $(stable/hadoop/tools/calc_resources.sh 50) stable/hadoop
```

> Note that you need at least 2GB of free memory per NodeManager pod, if your cluster isn't large enough, not all pods will be scheduled.


> Change the value of `storageClass` to match your volume driver. `standard` works for Google Container Engine clusters.

## Configuration

The following table lists the configurable parameters of the Hadoop chart and their default values.

| Parameter                                      | Description                                                                        | Default                                                          |
| -----------------------------------------------| -------------------------------                                                    | ---------------------------------------------------------------- |
| `image`                                        | Hadoop image ([source](https://github.com/Comcast/kube-yarn/tree/master/image))    | `mirror.jd.com/neo/hadoop:2.7.3`                                 |
| `imagePullPolicy`                              | Pull policy for the images                                                         | `IfNotPresent`                                                   |
| `hadoopVersion`                                | Version of hadoop libraries being used                                             | `2.7.3`                                                          |
| `antiAffinity`                                 | Pod antiaffinity, `hard` or `soft`                                                 | `soft`                                                           |
| `k8sDomain`                                    | your cluster domain                                                                | `dev.k8s.ovs.jd.local`                                           |
| `hdfs.nameNode.pdbMinAvailable`                | PDB for HDFS NameNode                                                              | `1`                                                              |
| `hdfs.nameNode.resources`                      | resources for the HDFS NameNode                                                    | `requests:memory=256Mi,cpu=10m,limits:memory=2048Mi,cpu=1000m`   |
| `hdfs.dataNode.replicas`                       | Number of HDFS DataNode replicas                                                   | `1`                                                              |
| `hdfs.dataNode.pdbMinAvailable`                | PDB for HDFS DataNode                                                              | `1`                                                              |
| `hdfs.dataNode.resources`                      | resources for the HDFS DataNode                                                    | `requests:memory=256Mi,cpu=10m,limits:memory=2048Mi,cpu=1000m`   |
| `yarn.resourceManager.pdbMinAvailable`         | PDB for the YARN ResourceManager                                                   | `1`                                                              |
| `yarn.resourceManager.resources`               | resources for the YARN ResourceManager                                             | `requests:memory=256Mi,cpu=10m,limits:memory=2048Mi,cpu=1000m`   |
| `yarn.nodeManager.pdbMinAvailable`             | PDB for the YARN NodeManager                                                       | `1`                                                              |
| `yarn.nodeManager.replicas`                    | Number of YARN NodeManager replicas                                                | `1`                                                              |
| `yarn.nodeManager.parallelCreate`              | Create all nodeManager statefulset pods in parallel (K8S 1.7+)                     | `false`                                                          |
| `yarn.nodeManager.resources`                   | Resource limits and requests for YARN NodeManager pods                             | `requests:memory=2048Mi,cpu=1000m,limits:memory=2048Mi,cpu=1000m`|
| `persistence.nameNode.enabled`                 | Enable/disable persistent volume                                                   | `true`                                                           | 
| `persistence.nameNode.storageClass`            | Name of the StorageClass to use per your volume provider                           | `sata-standard`                                                  |
| `persistence.nameNode.accessMode`              | Access mode for the volume                                                         | `ReadWriteOnce`                                                  |
| `persistence.nameNode.size`                    | Size of the volume                                                                 | `50Gi`                                                           |
| `persistence.dataNode.enabled`                 | Enable/disable persistent volume                                                   | `true`                                                           |
| `persistence.dataNode.storageClass`            | Name of the StorageClass to use per your volume provider                           | `sata-standard`                                                  |
| `persistence.dataNode.accessMode`              | Access mode for the volume                                                         | `ReadWriteOnce`                                                  |
| `persistence.dataNode.size`                    | Size of the volume                                                                 | `200Gi`                                                          |


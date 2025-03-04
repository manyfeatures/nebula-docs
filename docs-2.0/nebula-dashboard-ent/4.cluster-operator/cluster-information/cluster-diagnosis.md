# Cluster diagnositics

The cluster diagnostics feature in Dashboard Enterprise Edition is to locate and analyze the current cluster problems within a specified time range and summarize the diagnostic results and cluster monitoring information to web-based diagnostic reports.

## Features

- Diagnostic reports allow you to troubleshoot the current cluster problems within a specified time range.
- Quickly understand the basic information of the nodes, services, service configurations, and query sessions in the cluster.
- Based on the diagnostic reports, you can make operation and maintenance recommendations and cluster alerts.


## Entry

1. In the top navigation bar of the Dashboard Enterprise Edition page, click **Cluster Management**.
2. On the right side of the target cluster, click **Detail**.
3. In the left navigation bar, click **Information**->**Cluster Diagnostics**.

## Create diagnostic reports


1. Select a time range for diagnostics. You can customize the time range or set the range by selecting time intervals, including `1 Hour`, `6 Hours`, `12 Hours`, `1 Day`, `3 Days`, `7 Days`, and `14 Days`.

  !!! caution

        Note that the end time of the diagnostic range you set cannot be longer than the current time. If the end time is longer than the current time, the end time will be set to the current time.

2. On the **Cluster Diagnostics** page, click **Start**.

  ![diagnosepage](https://docs-cdn.nebula-graph.com.cn/figures/cluster-diagnose_2022-04-11_en.png)

3. Wait for the diagnostic report to be generated. When the diagnostic status is changed to **success** from **generating**, the diagnostic report is ready. 


## View diagnostic reports

In the diagnostic report list, you can view the diagnostic reports by clicking **Detail** on the right side of the target report. You can also download the diagnostic report in PDF format.

A diagnostic report contains the following information:

- Diagnosis Result
- Basic Info
- Load Info
- Network
- Session
- Service Info
- Configuration Info

### Diagnosis Result

- When the following parameters are abnormal, the corresponding information is displayed in the **Diagnosis Result** section, including the parameter name, type, severity, and details.

  | Parameter                               | Description |
  | ---------------------------------- | ---- |
  | `num_queries_hit_memory_watermark` |  The total number of nGQL statements that reach the memory high-water mark during execution.   |
  | `graphd_down  `                    |  Graph services stopped running.   |
  | `storaged_down`                    |  Storage services stopped running.    |
  | `metad_down`                       |  Meta services stopped running.    |
  | `node-exporter down`               |  The service used to collect data from the node stopped running. |

- When no abnormality is diagnosed, **no diagnostic information** is displayed in the diagnostic result.

### Basic Info

![basic-info](https://docs-cdn.nebula-graph.com.cn/figures/basicinfo_2022-04-13_en.png)

- **Report Time Range**: Displays the time range of the diagnostic report.

- **Node Info**: Displays the basic information of the node, including the node IP, number of services, CPU, memory, and disk.

  | Parameter                               | Description |
  | ---------------------------------- | ---- |
  | `HOST` | The IP address of the node.   |
  | `INSTANCE`                    |  The number of NebulaGraph services deployed on this node. Such as: `metad*1 graphd*1 storaged*1`.   |
  | `CPU`                    |  The number of CPU cores. Unit: Core.    |
  | `MEMORY`                      |  The memory size of the node. Unit: GB.    |
  | `DISK`               |  The disk size of the node. Unit: GB. |


- **Service Info**: Displays the type, node IP, HTTP port, and operational status of each NebulaGraph service.

- **Leader Distribution**: Displays the distribution of Leaders in Storage services.

  | Parameter                               | Description |
  | ---------------------------------- | ---- |
  | `Storage Service` |   Displays the access addresses for Storage services.                            |
  | `Number of Leaders`  |  Displays the number of Leaders in the corresponding Storage service.                            |
  | `Leader Distribution`  |   Displays the number of Leader distributions for different space graphs in the corresponding Storage service.                            |

### Load Info

![basic-info](https://docs-cdn.nebula-graph.com.cn/figures/load_2022-04-13_en.png)

Displays the load information of the node, including the average value (AVG), maximum value (MAX), minimum value (MIN) of the following metrics of the node within the time range: 

- **Memory Utilization**: Displays the node memory usage in %.

- **CPU Utilization**: Displays the node CPU usage in %.

- **Disk Utilization**: Displays the total disk utilization of the node and the utilization of each disk in the node in %.

### Network

![basic-info](https://docs-cdn.nebula-graph.com.cn/figures/network_2022-04-13.png)

Displays the network traffic information of all nodes in the cluster, including the average (AVG), maximum (MAX), and minimum (MIN) values of the following metrics: 

- **NetworkOut**: Displays the magnitude of network outflow speed for each node in the cluster, and the magnitude of outflow speed for each NIC in each node. Unit: Bytes/s.

- **NetworkIn**: Shows the magnitude of network inflow speed for each server node in the cluster and the magnitude of inflow speed for each NIC in each node. Unit: Bytes/s.

### Session

![basic-info](https://docs-cdn.nebula-graph.com.cn/figures/session_2022-04-13.png)

Displays the session-related information for all Graph services in the cluster.


| Parameter                             | Description |
| -------------------------------- | ---- |
| `num_opened_sessions`            | The number of sessions connected to the server.     |
| `num_auth_failed_sessions`       | The number of sessions in which login authentication failed.|
| `num_active_sessions`            | The number of currently active sessions.|
| `num_reclaimed_expired_sessions` | The number of expired sessions actively reclaimed by the server.     |

### Service Info

Displays metrics related to the stability of each service in the cluster.

- **Graph**: 

  ![basic-info](https://docs-cdn.nebula-graph.com.cn/figures/Service_Graph_2022-04-13_en.png)

  | Parameter          | Description                                                         |
  | ------------- | ------------------------------------------------------------ |
  | `METRIC_NAME` | `query`: The number of all queries.<br />    `slow_queries`: The number of slow queries.<br />`num_killed_queries`: The number of killed queries.<br />`num_queries_hit_memory_watermark`: The total number of nGQL statements that reach the memory high-water mark during execution.<br />`num_rpc_sent_to_metad`: The number of RPC requests that the Graphd service sent to the Metad service.|

- **Meta**: 

  ![basic-info](https://docs-cdn.nebula-graph.com.cn/figures/Service_meta_2022-04-13_en.png)

  | Parameter          | Description                                                         |
  | ------------- | ------------------------------------------------------------ |
  | `METRIC_NAME` | `heartbeat`: The number of heartbeats.                                         |


- **Storage**: 

  ![basic-info](https://docs-cdn.nebula-graph.com.cn/figures/Service_Storage_2022-04-13_en.png)

  | Parameter          | Description                                                         |
  | ------------- | ------------------------------------------------------------ |
  | `METRIC_NAME` | `delete_vertices`: The number of deleted vertices.<br />    `delete_edges`: The number of deleted edges.<br />`delete_tags`: The number of deleted tags.<br />`num_rpc_sent_to_metad`: The number of RPC requests that the Storaged service sent to the Metad service. |

The descriptions of other parameters are as follows: 

| Parameter          | Description                                                         |
| ------------- | ------------------------------------------------------------ |
| `TOTAL`      |      The total number of times this monitoring metric is executed.                                                      |  
| `ERROR`      |        The number of errors that occurred.                                                      |
| `P75`         |      The 75th percentile latency.                                                        |
| `P95`         |   The 95th percentile latency.                                                           |
| `P99`         |   The 99th percentile latency.                                                           |
| `P999`        |    The 99.9th percentile latency.                                                          |

### Configuration Info

Lists all configuration information for Graph, Meta, and Storage services in the current cluster.

For information about the configurations of each service in NebulaGraph, see [Configurations](../../../5.configurations-and-logs/1.configurations/1.configurations.md).

[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: CHEN Zhiheng
### Student Id: 21094212
### Email: zchenik@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Your answer goes here.
    > 
    > CPU test:
    > - Name: Phoronix Test Suite
    > - Configuration: Measures the CPU’s ability to perform data compression and decompression using the 7zip algorithm.
    > - Parameter: 7zip compression technique.
    > - Explanation of results: The measurement results represent the CPU’s performance in terms of execution time for the compression and decompression tasks handled by 7zip.
    >
    > Memory test:
    > - Name: Phoronix Test Suite
    > - Configuration:  Use pts/ramspeed test evaluates the system’s memory bandwidth and latency by performing a series of read and write operations to the system’s memory.
    > - Parameter: Copy and Add, Integer and Floating Point
    > - Explaination of results: RTT -> Round-trip time

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |3575 MIPS compression, 3069 MIPS decompression                 |10366.24 MB/s (Integer Add), 10634.10 MB/s (Integer Copy), 10530.80 MB/s (Floating Point Add), 10589.44 MB/s (Floating Point Copy)                    |
    | `t2.medium`  |9958 MIPS compression, 5948 MIPS decompression                |19032.69 MB/s (Integer Add), 19534.91 MB/s (Integer Copy), 19097.15 MB/s (Floating Point Add),  19180.90 MB/s (Floating Point Copy)                  |
    | `c5d.large` |7450 MIPS compression, 4885 MIPS decompression                 |14209.46 MB/s (Integer Add), 14037.21 MB/s (Integer Copy), 14262.13 MB/s (Floating Point Add), 13996.82 MB/s (Floating Point Copy)                   |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 26,200               | 0.026         |
    | `m5.large` - `m5.large`   | 25,600               | 0.019         |
    | `c5n.large` - `c5n.large` | 34,900               | 0.020         |
    | `t3.medium` - `c5n.large` | 21,700               | 0.657         |
    | `m5.large` - `c5n.large`  | 49,600               | 0.126         |
    | `m5.large` - `t3.medium`  | 26,000               | 0.597         |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 32,000               | 60.8         |
    | N. Virginia - N. Virginia | 40,800               | 0.018         |
    | Oregon - Oregon           | 40,600               | 0.019         |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.

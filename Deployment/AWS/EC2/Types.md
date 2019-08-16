# Types of EC2

## Types

Type, Specialty, Use Cases

C5, "Computation oriented", "The C series is all about raw CPU power.  Calculation heavy applications can benefit"
D2, "Disk IO", "High sequential read and write access to very large data sets, such as Hadoop distributed computing"
F, "FPGA", "Anayltics, big data, specialized research"
G3, Graphics, "Video encoding, 3D rendering, some cryptography"
H1, High disk speed, "high disk throughput and high sequential disk I/O access to very large data sets. MapReduce workloads"
I3, High speed storage, Data warehousing and Big Data
M4/M5, "General purpose", "Bigger, badder versions of the T series.  The differences between the M and T series are more subtle than raw specs."
P3, "GPU/Graphics", "Similar to G3 but oriented entirely around GPUs.  Used for crypto mining, Machine learning, etc"
R4, "Memory instensive", "Apps that require in-memory instensive applications"
T2/3, General purpose, "Web servers, small databases, etc"
X1, "Memory Optimized", "Apache Spark and other applications. Similar to R series. X series has more memory, R series more CPU"

## Ways to Be Charged

1. On-Demand: Pay a fixed price per hour (or even per second) for the resources you need.
2. Reserved: Agree to a contract for an extended term (years), thereby getting a reduced rate compared to on-demand.
3. Spot pricing: Bid for spare compute capacity. If the price of capacity drops below your bid, you are charged and your job is run. This is useful for jobs/tasks that don’t need a strict or urgent start time.
   Useful note: if Amazon terminates a spot job, you won’t get charged for that hour of usage. But if you terminate the job, you will be charged.
4. Dedicated hosting: These are dedicated physical hosts. This is mainly for companies that have licensed software that has a per-server cost. By buying dedicated hosting, companies get the fastest possible performance per dollar while still getting access to the full Amazon ecosystem.

### T2 Instances

Cheap, part of free tier

- 1 CPU Credit = 1 vCPU running at 100% for 1 minute, 1 per hour accumulated expire after 24 hours
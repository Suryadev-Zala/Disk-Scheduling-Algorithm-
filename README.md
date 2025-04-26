# Disk-Scheduling-Algorithm

# Disk Scheduling Algorithm Implementation (Project P19)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![Language: C++](https://img.shields.io/badge/Language-C%2B%2B-blue.svg)](https://isocpp.org/) ## Overview

This project provides a C++ simulation platform for implementing, evaluating, and comparing various disk scheduling algorithms. Disk I/O operations often represent a significant bottleneck in computing systems due to the mechanical latencies (seek time, rotational latency) of traditional Hard Disk Drives (HDDs). Efficient disk scheduling algorithms aim to mitigate these latencies by intelligently ordering pending I/O requests to minimize inefficient head movements, thereby improving overall system performance and responsiveness.

This simulator allows users to input disk parameters and request queues (or generate diverse workloads) and analyze the performance of different scheduling strategies based on key metrics.

**Institution:** Birla Institute of Technology and Science (BITS), Pilani - KK Birla Goa Campus

## Features

* **C++ Simulation Framework:** A robust platform built using standard C++ libraries.
* **Multiple Algorithm Implementations:** Includes 6 standard algorithms and 1 novel hybrid algorithm.
* **Comprehensive Performance Metrics:** Calculates and compares algorithms based on:
    * Total Head Movement
    * Average Seek Time
    * Maximum Seek Time
    * Standard Deviation of Seek Times (measures fairness/predictability)
    * Throughput (requests serviced per unit of movement)
* **Flexible Input:** Accepts initial head position, maximum cylinder number, and request queues either manually entered or generated.
* **Workload Generation Module:** Capable of generating diverse disk access patterns:
    * Uniform Random
    * Sequential
    * Clustered
    * Mixed (Random + Clustered)
* **Clear Output:** Presents results in a formatted table, highlighting the best-performing algorithm(s) for the given workload based on Total Head Movement.

## Implemented Algorithms

The simulator includes the following disk scheduling algorithms:

1.  **First-Come-First-Serve (FCFS):** Services requests strictly in their arrival order. Simple and fair, but offers no seek optimization.
2.  **Shortest Seek Time First (SSTF):** Selects the request closest to the current head position. Good average seek time but risks starvation.
3.  **SCAN (Elevator Algorithm):** The head sweeps back and forth across the disk, servicing requests in its path. More bounded wait times than SSTF.
4.  **C-SCAN (Circular SCAN):** Similar to SCAN, but the head only services requests in one direction, then jumps back to the beginning to start the sweep again. Provides more uniform wait times.
5.  **LOOK:** An optimization of SCAN. The head reverses direction only after servicing the last request in its current direction (doesn't necessarily travel to the end cylinder).
6.  **C-LOOK (Circular LOOK):** An optimization of C-SCAN. The head jumps back only to the first pending request in the queue, not necessarily to cylinder 0.
7.  **HDSA (Hybridized Disk Scheduling Algorithm):** A novel algorithm designed to dynamically analyze the request queue pattern and adapt its strategy (e.g., combining aspects of FCFS, SSTF, LOOK) to achieve consistent performance across various workloads.

## Performance Metrics Calculation

The simulation calculates the following based on the service sequence $S = [s_0, s_1, ..., s_N]$ (where $s_0$ is the start position and $s_1$ to $s_N$ are the serviced cylinders):

* **Total Head Movement (THM):** $\sum_{i=1}^{N} |s_i - s_{i-1}|$
* **Average Seek (AvgSeek):** $THM / N$
* **Maximum Seek (MaxSeek):** $\max_{i=1..N} (|s_i - s_{i-1}|)$
* **Standard Deviation of Seek Times (StdDevSeek):** Measures the variability of non-zero seek distances.
* **Throughput:** $N / THM$ (requests per unit movement)

## Workload Generation

The simulator can generate request queues based on different patterns:

* **Uniform Random:** Requests distributed randomly across the cylinder range.
* **Sequential:** Requests follow a generally unidirectional path.
* **Clustered:** Requests grouped around specific cluster centers.
* **Mixed:** A combination of Uniform Random and Clustered requests.

## Getting Started

*(Placeholder: Add instructions on how to compile and run the C++ code)*

1.  **Prerequisites:** Ensure you have a C++ compiler (like g++) installed.
2.  **Compilation:**
    ```bash
    # Example compilation command (adjust as needed)
    g++ your_simulator_file.cpp -o simulator -lm -std=c++11
    ```
3.  **Running the Simulator:**
    ```bash
    ./simulator
    ```
    The program will likely prompt for inputs interactively (Head Position, Max Cylinder, Manual/Generated Queue, Generation Parameters if applicable). Follow the on-screen prompts as shown in the report's example session.

## Simulation Examples & Key Findings

The project report includes detailed analyses of simulations run with various workloads (mixed, sequential edge cases). Key findings include:

* **HDSA Performance:** The Hybridized Disk Scheduling Algorithm (HDSA) consistently demonstrated optimal or tied-for-optimal performance across all tested workloads in terms of total head movement, average seek time, and throughput. It often combined overall efficiency with favorable variability metrics (low max seek, low standard deviation).
* **Workload Dependency:** Algorithm performance is highly dependent on the workload pattern. For instance, FCFS, typically inefficient, performed best in a specific sequential edge case where its simple order matched the optimal path.
* **No Universal Best:** No single standard algorithm is universally optimal across all possible workloads.
* **Trade-offs:** Algorithms present trade-offs between average performance (e.g., SSTF, LOOK) and fairness/predictability (e.g., SCAN, C-SCAN, C-LOOK). HDSA aims to balance these effectively.

## Limitations

The current simulation framework has some limitations:

* **Static Request Queue:** Does not model dynamic request arrivals.
* **Simplified Seek Model:** Assumes seek time is linear with distance; ignores non-linear factors and settling time.
* **No Rotational Latency:** Does not account for the time taken for the desired sector to rotate under the head.
* **No Controller/Transfer Time:** Ignores controller overhead and data transfer time.
* **Idealized Geometry:** Uses a simple linear cylinder model.
* **No Caching Effects:** Does not model OS or drive-level caching.

## Authors

* **Gladwin Kurian** (2024H1030040G)
* **Suryadevsinh Zala** (2024H1030127G)
* **Udit Chaudhary** (2024H1030021G)
    (Group 6)

## Acknowledgements

* **Dr. Kanchan Manna** (Supervisor)

## References

1.  Shankar, A., Ravat, A., & Pandey, A. K. (2019). Comparative study of disk scheduling algorithms and proposal of a new algorithm for better efficiency. *SSRN Electronic Journal*. https://doi.org/10.2139/ssrn.3349013
2.  An Hybridized Disk Scheduling Algorithm (HDSA). (n.d.). *International Journal of Scientific and Research Publications (IJSRP)*. Retrieved from https://www.ijsrp.org/research-paper-0319.php?rp=P878400


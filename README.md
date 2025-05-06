BubbleSortIST

This repository contains implementations of a parallel algorithm for constructing ( n-1 ) independent spanning trees (ISTs) in bubble-sort networks (( B_n )), based on the research paper "A Parallel Algorithm for Constructing Multiple Independent Spanning Trees in Bubble-Sort Networks" by Shih-Shun Kao et al. The project is developed as part of the Parallel and Distributed Computing (PDC) course, fulfilling requirements for both serial and parallel implementations using MPI.

Project Overview

The bubble-sort network ( B_n ) is an interconnection network with ( n! ) vertices (permutations of ( {1, 2, ..., n} )) and edges representing adjacent transpositions. The algorithm constructs ( n-1 ) ISTs, each rooted at the identity permutation (1, 2, ..., n), ensuring fault tolerance and efficient communication in parallel systems. The implementations include:





Serial Version (ist_bubble_sort_serial.c): A sequential C implementation for baseline performance.



Parallel Version (ist_bubble_sort.c): An MPI-based C implementation for parallel execution across multiple processes.

The project meets the research paper's requirements:





Constructs ( n-1 ) ISTs.



Supports full parallelization with constant-time parent computation.



Achieves ( \mathcal{O}(n \cdot n!) ) time complexity.



Bounds tree height by ( D(B_n) + n - 1 ), where ( D(B_n) = n(n-1)/2 ).



Handles vertex cases based on the last symbol and tree index.

It also aligns with the PDC project requirements by providing serial and parallel implementations, enabling scalability analysis, and supporting documentation.


Prerequisites





Serial Version:





A C compiler (e.g., gcc).



Standard C libraries (stdio.h, stdlib.h, string.h, assert.h).



Parallel Version:





An MPI implementation (e.g., MPICH or OpenMPI).



A C compiler compatible with MPI (e.g., mpicc).



Operating System: Linux, macOS, or Windows with a compatible environment.



Optional: Tools for performance analysis (e.g., Intel Trace Analyzer, VTune Amplifier) as suggested in the PDC project tutorial.

Installation





Clone the Repository:

git clone https://github.com/Muhammadomer902/BubbleSortIST_PDC_Parallel_And_Distributed_Computing.git
cd BubbleSortIST



Compile the Serial Version:

gcc ist_bubble_sort_serial.c -o ist_serial



Compile the Parallel Version:

mpicc ist_bubble_sort.c -o ist_mpi

Usage

Running the Serial Version

The serial implementation processes all ( n! ) vertices sequentially to construct ( n-1 ) ISTs.

./ist_serial

Output: Prints the parent assignments for each vertex in each tree to the console, in the format:

Independent Spanning Trees for B_4:
Tree 1:
Vertex 1 2 3 4 -> Parent 1 2 4 3
...

Running the Parallel Version

The parallel implementation distributes vertices across MPI processes for faster computation.

mpirun -np <num_processes> ./ist_mpi





<num_processes>: Number of MPI processes (ideally divides ( n! ), e.g., 4 or 8 for ( n=4 )).



Output: Same as the serial version, printed by the root process.

Note: The current implementation uses ( n=4 ) (24 vertices) for practicality. To change ( n ), modify MAX_N and MAX_VERTICES in the source files, but note that computation grows factorially with ( n ).

Performance Analysis

The PDC project requires comparing sequential and parallel performance. To analyze scalability:





Run the serial version to establish a baseline execution time.



Run the parallel version with varying numbers of processes (e.g., 2, 4, 8).



Measure execution time and compute speedup (( \text{serial time} / \text{parallel time} )) and scaling metrics (weak/strong scaling).



Use tools like Intel Trace Analyzer to identify MPI communication bottlenecks, as described in the provided tutorial.

A detailed performance analysis will be documented in docs/performance_analysis.md (to be completed).

Notes





Dataset: The algorithm does not require an external dataset, as it operates on the bubble-sort network ( B_n ), with vertices generated as all permutations of ( {1, 2, ..., n} ).



METIS: The PDC project mentions METIS for graph partitioning, but it is not used here, as IST construction does not require partitioning. Future extensions could integrate METIS for larger networks.



OpenMP/OpenCL: The current implementation uses MPI for parallelism. OpenMP could be added for intra-node parallelism, but it is not included in this version.



Limitations: The implementation is optimized for small ( n ) (e.g., 4) due to the factorial growth of ( n! ). For larger ( n ), memory and computation time increase significantly.

Future Work





Optimize MPI communication using non-blocking calls (e.g., MPI_Isend) to reduce serialization, as suggested in the Intel MPI tutorial.



Integrate OpenMP for hybrid parallelism within nodes.



Explore extensions to generalized bubble-sort graphs or other network topologies, as proposed in the research paper.



Add visualization tools to display the IST structures graphically.

References





Kao, S.-S., et al. "A Parallel Algorithm for Constructing Multiple Independent Spanning Trees in Bubble-Sort Networks." Journal of Parallel and Distributed Computing, 2023.



PDC Project Description (provided in course materials).



Intel Tutorial: "Analyzing MPI Applications" (for performance optimization guidance).
# Software Engineering
Software Engineering is part of computer engineering that treats process of software development and maintenance.

### Evolutionary Improvement of Programs

Topic : Search Based Software Engineering

<https://dl.acm.org/doi/10.1109/TEVC.2010.2083669>

Genetic Programming is part of SBSE that evolve program with genetic algorithm to optimize some constraint.
This paper tries to optimize the code in terms of execution time, while preserving the semantic correctness.
The genetic algorithm initialized with given program, and genetic algorithm tries to evolve the program
with fitness function of elapsed time and test case correctness. 
To enhance the performance, the author co-evolved the test case population, and used multi objective optimization.
For the result, the program successfully optimized, that modern compilers fails to optimize.

### Evolving Human Competitive Spectra-Based Fault Localisation Techniques

Topic : Search Based Software Engineering

<https://link.springer.com/chapter/10.1007/978-3-642-33119-0_18>

Spectra-based Fault Localisation is part of software debugging techniques.
First, spectra is summary of test case execution, that stores number of correct execution, buggy execution,
correct non-execution, buggy non-execution, per each line of code.
Then SBFL tries to find some formula that orders each line of code by possibility of faultyness.
This paper tries to tackle this problem by genetically evolve function with fitness function as ranking of faulty line.
The result of evolution was human-competitive, in a sense that there were some formula that exceeds human designed formulas.
For the follow up study, some of formula was proven that it is optimal.

### “Sampling” as a Baseline Optimizer for Search-based Software Engineering

Topic : Search Based Software Engineering

<https://arxiv.org/pdf/1608.07617.pdf>

Search Based Software Enginnering views SE problems as mathematical optimization problems, and tries to find sub-optimal solution.
Usual approach is evolutionary algorithm or random search, where random search is well used as a baseline optimizer.
However, the problem of random search is that it is cost expensive, since we need to evaluate all generated sample.
This paper proposes 'SWAY', as a baseline optimizer for general SBSE problems.
Roughly, SWAY first generates large sized sample, divide it and compare each representative, then remove not selected.
The algorithm slightly differ whether target space is discrete or continuous.
If space is continous, it first get two farthest points, A, B, and divide space into component parallel to line AB.
If space is discrete, first approach fails since most of space is empty. Instead, first divide samples by number of 1 (selected number).
Now fix random point, and view distance between fixed point and each point as angular component, then divide sample after normalizing it.
If the space is highly constraint, sample is generated by SAT solver.
In result, SWAY was able to generate good enough solutions while having short runtime, with enough diversity.
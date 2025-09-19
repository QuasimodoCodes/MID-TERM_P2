### MOVRP Project High-Level Checklist

Here is a simple, high-level checklist for your project using NSGA-II and MOGA, based on the provided assignment and lecture materials.

---

### 1. Pre-Implementation Setup

- **Form a group:** Confirm your group members as approved for Project 1[cite: 3673, 3674].
- **Select Objectives:**
  - Minimize Total Distance ($f_1$)[cite: 3726, 3728].
  - Choose and define a second objective ($f_2$) to minimize Route Balance (either Maximum Route Length or Standard Deviation of Route Lengths)[cite: 3727, 3729, 3731, 3734].
- **Download Data:** Get the recommended CVRPLIB instances[cite: 3799]:
  - [ ] Small: A-n32-k5 (32 customers, 5 vehicles)[cite: 3810].
  - [ ] Medium: B-n78-k10 (78 customers, 10 vehicles)[cite: 3811].
  - [ ] Large: X-n101-k25 (101 customers, 25 vehicles)[cite: 3812].

---

### 2. NSGA-II Implementation Workflow

- **Initialization:**
  - [ ] Set a fixed budget (e.g., population size, generations, crossover/mutation probabilities)[cite: 3822, 3823].
  - [ ] Randomly create an initial parent population, $P_t$, of size $N$[cite: 744, 745].
- **Main Loop (for a fixed number of generations):**
  - [ ] **Create Offspring:** Generate an offspring population, $Q_t$, of size $N$ from $P_t$ using genetic operators (crossover and mutation)[cite: 748, 749, 774, 778, 779].
  - [ ] **Combine Populations:** Merge parent and offspring populations to form a combined population, $R_t$, of size $2N$[cite: 747, 752].
  - [ ] **Non-Dominated Sorting:** Sort $R_t$ into non-dominated fronts ($F_1, F_2, F_3, ...$)[cite: 753].
  - [ ] **Form New Population:**
    - [ ] Add solutions from the best fronts ($F_1, F_2$, etc.) to a new population, $P_{t+1}$, until it reaches size $N$[cite: 770].
    - [ ] If the last front added makes the population size exceed $N$, use **Crowding Distance Sorting** to select the necessary number of solutions from that last front[cite: 688, 701, 804, 805, 808, 809].
  - [ ] **Repeat:** Use the new population $P_{t+1}$ as the parent population for the next generation[cite: 789].

---

### 3. MOGA Implementation Workflow

- **Initialization:**
  - [ ] Set a fixed budget (e.g., population size, generations, crossover/mutation probabilities)[cite: 3822, 3823].
  - [ ] Generate an initial population, $P_t$, of size $N$ (use a permutation-based or route-list representation)[cite: 1401].
  - [ ] Optionally initialize an external non-dominated archive, $P_{ext}$, for elitism and final result storage[cite: 1402].
- **Main Loop (for a fixed number of generations):**
  - [ ] **Fitness & Ranking:**
    - [ ] Compute objective values ($f_1$, $f_2$) for all individuals in $P_t$.
    - [ ] Assign Pareto ranks (non-dominated sorting) to population members (rank 1 = nondominated) and compute niche-sharing penalties within ranks to preserve diversity[cite: 1414, 1415, 1416].
  - [ ] **Selection:**
    - [ ] Perform selection (e.g., binary tournament) using rank + sharing-adjusted fitness to choose parents for reproduction[cite: 1443, 1444].
  - [ ] **Genetic Operations:**
    - [ ] Apply crossover and mutation suitable for VRP representations (e.g., OX + split, route-exchange, relocate) to create offspring[cite: 748, 749, 774].
    - [ ] Optionally apply local search (intra-route 2-opt, relocate moves) to offspring for improvement.
  - [ ] **Replacement & Archive Update:**
    - [ ] Replace the population (generational or steady-state) and update the external archive $P_{ext}$ with new non-dominated solutions.
    - [ ] If $P_{ext}$ exceeds the maximum size, reduce it using clustering or sharing-based truncation to maintain diversity[cite: 1391, 1457].
  - [ ] **Repeat:** Use the new population $P_{t+1}$ as the parent population for the next generation.

---

### 4. Post-Implementation & Deliverables

- **Run Experiments:**
  - [ ] Run each algorithm at least **20 times** for each of the three problem sizes (small, medium, large)[cite: 3822].
  - [ ] Record run time and the number of evaluations[cite: 3824].
  - [ ] Repeat this process for three different sets of MOEA parameters[cite: 3831].
- **Analysis:**
  - [ ] Compare the Pareto fronts of NSGA-II and MOGA for all test problems[cite: 3830].
  - [ ] Analyze and compare the solutions in terms of **convergence** and **diversity**[cite: 3829, 3830].
  - [ ] Analyze the effects of the three parameter sets on the algorithm's performance and correlation with the results[cite: 3831, 3859].
- **Final Report & Code:**
  - [ ] Write a report (1000-1500 words) discussing your design, objective function, analysis, and findings[cite: 3849, 3854, 3856, 3857, 3859, 3860].
  - [ ] Include a table summarizing the runtime for all test problems[cite: 3858].
  - [ ] Create a GitHub repository with your commented, executable code and a clear README file[cite: 3836, 3837, 3842, 3845].
  - [ ] Submit the GitHub link via email and the report via Canvas by the deadline[cite: 3676, 3678, 3848].

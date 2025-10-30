# Multi-Crane Scheduling Dataset

This repository provides the experimental dataset used in the following paper:

> **Woo-Jin Shin**, Hyun-Jung Kim.  
> *Advances in Multi-Crane Scheduling: Extended Non-Interference Modeling and Temporal-Constraint-Based Valid Inequalities*.  
> *European Journal of Operational Research*, 2025.  
> [https://doi.org/10.1016/j.ejor.2025.10.032](https://doi.org/10.1016/j.ejor.2025.10.032)

---

## 1. Overview

The dataset contains instance files used for the experiments in the above paper.  
Each instance represents a **multi-crane scheduling problem** defined under different scales characterized by:

- The **number of cranes per track**, and  
- The **number of jobs (not tasks)** to be scheduled.

---

## 2. Dataset Description

- Each **scale** is defined by a unique combination of:
  - Number of cranes per track
  - Number of jobs

- There are **30 instances per scale**.

- The total number of instances is **750**.  

- Each instance file is named as: {crane_count}_{job}_{idx}.json
  - Example: 2_15_4.json → 2 cranes per track, 15 jobs, 4th instance

- All instances are stored in the `Instances/` folder.

### Instance scales

| Cranes per track | Job sizes | #Instances |
|------------------|------------|-------------|
| 2 | {5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 60, 70, 80, 90, 100} | 15 × 30 = 450 |
| 3 | {5, 10, 15, 20, 25, 30, 35, 40, 45, 50} | 10 × 30 = 300 |

Each scale includes **2 tracks**, and the total number of cranes is therefore  
either 4 (for 2 cranes per track) or 6 (for 3 cranes per track).

---

## 3. Instance Structure

Each `.json` file contains a dictionary, where the keys correspond to the notation used in the paper.  
Values represent numerical parameters or lists associated with those symbols.

Example structure:
```json
{
  "hat(t)": 5,
  "lambda": 1.2,
  "T": [0, 1, 2, 3, 4],
  "task_tr": {"τ1": 1, "τ2": 1, "τ3": 2}
}
```
## 4. Parameter Definitions

Each key corresponds to a parameter in the paper, following the same notation.
For details, refer to Tables 10 and 11 in the Supplementary Material of the paper.

| JSON Key   | Symbol in Paper                     | Type         | Description                                    |
| ---------- | ----------------------------------- | ------------ | ---------------------------------------------- |
| `hat(t)`   | 𝑡̂                                   | Single value | Model parameter                                |
| `lambda`   | λ                                   | Single value | Model parameter                                |
| `gamma`    | γ                                   | Single value | Model parameter                                |
| `T`        | T                                   | List         | Set of time indices                            |
| `T^obj`    | T<sup>obj</sup>                     | List         | Subset of objective time indices               |
| `task_tr`  | tr<sub>τ</sub>                      | Dict         | Track index of each task                       |
| `r`        | r<sub>τ</sub>                       | Dict         | Release time                                   |
| `a`        | a<sub>τ</sub>                       | Dict         | Arrival time                                   |
| `b`        | b<sub>τ</sub>                       | Dict         | Due time (∞ indicates no upper bound)          |
| `l^1`      | l<sub>τ</sub><sup>1</sup>           | Dict         | Location 1                                     |
| `l^2`      | l<sub>τ</sub><sup>2</sup>           | Dict         | Location 2                                     |
| `g`        | g<sub>(τ,τ′)</sub>                  | Dict         | Binary parameter (may include negative values) |
| `Xi`       | Ξ                                   | List         | Set of time windows                            |
| `V`        | V                                   | List         | Set of cranes                                  |
| `V_tau`    | V<sub>τ</sub>                       | Dict         | Available cranes for each task                 |
| `l^0`      | l<sub>v</sub><sup>0</sup>           | Dict         | Initial location of each crane                 |
| `crane_tr` | —                                   | Dict         | Track index of each crane (not in paper)       |
| `es`       | es<sub>τ</sub>                      | Dict         | Earliest start time                            |
| `ls`       | ls<sub>τ</sub>                      | Dict         | Latest start time                              |
| `d`        | d<sub>(τ,τ′)</sub>                  | Dict         | Travel time between tasks                      |
| `M`        | M                                   | Single value | Big-M parameter (for MILP reproducibility)     |
| `h`        | h<sub>τ</sub>                       | Dict         | Processing time                                |
| `t^0`      | t<sub>(0,τ)<sup>v</sup></sub>       | Dict         | Travel time from initial to first task         |
| `t`        | t<sub>(τ,τ′)</sub>                  | Dict         | Travel time between tasks                      |
| `Theta`    | Θ                                   | List         | Feasible temporal relations                    |
| `Delta`    | Δ<sub>(τ,τ′)<sup>(v,v′)</sup></sub> | Dict         | Temporal interference parameter                |
| `Lambda^1` | Λ<sup>1</sup>                       | List         | Valid inequality set 1                         |
| `Lambda^2` | Λ<sup>2</sup>                       | List         | Valid inequality set 2                         |
| `Lambda^3` | Λ<sup>3</sup>                       | List         | Valid inequality set 3                         |
| `Lambda^4` | Λ<sup>4</sup>                       | List         | Valid inequality set 4                         |

## 5. Notes on Provided Parameters

- For job > 5, the following parameters are not included to reduce total file size,
  as they can be computed from other parameters:
  h_τ, t_(0,τ)^v, t_(τ,τ′), Θ, Δ_(τ,τ′)^(v,v′), Λ^1, Λ^2, Λ^3, Λ^4

- Parameters es_τ, ls_τ, and d_(τ,τ′) are included even though they are derivable,
  since their computation requires Floyd–Warshall algorithm.

- Parameter M is included to ensure reproducibility of MILP experiments.

- Values such as ∞ in b_τ indicate no upper bound.

- Negative values in g_(τ,τ′), d_(τ,τ′), and Δ_(τ,τ′)^(v,v′) are normal and valid.

## 6. Citation

If you use this dataset in academic work, please cite:

Woo-Jin Shin and Hyun-Jung Kim (2025).
Advances in Multi-Crane Scheduling: Extended Non-Interference Modeling and Temporal-Constraint-Based Valid Inequalities.
European Journal of Operational Research.
https://doi.org/10.1016/j.ejor.2025.10.032


© 2025 Woo-Jin Shin. This dataset is shared for academic and research use.

---

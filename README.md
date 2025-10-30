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

- Each instance file is named as: `{crane_count}_{job}_{idx}.json`
  - Example: `2_15_4.json` → 2 cranes per track, 15 jobs, 4th instance

- All instances are stored in the `instances/` folder.

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
  "lambda": 1,
  "T": [1, 2, 3, 4],
  "task_tr": {"1": 1, "2": 2, "3": 2, "4": 1}
}
```

---

## 4. Parameter Definitions

Each key corresponds to a parameter in the paper, following the same notation.  
For details, refer to **Tables 10 and 11** in the *Supplementary Material* of the paper.

| JSON Key | Symbol in Paper | Type | Example Representation |
|-----------|----------------|------|-------------------------|
| `hat(t)` | t̂ | Single value | `Data['hat(t)']` = t̂ |
| `lambda` | λ | Single value | `Data['lambda']` = λ |
| `gamma` | γ | Single value | `Data['gamma']` = γ |
| `T` | T | List | `Data['T'] =` T |
| `T^obj` | T<sup>obj</sup> | List | `Data['T^obj']` = T<sup>obj</sup> |
| `task_tr` | tr<sub>τ</sub> | Dict | `Data['task_tr']['τ']` = tr<sub>τ</sub> |
| `r` | r<sub>τ</sub> | Dict | `Data['r']['τ']` = r<sub>τ</sub> |
| `a` | a<sub>τ</sub> | Dict | `Data['a']['τ']` = a<sub>τ</sub> |
| `b` | b<sub>τ</sub> | Dict | `Data['b']['τ']` = b<sub>τ</sub> |
| `l^1` | l<sub>τ</sub><sup>1</sup> | Dict | `Data['l^1']['τ']` = l<sub>τ</sub><sup>1</sup> |
| `l^2` | l<sub>τ</sub><sup>2</sup> | Dict | `Data['l^2']['τ']` = l<sub>τ</sub><sup>2</sup> |
| `g` | g<sub>(τ,τ′)</sub> | Dict | `Data['g']['(τ,τ′)']` = g<sub>(τ,τ′)</sub> |
| `Xi` | Ξ | List | `Data['Xi']` = Ξ |
| `V` | V | List | `Data['V']` = V |
| `V_tau` | V<sub>τ</sub> | Dict | `Data['V_tau']['τ']` = V<sub>τ</sub> |
| `l^0` | l<sub>v</sub><sup>0</sup> | Dict | `Data['l^0']['v']` = l<sub>v</sub><sup>0</sup> |
| `crane_tr` | — | Dict | `Data['crane_tr']['v']` = track index of crane v |
| `es` | es<sub>τ</sub> | Dict | `Data['es']['τ']` = es<sub>τ</sub> |
| `ls` | ls<sub>τ</sub> | Dict | `Data['ls']['τ']` = ls<sub>τ</sub> |
| `d` | d<sub>(τ,τ′)</sub> | Dict | `Data['d']['(τ,τ′)']` = d<sub>(τ,τ′)</sub> |
| `M` | M | Single value | `Data['M']` = M |
| `h` | h<sub>τ</sub> | Dict | `Data['h']['τ']` = h<sub>τ</sub> |
| `t^0` | t<sub>(0,τ)</sub><sup>v</sup> | Dict | `Data['t^0']['(v,τ)']` = t<sub>(0,τ)</sub><sup>v</sup> |
| `t` | t<sub>(τ,τ′)</sub> | Dict | `Data['t']['(τ,τ′)']` = t<sub>(τ,τ′)</sub> |
| `Theta` | Θ | List | `Data['Theta']` = Θ |
| `Delta` | Δ<sub>(τ,τ′)</sub><sup>(v,v′)</sup> | Dict | `Data['Delta']['(τ,τ′,v,v′)']` = Δ<sub>(τ,τ′)</sub><sup>(v,v′)</sup> |
| `Lambda^1` | Λ<sup>1</sup> | List | `Data['Lambda^1']` = Λ<sup>1</sup> |
| `Lambda^2` | Λ<sup>2</sup> | List | `Data['Lambda^2']` = Λ<sup>2</sup> |
| `Lambda^3` | Λ<sup>3</sup> | List | `Data['Lambda^3']` = Λ<sup>3</sup> |
| `Lambda^4` | Λ<sup>4</sup> | List | `Data['Lambda^4']` = Λ<sup>4</sup> |

---

## 5. Notes on Provided Parameters

- For job > 5, the following parameters are not included to reduce total file size,
  as they can be computed from other parameters:  
  h<sub>τ</sub>, t<sub>(0,τ)</sub><sup>v</sup>, t<sub>(τ,τ′)</sub>, Θ, Δ<sub>(τ,τ′)</sub><sup>(v,v′)</sup>, Λ<sup>1</sup>, Λ<sup>3</sup>, Λ<sup>3</sup>, Λ<sup>4</sup>

- Parameters es<sub>τ</sub>, ls<sub>τ</sub>, and d<sub>(τ,τ′)</sub> are included even though they are derivable,
  since their computation requires Floyd–Warshall algorithm.

- Parameter M is included to ensure reproducibility of MILP experiments.

- Values such as ∞ in b<sub>τ</sub> indicate no upper bound.

- Negative values in g<sub>(τ,τ′)</sub>, d<sub>(τ,τ′)</sub>, and Δ<sub>(τ,τ′)</sub><sup>(v,v′)</sup> are normal and valid.

---

## 6. Citation

If you use this dataset in academic work, please cite:

Woo-Jin Shin and Hyun-Jung Kim (2025).
Advances in Multi-Crane Scheduling: Extended Non-Interference Modeling and Temporal-Constraint-Based Valid Inequalities.
European Journal of Operational Research.
https://doi.org/10.1016/j.ejor.2025.10.032


© 2025 Woo-Jin Shin. This dataset is shared for academic and research use.

---

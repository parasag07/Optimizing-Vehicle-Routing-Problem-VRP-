# Optimizing-Vehicle-Routing-Problem-VRP-
# 🚚 Supply Chain Route Optimization with QAOA

## 📌 Project Overview
This project demonstrates how **Quantum Approximate Optimization Algorithm (QAOA)** can be applied to a simplified **Vehicle Routing Problem (VRP)** in supply chain logistics.  

A manufacturing company needs to deliver parts from a central **depot (warehouse)** to **4 factories**.  
The company requires that **each trip starts and ends at the depot** (Depot → Factory → Depot).  
Our objective is to **minimize the total delivery distance** while ensuring all factories are served.

We compare:
1. **Classical Baseline** → nearest neighbor heuristic  
2. **Quantum-inspired Approach** → QAOA (using Qiskit)

---

## 📊 Dataset
We use a toy dataset (`vrp_toy.csv`) with depot and factory coordinates:

| location | x  | y  | earliest | latest |
|----------|----|----|----------|--------|
| depot    | 0  | 0  | 0        | 24     |
| F1       | 3  | 1  | 8        | 12     |
| F2       | -2 | 4  | 9        | 14     |
| F3       | 5  | -3 | 7        | 11     |
| F4       | -4 | -2 | 10       | 16     |

- **x, y** → coordinates  
- **earliest, latest** → time windows (can be used as constraints if extended)

---

## ⚙️ Project Workflow

### 1. Preprocessing & Baseline
- Load dataset using **Pandas**  
- Compute **pairwise Euclidean distances**  
- Implement a **nearest neighbor heuristic** for a simple classical baseline route  

### 2. QUBO Formulation
We represent the VRP as a **Quadratic Unconstrained Binary Optimization (QUBO)** problem:
- Binary variable `x_{i,k}` = 1 if position `k` in the route is factory `i`  
- Constraints:
  - Each factory visited **exactly once**  
  - Every trip starts and ends at **depot**  
  - Capacity & time windows (can be extended)  
- Penalty terms added for constraint violations  

Formulated in **Qiskit’s QuadraticProgram**.

### 3. QAOA Implementation
- Ansatz: QAOA with depth `p = 1` and `p = 2`  
- Optimizers: **COBYLA** or **SPSA**  
- Backends:  
  - **Statevector simulator** → noiseless ideal results  
  - **QASM simulator** → realistic quantum measurement with shots  

### 4. Results & Analysis
- Extract best bitstring → interpret as route  
- Compare **QAOA results vs. baseline heuristic**  
- Plot performance across QAOA depth and number of shots  

### 5. Scaling Discussion
- Adding more factories → exponential growth in qubits  
- Penalty scaling & mixer modifications may improve QAOA for larger VRPs  
- Hardware noise and circuit depth become bottlenecks  

---

## 📂 Files in Repository
- `vrp_toy.csv` → dataset  
- `VRP_QAOA.ipynb` → Jupyter notebook (Google Colab ready)  
- `README.md` → this file  


##📌 Conclusion

This project shows how Quantum Computing (via QAOA) can be applied to supply chain logistics.
Even though current quantum hardware is limited, this serves as a proof of concept for future applications of quantum optimization in real-world VRPs.
---
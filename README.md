# Bell State Preparation via Variational Quantum Circuit
Preparing the Bell state |Φ+⟩ = (|00⟩ + |11⟩)/√2 using a single-parameter
variational quantum circuit, optimised with a hand-implemented parameter-shift rule.

Built with [PennyLane](https://pennylane.ai/).

---
## What this does

A variational circuit consisting of an RY rotation followed by a CNOT gate
is trained to produce equal-weight superposition across |00⟩ and |11⟩.
The cost function minimises the expectation values ⟨Z₀⟩² + (⟨Z₀Z₁⟩ − 1)²,
driving the system toward the target entangled state.

Optimisation uses gradient descent with the **parameter-shift rule** — a
hardware-compatible method that estimates gradients using only circuit
evaluations at shifted parameters (p ± π/2), without accessing internal quantum state.
This makes the approach directly transferable to real hardware.

---

## Circuit

RY is drawn from a universal gate set {RX, RY, CNOT} adopted for this project —
sufficient for arbitrary single- and two-qubit operations.

```
RY(p) ──●──
        │
   I ───⊕──
```

<div>
  <img src="https://cdn.jsdelivr.net/gh/AnasOukhouya/bell-state-vqc@main/figures/circuit-diagram.png" width="60%" alt="Circuit diagram" title="Circuit diagram">
</div>
 
---
 
## Results

### Optimization Performance
The model was trained using Gradient Descent with a tolerance ($\epsilon$) of $10^{-4}$.

* **Convergence:** The algorithm reached the stopping criterion at **iteration 1410**.
* **Final Parameter ($p$):** $\approx 1.5956$ (converging toward the theoretical value of $\pi/2 \approx 1.5708$).
* **Final Error:** $0.0001$.

At the optimal parameter, the circuit produces $|00\rangle$ and $|11\rangle$ with equal probability ($\approx 0.5$ each), confirming successful Bell state preparation.

| Observable | Initial ($p = 3.0$) | Optimised |
| :--- | :--- | :--- |
| $P(\|00\rangle)$ | ~0.99 | ~0.50 |
| $P(\|11\rangle)$ | ~0.01 | ~0.50 |

<div>
  <img src="https://cdn.jsdelivr.net/gh/AnasOukhouya/bell-state-vqc@main/figures/states-probabilities.png" width="60%" alt="State probabilities" title="State probabilities">
</div>
<br>
<div>
  <img src="https://cdn.jsdelivr.net/gh/AnasOukhouya/bell-state-vqc@main/figures/parameter-evolution.png" width="60%" alt="Parameter evolution" title="Parameter evolution">
</div>

---

## Project structure

```
bell-state-vqc/
├── bell_state_vqc.ipynb   # main notebook
├── figures/               # plots saved by the notebook
│   ├── circuit.png
│   ├── state_probabilities.png
│   └── parameter_evolution.png
├── requirements.txt
└── README.md
```

---

## Run it

```bash
pip install -r requirements.txt
jupyter notebook bell_state_vqc.ipynb
```

## Requirements

```
pennylane
numpy
matplotlib
seaborn
```

---

## Notes

Code written independently as part of self-directed study into variational
quantum algorithms. Documentation refined iteratively.

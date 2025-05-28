## 📘 QuantHedge-MM: Computational Framework for Hedging in Regime-Switching Markets

This notebook provides a complete implementation of a computational framework for **pricing and hedging European options** in financial markets characterized by **Markov-modulated regime-switching dynamics**. The underlying model extends the classical Black-Scholes paradigm by allowing key market parameters—**volatility**, **drift**, and **interest rate**—to evolve stochastically according to a finite-state continuous-time **Markov chain**.

The asset price $S_t$ evolves under the regime-dependent geometric Brownian motion:

$$
dS_t = \mu(X_t) S_t \, dt + \sigma(X_t) S_t \, dW_t
$$

where $X_t \in \{1,2,3\}$ denotes the current regime. The hedging strategy is derived from the **Föllmer-Schweizer decomposition**, minimizing the **quadratic residual risk (QRR)** and its asymmetric variant, the **positive residual risk (PRR)**.

### 🔧 Core Components:

* **Volterra-type Integral Equations**: Solved numerically for the option price $\phi(t, s, i)$ and hedge ratio $\psi(t, s, i) = \frac{\partial \phi}{\partial s}$, offering improved efficiency over traditional PDE solvers.

* **Monte Carlo Simulations**: Assess hedging performance across thousands of regime paths, capturing the impact of transition frequency and volatility.

* **High-Performance Computing**: Leveraging `Numba` JIT compilation and vectorized operations, the framework achieves significant speed-ups suitable for large-scale risk analysis.

### 🎯 Key Features:

* Captures **regime-dependent hedging performance** and evaluates discrete vs continuous strategies.
* Highlights **model risk** from high-volatility transitions and **tracking errors** in practical hedging.
* Fully reproducible and extensible framework, enabling future research in **incomplete markets** and **risk-aware derivatives trading**.

> 📌 This implementation directly corresponds to the methods and experiments described in the paper:
> **“Computational Methods for Optimal Hedging in Markov Modulated Markets”** by
> Albin James Maliakal, Nagaraju Baydeti, Alen Peter Yimchunger, and Yongkong Kumzek Chang.
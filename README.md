# **QuantHedge-MM: Optimal Hedging in Markov Modulated Markets**

This notebook implements **QuantHedge-MM**, a Python-based framework for pricing and hedging options in markets characterized by **Markov-modulated regimes**. It generalizes the classical Black-Scholes model by allowing asset dynamics to evolve across multiple stochastic regimes, each defined by distinct parameters for volatility ($\sigma_i$), drift ($\mu_i$), and interest rate ($r_i$).

## **Model Dynamics**

* The asset price $S_t$ evolves as:

  $$
  dS_t = S_t \left( \mu(X_t) dt + \sigma(X_t) dW_t \right), \quad X_t \in \{1, 2, \dots, k\}
  $$

  where $X_t$ is a continuous-time Markov chain representing the regime, and its transitions are controlled by the generator matrix $\Lambda = [\lambda_{ij}]$.

## **Numerical Approach**

* Option prices $\varphi(t, s, i)$ are computed using an **integral equation**:

  $$
  \varphi(t,s,i) = \eta_i(t,s) + \int_t^T e^{-(r(i)+\lambda_i)(u-t)} \sum_{j \neq i} \lambda_{ij} \, \mathbb{E}[\varphi(u, S_u, j)] \, du
  $$
* The implementation includes:

  * Numba-accelerated **Monte Carlo simulation** for efficient computation.
  * A flexible solver for the integral equation governing the option prices.

## **Hedging and Risk Assessment**

* The notebook evaluates hedging performance via:

  * **Quadratic Residual Risk (QRR)**:

    $$
    \mathbb{E} \left[ \left( \int_0^T \xi_t \, dS_t - H(S_T) \right)^2 \right]
    $$
  * **Practitioner’s error**, measuring the discrepancy under discrete-time hedging strategies.

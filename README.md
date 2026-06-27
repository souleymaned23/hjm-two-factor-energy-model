# HJM Two-Factor Model for Energy Markets

## Overview

This project studies a two-factor Heath-Jarrow-Morton (HJM) model applied to energy markets.

The objective is to model the dynamics of spot and forward prices, analyze the shape of the forward curve, reproduce the Samuelson effect and calibrate the model on market data.

The notebook focuses on the financial interpretation of the model and the calibration procedure rather than implementation details.

## Motivation

Energy markets exhibit several stylized facts:

- strong short-term fluctuations,
- mean-reverting behavior,
- decreasing volatility with maturity,
- non-parallel movements of the forward curve.

A two-factor model provides a simple framework capable of reproducing these phenomena.

## Model Specification

The spot price is modeled as

$$
S_t = \exp(X_t + Y_t + \mu(t))
$$

where:

- $X_t$ is a mean-reverting factor,
- $Y_t$ is a long-term factor,
- $\mu(t)$ is a deterministic seasonality component.

The dynamics of the factors are

$$
dX_t = -\theta X_t\,dt + \sigma_1 dW_t^{(1)}
$$

and

$$
dY_t = \sigma_2 dW_t^{(2)}.
$$

The Brownian motions satisfy

$$
dW_t^{(1)}dW_t^{(2)} = \rho\,dt.
$$

The first factor captures temporary shocks while the second factor captures permanent market movements.

## Forward Price Formula

Under the risk-neutral measure, the forward price is

$$
F(t,T)=\mathbb{E}_t[S_T].
$$

Using the Gaussian properties of the factors, an analytical expression is obtained:

$$
F(t,T)=
\exp\Big(
A(t,T)
+
B(t,T)X_t
+
Y_t
\Big).
$$

This affine representation is one of the key advantages of the model.

## Interpretation of the Factors

The permanent factor mainly shifts the entire forward curve.

The mean-reverting factor mostly affects short maturities and modifies the slope of the curve.

Combining both factors allows the model to reproduce realistic deformations of observed forward curves.

## Samuelson Effect

One important property of commodity markets is the Samuelson effect.

The volatility of a forward contract decreases as maturity increases.

In the model, the forward volatility takes the form

$$
\sigma_F^2(t,T)=
\sigma_2^2
+
\sigma_1^2 e^{-2\theta (T-t)}
+
2\rho\sigma_1\sigma_2 e^{-\theta (T-t)}.
$$

As maturity increases, the contribution of the mean-reverting factor vanishes.

The model therefore naturally reproduces the Samuelson effect.

## Calibration Procedure

The calibration is performed in two stages.

### Step 1

Estimate the structural parameters

$$
\theta,\qquad \sigma_1,\qquad \sigma_2,\qquad \rho
$$

using market volatility information.

### Step 2

Estimate the state variables

$$
X_t,\qquad Y_t
$$

from the observed futures curve.

This separation improves both stability and interpretability.

## Results

The calibrated model successfully reproduces:

- the observed futures curve,
- the term structure of volatility,
- the Samuelson effect,
- realistic forward curve deformations.

## Main Takeaways

This project illustrates how a relatively simple Gaussian two-factor model can:

- provide analytical pricing formulas,
- reproduce key stylized facts of energy markets,
- remain computationally efficient,
- offer an intuitive economic interpretation of market movements.

## Author

**Souleymane Diabate**

MSc Probability and Finance (El Karoui)

Sorbonne Université

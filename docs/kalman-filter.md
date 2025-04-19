- Link to father file: [README.md](../README.md)

# Kalman Filter Documentation

The **Kalman Filter** is an algorithm that uses a series of measurements observed over time, containing noise and other inaccuracies, to estimate unknown variables more accurately.

## System Model

The Kalman Filter assumes a linear dynamic system:

### State Transition (Process Model)

$$\mathbf{x}_k = \mathbf{F}_k \mathbf{x}_{k-1} + \mathbf{B}_k \mathbf{u}_k + \mathbf{w}_k$$

### Measurement (Observation Model)

$$
\mathbf{z}_k = \mathbf{H}_k \mathbf{x}_k + \mathbf{v}_k
$$

Where:

- $\mathbf{x}_k$: State vector at time step $k$
- $\mathbf{F}_k$: State transition matrix
- $\mathbf{B}_k$: Control input matrix
- $\mathbf{u}_k$: Control vector
- $\mathbf{w}_k$: Process noise (zero-mean Gaussian with covariance $\mathbf{Q}_k$)
- $\mathbf{z}_k$: Measurement vector
- $\mathbf{H}_k$: Observation matrix
- $\mathbf{v}_k$: Observation noise (zero-mean Gaussian with covariance $\mathbf{R}_k$)

## Prediction Step

### Predicted State Estimate


$$\hat{\mathbf{x}}_{k|k-1} = \mathbf{F}_k \hat{\mathbf{x}}_{k-1|k-1} + \mathbf{B}_k \mathbf{u}_k$$


### Predicted Estimate Covariance

$$\mathbf{P}_{k|k-1} = \mathbf{F}_k \mathbf{P}_{k-1|k-1} \mathbf{F}_k^\top + \mathbf{Q}_k$$

## Update Step

### Kalman Gain

$$\mathbf{K}_k = \mathbf{P}_{k|k-1} \mathbf{H}_k^\top \left( \mathbf{H}_k \mathbf{P}_{k|k-1} \mathbf{H}_k^\top + \mathbf{R}_k \right)^{-1}$$


### Updated State Estimate

$$\hat{\mathbf{x}}_{k|k} = \hat{\mathbf{x}}_{k|k-1} + \mathbf{K}_k \left( \mathbf{z}_k - \mathbf{H}_k \hat{\mathbf{x}}_{k|k-1} \right)$$

### Updated Estimate Covariance

$$\mathbf{P}_{k|k} = \left( \mathbf{I} - \mathbf{K}_k \mathbf{H}_k \right) \mathbf{P}_{k|k-1}$$

### Matrix Dimensions

| Matrix         | Dimensions               | Description                         |
|----------------|--------------------------|-------------------------------------|
| $\mathbf{x}_k$     | $n \times 1$          | State vector (size $n$)          |
| $\mathbf{F}_k$     | $n \times n$          | State transition matrix            |
| $\mathbf{B}_k$     | $n \times m$          | Control input matrix               |
| $\mathbf{u}_k$     | $m \times 1$          | Control vector (size $m$)        |
| $\mathbf{w}_k$     | $n \times 1$          | Process noise (size $n$)         |
| $\mathbf{z}_k$     | $p \times 1$          | Measurement vector (size $p$)    |
| $\mathbf{H}_k$     | $p \times n$          | Observation matrix                 |
| $\mathbf{v}_k$     | $p \times 1$          | Observation noise (size $p$)     |
| $\mathbf{Q}_k$     | $n \times n$          | Process noise covariance matrix    |
| $\mathbf{R}_k$     | $p \times p$          | Measurement noise covariance matrix|


## Notes

- The Kalman Filter is optimal for **linear** systems with **Gaussian** noise.
- For **nonlinear** systems, consider using:
  - **Extended Kalman Filter (EKF)**
  - **Unscented Kalman Filter (UKF)**

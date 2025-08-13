## Project Overview
This project demonstrates the **forward kinematics** of a 2-DOF (two degrees of freedom) robotic arm. Forward kinematics is the process of calculating the position of the end effector (tool) given the joint angles and link lengths. The robot used in this project consists of two rotational joints and two links.

---

## Forward Kinematics Equations

Given:
- \( L_1 \) → Length of the first link
- \( L_2 \) → Length of the second link
- \( \theta_1 \) → Angle of the first joint relative to the base (in radians or degrees)
- \( \theta_2 \) → Angle of the second joint relative to the first link

The end-effector position \((x, y)\) in 2D space is calculated as:

\[
x = L_1 \cos(\theta_1) + L_2 \cos(\theta_1 + \theta_2)
\]
\[
y = L_1 \sin(\theta_1) + L_2 \sin(\theta_1 + \theta_2)
\]

---

## Matrix Form Using DH Parameters

Using the Denavit–Hartenberg (DH) convention, the transformation matrices are:

\[
T_1 =
\begin{bmatrix}
\cos(\theta_1) & -\sin(\theta_1) & 0 & L_1 \cos(\theta_1) \\
\sin(\theta_1) & \cos(\theta_1)  & 0 & L_1 \sin(\theta_1) \\
0              & 0               & 1 & 0 \\
0              & 0               & 0 & 1
\end{bmatrix}
\]

\[
T_2 =
\begin{bmatrix}
\cos(\theta_2) & -\sin(\theta_2) & 0 & L_2 \cos(\theta_2) \\
\sin(\theta_2) & \cos(\theta_2)  & 0 & L_2 \sin(\theta_2) \\
0              & 0               & 1 & 0 \\
0              & 0               & 0 & 1
\end{bmatrix}
\]

The final transformation from the base to the end effector is:
\[
T = T_1 \times T_2
\]

From \(T\), the position \((x, y)\) is extracted from the 4th column of the matrix.

---

## How to Use
1. **Define link lengths** `L1` and `L2`.
2. **Measure or input joint angles** `theta1` and `theta2`.
3. **Apply the equations** above to compute `(x, y)` coordinates.
4. (Optional) Implement in Python, MATLAB, or Arduino code for simulation or physical robot control.

Example in Python:
```python
import math

# Link lengths
L1 = 10
L2 = 8

# Joint angles in degrees
theta1 = 45
theta2 = 30

# Convert to radians
t1 = math.radians(theta1)
t2 = math.radians(theta2)

# Forward kinematics
x = L1 * math.cos(t1) + L2 * math.cos(t1 + t2)
y = L1 * math.sin(t1) + L2 * math.sin(t1 + t2)

print(f"End effector position: x = {x:.2f}, y = {y:.2f}")

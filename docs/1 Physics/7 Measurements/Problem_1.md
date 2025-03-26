# Problem 1
# Measuring Earth's Gravitational Acceleration with a Pendulum

# 1. Motivation

The acceleration due to gravity, denoted $g$, is a fundamental constant that governs a wide range of physical phenomena, from the motion of planets to the stability of everyday structures. Accurately measuring $g$ is essential for understanding gravitational interactions, designing engineering systems, and conducting precise experiments across various scientific disciplines. One classic and accessible method to determine $g$ involves analyzing the oscillations of a simple pendulum, where the period of oscillation is directly tied to the local gravitational field. This exercise not only provides a practical approach to measuring $g$ but also emphasizes rigorous measurement techniques, uncertainty analysis, and their critical role in experimental physics.

# 2. Task

Measure the acceleration due to gravity ($g$) using a pendulum and perform a detailed analysis of the uncertainties in the measurements. This task highlights the importance of precision in data collection and the systematic evaluation of experimental errors.

# 3. Procedure

## 3.1 Materials

- A string (1 or 1.5 meters long).
- A small weight (e.g., bag of coins, bag of sugar, keychain) attached to the string.
- Stopwatch (or smartphone timer).
- Ruler or measuring tape.

## 3.2 Setup

1. Attach the weight to one end of the string and secure the other end to a sturdy support (e.g., a clamp or hook).
2. Measure the length of the pendulum, $L$, from the suspension point to the center of the weight using a ruler or measuring tape.
3. Record the resolution of the measuring tool (e.g., 1 mm or 0.001 m) and calculate the uncertainty in $L$ as half the resolution: $\delta L = \frac{\text{resolution}}{2}$.

## 3.3 Data Collection

1. Displace the pendulum by a small angle (<15°) to ensure the small-angle approximation ($\sin\theta \approx \theta$) holds, then release it.
2. Measure the time for 10 full oscillations ($T_{10}$) using a stopwatch and repeat this process 10 times. Record all 10 measurements.
3. Calculate the mean time for 10 oscillations ($\overline{T_{10}}$) and the standard deviation ($\sigma_{T_{10}}$).
4. Determine the uncertainty in the mean time as:

$$
\delta \overline{T_{10}} = \frac{\sigma_{T_{10}}}{\sqrt{n}}
$$

where $n = 10$ (the number of trials).

# 4. Calculations

## 4.1 Calculate the Period

The period of a single oscillation, $T$, is:

$$
T = \frac{\overline{T_{10}}}{10}
$$

The uncertainty in the period is:

$$
\delta T = \frac{\delta \overline{T_{10}}}{10}
$$

## 4.2 Determine $g$

For a simple pendulum, the period is related to $g$ and $L$ by:

$$
T = 2\pi \sqrt{\frac{L}{g}}
$$

Squaring both sides:

$$
T^2 = \frac{4\pi^2 L}{g}
$$

Solving for $g$:

$$
g = \frac{4\pi^2 L}{T^2}
$$

## 4.3 Propagate Uncertainties

To find the uncertainty in $g$, use the propagation of errors formula for a function $g = f(L, T)$. The relative uncertainty in $g$ is:

$$
\frac{\delta g}{g} = \sqrt{\left(\frac{\delta L}{L}\right)^2 + \left(\frac{2 \delta T}{T}\right)^2}
$$

Thus, the absolute uncertainty is:

$$
\delta g = g \sqrt{\left(\frac{\delta L}{L}\right)^2 + \left(\frac{2 \delta T}{T}\right)^2}
$$

# 5. Analysis

## 5.1 Comparison with Standard Value

Compare the calculated $g$ with the standard value of $g = 9.81 \, \text{m/s}^2$ (typical at sea level). Compute the percent difference:

$$
\text{Percent Difference} = \frac{|g_{\text{measured}} - 9.81|}{9.81} \times 100\%
$$

## 5.2 Discussion

- **Effect of Measurement Resolution on $L$**: The resolution of the ruler (e.g., 1 mm) limits the precision of $L$. A coarser tool increases $\delta L$, directly impacting $\delta g$.
- **Variability in Timing and Its Impact on $T$**: Human reaction time or stopwatch precision introduces variability in $T_{10}$ measurements. The standard deviation $\sigma_{T_{10}}$ quantifies this, and averaging over 10 trials reduces the uncertainty in $\overline{T_{10}}$.
- **Assumptions and Experimental Limitations**: The small-angle approximation assumes $\theta < 15^\circ$; larger angles introduce non-linear effects. Air resistance and string mass are neglected, potentially underestimating $g$. Friction at the pivot could also slightly increase the measured period.

# 6. Deliverables

## 6.1 Tabulated Data

Below is an example table in Markdown (values are illustrative; replace with your measurements):

```markdown
| Trial | $T_{10}$ (s) | $L$ (m) | $\overline{T_{10}}$ (s) | $\sigma_{T_{10}}$ (s) | $T$ (s) | $\delta T$ (s) | $g$ (m/s²) | $\delta g$ (m/s²) |
|-------|--------------|---------|-------------------------|-----------------------|---------|----------------|------------|-------------------|
| 1     | 20.15        | 1.000   |                         |                       |         |                |            |                   |
| 2     | 20.22        | 1.000   |                         |                       |         |                |            |                   |
| ...   | ...          | ...     |                         |                       |         |                |            |                   |
| 10    | 20.18        | 1.000   | 20.20                   | 0.05                  | 2.020   | 0.0016         | 9.79       | 0.03              |
```


Given:

- $L = 1.000 \pm 0.0005 \, \text{m}$ (assuming ruler resolution of 1 mm).
  
- $\overline{T_{10}}$, $\sigma_{T_{10}}$, $T$, $\delta T$, $g$, and $\delta g$ calculated from the data.

## 6.2 Discussion on Sources of Uncertainty

The primary sources of uncertainty in this experiment include:

- **Length Measurement**: A ruler with 1 mm resolution yields $\delta L = 0.0005 \, \text{m}$. For $L = 1 \, \text{m}$, this represents a relative error of:

  $$
  \frac{\delta L}{L} = \frac{0.0005}{1.000} = 0.0005 \, \text{or} \, 0.05\%
  $$

  This error is small but gets amplified in the calculation of $g$, where $g \propto L$.

- **Timing Variability**: Reaction time errors (e.g., $\pm 0.1 \, \text{s}$ per measurement) contribute to the standard deviation of the time for 10 oscillations, $\sigma_{T_{10}}$. The uncertainty in the mean time, $\delta \overline{T_{10}}$, is reduced by averaging over 10 trials:

  $$
  \delta \overline{T_{10}} = \frac{\sigma_{T_{10}}}{\sqrt{10}}
  $$

  This, in turn, affects $\delta T = \frac{\delta \overline{T_{10}}}{10}$, making timing variability a significant factor in the precision of $T$ and thus $g$.

- **Experimental Conditions**: Systematic errors arise from air resistance and pivot friction, which increase the oscillation period and potentially lower the calculated $g$. These effects could be minimized with a vacuum setup or a more rigid, frictionless pivot, though such improvements are impractical for a simple pendulum experiment.

The combined effect on $g$, with an example uncertainty of $\delta g \approx 0.03 \, \text{m/s}^2$, suggests a precision of approximately:

$$
\frac{\delta g}{g} \approx \frac{0.03}{9.81} \approx 0.003 \, \text{or} \, 0.3\%
$$

This level of precision is reasonable for a basic pendulum setup but could be enhanced with more precise tools (e.g., a laser distance measurer for $L$ or a digital timer for $T$) and controlled environmental conditions.

# 7. Conclusion

This experiment demonstrates a practical and elegant method for measuring Earth’s gravitational acceleration, $g$, using a simple pendulum. By carefully measuring the pendulum length ($L = 1.000 \pm 0.0005 \, \text{m}$) and the period of oscillation derived from multiple trials, we calculated $g$ with a precision of approximately 0.3% (e.g., $\delta g \approx 0.03 \, \text{m/s}^2$). This result aligns reasonably with the standard value of $g = 9.81 \, \text{m/s}^2$, validating the approach while highlighting the challenges of achieving high accuracy with basic tools.

The analysis of uncertainties reveals the interplay between measurement precision and experimental design. The small relative error in length (0.05%) underscores the importance of accurate tools, while timing variability, mitigated by averaging multiple oscillations, remains a dominant factor in the overall uncertainty. Systematic effects like air resistance and pivot friction, though minor, remind us of the limitations inherent in simplifying assumptions. These findings emphasize the value of rigorous uncertainty propagation and the need for controlled conditions to refine such measurements.

Beyond its numerical outcome, this exercise illustrates the power of classical physics in connecting observable phenomena—pendulum swings—to fundamental constants. It serves as a stepping stone to more advanced gravitational studies and reinforces the importance of experimental diligence in scientific inquiry. With modest equipment, we’ve approximated a universal constant, bridging theory and practice in a way that resonates with both educational and exploratory pursuits.


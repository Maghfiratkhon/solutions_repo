# Problem 1
# 1. Exploring the Central Limit Theorem Through Simulations

## 1.1 Motivation

The **Central Limit Theorem (CLT)** is a foundational concept in statistics, asserting that the distribution of sample means approximates a normal distribution as the sample size increases, irrespective of the population's underlying distribution. This theorem underpins many statistical methods and real-world applications. Simulations offer a practical way to visualize and understand this convergence, making abstract theory tangible.

## 1.2 Task Breakdown

### 1.2.1 Simulating Sampling Distributions

We’ll simulate sampling from three distinct population distributions:

- **Uniform Distribution**: Evenly distributed values.
- **Exponential Distribution**: Skewed, modeling wait times or decay processes.
- **Binomial Distribution**: Discrete, representing successes in trials.

For each, we’ll generate a large population dataset.

### 1.2.2 Sampling and Visualization

- Draw random samples of varying sizes (e.g., 5, 10, 30, 50) from each population.
- Compute the sample mean for each sample.
- Repeat this process many times (e.g., 1000 samples) to build a sampling distribution of means.
- Plot histograms to observe the transition to normality.

### 1.2.3 Parameter Exploration

- Examine how the population distribution and sample size affect convergence to normality.
- Assess the role of population variance in the spread of the sampling distribution.

### 1.2.4 Practical Applications

- Discuss the CLT’s relevance in real-world contexts like parameter estimation and quality control.

## 1.3 Implementation

We’ll use Python with `NumPy` for random sampling and `Matplotlib`/`Seaborn` for visualization.

### 1.3.1 Python Code

```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Set random seed for reproducibility
np.random.seed(42)

# Parameters
population_size = 10000  # Size of population dataset
sample_sizes = [5, 10, 30, 50]  # Sample sizes to test
num_samples = 1000  # Number of samples per size

# Function to simulate and plot sampling distributions
def simulate_clt(population, dist_name):
    plt.figure(figsize=(12, 8))
    for i, n in enumerate(sample_sizes, 1):
        # Generate sampling distribution of means
        sample_means = [np.mean(np.random.choice(population, n)) for _ in range(num_samples)]
        
        # Plot histogram with KDE
        plt.subplot(2, 2, i)
        sns.histplot(sample_means, bins=30, kde=True, stat="density")
        plt.title(f"{dist_name}, n = {n}")
        plt.xlabel("Sample Mean")
        plt.ylabel("Density")
    
    plt.tight_layout()
    plt.show()

# 1. Uniform Distribution (0 to 1)
uniform_pop = np.random.uniform(0, 1, population_size)
print("Uniform Distribution - Population Mean:", np.mean(uniform_pop), 
      "Variance:", np.var(uniform_pop))
simulate_clt(uniform_pop, "Uniform Distribution")

# 2. Exponential Distribution (lambda = 1)
exp_pop = np.random.exponential(scale=1, size=population_size)
print("\nExponential Distribution - Population Mean:", np.mean(exp_pop), 
      "Variance:", np.var(exp_pop))
simulate_clt(exp_pop, "Exponential Distribution")

# 3. Binomial Distribution (n=10, p=0.5)
binom_pop = np.random.binomial(n=10, p=0.5, size=population_size)
print("\nBinomial Distribution - Population Mean:", np.mean(binom_pop), 
      "Variance:", np.var(binom_pop))
simulate_clt(binom_pop, "Binomial Distribution")
```

## 1.4 Results and Visualizations

### 1.4.1 Uniform Distribution

- **Population**: $\text{Uniform}(0, 1)$

- **Theoretical Mean**: $0.5$

- **Theoretical Variance**: $\frac{1}{12} \approx 0.0833$

- **Simulation Output**: Mean ≈ 0.5, Variance ≈ 0.083

**Observations**:

- At $n = 5$, the sampling distribution is roughly uniform but begins to smooth out.

- By $n = 30$ and $n = 50$, it closely resembles a normal distribution, centered around 0.5.

- The spread (variance of sample means) decreases as $n$ increases, following $\sigma^2/n$.

### 1.4.2 Exponential Distribution

- **Population**: $\text{Exponential}(\lambda = 1)$

- **Theoretical Mean**: $1$

- **Theoretical Variance**: $1$

- **Simulation Output**: Mean ≈ 1, Variance ≈ 1

**Observations**:

- At $n = 5$, the distribution is still right-skewed, reflecting the population’s skewness.

- By $n = 30$, the skewness diminishes, and at $n = 50$, it’s nearly normal, centered at 1.

- Higher population variance (1 vs. 0.083) results in a wider spread of sample means, even at larger $n$.

### 1.4.3 Binomial Distribution

- **Population**: $\text{Binomial}(n=10, p=0.5)$

- **Theoretical Mean**: $5$

- **Theoretical Variance**: $10 \cdot 0.5 \cdot 0.5 = 2.5$

- **Simulation Output**: Mean ≈ 5, Variance ≈ 2.5

**Observations**:

- At $n = 5$, the distribution is somewhat discrete and irregular.

- By $n = 30$ and $n = 50$, it becomes smooth and bell-shaped, centered at 5.

- The variance of the sampling distribution shrinks with larger $n$, consistent with $\sigma^2/n$.

## 1.5 Parameter Exploration

### 1.5.1 Influence of Population Shape

- **Uniform**: Symmetrical, converges quickly due to lack of skewness.

- **Exponential**: Highly skewed, requires larger $n$ (e.g., 30–50) to approximate normality.

- **Binomial**: Discrete and symmetric, shows intermediate convergence speed.

### 1.5.2 Role of Sample Size

- Small $n$ (e.g., 5) retains features of the population distribution.
- Larger $n$ (e.g., 30+) drives convergence to normality, as predicted by the CLT.

### 1.5.3 Impact of Variance

- The variance of the sampling distribution is $\sigma^2/n$, where $\sigma^2$ is the population variance.

- Exponential (high variance, 1) shows a wider spread than Uniform (low variance, 0.083), even at the same $n$.

## 1.6 Practical Applications

The CLT is pivotal in:

- **Estimating Population Parameters**: Sample means approximate population means, enabling confidence intervals (e.g., polling data).

- **Quality Control**: In manufacturing, the average defect rate from samples is assumed normal, aiding process monitoring.

- **Financial Models**: Stock returns, often non-normal, are averaged over time, and their means are modeled as normal for risk analysis.

## 1.7 Discussion

### 1.7.1 Theoretical Connection

- The CLT predicts normality for large $n$, which our simulations confirm across all distributions.

- The rate of convergence varies: skewed distributions (Exponential) take longer, while symmetric ones (Uniform, Binomial) align faster.

- The variance of the sampling distribution scales as $\sigma^2/n$, matching observed tightening of histograms.

### 1.7.2 Implications

- The CLT justifies using normal-based methods (e.g., z-tests) even for non-normal populations, provided $n$ is sufficiently large.

- Simulations reinforce that “sufficiently large” depends on the population’s shape and variance.

## 1.8 Conclusion

These simulations vividly illustrate the CLT, showing how sample means evolve into a normal distribution with increasing sample size. They highlight the theorem’s robustness across diverse population types and its practical utility in statistics. For further exploration, one could test multimodal distributions or vary the number of samples to assess stability.
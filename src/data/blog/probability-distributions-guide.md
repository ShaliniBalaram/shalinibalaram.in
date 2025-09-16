---
author: Shalini B
pubDatetime: 2024-09-15T18:30:00Z
title: "Which Distribution Should I Choose? A Journey Through Probability Distributions"
slug: probability-distributions-guide
featured: true
draft: false
tags:
  - probability
  - statistics
  - research
  - machine-learning
description: "Understanding probability distributions through interactive visualizations - from my journey recreating 80s research papers to choosing the right distribution for your data."
---

One of the first things my professor asked me to do after my coursework was to start recreating papers, and I started with papers from the 80s as they were easy to understand and recreate. I was using MATLAB then, so it made the whole exercise easier. I knew a few distributions, but I wanted to know how each of them behaved and how to choose the best one.

That simple question - "which distribution should I choose?" - turned out to be more profound than I initially thought. It's not just about fitting curves to data; it's about understanding the story your data is trying to tell.

## What I Learned from Those 80s Papers

Starting with older papers was brilliant advice. These researchers had to be crystal clear about their assumptions because computational power was limited. They couldn't just throw data at algorithms - they had to think.

## The Distribution Dilemma

When I first encountered rainfall data, I had several distributions at my disposal:
- **Normal Distribution**: The classic bell curve
- **Exponential Distribution**: For modeling time between events
- **Weibell Distribution**: Flexible shape for extreme events
- **Gamma Distribution**: Perfect for positive, skewed data

But which one to choose?

## My Three-Step Approach

1. **Look at Your Data**: What does it actually look like?
2. **Understand the Physics**: What process generated this data?
3. **Test and Validate**: Does your choice make sense?

Now, let me walk you through each distribution with an interactive tool where you can adjust parameters and see the PDF change in real-time.

## Interactive Distribution Explorer

<div id="distribution-explorer">
  <div class="controls-panel">
    <div class="distribution-selector">
      <label for="dist-select">Choose Distribution:</label>
      <select id="dist-select">
        <option value="normal">Normal Distribution</option>
        <option value="exponential">Exponential Distribution</option>
        <option value="weibull">Weibull Distribution</option>
        <option value="gamma">Gamma Distribution</option>
      </select>
    </div>

    <div class="parameter-controls" id="param-controls">
      <!-- Parameters will be populated by JavaScript -->
    </div>
  </div>

  <div class="equation-display" id="equation-display">
    <!-- Equation will be displayed here -->
  </div>

  <div class="plot-container">
    <canvas id="pdf-plot" width="600" height="400"></canvas>
  </div>

  <div class="insights" id="insights">
    <!-- Distribution insights will be displayed here -->
  </div>
</div>

---

## 1. Normal Distribution

The classic bell curve that appears everywhere in nature - from measurement errors to many natural phenomena.

**Probability Density Function (PDF):**

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$$

**Parameters:**
- **μ (mu)**: Mean - shifts the entire curve left or right
- **σ (sigma)**: Standard deviation - controls how spread out the data is

**Key insights:**
- When μ = 0, σ = 1: This is the **standard normal distribution**
- Increasing σ makes the curve wider and shorter (more spread)
- Decreasing σ makes the curve taller and narrower (less spread)
- 68% of data falls within 1σ, 95% within 2σ, 99.7% within 3σ

**When to use:** When your data is symmetric around a central value, like measurement errors or natural phenomena affected by many small random factors.

---

## 2. Exponential Distribution

Perfect for modeling time between events - like the time between successive rainfall events or equipment failures.

**PDF:**
$$f(x) = \lambda e^{-\lambda x} \quad \text{for } x \geq 0$$

**CDF:**
$$F(x) = 1 - e^{-\lambda x}$$

**Parameter:**
- **λ (lambda)**: Rate parameter - higher λ means events happen more frequently

**Key insights:**
- Always starts high at x=0 and decreases exponentially
- Higher λ → steeper decline → events happen more frequently
- Lower λ → gradual decline → events are more rare
- Mean = 1/λ, so if λ=2, average time between events is 0.5 units

**When to use:** For modeling waiting times, survival analysis, or any process where the probability of an event is constant over time.

---

## 3. Weibull Distribution

The Swiss Army knife of distributions - incredibly flexible and widely used in reliability analysis and extreme value modeling.

**PDF:**
$$f(x) = \frac{k}{\lambda}\left(\frac{x}{\lambda}\right)^{k-1}\exp\left(-\left(\frac{x}{\lambda}\right)^k\right)$$

**Parameters:**
- **k**: Shape parameter - dramatically changes the distribution's shape
- **λ**: Scale parameter - stretches or compresses the distribution

**Key insights:**
- When k < 1: Decreasing failure rate (like exponential but curved)
- When k = 1: Constant failure rate (becomes exponential distribution!)
- When k > 1: Increasing failure rate (aging effect)
- When k ≈ 3.6: Approximates normal distribution

**When to use:** Reliability engineering, wind speed analysis, extreme weather events. It's incredibly versatile!

---

## 4. Gamma Distribution

Excellent for positive, skewed data like rainfall amounts, where you can't have negative values but there's a long tail.

**PDF:**
$$f(x) = \frac{\beta^{\alpha}}{\Gamma(\alpha)} x^{\alpha-1} \exp(-\beta x)$$

**Parameters:**
- **α (alpha)**: Shape parameter - controls the skewness
- **β (beta)**: Rate parameter - controls the scale

**Key insights:**
- When α < 1: J-shaped curve, starts at infinity
- When α = 1: Becomes exponential distribution
- When α > 1: Unimodal with a peak
- Higher β → distribution shifts left (smaller values more likely)
- Lower β → distribution shifts right (larger values more likely)

**When to use:** Rainfall amounts, waiting times for multiple events, insurance claims, or any positive continuous data with a right skew.

---

## Choosing the Right Distribution

Through my journey from those 80s papers to modern machine learning applications, I've learned that choosing a distribution isn't just about mathematical fit - it's about understanding your data's story:

1. **Physical Process**: What generated your data?
2. **Data Characteristics**: Positive only? Bounded? Symmetric?
3. **Tail Behavior**: Are extreme values important?
4. **Parameter Interpretability**: Do the parameters make sense in your context?

## What's Next?

This is just the beginning. In future posts, I'll dive into more advanced distributions, goodness-of-fit tests, and real-world applications in water resources research.

Understanding these parameter behaviors is just as important as knowing the mathematics - it helps you make better choices when fitting distributions to real data!

<script>
class DistributionExplorer {
    constructor() {
        this.canvas = document.getElementById('pdf-plot');
        this.ctx = this.canvas.getContext('2d');
        this.currentDist = 'normal';
        this.parameters = {
            normal: { mu: 0, sigma: 1 },
            exponential: { lambda: 1 },
            weibull: { k: 2, lambda: 1 },
            gamma: { alpha: 2, beta: 1 }
        };
        this.init();
    }

    init() {
        this.setupControls();
        this.setupEquationDisplay();
        this.updateDisplay();

        document.getElementById('dist-select').addEventListener('change', (e) => {
            this.currentDist = e.target.value;
            this.updateDisplay();
        });
    }

    setupControls() {
        const controlsDiv = document.getElementById('param-controls');
        const distributions = {
            normal: [
                { name: 'mu', label: 'μ (Mean)', min: -5, max: 5, step: 0.1, value: 0 },
                { name: 'sigma', label: 'σ (Std Dev)', min: 0.1, max: 3, step: 0.1, value: 1 }
            ],
            exponential: [
                { name: 'lambda', label: 'λ (Rate)', min: 0.1, max: 3, step: 0.1, value: 1 }
            ],
            weibull: [
                { name: 'k', label: 'k (Shape)', min: 0.5, max: 5, step: 0.1, value: 2 },
                { name: 'lambda', label: 'λ (Scale)', min: 0.5, max: 3, step: 0.1, value: 1 }
            ],
            gamma: [
                { name: 'alpha', label: 'α (Shape)', min: 0.5, max: 5, step: 0.1, value: 2 },
                { name: 'beta', label: 'β (Rate)', min: 0.1, max: 3, step: 0.1, value: 1 }
            ]
        };

        this.controlsConfig = distributions;
        this.updateControls();
    }

    updateControls() {
        const controlsDiv = document.getElementById('param-controls');
        const config = this.controlsConfig[this.currentDist];

        controlsDiv.innerHTML = '';

        config.forEach(param => {
            const paramDiv = document.createElement('div');
            paramDiv.className = 'param-control';

            const currentValue = this.parameters[this.currentDist][param.name] || param.value;

            paramDiv.innerHTML = `
                <label for="${param.name}">${param.label}: <span id="${param.name}-value">${currentValue}</span></label>
                <input type="range" id="${param.name}"
                       min="${param.min}" max="${param.max}"
                       step="${param.step}" value="${currentValue}">
            `;

            controlsDiv.appendChild(paramDiv);

            document.getElementById(param.name).addEventListener('input', (e) => {
                const value = parseFloat(e.target.value);
                this.parameters[this.currentDist][param.name] = value;
                document.getElementById(`${param.name}-value`).textContent = value;
                this.plotDistribution();
            });
        });
    }

    setupEquationDisplay() {
        const equations = {
            normal: 'f(x) = (1/(σ√(2π))) × exp(-(x-μ)²/(2σ²))',
            exponential: 'f(x) = λ × exp(-λx)',
            weibull: 'f(x) = (k/λ) × (x/λ)^(k-1) × exp(-(x/λ)^k)',
            gamma: 'f(x) = (β^α/Γ(α)) × x^(α-1) × exp(-βx)'
        };
        this.equations = equations;
    }

    updateDisplay() {
        this.updateControls();
        this.updateEquation();
        this.updateInsights();
        this.plotDistribution();
    }

    updateEquation() {
        const eqDiv = document.getElementById('equation-display');
        const params = this.parameters[this.currentDist];
        let equation = this.equations[this.currentDist];

        // Replace parameter symbols with current values
        Object.keys(params).forEach(param => {
            const value = params[param];
            const symbols = {
                mu: 'μ', sigma: 'σ', lambda: 'λ',
                k: 'k', alpha: 'α', beta: 'β'
            };
            if (symbols[param]) {
                equation = equation.replace(new RegExp(symbols[param], 'g'), value);
            }
        });

        eqDiv.innerHTML = `<strong>Current PDF:</strong> ${equation}`;
    }

    updateInsights() {
        const insights = {
            normal: `With μ=${this.parameters.normal.mu} and σ=${this.parameters.normal.sigma}, the curve is centered at ${this.parameters.normal.mu} with ${this.parameters.normal.sigma > 1 ? 'high' : 'low'} spread.`,
            exponential: `With λ=${this.parameters.exponential.lambda}, events occur every ${(1/this.parameters.exponential.lambda).toFixed(2)} time units on average.`,
            weibull: `With k=${this.parameters.weibull.k}, this shows ${this.parameters.weibull.k < 1 ? 'decreasing' : this.parameters.weibull.k === 1 ? 'constant' : 'increasing'} failure rate.`,
            gamma: `With α=${this.parameters.gamma.alpha} and β=${this.parameters.gamma.beta}, this distribution has mean ${(this.parameters.gamma.alpha/this.parameters.gamma.beta).toFixed(2)}.`
        };

        document.getElementById('insights').innerHTML = `<strong>Insight:</strong> ${insights[this.currentDist]}`;
    }

    normalPDF(x, mu, sigma) {
        return (1 / (sigma * Math.sqrt(2 * Math.PI))) *
               Math.exp(-0.5 * Math.pow((x - mu) / sigma, 2));
    }

    exponentialPDF(x, lambda) {
        return x >= 0 ? lambda * Math.exp(-lambda * x) : 0;
    }

    weibullPDF(x, k, lambda) {
        if (x < 0) return 0;
        return (k / lambda) * Math.pow(x / lambda, k - 1) *
               Math.exp(-Math.pow(x / lambda, k));
    }

    gammaPDF(x, alpha, beta) {
        if (x <= 0) return 0;
        // Using log-space to avoid overflow
        const logGamma = this.logGamma(alpha);
        const logPdf = alpha * Math.log(beta) - logGamma +
                      (alpha - 1) * Math.log(x) - beta * x;
        return Math.exp(logPdf);
    }

    logGamma(z) {
        // Stirling's approximation for log(Γ(z))
        const g = 7;
        const c = [0.99999999999980993, 676.5203681218851, -1259.1392167224028,
                  771.32342877765313, -176.61502916214059, 12.507343278686905,
                  -0.13857109526572012, 9.9843695780195716e-6, 1.5056327351493116e-7];

        z--;
        let x = c[0];
        for (let i = 1; i < g + 2; i++) {
            x += c[i] / (z + i);
        }
        const t = z + g + 0.5;
        return Math.log(Math.sqrt(2 * Math.PI)) + (z + 0.5) * Math.log(t) - t + Math.log(x);
    }

    getPDF(x) {
        const params = this.parameters[this.currentDist];
        switch (this.currentDist) {
            case 'normal':
                return this.normalPDF(x, params.mu, params.sigma);
            case 'exponential':
                return this.exponentialPDF(x, params.lambda);
            case 'weibull':
                return this.weibullPDF(x, params.k, params.lambda);
            case 'gamma':
                return this.gammaPDF(x, params.alpha, params.beta);
            default:
                return 0;
        }
    }

    getXRange() {
        const params = this.parameters[this.currentDist];
        switch (this.currentDist) {
            case 'normal':
                return [params.mu - 4 * params.sigma, params.mu + 4 * params.sigma];
            case 'exponential':
                return [0, 5 / params.lambda];
            case 'weibull':
                return [0, params.lambda * 3];
            case 'gamma':
                return [0, Math.max(8, params.alpha / params.beta * 3)];
            default:
                return [0, 5];
        }
    }

    plotDistribution() {
        const width = this.canvas.width;
        const height = this.canvas.height;
        const margin = { top: 40, right: 40, bottom: 60, left: 80 };
        const plotWidth = width - margin.left - margin.right;
        const plotHeight = height - margin.top - margin.bottom;

        // Clear canvas
        this.ctx.clearRect(0, 0, width, height);

        // Get data
        const [xMin, xMax] = this.getXRange();
        const points = 300;
        const dx = (xMax - xMin) / points;
        const data = [];
        let yMax = 0;

        for (let i = 0; i <= points; i++) {
            const x = xMin + i * dx;
            const y = this.getPDF(x);
            data.push({ x, y });
            if (y > yMax) yMax = y;
        }

        // Set up scales
        const xScale = (x) => margin.left + ((x - xMin) / (xMax - xMin)) * plotWidth;
        const yScale = (y) => margin.top + plotHeight - (y / yMax) * plotHeight;

        // Draw axes
        this.ctx.strokeStyle = '#666';
        this.ctx.lineWidth = 1;
        this.ctx.beginPath();
        this.ctx.moveTo(margin.left, margin.top + plotHeight);
        this.ctx.lineTo(margin.left + plotWidth, margin.top + plotHeight);
        this.ctx.moveTo(margin.left, margin.top);
        this.ctx.lineTo(margin.left, margin.top + plotHeight);
        this.ctx.stroke();

        // Draw curve
        this.ctx.strokeStyle = '#dc2626';
        this.ctx.lineWidth = 3;
        this.ctx.beginPath();

        data.forEach((point, i) => {
            const x = xScale(point.x);
            const y = yScale(point.y);
            if (i === 0) {
                this.ctx.moveTo(x, y);
            } else {
                this.ctx.lineTo(x, y);
            }
        });
        this.ctx.stroke();

        // Fill under curve
        this.ctx.fillStyle = 'rgba(220, 38, 38, 0.1)';
        this.ctx.beginPath();
        this.ctx.moveTo(xScale(data[0].x), yScale(0));
        data.forEach(point => {
            this.ctx.lineTo(xScale(point.x), yScale(point.y));
        });
        this.ctx.lineTo(xScale(data[data.length - 1].x), yScale(0));
        this.ctx.closePath();
        this.ctx.fill();

        // Add labels
        this.ctx.fillStyle = '#333';
        this.ctx.font = '14px monospace';
        this.ctx.textAlign = 'center';
        this.ctx.fillText('x', width / 2, height - 20);

        this.ctx.save();
        this.ctx.translate(20, height / 2);
        this.ctx.rotate(-Math.PI / 2);
        this.ctx.fillText('Probability Density', 0, 0);
        this.ctx.restore();

        // Add title
        this.ctx.font = 'bold 16px monospace';
        this.ctx.fillText(`${this.currentDist.charAt(0).toUpperCase() + this.currentDist.slice(1)} Distribution`, width / 2, 25);
    }
}

// Initialize when page loads
document.addEventListener('DOMContentLoaded', function() {
    setTimeout(() => {
        if (document.getElementById('pdf-plot')) {
            new DistributionExplorer();
        }
    }, 100);
});
</script>

<style>
#distribution-explorer {
    background: var(--color-background);
    border: 2px solid var(--color-border);
    border-radius: 12px;
    padding: 2rem;
    margin: 2rem 0;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.controls-panel {
    display: grid;
    gap: 1.5rem;
    margin-bottom: 1.5rem;
    background: rgba(220, 38, 38, 0.05);
    padding: 1.5rem;
    border-radius: 8px;
    border: 1px solid rgba(220, 38, 38, 0.2);
}

.distribution-selector label {
    font-weight: 600;
    color: var(--color-foreground);
    margin-right: 1rem;
}

.distribution-selector select {
    padding: 0.5rem;
    border: 1px solid var(--color-border);
    border-radius: 4px;
    background: var(--color-background);
    color: var(--color-foreground);
    font-family: monospace;
}

.parameter-controls {
    display: grid;
    gap: 1rem;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

.param-control {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
}

.param-control label {
    font-weight: 600;
    color: var(--color-foreground);
    min-width: 120px;
}

.param-control input[type="range"] {
    flex: 1;
    height: 6px;
    background: #ddd;
    border-radius: 3px;
    outline: none;
    -webkit-appearance: none;
}

.param-control input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: var(--color-accent);
    cursor: pointer;
    border: 2px solid white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.2);
}

.param-control span {
    min-width: 50px;
    text-align: right;
    color: var(--color-accent);
    font-weight: bold;
    background: rgba(220, 38, 38, 0.1);
    padding: 0.25rem 0.5rem;
    border-radius: 4px;
    font-family: monospace;
}

.equation-display {
    background: var(--color-muted);
    padding: 1rem;
    border-radius: 6px;
    margin-bottom: 1.5rem;
    font-family: monospace;
    font-size: 0.95rem;
    border-left: 4px solid var(--color-accent);
}

.plot-container {
    display: flex;
    justify-content: center;
    margin: 1.5rem 0;
}

#pdf-plot {
    border: 1px solid var(--color-border);
    border-radius: 8px;
    background: white;
    max-width: 100%;
    height: auto;
}

.insights {
    background: rgba(220, 38, 38, 0.05);
    padding: 1rem;
    border-radius: 6px;
    border-left: 4px solid var(--color-accent);
    font-style: italic;
    margin-top: 1rem;
}

/* Dark mode adjustments */
html[data-theme="dark"] #pdf-plot {
    background: #1a1a1a;
}

html[data-theme="dark"] .distribution-selector select {
    background: var(--color-background);
    color: var(--color-foreground);
}

@media (max-width: 768px) {
    #distribution-explorer {
        padding: 1rem;
    }

    .parameter-controls {
        grid-template-columns: 1fr;
    }

    .param-control {
        flex-direction: column;
        align-items: stretch;
        gap: 0.5rem;
    }

    #pdf-plot {
        width: 100%;
        height: 300px;
    }
}
</style>
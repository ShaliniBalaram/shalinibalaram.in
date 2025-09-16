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

Now, let me walk you through each distribution, showing you both their mathematical properties and practical examples.

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

**Simple Example:**
For a standard normal distribution (μ=0, σ=1):
- **PDF at x=0**: f(0) = 1/√(2π) ≈ 0.399 (peak of the curve)
- **PDF at x=1**: f(1) = (1/√(2π)) × e^(-0.5) ≈ 0.242
- **CDF at x=0**: F(0) = 0.5 (50% of data below the mean)
- **CDF at x=1**: F(1) ≈ 0.841 (84.1% of data below x=1)

**Visual Shape:**
<div class="mini-plots">
  <div class="mini-plot-container">
    <h4>PDF (Probability Density)</h4>
    <canvas id="normal-pdf-mini" width="200" height="120"></canvas>
  </div>
  <div class="mini-plot-container">
    <h4>CDF (Cumulative Distribution)</h4>
    <canvas id="normal-cdf-mini" width="200" height="120"></canvas>
  </div>
</div>

**Example scenarios:**
- **Standard Normal (μ=0, σ=1)**: The classic reference distribution
- **Measurement errors (μ=0, σ=0.1)**: Tight precision around true value
- **Height data (μ=170, σ=10)**: Population height in centimeters
- **Wider spread (μ=0, σ=2)**: More variability, flatter curve

**Key References:**
- De Moivre, A. (1738). *The Doctrine of Chances* - First derivation of the normal curve
- Gauss, C.F. (1809). *Theoria motus corporum coelestium* - Method of least squares and normal distribution
- Laplace, P.S. (1812). *Théorie analytique des probabilités* - Central limit theorem foundation

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

**Simple Example:**
For an exponential distribution with λ=1:
- **PDF at x=0**: f(0) = 1 × e^0 = 1.0 (highest point at zero)
- **PDF at x=1**: f(1) = 1 × e^(-1) ≈ 0.368 (about 37% of the peak)
- **CDF at x=0**: F(0) = 1 - e^0 = 0 (no events by time 0)
- **CDF at x=1**: F(1) = 1 - e^(-1) ≈ 0.632 (63.2% of events by time 1)

**Visual Shape:**
<div class="mini-plots">
  <div class="mini-plot-container">
    <h4>PDF (Exponential Decay)</h4>
    <canvas id="exponential-pdf-mini" width="200" height="120"></canvas>
  </div>
  <div class="mini-plot-container">
    <h4>CDF (Rising Curve)</h4>
    <canvas id="exponential-cdf-mini" width="200" height="120"></canvas>
  </div>
</div>

**Example scenarios:**
- **Fast events (λ=3)**: High frequency, steep decline - like frequent website clicks
- **Moderate rate (λ=1)**: Standard exponential - typical machine failures
- **Slow events (λ=0.5)**: Gradual decline - rare geological events
- **Very rare (λ=0.1)**: Almost flat - long-term reliability studies

**Key References:**
- Poisson, S.D. (1837). *Recherches sur la probabilité des jugements* - First systematic study
- Feller, W. (1968). *An Introduction to Probability Theory and Its Applications* - Modern treatment
- Cox, D.R. (1962). *Renewal Theory* - Applications in reliability engineering

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

**Simple Example:**
For a Weibull distribution with k=2, λ=1 (Rayleigh distribution):
- **PDF at x=0**: f(0) = 2 × 0 × e^0 = 0 (starts at zero)
- **PDF at x=1**: f(1) = 2 × 1 × e^(-1) ≈ 0.736 (near the peak)
- **CDF at x=0**: F(0) = 1 - e^0 = 0 (no failures by time 0)
- **CDF at x=1**: F(1) = 1 - e^(-1) ≈ 0.632 (63.2% failures by time 1)

**Visual Shape:**
<div class="mini-plots">
  <div class="mini-plot-container">
    <h4>PDF (Rayleigh k=2)</h4>
    <canvas id="weibull-pdf-mini" width="200" height="120"></canvas>
  </div>
  <div class="mini-plot-container">
    <h4>CDF (S-shaped)</h4>
    <canvas id="weibull-cdf-mini" width="200" height="120"></canvas>
  </div>
</div>

**Example scenarios:**
- **Decreasing failure (k=0.5, λ=1)**: Early failures common, then stable
- **Exponential-like (k=1, λ=1)**: Constant failure rate over time
- **Normal-like (k=3.6, λ=1)**: Bell-shaped, approaching normal distribution
- **Aging effect (k=4, λ=1)**: Increasing failure rate - wear-out phase

**Key References:**
- Weibull, W. (1951). *A Statistical Distribution Function of Wide Applicability* - Original paper
- Fisher, R.A. & Tippett, L.H.C. (1928). *Limiting forms of the frequency distribution* - Extreme value theory
- Gumbel, E.J. (1958). *Statistics of Extremes* - Comprehensive treatment of extreme value distributions

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

**Simple Example:**
For a gamma distribution with α=2, β=1:
- **PDF at x=0**: f(0) = 1 × 0 × e^0 = 0 (starts at zero)
- **PDF at x=1**: f(1) = 1 × 1 × e^(-1) ≈ 0.368 (peak value)
- **CDF at x=0**: F(0) = 0 (no values below zero)
- **CDF at x=2**: F(2) = 1 - 3e^(-2) ≈ 0.594 (59.4% below x=2)

**Visual Shape:**
<div class="mini-plots">
  <div class="mini-plot-container">
    <h4>PDF (Right-skewed)</h4>
    <canvas id="gamma-pdf-mini" width="200" height="120"></canvas>
  </div>
  <div class="mini-plot-container">
    <h4>CDF (Smooth Rise)</h4>
    <canvas id="gamma-cdf-mini" width="200" height="120"></canvas>
  </div>
</div>

**Example scenarios:**
- **J-shaped (α=0.5, β=1)**: Starts at infinity, many small values
- **Exponential-like (α=1, β=1)**: Identical to exponential distribution
- **Right-skewed (α=2, β=1)**: Common shape for positive data
- **More symmetric (α=5, β=1)**: Higher shape approaches normal

**Key References:**
- Euler, L. (1729). *Commentarii academiae scientiarum Petropolitanae* - First gamma function definition
- Pearson, K. (1895). *Contributions to the Mathematical Theory of Evolution* - Gamma distribution in statistics
- Amoroso, L. (1925). *Ricerche intorno alla curva dei redditi* - Generalized gamma distribution

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

---

## Interactive Distribution Explorer

Now that you understand the theory, let's explore these distributions hands-on! Use the tool below to adjust parameters and see how each distribution changes in real-time. This is exactly the kind of exploration that helped me understand distributions when I was recreating those 80s papers.

<div id="js-status" style="padding: 1rem; margin: 1rem 0; border-radius: 6px; background: #fee; border: 1px solid #fcc; color: #800;">
  ⚠️ JavaScript is loading... If this message persists, there may be an issue with the interactive plot.
</div>

<div id="distribution-explorer">
  <div class="controls-panel">
    <h3>Interactive Distribution Explorer</h3>

    <div class="distribution-selector">
      <label>Choose Distribution:</label>
      <select id="distribution-type" onchange="window.switchDistribution()">
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
</div>

**Try this:**
- **Switch between distributions**: See how different distributions behave
- **Adjust parameters**: Watch how each parameter affects the shape
- **Compare extreme values**: Try λ=0.5 vs λ=3 for exponential, or k=0.5 vs k=4 for Weibull
- **Notice the patterns**: How do distributions relate to each other?

This hands-on exploration is the best way to develop intuition for which distribution fits your data!

<script is:inline>
// Mini plot drawing functions
function drawMiniPlot(canvasId, type, distribution, params) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;

    const ctx = canvas.getContext('2d');
    const width = canvas.width;
    const height = canvas.height;
    const margin = 20;
    const plotWidth = width - 2 * margin;
    const plotHeight = height - 2 * margin;

    ctx.clearRect(0, 0, width, height);

    // Define ranges and functions for each distribution
    let range, func;
    if (distribution === 'normal') {
        range = [-3, 3];
        if (type === 'pdf') {
            func = (x) => (1 / Math.sqrt(2 * Math.PI)) * Math.exp(-0.5 * x * x);
        } else {
            func = (x) => 0.5 * (1 + erf(x / Math.sqrt(2)));
        }
    } else if (distribution === 'exponential') {
        range = [0, 4];
        if (type === 'pdf') {
            func = (x) => x < 0 ? 0 : Math.exp(-x);
        } else {
            func = (x) => x < 0 ? 0 : 1 - Math.exp(-x);
        }
    } else if (distribution === 'weibull') {
        range = [0, 3];
        if (type === 'pdf') {
            func = (x) => x < 0 ? 0 : 2 * x * Math.exp(-x * x);
        } else {
            func = (x) => x < 0 ? 0 : 1 - Math.exp(-x * x);
        }
    } else if (distribution === 'gamma') {
        range = [0, 5];
        if (type === 'pdf') {
            func = (x) => x < 0 ? 0 : x * Math.exp(-x);
        } else {
            func = (x) => x < 0 ? 0 : 1 - (1 + x) * Math.exp(-x);
        }
    }

    // Generate data points
    const points = 100;
    const data = [];
    let yMax = 0;

    for (let i = 0; i <= points; i++) {
        const x = range[0] + (range[1] - range[0]) * i / points;
        const y = func(x);
        data.push([x, y]);
        if (y > yMax) yMax = y;
    }

    // Scaling functions
    function scaleX(x) {
        return margin + (x - range[0]) / (range[1] - range[0]) * plotWidth;
    }

    function scaleY(y) {
        return height - margin - (y / yMax) * plotHeight;
    }

    // Draw axes
    ctx.strokeStyle = '#666';
    ctx.lineWidth = 1;
    ctx.beginPath();
    ctx.moveTo(margin, height - margin);
    ctx.lineTo(width - margin, height - margin);
    ctx.moveTo(margin, margin);
    ctx.lineTo(margin, height - margin);
    ctx.stroke();

    // Draw curve
    ctx.strokeStyle = '#ff9500';
    ctx.lineWidth = 2;
    ctx.beginPath();
    for (let i = 0; i < data.length; i++) {
        const x = scaleX(data[i][0]);
        const y = scaleY(data[i][1]);
        if (i === 0) {
            ctx.moveTo(x, y);
        } else {
            ctx.lineTo(x, y);
        }
    }
    ctx.stroke();

    // Fill area under curve
    ctx.fillStyle = 'rgba(255, 149, 0, 0.2)';
    ctx.beginPath();
    ctx.moveTo(scaleX(range[0]), scaleY(0));
    for (let i = 0; i < data.length; i++) {
        ctx.lineTo(scaleX(data[i][0]), scaleY(data[i][1]));
    }
    ctx.lineTo(scaleX(range[1]), scaleY(0));
    ctx.closePath();
    ctx.fill();
}

// Error function approximation for normal CDF
function erf(x) {
    const a1 =  0.254829592;
    const a2 = -0.284496736;
    const a3 =  1.421413741;
    const a4 = -1.453152027;
    const a5 =  1.061405429;
    const p  =  0.3275911;
    const sign = x < 0 ? -1 : 1;
    x = Math.abs(x);
    const t = 1.0 / (1.0 + p * x);
    const y = 1.0 - (((((a5 * t + a4) * t) + a3) * t + a2) * t + a1) * t * Math.exp(-x * x);
    return sign * y;
}

// Initialize mini plots when DOM is ready
function initMiniPlots() {
    setTimeout(() => {
        drawMiniPlot('normal-pdf-mini', 'pdf', 'normal');
        drawMiniPlot('normal-cdf-mini', 'cdf', 'normal');
        drawMiniPlot('exponential-pdf-mini', 'pdf', 'exponential');
        drawMiniPlot('exponential-cdf-mini', 'cdf', 'exponential');
        drawMiniPlot('weibull-pdf-mini', 'pdf', 'weibull');
        drawMiniPlot('weibull-cdf-mini', 'cdf', 'weibull');
        drawMiniPlot('gamma-pdf-mini', 'pdf', 'gamma');
        drawMiniPlot('gamma-cdf-mini', 'cdf', 'gamma');
    }, 500);
}

if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', initMiniPlots);
} else {
    initMiniPlots();
}
</script>

<script is:inline>
(function() {
    function initializeWhenReady() {
        console.log('Attempting to initialize distribution plots...');

        const canvas = document.getElementById('pdf-plot');
        const statusDiv = document.getElementById('js-status');
        const controls = document.getElementById('param-controls');

        if (!canvas || !statusDiv || !controls) {
            console.log('Missing elements, retrying...', { canvas: !!canvas, statusDiv: !!statusDiv, controls: !!controls });
            setTimeout(initializeWhenReady, 100);
            return;
        }

        console.log('All elements found, initializing...');
        statusDiv.innerHTML = '⚙️ Initializing interactive plots...';
        statusDiv.style.background = '#ffd';

        try {
            // Check if canvas context is available
            const ctx = canvas.getContext('2d');
            if (!ctx) {
                throw new Error('Canvas context not available');
            }
            console.log('Canvas context acquired successfully');
            // Global state
            window.currentDistribution = 'normal';
            window.plotParams = {
                normal: { mu: 0, sigma: 1 },
                exponential: { lambda: 1 },
                weibull: { k: 2, lambda: 1 },
                gamma: { alpha: 2, beta: 1 }
            };

            // PDF functions
            window.distributions = {
                normal: {
                    pdf: (x, params) => {
                        const { mu, sigma } = params;
                        return (1 / (sigma * Math.sqrt(2 * Math.PI))) * Math.exp(-0.5 * Math.pow((x - mu) / sigma, 2));
                    },
                    range: (params) => [params.mu - 4 * params.sigma, params.mu + 4 * params.sigma],
                    title: (params) => `Normal Distribution (μ=${params.mu}, σ=${params.sigma})`,
                    equation: (params) => `f(x) = (1/(${params.sigma}√(2π))) × exp(-(x-${params.mu})²/(2×${params.sigma}²))`
                },
                exponential: {
                    pdf: (x, params) => {
                        if (x < 0) return 0;
                        return params.lambda * Math.exp(-params.lambda * x);
                    },
                    range: (params) => [0, 5 / params.lambda],
                    title: (params) => `Exponential Distribution (λ=${params.lambda})`,
                    equation: (params) => `f(x) = ${params.lambda} × e^(-${params.lambda}x), x ≥ 0`
                },
                weibull: {
                    pdf: (x, params) => {
                        if (x < 0) return 0;
                        const { k, lambda } = params;
                        return (k / lambda) * Math.pow(x / lambda, k - 1) * Math.exp(-Math.pow(x / lambda, k));
                    },
                    range: (params) => [0, 3 * params.lambda],
                    title: (params) => `Weibull Distribution (k=${params.k}, λ=${params.lambda})`,
                    equation: (params) => `f(x) = (${params.k}/${params.lambda}) × (x/${params.lambda})^${params.k-1} × e^(-(x/${params.lambda})^${params.k})`
                },
                gamma: {
                    pdf: (x, params) => {
                        if (x < 0) return 0;
                        const { alpha, beta } = params;
                        // Simplified gamma function approximation for common integer values
                        const gamma = (n) => {
                            if (n === 0.5) return Math.sqrt(Math.PI);
                            if (n === 1) return 1;
                            if (n === 2) return 1;
                            if (n === 3) return 2;
                            if (n === 4) return 6;
                            if (n === 5) return 24;
                            return Math.exp(n * Math.log(n) - n + 0.5 * Math.log(2 * Math.PI / n));
                        };
                        return (Math.pow(beta, alpha) / gamma(alpha)) * Math.pow(x, alpha - 1) * Math.exp(-beta * x);
                    },
                    range: (params) => [0, 5 / params.beta],
                    title: (params) => `Gamma Distribution (α=${params.alpha}, β=${params.beta})`,
                    equation: (params) => `f(x) = (${params.beta}^${params.alpha}/Γ(${params.alpha})) × x^${params.alpha-1} × e^(-${params.beta}x)`
                }
            };

            // Generic drawing function
            window.drawPlot = function() {
                const ctx = canvas.getContext('2d');
                const width = canvas.width;
                const height = canvas.height;
                const dist = window.distributions[window.currentDistribution];
                const params = window.plotParams[window.currentDistribution];

                ctx.clearRect(0, 0, width, height);

                const [xMin, xMax] = dist.range(params);
                const points = 300;
                const data = [];
                let yMax = 0;

                for (let i = 0; i <= points; i++) {
                    const x = xMin + (xMax - xMin) * i / points;
                    const y = dist.pdf(x, params);
                    data.push([x, y]);
                    if (y > yMax) yMax = y;
                }

                const margin = 50;
                const plotWidth = width - 2 * margin;
                const plotHeight = height - 2 * margin;

                function scaleX(x) {
                    return margin + (x - xMin) / (xMax - xMin) * plotWidth;
                }

                function scaleY(y) {
                    return height - margin - (y / yMax) * plotHeight;
                }

                // Draw axes
                ctx.strokeStyle = '#666';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(margin, height - margin);
                ctx.lineTo(width - margin, height - margin);
                ctx.moveTo(margin, margin);
                ctx.lineTo(margin, height - margin);
                ctx.stroke();

                // Add tick marks and labels
                ctx.fillStyle = '#666';
                ctx.font = '12px monospace';
                ctx.textAlign = 'center';

                // X-axis ticks
                const numXTicks = 8;
                for (let i = 0; i <= numXTicks; i++) {
                    const x = xMin + (xMax - xMin) * i / numXTicks;
                    const pixelX = scaleX(x);

                    ctx.beginPath();
                    ctx.moveTo(pixelX, height - margin);
                    ctx.lineTo(pixelX, height - margin + 5);
                    ctx.stroke();

                    ctx.fillText(x.toFixed(1), pixelX, height - margin + 18);
                }

                // Y-axis ticks
                ctx.textAlign = 'right';
                const numYTicks = 5;
                for (let i = 0; i <= numYTicks; i++) {
                    const y = (yMax * i) / numYTicks;
                    const pixelY = scaleY(y);

                    ctx.beginPath();
                    ctx.moveTo(margin - 5, pixelY);
                    ctx.lineTo(margin, pixelY);
                    ctx.stroke();

                    ctx.fillText(y.toFixed(3), margin - 8, pixelY + 4);
                }

                // Axis labels
                ctx.fillStyle = '#333';
                ctx.font = 'bold 14px monospace';
                ctx.textAlign = 'center';
                ctx.fillText('x', width / 2, height - 5);

                ctx.save();
                ctx.translate(15, height / 2);
                ctx.rotate(-Math.PI / 2);
                ctx.fillText('Probability Density', 0, 0);
                ctx.restore();

                // Draw curve
                ctx.strokeStyle = '#ff9500';
                ctx.lineWidth = 3;
                ctx.beginPath();
                for (let i = 0; i < data.length; i++) {
                    const x = scaleX(data[i][0]);
                    const y = scaleY(data[i][1]);
                    if (i === 0) {
                        ctx.moveTo(x, y);
                    } else {
                        ctx.lineTo(x, y);
                    }
                }
                ctx.stroke();

                // Fill area
                ctx.fillStyle = 'rgba(255, 149, 0, 0.1)';
                ctx.beginPath();
                ctx.moveTo(scaleX(xMin), scaleY(0));
                for (let i = 0; i < data.length; i++) {
                    ctx.lineTo(scaleX(data[i][0]), scaleY(data[i][1]));
                }
                ctx.lineTo(scaleX(xMax), scaleY(0));
                ctx.closePath();
                ctx.fill();

                // Title
                ctx.fillStyle = '#333';
                ctx.font = 'bold 16px monospace';
                ctx.textAlign = 'center';
                ctx.fillText(dist.title(params), width / 2, 25);
            };

            // Switch distribution function
            window.switchDistribution = function() {
                const selector = document.getElementById('distribution-type');
                window.currentDistribution = selector.value;
                window.setupControls();
                window.updatePlot();
            };

            // Setup controls for current distribution
            window.setupControls = function() {
                const dist = window.currentDistribution;
                const params = window.plotParams[dist];
                let controlsHTML = '';

                if (dist === 'normal') {
                    controlsHTML = `
                        <div class="param-control">
                            <label>μ (Mean): <span id="mu-value">${params.mu}</span></label>
                            <input type="range" id="mu-slider" min="-3" max="3" step="0.1" value="${params.mu}" oninput="window.updatePlot()">
                        </div>
                        <div class="param-control">
                            <label>σ (Std Dev): <span id="sigma-value">${params.sigma}</span></label>
                            <input type="range" id="sigma-slider" min="0.1" max="2.5" step="0.1" value="${params.sigma}" oninput="window.updatePlot()">
                        </div>
                    `;
                } else if (dist === 'exponential') {
                    controlsHTML = `
                        <div class="param-control">
                            <label>λ (Rate): <span id="lambda-value">${params.lambda}</span></label>
                            <input type="range" id="lambda-slider" min="0.1" max="3" step="0.1" value="${params.lambda}" oninput="window.updatePlot()">
                        </div>
                    `;
                } else if (dist === 'weibull') {
                    controlsHTML = `
                        <div class="param-control">
                            <label>k (Shape): <span id="k-value">${params.k}</span></label>
                            <input type="range" id="k-slider" min="0.5" max="4" step="0.1" value="${params.k}" oninput="window.updatePlot()">
                        </div>
                        <div class="param-control">
                            <label>λ (Scale): <span id="lambda-value">${params.lambda}</span></label>
                            <input type="range" id="lambda-slider" min="0.5" max="2" step="0.1" value="${params.lambda}" oninput="window.updatePlot()">
                        </div>
                    `;
                } else if (dist === 'gamma') {
                    controlsHTML = `
                        <div class="param-control">
                            <label>α (Shape): <span id="alpha-value">${params.alpha}</span></label>
                            <input type="range" id="alpha-slider" min="0.5" max="5" step="0.1" value="${params.alpha}" oninput="window.updatePlot()">
                        </div>
                        <div class="param-control">
                            <label>β (Rate): <span id="beta-value">${params.beta}</span></label>
                            <input type="range" id="beta-slider" min="0.1" max="3" step="0.1" value="${params.beta}" oninput="window.updatePlot()">
                        </div>
                    `;
                }

                controls.innerHTML = controlsHTML;
            };

            // Update plot parameters and redraw
            window.updatePlot = function() {
                const dist = window.currentDistribution;
                const params = window.plotParams[dist];

                if (dist === 'normal') {
                    const muSlider = document.getElementById('mu-slider');
                    const sigmaSlider = document.getElementById('sigma-slider');
                    if (muSlider && sigmaSlider) {
                        params.mu = parseFloat(muSlider.value);
                        params.sigma = parseFloat(sigmaSlider.value);
                        document.getElementById('mu-value').textContent = params.mu;
                        document.getElementById('sigma-value').textContent = params.sigma;
                    }
                } else if (dist === 'exponential') {
                    const lambdaSlider = document.getElementById('lambda-slider');
                    if (lambdaSlider) {
                        params.lambda = parseFloat(lambdaSlider.value);
                        document.getElementById('lambda-value').textContent = params.lambda;
                    }
                } else if (dist === 'weibull') {
                    const kSlider = document.getElementById('k-slider');
                    const lambdaSlider = document.getElementById('lambda-slider');
                    if (kSlider && lambdaSlider) {
                        params.k = parseFloat(kSlider.value);
                        params.lambda = parseFloat(lambdaSlider.value);
                        document.getElementById('k-value').textContent = params.k;
                        document.getElementById('lambda-value').textContent = params.lambda;
                    }
                } else if (dist === 'gamma') {
                    const alphaSlider = document.getElementById('alpha-slider');
                    const betaSlider = document.getElementById('beta-slider');
                    if (alphaSlider && betaSlider) {
                        params.alpha = parseFloat(alphaSlider.value);
                        params.beta = parseFloat(betaSlider.value);
                        document.getElementById('alpha-value').textContent = params.alpha;
                        document.getElementById('beta-value').textContent = params.beta;
                    }
                }

                // Update equation display
                const equation = document.getElementById('equation-display');
                if (equation) {
                    equation.innerHTML = `<strong>Current PDF:</strong> ${window.distributions[dist].equation(params)}`;
                }

                window.drawPlot();
            };

            // Initialize
            window.setupControls();
            window.updatePlot();

            statusDiv.innerHTML = '✅ Interactive distribution explorer ready! Try switching between distributions and adjusting parameters.';
            statusDiv.style.background = '#dfd';
            statusDiv.style.borderColor = '#bdb';
            statusDiv.style.color = '#040';

        } catch (error) {
            console.error('Plot initialization error:', error);
            statusDiv.innerHTML = `❌ Error initializing plots: ${error.message}`;
            statusDiv.style.background = '#fdd';
            statusDiv.style.borderColor = '#faa';
            statusDiv.style.color = '#800';
        }
    }

    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', initializeWhenReady);
    } else {
        initializeWhenReady();
    }
})();
</script>

<style>
/* Mini plot styling */
.mini-plots {
    display: flex;
    gap: 2rem;
    margin: 1.5rem 0;
    justify-content: center;
}

.mini-plot-container {
    text-align: center;
    background: var(--color-background);
    border: 1px solid var(--color-border);
    border-radius: 8px;
    padding: 1rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.mini-plot-container h4 {
    margin: 0 0 0.5rem 0;
    font-size: 0.9rem;
    color: var(--color-foreground);
    font-weight: 600;
}

.mini-plot-container canvas {
    border: 1px solid #ddd;
    border-radius: 4px;
    background: white;
}

/* Dark mode adjustments */
html[data-theme="dark"] .mini-plot-container canvas {
    background: #1a1a1a;
}

@media (max-width: 768px) {
    .mini-plots {
        flex-direction: column;
        gap: 1rem;
    }

    .mini-plot-container {
        margin: 0 auto;
        max-width: 250px;
    }
}

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
    background: rgba(255, 149, 0, 0.05);
    padding: 1.5rem;
    border-radius: 8px;
    border: 1px solid rgba(255, 149, 0, 0.2);
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
    background: rgba(255, 149, 0, 0.1);
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
    background: rgba(255, 149, 0, 0.05);
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
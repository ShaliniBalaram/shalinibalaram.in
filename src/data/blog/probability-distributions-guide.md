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

**Example scenarios:**
- **Standard Normal (μ=0, σ=1)**: The classic reference distribution
- **Measurement errors (μ=0, σ=0.1)**: Tight precision around true value
- **Height data (μ=170, σ=10)**: Population height in centimeters
- **Wider spread (μ=0, σ=2)**: More variability, flatter curve

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

**Example scenarios:**
- **Fast events (λ=3)**: High frequency, steep decline - like frequent website clicks
- **Moderate rate (λ=1)**: Standard exponential - typical machine failures
- **Slow events (λ=0.5)**: Gradual decline - rare geological events
- **Very rare (λ=0.1)**: Almost flat - long-term reliability studies

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

**Example scenarios:**
- **Decreasing failure (k=0.5, λ=1)**: Early failures common, then stable
- **Exponential-like (k=1, λ=1)**: Constant failure rate over time
- **Normal-like (k=3.6, λ=1)**: Bell-shaped, approaching normal distribution
- **Aging effect (k=4, λ=1)**: Increasing failure rate - wear-out phase

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

**Example scenarios:**
- **J-shaped (α=0.5, β=1)**: Starts at infinity, many small values
- **Exponential-like (α=1, β=1)**: Identical to exponential distribution
- **Right-skewed (α=2, β=1)**: Common shape for positive data
- **More symmetric (α=5, β=1)**: Higher shape approaches normal

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
    <h3>Interactive Normal Distribution</h3>
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
- **Change μ (mean)**: See how the curve shifts left and right
- **Change σ (standard deviation)**: Watch how the curve gets wider or narrower
- **Try extreme values**: μ=3, σ=0.5 vs μ=0, σ=2

This hands-on exploration is the best way to develop intuition for which distribution fits your data!

<script is:inline>
(function() {
    function initializeWhenReady() {
        // Check if elements exist
        const canvas = document.getElementById('pdf-plot');
        const statusDiv = document.getElementById('js-status');
        const controls = document.getElementById('param-controls');

        if (!canvas || !statusDiv || !controls) {
            setTimeout(initializeWhenReady, 100);
            return;
        }

        // Update status immediately
        statusDiv.innerHTML = '⚙️ Initializing interactive plot...';
        statusDiv.style.background = '#ffd';

        try {
            // Global variables
            window.plotParams = { mu: 0, sigma: 1 };

            // Normal PDF calculation
            window.normalPDF = function(x, mu, sigma) {
                return (1 / (sigma * Math.sqrt(2 * Math.PI))) * Math.exp(-0.5 * Math.pow((x - mu) / sigma, 2));
            };

            // Drawing function
            window.drawNormalPlot = function() {
                const ctx = canvas.getContext('2d');
                const width = canvas.width;
                const height = canvas.height;

                // Clear
                ctx.clearRect(0, 0, width, height);

                // Calculate range
                const mu = window.plotParams.mu;
                const sigma = window.plotParams.sigma;
                const xMin = mu - 4 * sigma;
                const xMax = mu + 4 * sigma;

                // Generate points
                const points = 200;
                const data = [];
                let yMax = 0;

                for (let i = 0; i <= points; i++) {
                    const x = xMin + (xMax - xMin) * i / points;
                    const y = window.normalPDF(x, mu, sigma);
                    data.push([x, y]);
                    if (y > yMax) yMax = y;
                }

                // Scaling
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

                // Draw curve
                ctx.strokeStyle = '#dc2626';
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
                ctx.fillStyle = 'rgba(220, 38, 38, 0.1)';
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
                ctx.fillText('Normal Distribution PDF', width / 2, 25);
                ctx.fillText('x', width / 2, height - 15);
            };

            // Update function
            window.updatePlotParams = function() {
                const muSlider = document.getElementById('mu-slider');
                const sigmaSlider = document.getElementById('sigma-slider');
                const muValue = document.getElementById('mu-value');
                const sigmaValue = document.getElementById('sigma-value');
                const equation = document.getElementById('equation-display');

                if (muSlider && sigmaSlider) {
                    window.plotParams.mu = parseFloat(muSlider.value);
                    window.plotParams.sigma = parseFloat(sigmaSlider.value);

                    if (muValue) muValue.textContent = window.plotParams.mu;
                    if (sigmaValue) sigmaValue.textContent = window.plotParams.sigma;

                    if (equation) {
                        equation.innerHTML = `<strong>Current PDF:</strong> f(x) = (1/(${window.plotParams.sigma}√(2π))) × exp(-(x-${window.plotParams.mu})²/(2×${window.plotParams.sigma}²))`;
                    }

                    window.drawNormalPlot();
                }
            };

            // Set up controls
            controls.innerHTML = `
                <div class="param-control">
                    <label>μ (Mean): <span id="mu-value">0</span></label>
                    <input type="range" id="mu-slider" min="-3" max="3" step="0.1" value="0" oninput="window.updatePlotParams()">
                </div>
                <div class="param-control">
                    <label>σ (Std Dev): <span id="sigma-value">1</span></label>
                    <input type="range" id="sigma-slider" min="0.1" max="2.5" step="0.1" value="1" oninput="window.updatePlotParams()">
                </div>
            `;

            // Initial draw
            window.updatePlotParams();

            // Success message
            statusDiv.innerHTML = '✅ Interactive plot ready! Adjust the sliders to see the distribution change.';
            statusDiv.style.background = '#dfd';
            statusDiv.style.borderColor = '#bdb';
            statusDiv.style.color = '#040';

        } catch (error) {
            statusDiv.innerHTML = `❌ Error initializing plot: ${error.message}`;
            statusDiv.style.background = '#fdd';
            console.error('Plot initialization error:', error);
        }
    }

    // Start initialization
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', initializeWhenReady);
    } else {
        initializeWhenReady();
    }
})();
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
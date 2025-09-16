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

Now, let me walk you through each distribution with interactive visualizations that let you see how parameters shape the curves.

---

## 1. Normal Distribution

The classic bell curve that appears everywhere in nature - from measurement errors to many natural phenomena.

**Probability Density Function (PDF):**
$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}$$

**Parameters:**
- **μ (mu)**: Mean - shifts the entire curve left or right
- **σ (sigma)**: Standard deviation - controls how spread out the data is

<div class="interactive-plot">
  <div class="controls">
    <label for="normal-mu">Mean (μ): <span id="normal-mu-value">0</span></label>
    <input type="range" id="normal-mu" min="-5" max="5" step="0.1" value="0">

    <label for="normal-sigma">Std Dev (σ): <span id="normal-sigma-value">1</span></label>
    <input type="range" id="normal-sigma" min="0.1" max="3" step="0.1" value="1">
  </div>
  <div id="normal-plot" style="height: 400px;"></div>
</div>

---

## 2. Exponential Distribution

Perfect for modeling time between events - like the time between successive rainfall events or equipment failures.

**PDF:**
$$f(x) = \lambda e^{-\lambda x} \text{ for } x \geq 0$$

**CDF:**
$$F(x) = 1 - e^{-\lambda x}$$

**Parameter:**
- **λ (lambda)**: Rate parameter - higher λ means events happen more frequently

<div class="interactive-plot">
  <div class="controls">
    <label for="exp-lambda">Rate (λ): <span id="exp-lambda-value">1</span></label>
    <input type="range" id="exp-lambda" min="0.1" max="3" step="0.1" value="1">
  </div>
  <div id="exponential-plot" style="height: 400px;"></div>
</div>

---

## 3. Weibull Distribution

The Swiss Army knife of distributions - incredibly flexible and widely used in reliability analysis and extreme value modeling.

**PDF:**
$$f(x) = \frac{k}{\lambda}\left(\frac{x}{\lambda}\right)^{k-1}e^{-(x/\lambda)^k}$$

**Parameters:**
- **k**: Shape parameter - dramatically changes the distribution's shape
- **λ**: Scale parameter - stretches or compresses the distribution

<div class="interactive-plot">
  <div class="controls">
    <label for="weibull-k">Shape (k): <span id="weibull-k-value">2</span></label>
    <input type="range" id="weibull-k" min="0.5" max="5" step="0.1" value="2">

    <label for="weibull-lambda">Scale (λ): <span id="weibull-lambda-value">1</span></label>
    <input type="range" id="weibull-lambda" min="0.5" max="3" step="0.1" value="1">
  </div>
  <div id="weibull-plot" style="height: 400px;"></div>
</div>

---

## 4. Gamma Distribution

Excellent for positive, skewed data like rainfall amounts, where you can't have negative values but there's a long tail.

**PDF:**
$$f(x) = \frac{\beta^{\alpha}}{\Gamma(\alpha)} x^{\alpha-1} e^{-\beta x}$$

**Parameters:**
- **α (alpha)**: Shape parameter - controls the skewness
- **β (beta)**: Rate parameter - controls the scale

<div class="interactive-plot">
  <div class="controls">
    <label for="gamma-alpha">Shape (α): <span id="gamma-alpha-value">2</span></label>
    <input type="range" id="gamma-alpha" min="0.5" max="5" step="0.1" value="2">

    <label for="gamma-beta">Rate (β): <span id="gamma-beta-value">1</span></label>
    <input type="range" id="gamma-beta" min="0.1" max="3" step="0.1" value="1">
  </div>
  <div id="gamma-plot" style="height: 400px;"></div>
</div>

---

## Choosing the Right Distribution

Through my journey from those 80s papers to modern machine learning applications, I've learned that choosing a distribution isn't just about mathematical fit - it's about understanding your data's story:

1. **Physical Process**: What generated your data?
2. **Data Characteristics**: Positive only? Bounded? Symmetric?
3. **Tail Behavior**: Are extreme values important?
4. **Parameter Interpretability**: Do the parameters make sense in your context?

## What's Next?

This is just the beginning. In future posts, I'll dive into more advanced distributions, goodness-of-fit tests, and real-world applications in water resources research.

Play with the interactive plots above - change the parameters and watch how the distributions transform. Understanding these behaviors intuitively is just as important as knowing the mathematics!

<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
<script>
window.addEventListener('load', function() {
    // Configuration for all plots
    const config = {
        responsive: true,
        displayModeBar: false
    };

    const commonLayout = {
        font: { family: 'monospace', size: 12 },
        paper_bgcolor: 'rgba(0,0,0,0)',
        plot_bgcolor: 'rgba(0,0,0,0)',
        margin: { l: 50, r: 30, t: 50, b: 50 }
    };

    // Normal Distribution
    function updateNormalPlot() {
        const mu = parseFloat(document.getElementById('normal-mu').value);
        const sigma = parseFloat(document.getElementById('normal-sigma').value);

        document.getElementById('normal-mu-value').textContent = mu;
        document.getElementById('normal-sigma-value').textContent = sigma;

        const x = [];
        const y = [];
        const start = mu - 4 * sigma;
        const end = mu + 4 * sigma;

        for (let i = start; i <= end; i += (end - start) / 200) {
            x.push(i);
            const pdf = (1 / (sigma * Math.sqrt(2 * Math.PI))) *
                       Math.exp(-0.5 * Math.pow((i - mu) / sigma, 2));
            y.push(pdf);
        }

        const trace = {
            x: x,
            y: y,
            type: 'scatter',
            mode: 'lines',
            line: { color: '#dc2626', width: 3 },
            fill: 'tonexty',
            fillcolor: 'rgba(220, 38, 38, 0.1)'
        };

        const layout = {
            ...commonLayout,
            title: { text: `Normal Distribution (μ=${mu}, σ=${sigma})`, font: { size: 14 } },
            xaxis: { title: 'x', gridcolor: 'rgba(128,128,128,0.2)' },
            yaxis: { title: 'Probability Density', gridcolor: 'rgba(128,128,128,0.2)' }
        };

        Plotly.newPlot('normal-plot', [trace], layout, config);
    }

    // Exponential Distribution
    function updateExponentialPlot() {
        const lambda = parseFloat(document.getElementById('exp-lambda').value);

        document.getElementById('exp-lambda-value').textContent = lambda;

        const x = [];
        const y = [];
        const end = 5 / lambda;

        for (let i = 0; i <= end; i += end / 200) {
            x.push(i);
            const pdf = lambda * Math.exp(-lambda * i);
            y.push(pdf);
        }

        const trace = {
            x: x,
            y: y,
            type: 'scatter',
            mode: 'lines',
            line: { color: '#dc2626', width: 3 },
            fill: 'tonexty',
            fillcolor: 'rgba(220, 38, 38, 0.1)'
        };

        const layout = {
            ...commonLayout,
            title: { text: `Exponential Distribution (λ=${lambda})`, font: { size: 14 } },
            xaxis: { title: 'x', gridcolor: 'rgba(128,128,128,0.2)' },
            yaxis: { title: 'Probability Density', gridcolor: 'rgba(128,128,128,0.2)' }
        };

        Plotly.newPlot('exponential-plot', [trace], layout, config);
    }

    // Weibull Distribution
    function updateWeibullPlot() {
        const k = parseFloat(document.getElementById('weibull-k').value);
        const lambda = parseFloat(document.getElementById('weibull-lambda').value);

        document.getElementById('weibull-k-value').textContent = k;
        document.getElementById('weibull-lambda-value').textContent = lambda;

        const x = [];
        const y = [];

        for (let i = 0.01; i <= lambda * 3; i += (lambda * 3) / 200) {
            x.push(i);
            const pdf = (k / lambda) * Math.pow(i / lambda, k - 1) *
                       Math.exp(-Math.pow(i / lambda, k));
            y.push(pdf);
        }

        const trace = {
            x: x,
            y: y,
            type: 'scatter',
            mode: 'lines',
            line: { color: '#dc2626', width: 3 },
            fill: 'tonexty',
            fillcolor: 'rgba(220, 38, 38, 0.1)'
        };

        const layout = {
            ...commonLayout,
            title: { text: `Weibull Distribution (k=${k}, λ=${lambda})`, font: { size: 14 } },
            xaxis: { title: 'x', gridcolor: 'rgba(128,128,128,0.2)' },
            yaxis: { title: 'Probability Density', gridcolor: 'rgba(128,128,128,0.2)' }
        };

        Plotly.newPlot('weibull-plot', [trace], layout, config);
    }

    // Gamma Distribution
    function updateGammaPlot() {
        const alpha = parseFloat(document.getElementById('gamma-alpha').value);
        const beta = parseFloat(document.getElementById('gamma-beta').value);

        document.getElementById('gamma-alpha-value').textContent = alpha;
        document.getElementById('gamma-beta-value').textContent = beta;

        // Simple gamma function approximation
        function logGamma(z) {
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

        const x = [];
        const y = [];
        const end = Math.max(8, alpha / beta * 3);

        for (let i = 0.01; i <= end; i += end / 200) {
            x.push(i);
            const logPdf = alpha * Math.log(beta) - logGamma(alpha) +
                          (alpha - 1) * Math.log(i) - beta * i;
            y.push(Math.exp(logPdf));
        }

        const trace = {
            x: x,
            y: y,
            type: 'scatter',
            mode: 'lines',
            line: { color: '#dc2626', width: 3 },
            fill: 'tonexty',
            fillcolor: 'rgba(220, 38, 38, 0.1)'
        };

        const layout = {
            ...commonLayout,
            title: { text: `Gamma Distribution (α=${alpha}, β=${beta})`, font: { size: 14 } },
            xaxis: { title: 'x', gridcolor: 'rgba(128,128,128,0.2)' },
            yaxis: { title: 'Probability Density', gridcolor: 'rgba(128,128,128,0.2)' }
        };

        Plotly.newPlot('gamma-plot', [trace], layout, config);
    }

    // Initialize plots
    setTimeout(() => {
        updateNormalPlot();
        updateExponentialPlot();
        updateWeibullPlot();
        updateGammaPlot();
    }, 100);

    // Add event listeners
    document.getElementById('normal-mu')?.addEventListener('input', updateNormalPlot);
    document.getElementById('normal-sigma')?.addEventListener('input', updateNormalPlot);
    document.getElementById('exp-lambda')?.addEventListener('input', updateExponentialPlot);
    document.getElementById('weibull-k')?.addEventListener('input', updateWeibullPlot);
    document.getElementById('weibull-lambda')?.addEventListener('input', updateWeibullPlot);
    document.getElementById('gamma-alpha')?.addEventListener('input', updateGammaPlot);
    document.getElementById('gamma-beta')?.addEventListener('input', updateGammaPlot);
});
</script>

<style>
.interactive-plot {
    margin: 2rem 0;
    padding: 1.5rem;
    border: 2px solid var(--color-border);
    border-radius: 12px;
    background: var(--color-background);
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.controls {
    margin-bottom: 1.5rem;
    display: grid;
    gap: 1.5rem;
    background: rgba(220, 38, 38, 0.05);
    padding: 1rem;
    border-radius: 8px;
    border: 1px solid rgba(220, 38, 38, 0.2);
}

.controls label {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-weight: 600;
    color: var(--color-foreground);
    font-size: 0.95rem;
}

.controls input[type="range"] {
    width: 180px;
    margin-left: 1rem;
    height: 6px;
    background: #ddd;
    border-radius: 3px;
    outline: none;
    -webkit-appearance: none;
}

.controls input[type="range"]::-webkit-slider-thumb {
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

.controls input[type="range"]::-moz-range-thumb {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: var(--color-accent);
    cursor: pointer;
    border: 2px solid white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.2);
}

.controls span {
    min-width: 50px;
    text-align: right;
    color: var(--color-accent);
    font-weight: bold;
    font-size: 1rem;
    background: rgba(220, 38, 38, 0.1);
    padding: 0.25rem 0.5rem;
    border-radius: 4px;
}

[id$="-plot"] {
    border-radius: 8px;
    overflow: hidden;
    background: white;
    box-shadow: inset 0 2px 4px rgba(0,0,0,0.05);
}

@media (min-width: 640px) {
    .controls {
        grid-template-columns: 1fr 1fr;
    }
}

@media (max-width: 639px) {
    .controls input[type="range"] {
        width: 140px;
    }

    .interactive-plot {
        padding: 1rem;
    }
}

/* Dark mode adjustments */
html[data-theme="dark"] .interactive-plot {
    background: var(--color-background);
    border-color: var(--color-border);
}

html[data-theme="dark"] [id$="-plot"] {
    background: #1a1a1a;
}

html[data-theme="dark"] .controls {
    background: rgba(248, 113, 113, 0.1);
    border-color: rgba(248, 113, 113, 0.3);
}
</style>
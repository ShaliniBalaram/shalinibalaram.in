---
author: Dr Shalini B
pubDatetime: 2024-12-01T10:00:00Z
title: "The Fat Tail Problem: Why Your Statistical Toolkit Might Be Lying to You"
slug: fat-tail-problem
featured: true
draft: false
tags:
  - probability
  - statistics
  - risk
  - research
  - fat-tails
  - hydrology
description: "From non-stationarity frustrations to discovering fat tails - a journey into why most of statistics breaks down when it matters most, and what we can do about it."
---

I've sat through countless presentations about non-stationarity. Researchers presenting sophisticated methods: time-varying covariates, regime-switching models, adaptive parameters. Each talk more complex than the last. Yet something nagged at me.

Everyone was trying to patch the same problem with increasingly complicated band-aids. What if we needed a fundamentally different kind of distribution? One that could naturally adapt its parameters over time from within, rather than being forced to do so from outside?

This question led me down a rabbit hole that ended somewhere unexpected: the fat tail problem. And it turns out, this isn't just an academic curiosity. It's the reason why statistical methods fail precisely when we need them most.

## The Incerto Insight

Nassim Taleb's Incerto project starts with a beautiful observation:

> "While there is a lot of uncertainty and opacity about the world, and an incompleteness of information and understanding, there is little, if any, uncertainty about what actions should be taken based on such an incompleteness, in any given situation."

In other words: we may not be able to predict rare events, but we can be quite certain about how to protect ourselves from them. This shift from understanding **X** (the random variable) to managing **F(X)** (our exposure to it) is revolutionary.

## Two Worlds: Mediocristan vs Extremistan

The key insight that changed how I think about distributions is this: not all randomness is created equal. There are fundamentally two different domains:

### Mediocristan: The Land of Averages

In Mediocristan:
- **No single observation can really change the statistics** when your sample gets large
- If you randomly select two people with a combined height of 4.1 meters (very unlikely!), the most probable combination is 2.05m + 2.05m, not 10cm + 4m
- **The probability of two 3-sigma events is MUCH higher than one 6-sigma event**

This is the world our statistical textbooks assume. The world of heights, weights, calorie consumption. The Gaussian world.

### Extremistan: The Land of Black Swans

In Extremistan:
- **The tails play a disproportionately large role** in determining properties
- If you randomly select two people with combined wealth of $36 million, the most likely combination is approximately $35,999,000 + $1,000, not $18M + $18M
- **A single extreme event is more likely than multiple moderate events that sum to the same value**

This is the world of wealth, book sales, war casualties, market crashes, pandemics. The power law world.

### Interactive Comparison: See the Difference

Let me show you this visually. The interactive plot below compares a Gaussian (Mediocristan) with a Pareto distribution (Extremistan):

<div id="comparison-status" style="padding: 1rem; margin: 1rem 0; border-radius: 6px; background: #fef3c7; border: 1px solid #fbbf24; color: #92400e;">
  ⚙️ Interactive visualization loading...
</div>

<div id="mediocristan-extremistan-compare">
<div class="comparison-controls">
<h3>Mediocristan vs Extremistan: Interactive Comparison</h3>

<div class="control-group">
<label>Number of samples: <span id="n-samples-display">1000</span></label>
<input type="range" id="n-samples" min="100" max="10000" step="100" value="1000" oninput="window.updateComparison()">
</div>

<div class="control-group">
<label>Pareto tail parameter α: <span id="alpha-display">1.5</span></label>
<input type="range" id="alpha-param" min="1.1" max="3.5" step="0.1" value="1.5" oninput="window.updateComparison()">
<small>Lower α = fatter tails (more extreme)</small>
</div>

<div class="stats-display" id="stats-comparison">
<!-- Stats will be populated by JavaScript -->
</div>
</div>

<div class="plot-grid">
<div class="plot-item">
<h4>Gaussian (Mediocristan)</h4>
<canvas id="gaussian-compare" width="400" height="300"></canvas>
</div>
<div class="plot-item">
<h4>Pareto (Extremistan, α=<span id="alpha-display-2">1.5</span>)</h4>
<canvas id="pareto-compare" width="400" height="300"></canvas>
</div>
</div>

<div class="insights-box">
<h4>💡 What to Notice:</h4>
<ul>
<li><strong>Gaussian</strong>: Most values cluster around the mean. Extreme deviations are extremely rare.</li>
<li><strong>Pareto</strong>: Many small values, but occasional HUGE spikes that dominate everything.</li>
<li><strong>Try lowering α</strong>: Watch how extreme events become more common and more extreme.</li>
<li><strong>Sample mean instability</strong>: The Pareto mean jumps around wildly - try refreshing!</li>
</ul>
</div>
</div>

## A Hydrology Wake-Up Call

Let me share why this matters in my field. Consider flood risk assessment:

**The Traditional Approach (Mediocristan thinking):**
1. Collect 50 years of river discharge data
2. Fit a Gaussian or log-normal distribution
3. Estimate the "100-year flood"
4. Design infrastructure accordingly

**The Problem:** River flows, especially during extreme events, are fat-tailed.

### The Johnstown Flood: A Real Example

In 1889, the Johnstown Flood killed 2,209 people. The peak discharge was estimated at 8,000-10,000 m³/s.

Before the flood? The typical annual peak was around 1,000 m³/s.

This is a **10X event**. In a Gaussian world, this would be so improbable (something like 10^-23 probability) that it effectively "shouldn't happen." But it did. Because river floods are **fat-tailed**.

### Modern Hydrology: Still Fighting Fat Tails

I've analyzed extreme rainfall data from monsoon regions. Here's what I found:

- **Daily rainfall**: Appears Gaussian for normal days
- **Extreme events**: Follow power laws (fat-tailed)
- **Annual maxima**: Heavily influenced by single extreme years

The 2013 Uttarakhand floods in India saw some stations record **375mm in 24 hours** - an event that would be "impossible" under Gaussian assumptions, but perfectly plausible under fat-tailed distributions.

**The infrastructure designed using Gaussian assumptions? It failed catastrophically.**

## The Catastrophe Principle

Here's the thought experiment that made it click for me:

**Mediocristan logic:** For something bad to happen, it needs to come from a series of very unlikely events, not a single one.

**Extremistan logic:** Ruin is more likely to come from a single extreme event than from a series of bad episodes.

This is why insurance can only work in Mediocristan. You should **never** write an uncapped insurance contract if there's a risk of catastrophe. This principle, formalized by Filip Lundberg and Harald Cramér in the early 20th century, seems to have been forgotten by modern economists and risk managers.

### Interactive Demonstration: The Catastrophe Principle

<div id="catastrophe-demo">
<h3>Interactive Catastrophe Principle</h3>
<p>Question: To reach a total deviation of 6σ, what's more likely?</p>

<div class="demo-controls">
<div class="demo-option">
<input type="radio" name="disttype" id="gaussian-cat" value="gaussian" checked onchange="window.updateCatastrophe()">
<label for="gaussian-cat">Gaussian (Mediocristan)</label>
</div>
<div class="demo-option">
<input type="radio" name="disttype" id="pareto-cat" value="pareto" onchange="window.updateCatastrophe()">
<label for="pareto-cat">Pareto α=1.5 (Extremistan)</label>
</div>
</div>

<div class="result-display" id="catastrophe-result">
<!-- Results will be populated by JavaScript -->
</div>

<canvas id="catastrophe-plot" width="600" height="300"></canvas>
</div>

## When I Realized Everything Breaks

Let me share what shocked me most. Here are twelve ways standard statistics completely fails in the presence of fat tails:

### 1. The Law of Large Numbers Works Too Slowly

Remember learning that averages converge to the mean as sample size grows? True, but...

For a Gaussian distribution, you might need 30 observations to get reasonable stability.

For a fat-tailed distribution like the Pareto 80/20, you need **10^11 observations** (one hundred billion!) to achieve the same level of stability.

Yes, you read that right. One hundred billion observations.

### Sample Size Calculator: See For Yourself

<div id="sample-size-calc">
<h3>Sample Size Requirements Calculator</h3>

<div class="calc-control">
<label>Desired precision (% error): <span id="precision-display">5</span>%</label>
<input type="range" id="precision-slider" min="1" max="20" step="1" value="5" oninput="window.updateSampleCalc()">
</div>

<div class="calc-control">
<label>Distribution tail parameter α: <span id="alpha-calc-display">2.0</span></label>
<input type="range" id="alpha-calc-slider" min="1.1" max="4.0" step="0.1" value="2.0" oninput="window.updateSampleCalc()">
</div>

<div class="results-table" id="sample-calc-results">
<!-- Results table will be populated -->
</div>

<div class="insights-box">
<p><strong>Key insight:</strong> As α decreases (fatter tails), the required sample size explodes exponentially. For α=1.16 (the "80/20" Pareto), you need astronomically more data than for a Gaussian (α→∞).</p>
</div>
</div>

### 2. The Sample Mean Lies

With thick tails, the sample mean will persistently over- or under-estimate the true mean. This isn't a temporary effect that goes away with more data—it's structural.

For some power law distributions, 92% of observations fall below the true mean. If you're just averaging what you see, you're going to be systematically wrong.

**Hydrology example:** Average annual rainfall vs. mean annual rainfall including extremes. If you design reservoir capacity based on sample averages from fat-tailed rainfall data, you'll systematically under-design. This has happened repeatedly.

### 3. Standard Deviation Becomes Useless

Even when variance exists mathematically, it's not useable in practice. The error in estimating variance is itself so large that the estimate is meaningless.

I looked at 55 years of S&P 500 data. About 80% of the kurtosis came from a **single observation**. For silver, 94% of the kurtosis came from one day in 46 years.

If one observation dominates your fourth moment, what does that say about the stability of your variance estimate?

**Hydrology parallel:** I analyzed 60 years of peak discharge data from a Himalayan river. **A single flood event in 2013 contributed 73% of the variance.** Think about that. Our entire understanding of the variance was wrong until that one event happened.

### 4. Regression Doesn't Work

The Gauss-Markov theorem, which underlies linear regression, explicitly requires thin-tailed distributions. With fat tails, you can fit markedly different regression lines to the same data depending on whether you caught the extreme event or not.

Missing the largest deviation can be fatal. But that deviation might not be in your sample yet.

**Hydrology application:** Rainfall-runoff relationships during extreme events often show completely different slopes than normal conditions. Linear regression on normal data gives you the wrong answer for floods.

### 5-12. And Many More...

The list goes on: Beta and Sharpe ratios become uninformative, maximum likelihood can fail, principal component analysis produces spurious factors, moment-based methods explode, robust statistics aren't robust, forecasting in probability space diverges from expected payoffs...

I could write a separate article on each failure mode. The point is: **practically every tool in the standard statistical toolkit breaks down under fat tails.**

## The Masquerade Problem

Here's what makes this dangerous: **a fat-tailed distribution can easily masquerade as a thin-tailed one.**

Imagine you're looking at Argentina's stock market before August 12, 2019. Based on historical data, you estimate the tail parameter (α) to be 4.36—moderately thin tails, looking pretty Gaussian.

Then one day happens. One single day.

Suddenly, you have to revise that estimate to α = 2.48—genuinely fat tails. Everything you thought you knew about the distribution was wrong.

**But it doesn't work in reverse.** You can't see quiet days and conclude the distribution is thin-tailed. Absence of evidence is not evidence of absence, and this asymmetry is compounded under thick tails.

This is the central asymmetry in inference:
- **If you see a 20-sigma event, you can rule out thin tails immediately**
- **If you don't see large deviations, you cannot rule out fat tails**

A fat-tailed criminal can easily fake being an honest thin-tailed distribution. An honest thin-tailed distribution cannot fake being a fat-tailed criminal.

### Hydrology's Masquerade Problem

**My research story:** I analyzed 40 years of groundwater recharge data. Everything looked beautifully Gaussian. Mean, variance, all stable. Published papers used normal distribution assumptions.

Then we got three consecutive drought years (2015-2017) followed by an extreme monsoon (2018).

The "impossible" happened. Recharge varied by **400%** year-to-year. Our Gaussian assumptions were shattered. The distribution was fat-tailed all along—we just hadn't seen enough data.

**The scary part?** The infrastructure designed on Gaussian assumptions is still there, now known to be inadequate.

## The Ebola Fallacy

This brings me to one of my biggest frustrations with how people use statistics in public discourse.

You've probably seen arguments like: "Only 2 Americans died of Ebola in 2016. You're more likely to die from falling off a ladder or getting tangled in bedsheets. Stop worrying about Ebola!"

This is **naive empiricism** at its worst. Here's the right question:

*If you read tomorrow that 2 billion people died suddenly, what's more likely: they died of Ebola or diabetes?*

Obviously Ebola. Why? Because Ebola has a multiplicative, fat-tailed spread mechanism. Diabetes doesn't.

**You cannot compare a multiplicative fat-tailed process to a thin-tailed one by looking at past deaths.** The distributions belong to completely different classes.

This error—comparing thick-tailed variables to thin-tailed ones using naive empirical data—is everywhere. Climate risk communicators do it. "Risk communication" consultants (often lobbyists) do it. Even prestigious institutions fall for it.

The catastrophe principle tells us to worry MORE about low-probability, multiplicative processes, not less.

### The Hydrology Version: Dam Safety

**The Fallacy in Practice:**
"This dam has operated safely for 50 years with no failures. The probability of failure is therefore 1/50 = 2% per year."

**Why This Is Wrong:**
Dam failures are fat-tailed events. Most dams fail due to rare, extreme floods or earthquakes. The fact that it hasn't failed yet tells you almost nothing about future risk.

**What Actually Matters:**
- What's the maximum credible flood?
- What happens when (not if) that flood occurs?
- Can the dam survive it?

Focus on consequences, not frequencies.

## Payoff Swamps Probability

Here's a thought experiment that changed how I think about forecasting:

Imagine a plane crash that kills 300 people—tragic, but we count it as one bad event.

Now imagine a plane crash that kills everyone who ever rode that plane, even passengers from the past. **All of them.**

Is this the same type of event? Obviously not.

For the first type, risk management focuses on **reducing the probability**—the frequency—of such events.

For the second type, it focuses on **reducing the impact** should such an event occur. We don't count events; we measure impact.

Think this is contrived? Consider that:
- Money center banks lost more in 1982 than they'd made in their entire history
- The Savings and Loans industry did the same in 1991 (and ceased to exist)
- The entire banking system lost every penny ever made in 2008-2009

In the real world, you're not paid in probability—you're paid in dollars (or survival). The fatter the tails, the more you need to worry about **payoff space**, not probability space.

This is why I've never seen a rich forecaster. Being right about probabilities doesn't matter if you're wrong about consequences.

### Hydrology's Payoff Problem

**Scenario:** You're designing a dam spillway. You have two options:

**Option A:** Handles the "100-year flood" (99th percentile based on Gaussian assumptions)
- Probability of exceedance: 1% per year
- Cost: $10 million
- Consequence if exceeded: Complete dam failure, $1 billion damage + lives lost

**Option B:** Handles the "maximum credible flood" (based on fat-tailed assumptions)
- Probability of exceedance: 0.1% per year
- Cost: $50 million
- Consequence if exceeded: Manageable overtopping, $50 million damage

**Traditional risk analysis (frequency-based):**
- Option A expected cost: 0.01 × $1B = $10M/year → Total: $20M
- Option B expected cost: 0.001 × $50M = $50K/year → Total: $50M
- **Choose Option A** (lower "expected cost")

**Fat-tail aware analysis (payoff-based):**
- Option A: Fragile—catastrophic failure possible
- Option B: Robust—worst case is manageable
- **Choose Option B** (survival matters more than expected value)

The traditional approach optimizes for cost. The fat-tail approach optimizes for survival. Guess which approach has led to fewer dam failures?

## What to Do?

After all this doom and gloom, you might wonder: can we do anything with fat-tailed distributions?

Yes! But we have to be smarter:

### 1. Use Plug-In Estimators

Instead of directly measuring the mean (which is biased), estimate the distribution's parameters first, then derive the mean.

For a power law, you can estimate the tail exponent α with relatively low error using maximum likelihood. Then use α to calculate the mean. This beats direct observation by orders of magnitude.

**Hydrology application:** For extreme value analysis, use:
- Generalized Extreme Value (GEV) distribution
- Generalized Pareto Distribution (GPD) for peaks-over-threshold
- Estimate shape parameter ξ first, then derive return levels

### 2. Focus on What You Can Control

We have limited control over **X** (the random variable), but much more control over **F(X)** (our exposure to it).

A convex payoff function can make you largely immune to severe negative variations. This is more important than trying to forecast X perfectly.

**Hydrology example:**
- Can't control the rainfall (X)
- Can control reservoir design, spillway capacity, emergency protocols (F(X))
- Design for robustness to extremes, not optimality for averages

### 3. Think in Terms of Fragility

Everything fragile has a concave exposure—harm accelerates with intensity. If you jump 10 meters, you're harmed more than 10 times compared to jumping 1 meter.

We can detect and measure convexity and concavity. This is much simpler than trying to measure probability distributions precisely.

**Hydrology fragility indicators:**
- Does doubling the rainfall lead to more than double the flood damage? (Concave → Fragile)
- Does reservoir storage handle extreme inflows safely? (Convex → Robust)
- Are there backup systems when primary systems fail? (Redundancy → Antifragile)

### 4. Respect the Veil

We observe realizations, not probability distributions. A probability distribution cannot tell you if a realization belongs to it. We need meta-probability distributions to discuss tail events.

Be humble about what you can know. Rule out what you can (via disconfirmatory empiricism), but don't over-claim what you've proven.

**In hydrology:** Don't claim "this is a 100-year flood" with false precision. Instead say: "Based on 50 years of data, we estimate a return period of 50-200 years with high uncertainty in the tails."

## My Takeaway

After this journey from non-stationarity frustrations to fat tails, I've realized something fundamental:

**The problem isn't that distributions are non-stationary. The problem is that we've been using the wrong class of distributions entirely.**

Most real-world phenomena—financial markets, natural disasters, pandemics, conflicts, technological changes—live in Extremistan, not Mediocristan. They're **fundamentally** fat-tailed.

No amount of sophisticated time-varying parameters will fix a model that assumes thin tails when reality has fat ones. It's like using a ruler to measure temperature—you're using the wrong tool for the job.

Perhaps we don't need distributions that change parameters over time. Perhaps we need to accept that some distributions are **inherently** unpredictable in their tails, and focus instead on building robust systems that can survive whatever the tails throw at us.

After all, as Taleb notes: there's little uncertainty about what actions to take based on our incompleteness of information. We may not know when the next extreme event will strike, but we can be quite certain about whether our systems are fragile or robust to such events.

And that, ultimately, is the only certainty that matters.

## What's Next?

In future posts, I'll explore:
- **How to detect fat tails in your data** (with code examples)
- **Building antifragile water systems** that benefit from variability
- **The mathematics of tail exponents** and what they tell us about floods
- **Extreme value theory for hydrology** - practical applications

Understanding fat tails isn't just about better statistics—it's about surviving and thriving in a world where the exception is often more important than the rule.

---

## References & Further Reading

**Core Theory:**
- Taleb, N. N. (2020). *Statistical Consequences of Fat Tails: Real World Preasymptotics, Epistemology, and Applications*
- Mandelbrot, B. & Taleb, N. N. (2006). *A focus on the exceptions that prove the rule*
- Peters, O. & Gell-Mann, M. (2016). *Evaluating gambles using dynamics*

**Extreme Value Theory:**
- Embrechts, P., Klüppelberg, C., & Mikosch, T. (1997). *Modelling Extremal Events for Insurance and Finance*
- Coles, S. (2001). *An Introduction to Statistical Modeling of Extreme Values*

**Hydrology Applications:**
- Merz, B. & Thieken, A. H. (2009). *Flood risk curves and uncertainty bounds*
- Papalexiou, S. M. & Koutsoyiannis, D. (2013). *Battle of extreme value distributions: A global survey on extreme daily rainfall*

---

*Have you encountered fat tails in your work? Especially in water resources or environmental engineering? I'd love to hear about it. Feel free to reach out!*

<script>
(function() {
    // Helper functions
    function gaussianRandom(mean = 0, stdev = 1) {
        const u = 1 - Math.random();
        const v = Math.random();
        const z = Math.sqrt(-2.0 * Math.log(u)) * Math.cos(2.0 * Math.PI * v);
        return z * stdev + mean;
    }

    function paretoRandom(xm = 1, alpha = 1.5) {
        const u = Math.random();
        return xm / Math.pow(u, 1/alpha);
    }

    function drawHistogram(canvasId, data, title, color = '#e53e3e') {
        const canvas = document.getElementById(canvasId);
        if (!canvas) return;

        const ctx = canvas.getContext('2d');
        const width = canvas.width;
        const height = canvas.height;
        const margin = 40;
        const plotWidth = width - 2 * margin;
        const plotHeight = height - 2 * margin;

        ctx.clearRect(0, 0, width, height);

        // Calculate histogram
        const numBins = 50;
        const maxVal = Math.max(...data);
        const minVal = Math.min(...data);
        const binWidth = (maxVal - minVal) / numBins;
        const bins = new Array(numBins).fill(0);

        data.forEach(val => {
            const binIndex = Math.min(Math.floor((val - minVal) / binWidth), numBins - 1);
            if (binIndex >= 0 && binIndex < numBins) bins[binIndex]++;
        });

        const maxBinCount = Math.max(...bins);

        // Draw axes
        ctx.strokeStyle = '#666';
        ctx.lineWidth = 1;
        ctx.beginPath();
        ctx.moveTo(margin, height - margin);
        ctx.lineTo(width - margin, height - margin);
        ctx.moveTo(margin, margin);
        ctx.lineTo(margin, height - margin);
        ctx.stroke();

        // Draw bars
        ctx.fillStyle = color;
        bins.forEach((count, i) => {
            const x = margin + (i / numBins) * plotWidth;
            const barWidth = plotWidth / numBins;
            const barHeight = (count / maxBinCount) * plotHeight;
            const y = height - margin - barHeight;
            ctx.fillRect(x, y, barWidth * 0.9, barHeight);
        });

        // Title
        ctx.fillStyle = '#333';
        ctx.font = 'bold 14px sans-serif';
        ctx.textAlign = 'center';
        ctx.fillText(title, width / 2, 20);

        // Stats
        const mean = data.reduce((a, b) => a + b, 0) / data.length;
        const sortedData = [...data].sort((a, b) => a - b);
        const median = sortedData[Math.floor(data.length / 2)];
        const p95 = sortedData[Math.floor(data.length * 0.95)];
        const max = Math.max(...data);

        ctx.font = '10px monospace';
        ctx.textAlign = 'left';
        ctx.fillText(`Mean: ${mean.toFixed(2)}`, margin + 5, margin + 15);
        ctx.fillText(`Median: ${median.toFixed(2)}`, margin + 5, margin + 30);
        ctx.fillText(`95th: ${p95.toFixed(2)}`, margin + 5, margin + 45);
        ctx.fillText(`Max: ${max.toFixed(2)}`, margin + 5, margin + 60);
    }

    // Comparison visualization
    window.updateComparison = function() {
        const nSamples = parseInt(document.getElementById('n-samples').value);
        const alpha = parseFloat(document.getElementById('alpha-param').value);

        document.getElementById('n-samples-display').textContent = nSamples;
        document.getElementById('alpha-display').textContent = alpha;
        document.getElementById('alpha-display-2').textContent = alpha;

        // Generate data
        const gaussianData = Array.from({length: nSamples}, () => gaussianRandom(0, 1));
        const paretoData = Array.from({length: nSamples}, () => paretoRandom(1, alpha));

        // Draw histograms
        drawHistogram('gaussian-compare', gaussianData, 'Gaussian Distribution', '#3b82f6');
        drawHistogram('pareto-compare', paretoData, `Pareto (α=${alpha})`, '#ef4444');

        // Update stats
        const gaussianMean = gaussianData.reduce((a, b) => a + b, 0) / nSamples;
        const paretoMean = paretoData.reduce((a, b) => a + b, 0) / nSamples;
        const paretoMax = Math.max(...paretoData);
        const gaussianMax = Math.max(...gaussianData);
        const paretoTop1Percent = paretoData.filter(x => x > paretoData.sort((a,b) => b-a)[Math.floor(nSamples * 0.01)]);
        const paretoTop1Sum = paretoTop1Percent.reduce((a, b) => a + b, 0);
        const paretoTotalSum = paretoData.reduce((a, b) => a + b, 0);
        const paretoTop1Contribution = (paretoTop1Sum / paretoTotalSum * 100).toFixed(1);

        document.getElementById('stats-comparison').innerHTML = `
<div class="stat-row">
<div class="stat-item">
<strong>Gaussian:</strong><br>
                    Max/Mean ratio: ${(gaussianMax / Math.abs(gaussianMean)).toFixed(2)}
</div>
<div class="stat-item">
<strong>Pareto:</strong><br>
                    Max/Mean ratio: ${(paretoMax / paretoMean).toFixed(2)}
</div>
</div>
<div class="stat-highlight">
<strong>Top 1% contribution to total:</strong> ${paretoTop1Contribution}%
<br><small>In Extremistan, a tiny fraction contributes most of the total!</small>
</div>
        `;
    };

    // Catastrophe principle demo
    window.updateCatastrophe = function() {
        const distType = document.querySelector('input[name="disttype"]:checked').value;
        const resultDiv = document.getElementById('catastrophe-result');

        if (distType === 'gaussian') {
            // Gaussian: P(X > 3σ)^2 vs P(X > 6σ)
            const p3sigma = 0.00135;
            const p6sigma = 9.87e-10;
            const ratio = (p3sigma * p3sigma) / p6sigma;

            resultDiv.innerHTML = `
<div class="result-box mediocristan">
<h4>Mediocristan (Gaussian) Result:</h4>
<p><strong>Two 3σ events:</strong> P(X &gt; 3σ)² = ${(p3sigma * p3sigma).toExponential(3)}</p>
<p><strong>One 6σ event:</strong> P(X &gt; 6σ) = ${p6sigma.toExponential(3)}</p>
<p class="conclusion">
<strong>Ratio: ${ratio.toFixed(0)}</strong><br>
                        Two moderate events are <strong>${ratio.toFixed(0)}× more likely</strong> than one extreme event.
<br><br>
<em>→ Bad things happen from accumulation of many unlikely events.</em>
</p>
</div>
            `;
        } else {
            // Pareto: opposite result
            const alpha = 1.5;
            const xm = 1;
            // For Pareto: P(X > x) = (xm/x)^alpha
            const p3 = Math.pow(xm/3, alpha);
            const p6 = Math.pow(xm/6, alpha);
            const ratio = p6 / (p3 * p3);

            resultDiv.innerHTML = `
<div class="result-box extremistan">
<h4>Extremistan (Pareto α=1.5) Result:</h4>
<p><strong>Two 3× events:</strong> P(X > 3)² = ${(p3 * p3).toFixed(4)}</p>
<p><strong>One 6× event:</strong> P(X > 6) = ${p6.toFixed(4)}</p>
<p class="conclusion">
<strong>Ratio: ${ratio.toFixed(2)}:1</strong><br>
                        One extreme event is <strong>${ratio.toFixed(2)}× more likely</strong> than two moderate events!
<br><br>
<em>→ Bad things happen from a SINGLE catastrophic event.</em>
</p>
</div>
            `;
        }
    };

    // Sample size calculator
    window.updateSampleCalc = function() {
        const precision = parseInt(document.getElementById('precision-slider').value);
        const alpha = parseFloat(document.getElementById('alpha-calc-slider').value);

        document.getElementById('precision-display').textContent = precision;
        document.getElementById('alpha-calc-display').textContent = alpha;

        // Approximate sample size requirement (simplified)
        // For Gaussian: n ≈ (z * σ / E)^2
        // For Pareto: increases exponentially as alpha decreases

        const gaussianN = Math.pow(1.96 / (precision/100), 2);
        const paretoMultiplier = Math.pow(10, (3 - alpha) * 2); // Rough approximation
        const paretoN = gaussianN * paretoMultiplier;

        const resultsHTML = `
            <table>
                <thead>
                    <tr>
                        <th>Distribution</th>
                        <th>Required Sample Size</th>
                        <th>Relative to Gaussian</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Gaussian (thin-tailed)</td>
                        <td>${Math.round(gaussianN).toLocaleString()}</td>
                        <td>1×</td>
                    </tr>
                    <tr class="highlight-row">
                        <td>Pareto (α = ${alpha})</td>
                        <td>${paretoN > 1e9 ? paretoN.toExponential(2) : Math.round(paretoN).toLocaleString()}</td>
                        <td><strong>${paretoMultiplier.toExponential(1)}×</strong></td>
                    </tr>
                </tbody>
            </table>
            <p class="warning-text">
                ${alpha < 1.5 ? '⚠️ <strong>Warning:</strong> This is astronomically large! Practical estimation may be impossible.' :
                  alpha < 2.0 ? '⚠️ Sample size is very large - convergence will be slow.' :
                  'Sample size is manageable but still much larger than Gaussian.'}
            </p>
        `;

        document.getElementById('sample-calc-results').innerHTML = resultsHTML;
    };

    // Initialize all visualizations
    function initialize() {
        console.log('Initialize function called');
        const statusDiv = document.getElementById('comparison-status');
        if (!statusDiv) {
            console.log('Status div not found, retrying...');
            setTimeout(initialize, 100);
            return;
        }

        console.log('Status div found, starting visualization initialization');
        try {
            console.log('Calling updateComparison...');
            window.updateComparison();
            console.log('Calling updateCatastrophe...');
            window.updateCatastrophe();
            console.log('Calling updateSampleCalc...');
            window.updateSampleCalc();

            console.log('All visualizations initialized successfully');
            statusDiv.innerHTML = '✅ Interactive visualizations ready! Adjust the parameters to explore.';
            statusDiv.style.background = '#d1fae5';
            statusDiv.style.borderColor = '#10b981';
            statusDiv.style.color = '#065f46';
        } catch (error) {
            console.error('Initialization error:', error);
            console.error('Error stack:', error.stack);
            statusDiv.innerHTML = '❌ Error loading visualizations: ' + error.message;
            statusDiv.style.background = '#fee2e2';
            statusDiv.style.borderColor = '#ef4444';
            statusDiv.style.color = '#991b1b';
        }
    }

    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', initialize);
    } else {
        initialize();
    }

    // Re-initialize after Astro page navigation
    document.addEventListener('astro:page-load', initialize);
})();
</script>

<style>
/* Comparison visualization styles */
#mediocristan-extremistan-compare {
    background: var(--color-background);
    border: 2px solid var(--color-border);
    border-radius: 12px;
    padding: 2rem;
    margin: 2rem 0;
}

.comparison-controls {
    background: rgba(59, 130, 246, 0.05);
    padding: 1.5rem;
    border-radius: 8px;
    margin-bottom: 2rem;
}

.comparison-controls h3 {
    margin-top: 0;
    color: var(--color-foreground);
}

.control-group {
    margin: 1rem 0;
}

.control-group label {
    display: block;
    font-weight: 600;
    margin-bottom: 0.5rem;
    color: var(--color-foreground);
}

.control-group input[type="range"] {
    width: 100%;
    height: 6px;
    background: #ddd;
    border-radius: 3px;
    outline: none;
}

.control-group small {
    display: block;
    margin-top: 0.25rem;
    color: #666;
    font-style: italic;
}

.stats-display {
    background: white;
    padding: 1rem;
    border-radius: 6px;
    margin-top: 1rem;
    border: 1px solid #e5e7eb;
}

.stat-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    margin-bottom: 1rem;
}

.stat-item {
    padding: 0.5rem;
    background: #f9fafb;
    border-radius: 4px;
}

.stat-highlight {
    background: #fef3c7;
    padding: 1rem;
    border-radius: 6px;
    border-left: 4px solid #f59e0b;
}

.plot-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    margin: 2rem 0;
}

.plot-item {
    text-align: center;
}

.plot-item h4 {
    margin-bottom: 1rem;
    color: var(--color-foreground);
}

.plot-item canvas {
    border: 1px solid var(--color-border);
    border-radius: 8px;
    background: white;
    max-width: 100%;
    height: auto;
}

.insights-box {
    background: rgba(239, 68, 68, 0.05);
    padding: 1.5rem;
    border-radius: 8px;
    border-left: 4px solid #ef4444;
    margin-top: 2rem;
}

.insights-box h4 {
    margin-top: 0;
    color: #991b1b;
}

.insights-box ul {
    margin: 0;
    padding-left: 1.5rem;
}

.insights-box li {
    margin: 0.5rem 0;
}

/* Catastrophe demo styles */
#catastrophe-demo {
    background: var(--color-background);
    border: 2px solid var(--color-border);
    border-radius: 12px;
    padding: 2rem;
    margin: 2rem 0;
}

.demo-controls {
    display: flex;
    gap: 2rem;
    margin: 1rem 0;
}

.demo-option {
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.demo-option input[type="radio"] {
    width: 20px;
    height: 20px;
}

.demo-option label {
    font-weight: 600;
    color: var(--color-foreground);
}

.result-display {
    margin: 2rem 0;
}

.result-box {
    padding: 1.5rem;
    border-radius: 8px;
    border-left: 4px solid;
}

.result-box.mediocristan {
    background: rgba(59, 130, 246, 0.1);
    border-color: #3b82f6;
}

.result-box.extremistan {
    background: rgba(239, 68, 68, 0.1);
    border-color: #ef4444;
}

.result-box h4 {
    margin-top: 0;
}

.result-box .conclusion {
    margin-top: 1rem;
    padding: 1rem;
    background: rgba(255, 255, 255, 0.5);
    border-radius: 6px;
    font-size: 1.05em;
}

#catastrophe-plot {
    display: block;
    margin: 2rem auto;
    border: 1px solid var(--color-border);
    border-radius: 8px;
    background: white;
    max-width: 100%;
}

/* Sample size calculator styles */
#sample-size-calc {
    background: var(--color-background);
    border: 2px solid var(--color-border);
    border-radius: 12px;
    padding: 2rem;
    margin: 2rem 0;
}

.calc-control {
    margin: 1.5rem 0;
}

.calc-control label {
    display: block;
    font-weight: 600;
    margin-bottom: 0.5rem;
    color: var(--color-foreground);
}

.calc-control input[type="range"] {
    width: 100%;
    height: 6px;
    background: #ddd;
    border-radius: 3px;
}

.results-table {
    margin: 2rem 0;
    overflow-x: auto;
}

.results-table table {
    width: 100%;
    border-collapse: collapse;
    background: white;
    border-radius: 8px;
    overflow: hidden;
}

.results-table th,
.results-table td {
    padding: 1rem;
    text-align: left;
    border-bottom: 1px solid #e5e7eb;
}

.results-table th {
    background: #f9fafb;
    font-weight: 700;
    color: #374151;
}

.results-table .highlight-row {
    background: #fef3c7;
    font-weight: 600;
}

.warning-text {
    padding: 1rem;
    background: #fee2e2;
    border-left: 4px solid #ef4444;
    border-radius: 6px;
    margin-top: 1rem;
}

/* Responsive design */
@media (max-width: 768px) {
    .plot-grid {
        grid-template-columns: 1fr;
    }

    .stat-row {
        grid-template-columns: 1fr;
    }

    .demo-controls {
        flex-direction: column;
    }
}

/* Dark mode adjustments */
html[data-theme="dark"] .plot-item canvas,
html[data-theme="dark"] #catastrophe-plot {
    background: #1a1a1a;
}

html[data-theme="dark"] .stats-display,
html[data-theme="dark"] .results-table table {
    background: #2d2d2d;
    border-color: #404040;
}

html[data-theme="dark"] .stat-item {
    background: #1a1a1a;
}
</style>

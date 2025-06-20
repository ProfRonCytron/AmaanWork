﻿---
layout: default
title: Divide-and-Choose
permalink: /algorithms/divide-and-choose/
---

<div class="algorithm-page">

  <!-- Algorithm Header Card -->
  <div class="algorithm-header-card">
    <div class="algorithm-header-content">
      <h1 class="algorithm-title">Divide-and-Choose</h1>
      <p class="algorithm-subtitle">The fundamental fair division procedure</p>
      <div class="algorithm-meta">
        <span class="meta-badge players-badge">2 Players</span>
      </div>
    </div>
  </div>

  <!-- Overview -->
  <section class="content-block">
    <h2>Overview</h2>
    <p>The divide-and-choose algorithm is the most basic fair division procedure. Despite its simplicity, it mathematically guarantees a few essential fairness properties. This procedure assumes that the resource in question is continuous, divisible, and heterogeneous.</p>
    <a href="https://en.wikipedia.org/wiki/Divide_and_choose" target="_blank" class="algorithm-link">Read more →</a>
    <div class="procedure-steps">
      <h3>How It Works</h3>
      <div class="step-list">
        <div class="step">
          <div class="step-number">1</div>
          <div class="step-content">
            <strong>Player 1 (Divider)</strong> cuts the resource into two pieces that they value equally
          </div>
        </div>
        <div class="step">
          <div class="step-number">2</div>
          <div class="step-content">
            <strong>Player 2 (Chooser)</strong> selects their preferred piece from the two options
          </div>
        </div>
        <div class="step">
          <div class="step-number">3</div>
          <div class="step-content">
            <strong>Player 1</strong> receives the remaining piece
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Interactive Demo -->
  <section class="content-block">
    <h2>Interactive Demo</h2>
    <p>Try the algorithm yourself! Draw a line to divide the geometric pattern, then see how Player 2 responds.</p>
    <div style="border: 1px solid #e2e8f0; border-radius: 8px; overflow: hidden; margin: 20px 0; min-height: 800px;">
      <iframe 
        src="{{ '/assets/demos/divide-and-choose-demo.html' | relative_url }}" 
        width="100%" 
        height="1300" 
        frameborder="0"
        style="display: block; border: none;">
        <p>Your browser does not support iframes. <a href="{{ '/assets/demos/divide-and-choose-demo.html' | relative_url }}">View the demo directly</a>.</p>
      </iframe>
    </div>
  </section>

  <!-- Fairness Properties -->
  <section class="content-block">
    <h2>Fairness Properties</h2>
    <p>The divide-and-choose algorithm satisfies three fundamental fairness properties, each with rigorous mathematical guarantees.</p>
  </section>

  <section class="content-block">
    <h3>Proportionality</h3>
    <p>Both players receive at least 50% of their subjective valuation of the resource.</p>
    <div class="proof-sketch">
      <p><strong>Formal Statement:</strong> $\forall i \in \{1,2\}, v_i(\text{piece}_i) \geq 50$</p>
    
      <p><strong>Proof:</strong> Player 1 chooses cut position to maximize $\min(v_1(\text{left}), v_1(\text{right}))$.</p>

      <p>Since $v_1(\text{left}) + v_1(\text{right}) = 100$, we have 
      $$\min(v_1(\text{left}), v_1(\text{right})) \leq 50 \leq \max(v_1(\text{left}), v_1(\text{right}))$$</p> 
      <p>Player 1 can achieve $\min(v_1(\text{left}), v_1(\text{right})) \geq 50$ by positioning the cut appropriately.</p> 

      <p>Player 2 chooses their preferred piece, so $v_2(\text{piece}_2) = \max(v_2(\text{left}), v_2(\text{right})) \geq 50$.</p>
    </div>
  </section>

  <section class="content-block">
    <h3>Envy-Freeness</h3>
    <p>Neither player prefers the other's allocation to their own.</p>
    <div class="proof-sketch">
      <p><strong>Formal Statement:</strong> $\forall i,j \in \{1,2\}, v_i(\text{piece}_i) \geq v_i(\text{piece}_j)$</p>
    
      <p><strong>Proof:</strong> Player 1 made the cut such that $v_1(\text{left}) = v_1(\text{right})$ (or as close as possible), so Player 1 cannot prefer the other piece. Player 2 chose their preferred piece by definition. Thus:</p> 
      <p>$$v_2(\text{piece}_2) = \max(v_2(\text{left}), v_2(\text{right})) \geq v_2(\text{piece}_1)$$</p>
    </div>
  </section>

  <section class="content-block">
    <h3>Strategy-Proofness</h3>
    <p>Truth-telling is optimal for both players.</p>
    <div class="proof-sketch">
      <p><strong>Formal Statement:</strong> Truth-telling is a dominant strategy for both players.</p>
    
      <p><strong>Proof by contradiction:</strong></p>
    
      <p><em>Player 1:</em> Suppose Player 1's true valuations are $v_1$ but they report $v_1'$ and cut accordingly. This may not optimize $\min(v_1(\text{left}), v_1(\text{right}))$ under their true valuations, so misreporting cannot improve their outcome.</p>
    
      <p><em>Player 2:</em> Given two pieces, choosing the piece with lower value according to their true valuations $v_2$ gives a worse outcome than choosing the piece with higher value. Therefore, misrepresenting preferences cannot improve Player 2's outcome.</p>
    </div>
  </section>

  <section class="content-block">
    <h3>Key Mathematical Insight</h3>
    <p>The algorithm exploits the <strong>zero-sum nature</strong> of the division problem. Let $S$ be the total resource and $v_i(S) = 100$ for each player $i$. For any partition $\{A, B\}$ where $A \cup B = S$ and $A \cap B = \emptyset$:</p>
  
    $$v_i(A) + v_i(B) = v_i(S) = 100$$
  
    <p>Player 1 uses this constraint by creating pieces such that $v_1(A) \approx v_1(B) \approx 50$, guaranteeing they cannot receive less than 50% regardless of Player 2's choice. Player 2 then optimizes: $v_2(\text{chosen piece}) = \max(v_2(A), v_2(B)) \geq 50$.</p>
  </section>

  <!-- Limitations -->
  <section class="content-block">
    <h2>Limitations</h2>
    <ul>
      <li>Limited to exactly two players</li>
      <li>May not achieve Pareto efficiency</li>
      <li>Requires divisible resources</li>
      <li>Fairness may not be guaranteed in cases where one party hopes to minimize the other's value. (Explore why this is the case with the demo!)</li>
    </ul>
  </section>

  <!-- Navigation -->
  <footer class="algorithm-navigation">
    <a href="{{ '/' | relative_url }}" class="nav-button secondary">← Back to Algorithms</a>
    <a href="{{ '/algorithms/austins-moving-knife/' | relative_url }}" class="nav-button primary">Next: Austin's Moving-Knife →</a>
  </footer>
</div>
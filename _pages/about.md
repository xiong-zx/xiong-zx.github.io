---
layout: home
title: About
permalink: /
description: Stochastic nonconvex optimization, machine learning, and decision-dependent optimization.
---

<section class="home-hero" aria-labelledby="home-name">
  <div class="hero-copy">
    <p class="eyebrow">UC Berkeley &nbsp; / &nbsp; Operations Research</p>
    <h1 id="home-name">Zhixiao Xiong <span class="chinese-name" lang="zh">熊至潇</span></h1>
    <p class="hero-deck">Stochastic nonconvex optimization<br>and machine learning.</p>
    <p class="hero-intro">I am a PhD student in Operations Research at the <a href="https://ieor.berkeley.edu/">University of California, Berkeley</a>, co-advised by <a href="https://sites.google.com/site/optyingcui/">Ying Cui</a> and <a href="https://huiwen-j.github.io/">Huiwen Jia</a>. My research explores the mathematical foundations of optimization and their connections to learning.</p>
    <div class="hero-links" aria-label="Profile links">
      <a href="{{ '/cv/' | relative_url }}">CV <span aria-hidden="true">&rarr;</span></a>
      <a href="{{ '/publications/' | relative_url }}">Publications <span aria-hidden="true">&rarr;</span></a>
      <a href="https://github.com/{{ site.data.socials.github_username }}">GitHub <span aria-hidden="true">&#8599;</span></a>
      <a href="mailto:{{ site.data.socials.email }}">Email <span aria-hidden="true">&#8599;</span></a>
    </div>
  </div>
  <div class="home-portrait">
    {% include figure.liquid path="assets/img/pic_1.jpg" alt="Portrait of Zhixiao Xiong" sizes="(max-width: 575px) 140px, 220px" loading="eager" cache_bust=true %}
  </div>
</section>

<section class="home-section" aria-labelledby="research-title">
  <div class="section-label">
    <span class="section-number" aria-hidden="true">01</span>
    <h2 id="research-title">Research</h2>
  </div>
  <div class="research-columns">
    <div>
      <h3>Stochastic nonconvex optimization</h3>
      <p>I study optimization algorithms in the presence of randomness, motivated by the methods used in machine learning. I am interested in how noise shapes their behavior, what can be guaranteed, and how theoretical insights can inform algorithm design.</p>
    </div>
    <div>
      <h3>Learning while optimizing</h3>
      <p>I am also interested in decision-dependent optimization, where decisions influence the data available for learning. With a limited budget, how should we balance improving a decision with collecting new data? This perspective brings learning and optimization into the same iterative process.</p>
    </div>
  </div>
</section>

<section class="home-section" aria-labelledby="work-title">
  <div class="section-label">
    <span class="section-number" aria-hidden="true">02</span>
    <h2 id="work-title">Selected work</h2>
    <a class="section-link" href="{{ '/publications/' | relative_url }}">All publications <span aria-hidden="true">&rarr;</span></a>
  </div>
  <div class="selected-work">
    <article class="work-entry">
      <p class="work-meta">Lean 4 library <span aria-hidden="true">/</span> 2026</p>
      <h3><a href="https://github.com/xiong-zx/heavy-tailed-noise-lean">Heavy-tailed noise in Lean 4 <span aria-hidden="true">&#8599;</span></a></h3>
      <p>A library of oracle models and complexity bounds for stochastic optimization under heavy-tailed noise. Formal statements make the assumptions and the information available to an algorithm explicit.</p>
      <a class="work-link" href="https://github.com/xiong-zx/heavy-tailed-noise-lean">heavy-tailed-noise-lean <span aria-hidden="true">&#8599;</span></a>
    </article>
    <article class="work-entry">
      <p class="work-meta">Preprint <span aria-hidden="true">/</span> 2024</p>
      <h3><a href="https://arxiv.org/abs/2410.03720">NeuralQP <span aria-hidden="true">&#8599;</span></a></h3>
      <p>A hypergraph-based framework for large-scale quadratically constrained quadratic programs, combining learned solution prediction with neighborhood optimization to improve candidate solutions.</p>
      <a class="work-link" href="https://arxiv.org/abs/2410.03720">Read the paper <span aria-hidden="true">&#8599;</span></a>
    </article>
    <article class="work-entry">
      <p class="work-meta">ICML <span aria-hidden="true">/</span> 2024</p>
      <h3><a href="https://proceedings.mlr.press/v235/zhou24o.html">CurBench <span aria-hidden="true">&#8599;</span></a></h3>
      <p>A benchmark and toolkit for curriculum learning, comparing training curricula across vision, language, and graph tasks through both learning performance and computational complexity.</p>
      <a class="work-link" href="https://proceedings.mlr.press/v235/zhou24o.html">Read the paper <span aria-hidden="true">&#8599;</span></a>
    </article>
  </div>
</section>

<section class="home-section" aria-labelledby="background-title">
  <div class="section-label">
    <span class="section-number" aria-hidden="true">03</span>
    <h2 id="background-title">A little background</h2>
  </div>
  <div class="background-copy">
    <p>Before Berkeley, I studied mathematics, physics, and industrial engineering at Tsinghua University's Weiyang College. In Fall 2023, I spent a semester at the University of Toronto, working with <a href="https://cglee.mie.utoronto.ca/">Chi-Guhn Lee</a>. I received an M.S. in Engineering from Berkeley in May 2026.</p>
    <p class="personal-note">Outside research, I enjoy tennis and skiing.</p>
  </div>
</section>

<div class="home-closing">
  <section class="home-news" aria-labelledby="news-title">
    <div class="closing-heading">
      <h2 id="news-title">News</h2>
      <a class="section-link" href="{{ '/news/' | relative_url }}">All updates <span aria-hidden="true">&rarr;</span></a>
    </div>
    {% include news.liquid %}
  </section>
  <section class="home-contact" aria-labelledby="contact-title">
    <h2 id="contact-title">Get in touch</h2>
    <p>For research questions and collaborations, please get in touch.</p>
    <a href="mailto:{{ site.data.socials.email }}">{{ site.data.socials.email }} <span aria-hidden="true">&#8599;</span></a>
  </section>
</div>

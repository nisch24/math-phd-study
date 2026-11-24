---
layout: default
title: "Readiness & Gap Analysis"
nav_order: 2
permalink: /readiness/
---

# 🧭 Readiness &amp; Gap Analysis

> *Before choosing where to start, find out where you actually are. This page is a self-diagnostic for applicants targeting top PhD programs in applied mathematics or statistics. It is especially aimed at applicants coming from computer science, engineering, data science, or analytics, whose mathematics was strong but mostly computational.*

---

## What Top Programs Expect

Admissions committees at research-intensive programs read your record for **evidence of mathematical maturity**: the ability to read, construct, and write rigorous proofs. Strong grades in computational courses (calculus sequences, applied statistics, machine learning) show ability, but they don't show this particular skill. The courses that do show it are listed below.

| Area | Applied Mathematics | Statistics | Where it's covered |
|------|:-------------------:|:----------:|--------------------|
| Proof-based real analysis | **Essential** | **Essential** | [Module 0.2]({{ site.baseurl }}/module_0/undergraduate_analysis/) → [Module A]({{ site.baseurl }}/module_a/real_analysis/) |
| Proof-based linear algebra | **Essential** | **Essential** | [Module 0.3]({{ site.baseurl }}/module_0/linear_algebra/) → [Module A]({{ site.baseurl }}/module_a/matrix_analysis/) |
| Calculus-based probability | Strongly expected | **Essential** | [Module 0.4]({{ site.baseurl }}/module_0/probability_statistics/) → [Module B]({{ site.baseurl }}/module_b/) |
| Mathematical statistics | Helpful | **Essential** | [Module 0.4]({{ site.baseurl }}/module_0/probability_statistics/) → [Module C]({{ site.baseurl }}/module_c/) |
| ODEs / PDEs | **Essential** | Helpful | [Module F.1]({{ site.baseurl }}/module_f/differential_equations/) |
| Numerical analysis | **Essential** | Helpful | [Module F.2]({{ site.baseurl }}/module_f/numerical_analysis/) |
| Optimization | Helpful | Helpful | [Module D]({{ site.baseurl }}/module_d/) |
| Measure-theoretic probability | Helpful | Strong signal | [Module B]({{ site.baseurl }}/module_b/) |
| Complex analysis, abstract algebra | Helpful for math-department programs | Rarely required | Not covered here |

{: .warning }
> Requirements differ by program, and even by track within a department. Some applied-math programs sit inside a mathematics department and expect pure-math breadth, while others are interdisciplinary. Read each program's admissions page and the coursework of its recent admits. Treat this table as a typical profile, not a rulebook.

---

## The Common Gap Profile

Applicants from technical but non-mathematics backgrounds tend to share a pattern:

- **Strong**: computation, programming, applied statistics and ML, research experience with real data.
- **Missing**: proof-based analysis, proof-based linear algebra, the theory behind statistical procedures, and (for applied math) differential equations and numerical analysis.

The good news is that this gap is well defined and can be closed in about two to three semesters of focused work. The harder part is making it **visible** to admissions committees (see below).

---

## Self-Check Diagnostic

For each item, try to produce a complete, rigorous answer **without notes in about 10 minutes**. Be strict with yourself: "I know roughly how it goes" counts as *no*.

### Proofs and Logic → [Module 0.1]({{ site.baseurl }}/module_0/proofs/)
1. Negate the statement "$f$ is uniformly continuous on $\mathbb{R}$" with no "not" in front of a quantifier.
2. Prove that $\sqrt{2}$ is irrational.
3. Prove that $\mathbb{R}$ is uncountable.

### Analysis → [Module 0.2]({{ site.baseurl }}/module_0/undergraduate_analysis/)
1. Prove from the definition that $\frac{n}{n+1} \to 1$.
2. Prove that a continuous function on $[a,b]$ attains its maximum.
3. Prove that $x^2$ is not uniformly continuous on $\mathbb{R}$.
4. State the Mean Value Theorem and use it to prove that $f' = 0$ on an interval implies $f$ is constant.

### Linear Algebra → [Module 0.3]({{ site.baseurl }}/module_0/linear_algebra/)
1. Prove that eigenvectors for distinct eigenvalues are linearly independent.
2. State and prove the rank–nullity theorem.
3. Prove that a real symmetric matrix has real eigenvalues.
4. Explain why least squares is an orthogonal projection, and prove the projection minimizes distance.

### Probability and Statistics → [Module 0.4]({{ site.baseurl }}/module_0/probability_statistics/)
1. Prove Chebyshev's inequality and use it to prove the Weak Law of Large Numbers.
2. State and prove the law of total variance.
3. Show that $S^2 = \frac{1}{n-1}\sum(X_i - \bar{X})^2$ is unbiased for $\sigma^2$.
4. Derive the MLE for $\operatorname{Uniform}(0, \theta)$ and show it is biased.

### Applied Mathematics → [Module F]({{ site.baseurl }}/module_f/)
1. Solve $\dot{x} = Ax$ for a $2 \times 2$ matrix $A$ and classify the origin using the trace and determinant.
2. Explain why forward Euler is unstable on $y' = -100y$ with $h = 0.1$.
3. Explain the difference between an ill-conditioned problem and an unstable algorithm.

**Scoring**: if you fully succeed on at least 3 of 4 items in a section, skim that Module 0 course and move on. Otherwise, work through it properly, since every later module assumes it.

---

## A Suggested Roadmap

<div class="timeline">
  <div class="semester-col">
    <h4>Phase 1 — Bridge</h4>
    <div class="course-chip"><strong>0.1</strong> Proofs &amp; Logic</div>
    <div class="course-chip"><strong>0.2</strong> Real-Line Analysis</div>
    <div class="course-chip"><strong>0.3</strong> Linear Algebra</div>
    <div class="course-chip"><strong>0.4</strong> Prob. &amp; Math. Stats</div>
  </div>
  <div class="semester-col">
    <h4>Phase 2 — Core</h4>
    <div class="course-chip"><strong>A</strong> Real Analysis</div>
    <div class="course-chip"><strong>A</strong> Matrix Analysis</div>
    <div class="course-chip"><strong>B</strong> Probability Theory I</div>
  </div>
  <div class="semester-col">
    <h4>Phase 3a — Statistics track</h4>
    <div class="course-chip"><strong>C</strong> Statistical Theory I &amp; II</div>
    <div class="course-chip"><strong>B</strong> Probability Theory II</div>
    <div class="course-chip"><strong>F.2</strong> Conditioning (Unit 1)</div>
  </div>
  <div class="semester-col">
    <h4>Phase 3b — Applied track</h4>
    <div class="course-chip"><strong>F.1</strong> ODEs &amp; PDEs</div>
    <div class="course-chip"><strong>F.2</strong> Numerical Analysis</div>
    <div class="course-chip"><strong>D</strong> Optimization</div>
  </div>
</div>

Phase 1 typically takes 4–6 months at 10–12 hours per week. In an application year, prioritize Phase 1 and the first half of Phase 2: real analysis and proof-based linear algebra are the two subjects committees look for first.

---

## Making It Visible to Admissions

Self-study builds the skill, but admissions committees can only weigh what they can verify. Turn this work into evidence:

1. **Take at least one proof-based course for a grade.** A transcripted grade in real analysis (or proof-based linear algebra) is the strongest single signal you can add. Look for non-degree or extension enrollment at a university, or a summer session.
2. **Ask a mathematician to evaluate your work.** A letter from a faculty member who has read your proofs carries much more weight than a list of self-studied topics.
3. **Show it in your research.** If your research has mathematical content (a convergence argument, a constrained estimator, a stability analysis), make that content prominent in your writing sample and statement.
4. **Describe it concretely in your statement.** One sentence naming the texts you worked through and what you proved is credible; a long list of topics is not.
5. **Check standardized-test policies.** Some programs recommend or accept the GRE Mathematics Subject Test, which directly tests undergraduate analysis, algebra, and calculus. Policies change frequently, so verify each program's current stance.

---

## Equivalent Courses at MIT (OpenCourseWare)

To calibrate against a specific top program, each module maps to freely available MIT courses:

| This site | MIT OCW equivalent |
|-----------|--------------------|
| Module 0.1 Proofs | 6.042J Mathematics for Computer Science |
| Module 0.2 Analysis | 18.100A Real Analysis |
| Module 0.3 Linear Algebra | 18.700 Linear Algebra |
| Module 0.4 Probability &amp; Statistics | 18.600 Probability and Random Variables; 18.650 Statistics for Applications |
| Module A | 18.100B Analysis I; 18.065 Matrix Methods |
| Module B | 18.175 Theory of Probability; 18.445 Stochastic Processes |
| Module C | 18.655 Mathematical Statistics |
| Module D | 6.079 Introduction to Convex Optimization |
| Module F | 18.03 Differential Equations; 18.152 PDEs; 18.330 Numerical Analysis; 18.335J Numerical Methods |

Links for all of these are on the [Resources]({{ site.baseurl }}/resources/) page.

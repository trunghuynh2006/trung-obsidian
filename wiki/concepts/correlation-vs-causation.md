---
type: concept
name: Correlation vs. Causation
aliases: [spurious correlation, reverse causation, confounding]
tags: [methodology, statistics, epistemology]
sources: 1
---

# Correlation vs. Causation

## Definition

A **correlation** is a statistical relationship between two variables — when one rises, the other tends to rise (or fall). **Causation** means one variable directly produces the other. Correlation does not imply causation: the relationship may be reverse (Y causes X, not X causes Y), confounded (a third variable Z causes both), or spurious (coincidence at scale).

## Detail

Levitt treats the correlation/causation distinction as the most important methodological tool in applied economics — and the most commonly violated principle in public reasoning. Three failure modes:

**1. Reverse causation:** The direction is correct but backwards. Campaign spending and electoral wins are correlated. CW says money causes wins. Data says: appealing candidates attract both donors and voters. The candidate's appeal is Z; it causes both spending and votes. Controlling for appeal (by tracking the same two candidates across consecutive races), doubling spend shifts the vote by just 1% [[wiki/sources/freakonomics-introduction]].

**2. Confounded causation:** Both variables share a hidden cause. Cities with many murders also have many police. Naive conclusion: police cause murders. Actual structure: dangerous cities hire more police *in response to* crime. Z (danger level) causes both [[wiki/sources/freakonomics-introduction]]. Levitt's illustration: a czar learning that the most disease-ridden province also had the most doctors — and ordering the doctors shot.

**3. Distant causation:** The causal relationship is real but temporally displaced and non-obvious. Crime fell in the 1990s because of a demographic shift caused by abortion legalization in 1973. The cause preceded the effect by 18–20 years and involved a mechanism (birth cohort composition) that was invisible to real-time observation [[wiki/sources/freakonomics-introduction]].

## Methodological response

Levitt's preferred method: **natural experiments and controlled comparisons** that isolate the variable of interest while holding others constant:
- Same two candidates, consecutive races → controls for candidate appeal
- Agent's own home vs. client's home → controls for house characteristics
- Crime rates among cohorts born before and after Roe v. Wade → controls for macroeconomic cycles

The goal is always to find a setting where the causal variable changes while everything else plausibly stays the same.

## Connections

- [[wiki/concepts/conventional-wisdom]] — CW is typically a correlation that has been misread as causation, often because the true cause is distant, subtle, or politically inconvenient
- [[wiki/concepts/expert-incentive-misalignment]] — experts who benefit from a false causal story have incentives to maintain it
- [[wiki/entities/steven-levitt]] — the methodological core of his approach

## Sources

- [[wiki/sources/freakonomics-introduction]] — campaign finance, police/murders, and crime-drop cases

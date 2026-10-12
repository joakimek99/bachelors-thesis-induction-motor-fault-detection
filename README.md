# Vibration Analysis of Faulty Electric Motor in the Frequency Domain
A Study on Spectral Centroid as Fault Indicator for Misalignment

Author: Joakim Eklund  
Programme: Bachelor’s Programme in Electrical and Electronics Engineering  
Date: 26.8.2025  
Pages: 35 + 5 appendix  
Status: Completed (Bachelor’s Thesis, 2025)  
Copyright © 2025 Joakim Eklund

## Overview
This repository contains my bachelor’s thesis on using spectral centroid (SC) as a vibration-domain indicator for detecting parallel shaft misalignment in induction motors. The work compares healthy, 0.5 mm, and 1 mm misalignment conditions across three axes (X, Y, Z) and four load levels (0%, 50%, 75%, 100%). The focus is on direct-on-line (DOL) operation at 60 Hz using openly available lab data. [3] [5] [9]

- Goal: Evaluate whether SC can separate healthy from misaligned motor conditions and how load/axis affect reliability.
- Scope limits: Only misalignment fault type (parallel). Emphasis on basic stats, FFT, and Spectral Centroid.

## Abstract
Induction motors develop faults such as shaft misalignment. This study investigates spectral centroid (SC)—the center of mass of the frequency spectrum—as a simple indicator of misalignment from vibration signals. Results show SC tends to be higher for misaligned motors in X and Y directions and under lighter loads in Z, while differences shrink with increased load; in Z at higher loads the healthy SC may exceed misaligned. Time‑domain standard deviation rises with misalignment, while skewness and kurtosis remain similar. SC shows potential under lighter loads but is sensitive to axis and load, and findings are limited by dataset size.

## Key findings
- X‑axis SC increases with misalignment at all loads; example SC (Hz):  
  0%: 45.67 (healthy), 58.56 (0.5 mm), 80.68 (1 mm)  
  50%: 52.59, 62.84, 69.45  
  75%: 57.10, 65.05, 69.43  
  100%: 59.22, 65.33, 72.73
- Y‑axis: Misaligned > healthy, but differences are smaller (e.g., +25.25 Hz at 0% load; +2.74 Hz at 100%). SC range ≈145–175 Hz.
- Z‑axis: Less consistent; at higher loads, healthy SC can exceed misaligned by ≈0.45–4.04 Hz. SC range ≈103–141 Hz.
- Time‑domain statistics (X‑axis): Standard deviation increases with misalignment; +10–20% for 0.5 mm vs healthy; up to ≈2× for 1 mm vs healthy. Skewness and kurtosis remain close across conditions.
- Frequency‑domain verification: Clear rotor‑speed peak around ≈29–30 Hz and pronounced ≈2× component around 58–59 Hz in misalignment, consistent with theory

## Data and methods
- Dataset: Electrical Energy Conversion System Lab (EECSL), Korea University.  
  “Motor vibration signal database” (public). Accessed 1.7.2025.  
  https://home.eecs.korea.ac.kr/publications/database
- Conditions used: DOL at 60 Hz; loads 0/50/75/100%; misalignment 0.5 mm and 1 mm; axes X, Y, Z. One recording per condition (limits robustness).
- Processing: MATLAB—NaN removal, scaling per dataset factor, FFT (0–400 Hz), SC calculation. Sampling frequency 800 Hz; ≈4800 points per sample.
- Spectral centroid definition: c = Σ(f_k m_k) / Σ(m_k) (frequency‑weighted mean of spectral magnitudes).

## Repository structure
- thesis/ — Thesis PDF and figures
- README.md — This file

## How to reproduce
1) Download data  
   - Source: EECSL “Motor vibration signal database” (see link above).  
   - Use DOL 60 Hz misalignment and healthy sets for X/Y/Z at 0/50/75/100% load.

2) Run MATLAB workflows  
   - Preprocess and FFT (example in Appendix Code 4.1/4.2): remove NaNs, scale amplitudes, compute FFT up to 400 Hz (Fs=800 Hz).
   - Compute stats (mean, median, skewness, kurtosis, std) per signal (Code 4.3).
   - Compute SC per condition and overlay on spectra (Code 4.4).

3) Verify against reported patterns  
   - Rotor‑speed peak ≈29–30 Hz; misalignment exhibits notable ≈2× rotor‑speed peak ≈58–59 Hz. 
   - X‑axis SC table should match values listed above.

## Limitations
- Single recording per condition; conclusions rely on trends rather than statistical tests.
- Controlled lab setup; real‑world noise and variability not covered.
- SC is axis/load sensitive and averages spectrum content; complementary features or filtering may improve reliability.

## Recommendations (future work)
- Validate in real‑world environments (factories/industrial settings).
- Include VFD data; broaden to multiple motors, manufacturers, and additional fault types.
- Explore filtering/windowing, advanced statistics, and ML/AI; combine vibration with other modalities (e.g., MCSA).
- Promote open datasets/benchmarks to compare methods.

## License
Copyright © 2025 Joakim Eklund.  
If you want to reuse text, figures, or code, please contact me.

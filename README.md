📖 README: 16-QAM SIGNAL ANALYZER
🎯 Project Overview
This is a complete 16-QAM (Quadrature Amplitude Modulation) Signal Analyzer implemented in Python. It simulates the entire digital communication chain from bit generation through modulation, AWGN channel impairment, demodulation, and BER (Bit Error Rate) analysis.
The project generates 1,000 complex symbols, transmits them through a simulated AWGN channel at various SNR levels (0–20 dB), demodulates using maximum-likelihood detection, and compares simulated BER against theoretical predictions.

📋 Features
✅ Complete 16-QAM Transceiver Simulation

Bit stream generation (4,000 random bits)
Serial-to-parallel conversion & symbol mapping
16-point I/Q constellation (4×4 grid)
Modulation to complex baseband symbols

✅ AWGN Channel Model

Zero-mean Gaussian noise
Independent I and Q channel noise
SNR control (0–20 dB in 1 dB steps)

✅ Maximum-Likelihood Demodulation

Euclidean distance-based nearest neighbor detection
Optimal demodulation under AWGN
1,000 symbols recovered per run

✅ Performance Analysis

Bit error rate (BER) calculation at each SNR
Simulated BER curve
Theoretical BER from Proakis formula
Visual constellation diagrams (clean & noisy)

✅ Professional Visualizations

Constellation Clean → 16 ideal symbols, no noise
Constellation Noisy → Side-by-side comparison at SNR = 15 dB
BER vs SNR → Log-scale plot showing simulated vs theoretical


🔧 Requirements
Software

Python 3.10 or 3.11 (avoid 3.14 due to NumPy issues)
NumPy 1.24+ → Array math, complex numbers, random generation
Matplotlib 3.7+ → Plotting constellations and BER curves
SciPy 1.10+ → erfc() function for theoretical BER

Installation
bashpip install numpy scipy matplotlib
If installation fails, run the provided INSTALL_FIX.bat file:
bashINSTALL_FIX.bat

🚀 How to Run
Option 1: Command Prompt
bashcd path/to/your/project
python qam_analyzer.py
Option 2: VS Code

Open qam_analyzer.py
Click the ▶ (Run) button, or press F5

Option 3: Python IDLE

File → Open → select qam_analyzer.py
Press F5


📐 Mathematical Foundation
Signal Model (AWGN Channel)
r(t) = s(t) + n(t)
where:
  r(t) = received signal
  s(t) = transmitted symbol
  n(t) = Gaussian noise ~ CN(0, σ²)
SNR to Noise Power
SNR_linear = 10^(SNR_dB / 10)
σ² = P_signal / SNR_linear
Demodulation (Euclidean Distance)
Nearest point = argmin_k |r[n] - s_k|
where s_k are the 16 constellation points
Bit Error Rate
BER = (number of bit errors) / (total bits)
Theoretical BER (16-QAM, Proakis)
BER_theory = (3/8) × erfc(√(SNR / 10))

🎓 Project Structure
qam_analyzer.py
├── Stage 1: Imports (NumPy, Matplotlib, SciPy)
├── Stage 2: Bit generation & symbol mapping
├── Stage 3: Constellation diagram (clean)
├── Stage 4: AWGN noise & demodulation
├── Stage 5: BER vs SNR curve
└── Output: 3 PNG plots + console stats

🔑 Key Concepts Explained
What is 16-QAM?
QAM = Quadrature Amplitude Modulation

Uses two carriers 90° apart: I (in-phase) and Q (quadrature)
16 means 16 unique constellation points (4 bits per symbol)
Grid: I, Q ∈ {−3, −1, +1, +3} → 4×4 = 16 points

Why I and Q?

I component (cosine): controls horizontal position
Q component (sine): controls vertical position
Together: form a 2D constellation plane

What is AWGN?

A = Additive (noise added to signal)
W = White (all frequencies affected equally)
G = Gaussian (noise follows bell curve)
N = Noise (random, zero-mean)

What is BER?
Fraction of bits incorrectly received:
BER = (error bits) / (total bits)
Example: If 52 out of 4,000 bits wrong, BER = 0.013 = 1.3%
What is SNR?
Signal-to-Noise Ratio:
SNR_dB = 10 × log₁₀(P_signal / P_noise)
0 dB → equal power
10 dB → signal 10× stronger
20 dB → signal 100× stronger

📊 How It Works (High Level)
1. Generate 4,000 random bits
   ↓
2. Group into 1,000 groups of 4 bits
   ↓
3. Map each group to one of 16 symbols (complex I/Q point)
   ↓
4. Add AWGN noise at controlled SNR level
   ↓
5. For each noisy symbol, find nearest ideal point (demodulate)
   ↓
6. Decode back to 4 bits
   ↓
7. Compare with original → count errors → calculate BER
   ↓
8. Repeat steps 4–7 for SNR = 0, 1, 2, ..., 20 dB
   ↓
9. Plot results:
   - Constellation diagrams
   - BER vs SNR curve
   - Compare with theory

🎯 16-QAM Constellation Grid
Q (Quadrature)
    +3  ●   ●   ●   ●
    +1  ●   ●   ●   ●
    -1  ●   ●   ●   ●
    -3  ●   ●   ●   ●
        -3  -1  +1  +3  → I (In-Phase)

Total: 16 points (4×4 grid)
Each point = one of 16 possible 4-bit patterns

📈 Expected Results
SNR (dB)Simulated BERTheoretical BERInterpretation0~0.460.47Heavy noise, ~46% errors5~0.160.16Moderate noise, ~16% errors10~0.0130.014Light noise, ~1.3% errors15~0.000010.0002Very clean, <0.001% errors20<0.00001<0.00001Excellent, negligible errors
Key insight: BER improves exponentially with SNR!

Excellent. If you deeply understand the DFT, then FFT, STFT, GCC-PHAT, beamforming, and MUSIC become much easier.

So now let’s go much deeper into DFT from:

* mathematical
* geometric
* physical
* signal-processing
* audio
* localization

perspectives.

---

# PART 1 — THE CORE IDEA OF DFT

The DFT answers this question:

> “What frequencies exist inside a discrete signal?”

Suppose a microphone records:

[
x[n]
]

The signal may contain:

* speech
* noise
* multiple tones
* echoes

The DFT decomposes it into:

* sine waves
* cosine waves

of different frequencies.

---

# Fundamental Assumption of Fourier Analysis

Fourier theory says:

> Any signal can be represented as a sum of sinusoids.

So:

[
x[n]
====

\text{sum of many frequencies}
]

The DFT extracts those frequencies.

---

# PART 2 — Continuous vs Discrete Fourier Transform

---

# Continuous Fourier Transform

For continuous signals:

[
X(f)
====

\int_{-\infty}^{\infty}
x(t)e^{-j2\pi ft}dt
]

But computers cannot process:

* continuous time
* infinite signals

So we sample.

---

# Sampling

Suppose sampling rate:

[
f_s = 8000 \text{ Hz}
]

Then:

[
x(t)
\rightarrow
x[n]
]

where:

[
n = 0,1,2,...
]

Now signal becomes discrete.

---

# DFT

The DFT works on:

* finite
* discrete

signals.

Formula:

[
X[k]
====

\sum_{n=0}^{N-1}
x[n]e^{-j2\pi kn/N}
]

---

# PART 3 — Understanding Every Symbol Deeply

---

# 1. (x[n])

Input signal.

Example:

[
x[n]=[1,2,0,-1]
]

This means:

| n | x[n] |
| - | ---- |
| 0 | 1    |
| 1 | 2    |
| 2 | 0    |
| 3 | -1   |

---

# 2. (N)

Number of samples.

Example:

[
N=1024
]

DFT analyzes these 1024 samples.

Important:
DFT assumes these samples are periodic.

This is VERY important.

---

# 3. (k)

Frequency bin index.

Each (k) represents one sinusoidal frequency.

Range:

[
k=0,1,2,...,N-1
]

---

# 4. Complex Exponential

Core of DFT:

[
e^{-j2\pi kn/N}
]

This is a rotating complex sinusoid.

Using Euler formula:

[
e^{j\theta}
===========

\cos\theta+j\sin\theta
]

So:

[
e^{-j2\pi kn/N}
===============

## \cos\left(\frac{2\pi kn}{N}\right)

j\sin\left(\frac{2\pi kn}{N}\right)
]

Meaning:
DFT compares signal with:

* cosine waves
* sine waves

simultaneously.

---

# PART 4 — Geometric Interpretation

This is the most important intuition.

---

# Complex Plane

Complex numbers have:

* real axis
* imaginary axis

A complex exponential:

[
e^{j\theta}
]

rotates on a circle.

---

# Rotation Speed = Frequency

Higher frequency:

* rotates faster.

Lower frequency:

* rotates slower.

---

# What DFT Actually Does

For each frequency bin (k):

1. Generate rotating vector
2. Multiply signal by it
3. Sum everything

If signal contains that frequency:

* vectors align
* large output

If not:

* vectors cancel
* small output

---

# Think of It Like This

Suppose signal contains 1000 Hz.

When DFT checks 1000 Hz:

* vectors point same direction
* sum becomes large

When DFT checks 3000 Hz:

* vectors rotate inconsistently
* cancellation occurs

This is the heart of frequency detection.

---

# PART 5 — Orthogonality

This is the mathematical foundation.

Different sinusoids are orthogonal.

Meaning:

[
\sum
\sin(f_1)\sin(f_2)=0
]

if frequencies differ.

Like perpendicular vectors.

---

# Why This Matters

Because each DFT frequency basis is independent.

So:

* 1000 Hz does not interfere with 2000 Hz
* DFT can isolate frequencies cleanly

---

# PART 6 — DFT Basis Functions

DFT uses basis functions:

[
e^{-j2\pi kn/N}
]

for different (k).

These are:

* rotating waves
* frequency templates

The DFT projects signal onto these templates.

---

# Linear Algebra Interpretation

This is extremely important for advanced DSP.

DFT is basically:

[
X = Wx
]

where:

* (x) = signal vector
* (W) = DFT matrix
* (X) = frequency coefficients

---

# DFT Matrix

[
W=
\begin{bmatrix}
1 & 1 & 1 & 1 \
1 & W & W^2 & W^3 \
1 & W^2 & W^4 & W^6 \
1 & W^3 & W^6 & W^9
\end{bmatrix}
]

where:

[
W=e^{-j2\pi/N}
]

This is essentially:

* coordinate transformation

from:

* time basis
  to:
* frequency basis

---

# PART 7 — Frequency Bins

---

# Actual Frequency

Each bin corresponds to:

[
f_k = \frac{k f_s}{N}
]

Example:

* (f_s=8000)
* (N=8)

Then:

| k | Frequency |
| - | --------- |
| 0 | 0         |
| 1 | 1000      |
| 2 | 2000      |
| 3 | 3000      |
| 4 | 4000      |

---

# Frequency Resolution

Spacing:

[
\Delta f = \frac{f_s}{N}
]

Larger (N):

* better resolution

---

# PART 8 — Magnitude and Phase

DFT output is complex:

[
X[k]=a+jb
]

---

# Magnitude

Strength of frequency:

[
|X[k]|
======

\sqrt{a^2+b^2}
]

---

# Phase

Shift of sinusoid:

[
\angle X[k]
===========

\tan^{-1}(b/a)
]

---

# Why Phase Matters

For localization:

* phase difference between microphones
  gives:
* time delay
* direction

MUSIC and GCC-PHAT depend heavily on phase.

---

# PART 9 — DFT of Simple Signals

---

# 1. Constant Signal

[
x[n]=1
]

DFT:

* only DC component exists

So:

* (X[0]) large
* others zero

---

# 2. Pure Sine Wave

Suppose:

[
x[n]=\sin(2\pi 1000 t)
]

DFT:

* peak at 1000 Hz

---

# 3. Multiple Frequencies

[
x[n]
====

\sin(1000)+0.5\sin(3000)
]

DFT shows:

* strong 1000 Hz peak
* weaker 3000 Hz peak

---

# PART 10 — Real Signals and Symmetry

For real signals:

[
X[N-k]=X^*[k]
]

Meaning:
second half mirrors first half.

This is why we usually plot only half-spectrum.

---

# PART 11 — DFT Assumes Periodicity

VERY IMPORTANT.

DFT assumes signal repeats infinitely.

Meaning:

[
x[0]
\rightarrow
x[N-1]
]

must connect smoothly.

If not:

* discontinuity occurs
* spectral leakage appears

This is why windowing exists.

---

# PART 12 — Spectral Leakage

Suppose signal frequency:

* not perfectly aligned to FFT bin

Energy spreads into neighboring bins.

Instead of sharp spike:

* smeared spectrum appears.

This is called:

* leakage

Windowing reduces this.

---

# PART 13 — Circular Nature of DFT

DFT assumes signals wrap around circularly.

So convolution becomes:

* circular convolution

not normal linear convolution.

This becomes important in:

* filtering
* overlap-add
* STFT

---

# PART 14 — Parseval’s Theorem

Energy in time domain equals energy in frequency domain.

[
\sum |x[n]|^2
=============

\frac1N
\sum |X[k]|^2
]

Important in:

* power estimation
* signal energy
* PSD

---

# PART 15 — Inverse DFT

Recover original signal:

[
x[n]
====

\frac1N
\sum_{k=0}^{N-1}
X[k]e^{j2\pi kn/N}
]

Negative sign:

* forward transform

Positive sign:

* inverse transform

---

# PART 16 — Why DFT is SO Important in Audio DSP

Because:

* convolution becomes multiplication
* filtering becomes easier
* phase analysis becomes possible

Many advanced algorithms operate entirely in frequency domain.

---

# PART 17 — DFT in Sound Localization

Critical ideas:

---

## Time Delay → Phase Shift

Suppose sound reaches:

* mic1 first
* mic2 later

Delay causes:

[
\Delta \phi
===========

2\pi f\tau
]

where:

* (f)=frequency
* (\tau)=delay

DFT extracts phase differences.

---

## Localization Algorithms Use This

Examples:

* GCC-PHAT
* MUSIC
* SRP-PHAT
* Beamforming

all rely on:

* FFT/DFT phase information.

---

# PART 18 — The Deepest Intuition

DFT is basically:

> measuring how much the signal resembles each sinusoid.

Mathematically:

* projection
* correlation
* inner product

between:

* signal
  and:
* frequency basis functions

---

# PART 19 — Visual Intuition

Imagine:

* many rotating arrows

Correct frequency:

* arrows align
* huge sum

Wrong frequency:

* arrows cancel

That is literally what the DFT computes.

---

# PART 20 — Most Important Concepts to Master

You should deeply understand:

---

## Essential DSP Concepts

### 1. Complex Numbers

Absolutely mandatory.

### 2. Euler Formula

[
e^{j\theta}
===========

\cos\theta+j\sin\theta
]

### 3. Orthogonality

### 4. Frequency Bins

### 5. Phase

### 6. Spectral Leakage

### 7. Sampling Theorem

### 8. Circular Periodicity

---

# What Comes Next

The next topic should be:

# Windowing

because it solves:

* spectral leakage
* discontinuity problems

and becomes essential for:

* STFT
* spectrograms
* GCC-PHAT
* MUSIC

Without understanding windowing, practical FFT systems will confuse you badly.





Perfect. Now we go deeply into the **FFT (Fast Fourier Transform)** the same way.

This is one of the most important algorithms ever invented in engineering and computer science.

Without FFT:

* modern audio
* wireless communication
* WiFi
* radar
* MRI
* speech recognition
* beamforming
* music analysis
* sound localization

would be computationally impractical.

---

# PART 1 — What FFT Actually Is

---

# FFT is NOT a Different Transform

This is the most important thing first.

FFT does NOT change the mathematics.

The transform is still:

[
X[k]
====

\sum_{n=0}^{N-1}
x[n]e^{-j2\pi kn/N}
]

FFT is ONLY:

> a faster algorithm to compute the DFT.

So:

| Name | Meaning                     |
| ---- | --------------------------- |
| DFT  | Mathematical transform      |
| FFT  | Efficient algorithm for DFT |

---

# PART 2 — Why DFT is Slow

Suppose:

* signal length = (N)

To compute ONE frequency bin:

* need (N) multiplications

To compute ALL bins:

* need:

[
N \times N = N^2
]

operations.

---

# Example

Suppose:

[
N = 1024
]

Then:

* about 1 million operations

Now imagine:

* 48kHz audio
* real-time microphone arrays
* many microphones

DFT becomes too slow.

---

# FFT Reduces Complexity

FFT reduces:

[
O(N^2)
\rightarrow
O(N\log N)
]

Example:

| N    | DFT Ops   | FFT Ops |
| ---- | --------- | ------- |
| 1024 | 1,048,576 | 10,240  |

Massive improvement.

---

# PART 3 — Core FFT Idea

FFT exploits:

1. Symmetry
2. Periodicity
3. Repeated calculations

inside the DFT equation.

---

# Key Insight

The DFT repeatedly computes the same complex exponentials.

FFT avoids recomputing them.

---

# PART 4 — Even/Odd Decomposition

This is the heart of FFT.

Suppose:

[
x[n]
====

[x_0,x_1,x_2,x_3,x_4,x_5,x_6,x_7]
]

Split into:

---

## Even Samples

[
x_e[n]
======

[x_0,x_2,x_4,x_6]
]

---

## Odd Samples

[
x_o[n]
======

[x_1,x_3,x_5,x_7]
]

---

# Why Split?

Because smaller DFTs can be reused.

Instead of one big DFT:

* compute two smaller DFTs.

Then combine results cleverly.

---

# PART 5 — Deriving FFT from DFT

Start with:

[
X[k]
====

\sum_{n=0}^{N-1}
x[n]W_N^{kn}
]

where:

[
W_N=e^{-j2\pi/N}
]

Now separate:

* even indices
* odd indices

---

# Even Terms

[
\sum x[2m]W_N^{2mk}
]

---

# Odd Terms

[
\sum x[2m+1]W_N^{(2m+1)k}
]

Factorize:

[
X[k]
====

E[k]
+
W_N^k O[k]
]

where:

* (E[k])=DFT of even samples
* (O[k])=DFT of odd samples

This is the fundamental FFT equation.

---

# PART 6 — Recursive Structure

Now:

* compute smaller DFTs recursively

Each smaller DFT:

* splits again into even/odd

until:

* size becomes 2

This creates FFT tree structure.

---

# PART 7 — Butterfly Operation

The butterfly is the basic FFT computation block.

It combines:

* even result
* odd result

using:

[
X[k]=E[k]+W_N^kO[k]
]

and

[
X[k+N/2]
========

E[k]-W_N^kO[k]
]

---

# Why Called Butterfly?

Because diagram looks like butterfly wings.

This structure appears repeatedly throughout FFT.

---

# PART 8 — Twiddle Factors

Very important concept.

These are:

[
W_N^k=e^{-j2\pi k/N}
]

called:

* twiddle factors

They are:

* rotating complex numbers

used to combine smaller FFTs.

---

# PART 9 — Radix-2 FFT

Most common FFT algorithm.

Requires:

[
N=2^m
]

Examples:

* 256
* 512
* 1024
* 2048

because repeated halving becomes easy.

---

# Why Power of 2?

FFT repeatedly divides:

* (N\rightarrow N/2\rightarrow N/4\rightarrow ...)

So powers of 2 are computationally optimal.

---

# PART 10 — FFT Flow

For (N=8):

Stage 1:

* split into 4-point FFTs

Stage 2:

* split into 2-point FFTs

Stage 3:

* butterfly combinations

Final:

* full FFT output

---

# PART 11 — Bit Reversal

This confuses many people.

FFT rearranges indices into:

* bit-reversed order

Example:

| Decimal | Binary | Reversed | New Index |
| ------- | ------ | -------- | --------- |
| 0       | 000    | 000      | 0         |
| 1       | 001    | 100      | 4         |
| 2       | 010    | 010      | 2         |
| 3       | 011    | 110      | 6         |

This helps FFT compute efficiently in-place.

---

# PART 12 — In-Place Computation

FFT often overwrites input memory directly.

Benefits:

* less RAM
* faster cache performance

Very important in embedded DSP.

---

# PART 13 — Geometric Interpretation

This is crucial.

DFT:

* measures projection onto rotating vectors.

FFT:

* computes those projections efficiently.

The mathematics is identical.

---

# PART 14 — Frequency Bins in FFT

Same as DFT:

[
f_k=\frac{kf_s}{N}
]

Example:

* (f_s=16000)
* (N=1024)

Then:

[
\Delta f
========

15.625\text{ Hz}
]

Each bin represents 15.625 Hz.

---

# PART 15 — FFT Output Structure

FFT output:

[
X[k]
]

contains:

* real part
* imaginary part

From these we compute:

---

## Magnitude

[
|X[k]|
======

\sqrt{Re^2+Im^2}
]

---

## Phase

[
\angle X[k]
===========

\tan^{-1}(Im/Re)
]

---

# PART 16 — Real Signal Symmetry

For microphone signals:

[
x[n]\in \mathbb{R}
]

FFT output has conjugate symmetry:

[
X[N-k]=X^*[k]
]

Meaning:
second half mirrors first half.

So only first half is unique.

---

# PART 17 — FFT Example Physically

Suppose signal contains:

* 1000 Hz
* 3000 Hz

FFT outputs:

* peak at 1000 Hz
* peak at 3000 Hz

Amplitude of peaks:

* indicates signal strength.

---

# PART 18 — FFT and Sampling Rate

Maximum detectable frequency:

[
f_{max}
=======

\frac{f_s}{2}
]

called:

* Nyquist frequency.

---

# Example

If:

* (f_s=44100)

then:

* max frequency = 22050 Hz.

---

# PART 19 — FFT Resolution Tradeoff

---

## Large FFT

Advantages:

* better frequency precision

Disadvantages:

* slower
* worse time resolution

---

## Small FFT

Advantages:

* better time localization

Disadvantages:

* poorer frequency resolution

This becomes critical in STFT.

---

# PART 20 — Zero Padding

Suppose:

* FFT size = 1024
* signal length = 600

Add zeros.

Benefits:

* smoother spectrum
* better visualization

BUT:

* does NOT increase true resolution.

This misconception is common.

---

# PART 21 — FFT Leakage Problem

Huge practical issue.

Suppose:

* signal frequency lies between FFT bins

Energy spreads across neighboring bins.

This is:

* spectral leakage.

Cause:

* DFT assumes periodic repetition.

Solution:

* windowing.

---

# PART 22 — FFT in Audio Systems

FFT is everywhere:

---

## Speech Processing

* MFCC
* spectrograms
* voice recognition

---

## Sound Localization

* GCC-PHAT
* MUSIC
* beamforming

---

## Noise Reduction

* spectral subtraction

---

## Compression

* MP3
* AAC

---

# PART 23 — FFT in Sound Localization

This is especially important for your project.

---

# Why Frequency Domain?

Time-domain correlation:

* noisy
* sensitive

Frequency-domain methods:

* more robust
* phase-aware

---

# Delay Becomes Phase Shift

If sound arrives later:

[
\tau
]

then phase shift:

[
\Delta\phi
==========

2\pi f\tau
]

FFT extracts phase information directly.

This is fundamental to:

* GCC-PHAT
* beamforming
* MUSIC.

---

# PART 24 — FFT and Convolution

One of the biggest DSP advantages.

Time-domain convolution:

[
x*h
]

becomes:

[
X[k]H[k]
]

in frequency domain.

Meaning:

* filtering becomes multiplication.

Huge speed improvement.

---

# PART 25 — FFT Algorithm Families

---

## Radix-2 FFT

Most common.

---

## Radix-4 FFT

Faster in some CPUs.

---

## Mixed-Radix FFT

Supports arbitrary sizes.

---

## FFTW Library

Highly optimized FFT library.

Used widely in research.

---

# PART 26 — Numerical Issues

FFT uses floating-point arithmetic.

Potential issues:

* rounding errors
* phase precision
* quantization noise

Very important in:

* embedded systems
* microphone arrays

---

# PART 27 — Deep Intuition

The FFT is essentially:

> an efficient frequency analyzer.

It checks:

* how strongly each rotating frequency exists in the signal.

Instead of recomputing everything:

* FFT reuses partial results cleverly.

---

# PART 28 — Most Important Concepts to Master

Before moving ahead, deeply understand:

---

## Mandatory Concepts

### 1. Complex numbers

### 2. Euler equation

[
e^{j\theta}
===========

\cos\theta+j\sin\theta
]

### 3. Frequency bins

### 4. Phase

### 5. Spectral leakage

### 6. Sampling theorem

### 7. Orthogonality

### 8. Conjugate symmetry

### 9. Even/odd decomposition

### 10. Butterfly operation

---

# PART 29 — Why FFT Changed the World

FFT was revolutionary because:

* DFT became practical
* real-time DSP became possible

This enabled:

* digital audio
* modern telecommunications
* radar
* MRI
* OFDM
* WiFi
* 5G
* speech AI

Almost every modern signal-processing system depends on FFT.

---

# Next Topic

Now the PERFECT next step is:

# Windowing (Hamming/Hann)

because FFT in real systems suffers from:

* spectral leakage
* discontinuity artifacts

Windowing solves those problems and becomes essential for:

* STFT
* spectrograms
* GCC-PHAT
* beamforming
* MUSIC.



Excellent. Now we go into the **actual FFT algorithm itself**, not just the idea.

We’ll understand:

* how FFT recursively works
* why even/odd splitting works
* butterfly computation
* twiddle factors
* recursion tree
* bit reversal
* computational savings

This is the real engineering-level understanding.

---

# PART 1 — Starting from the DFT

The DFT is:

[
X[k]
====

\sum_{n=0}^{N-1}
x[n]e^{-j2\pi kn/N}
]

Define:

[
W_N = e^{-j2\pi/N}
]

Then:

[
X[k]
====

\sum_{n=0}^{N-1}
x[n]W_N^{kn}
]

This notation simplifies FFT derivation.

---

# PART 2 — The Problem

Suppose:

[
N=8
]

Then each output bin needs:

* 8 multiplications

Total:

* (8 \times 8 = 64)

For large (N):

* extremely expensive.

FFT avoids repeated calculations.

---

# PART 3 — The Core FFT Trick

This is THE central idea:

Split the signal into:

* even-indexed samples
* odd-indexed samples

---

# Example

Suppose:

[
x[n]
====

[x_0,x_1,x_2,x_3,x_4,x_5,x_6,x_7]
]

---

# Even Samples

[
x_e[n]
======

[x_0,x_2,x_4,x_6]
]

---

# Odd Samples

[
x_o[n]
======

[x_1,x_3,x_5,x_7]
]

Now compute smaller DFTs.

---

# PART 4 — Splitting the DFT Equation

Start:

[
X[k]
====

\sum_{n=0}^{N-1}
x[n]W_N^{kn}
]

Separate:

* even (n=2m)
* odd (n=2m+1)

---

# Even Part

[
\sum_{m=0}^{N/2-1}
x[2m]W_N^{k(2m)}
]

Using property:

[
W_N^{2k}=W_{N/2}^{k}
]

This becomes:

[
\sum_{m=0}^{N/2-1}
x[2m]W_{N/2}^{km}
]

This is a smaller DFT.

Call it:

[
E[k]
]

---

# Odd Part

Similarly:

[
\sum_{m=0}^{N/2-1}
x[2m+1]W_N^{k(2m+1)}
]

Factorize:

# [

W_N^k
\sum_{m=0}^{N/2-1}
x[2m+1]W_{N/2}^{km}
]

Call smaller DFT:

[
O[k]
]

So:

[
X[k]
====

E[k]
+
W_N^kO[k]
]

This is the FFT breakthrough.

---

# PART 5 — The Magic

Instead of one large DFT:

* compute two smaller DFTs.

Then combine them.

---

# Computational Savings

Original:

* size (N)

Now:

* two DFTs of size (N/2)

Then recursively repeat.

This creates:

[
N\log_2N
]

complexity.

---

# PART 6 — Recursive Decomposition

Suppose:

[
N=8
]

---

# Level 1

Split into:

* two 4-point DFTs

---

# Level 2

Each 4-point DFT splits into:

* two 2-point DFTs

---

# Level 3

Each 2-point DFT splits into:

* two 1-point DFTs

At size 1:

* DFT is trivial.

Then combine upward.

---

# PART 7 — FFT Tree Structure

FFT forms a recursion tree.

For (N=8):

```text
8
├── 4
│   ├── 2
│   │   ├──1
│   │   └──1
│   └── 2
│       ├──1
│       └──1
└── 4
    ├── 2
    │   ├──1
    │   └──1
    └── 2
        ├──1
        └──1
```

This recursive structure is FFT.

---

# PART 8 — Butterfly Operation

Now the most important computation.

Suppose:

* even result = (E[k])
* odd result = (O[k])

Then:

[
X[k]
====

E[k]+W_N^kO[k]
]

and

[
X[k+N/2]
========

E[k]-W_N^kO[k]
]

This pair is called a butterfly.

---

# Why Two Outputs?

Because DFT periodicity gives:

[
X[k+N/2]
========

E[k]-W_N^kO[k]
]

So one computation gives two bins.

Huge efficiency gain.

---

# PART 9 — Butterfly Geometry

Think of:

* (E[k])
* rotated (O[k])

as vectors.

FFT:

1. rotates odd component
2. adds/subtracts vectors

This creates:

* constructive/destructive combinations.

---

# PART 10 — Twiddle Factors

The term:

[
W_N^k=e^{-j2\pi k/N}
]

is called:

* twiddle factor

It rotates odd-term vectors.

---

# Why Important?

These rotations align phases correctly when combining sub-DFTs.

Without twiddle factors:

* smaller FFTs cannot reconstruct full FFT.

---

# PART 11 — Example of Twiddle Factors

Suppose:

[
N=8
]

Then:

[
W_8=e^{-j2\pi/8}
]

Values:

| k | (W_8^k)        |
| - | -------------- |
| 0 | 1              |
| 1 | (e^{-j\pi/4})  |
| 2 | (-j)           |
| 3 | (e^{-j3\pi/4}) |

These are rotations on unit circle.

---

# PART 12 — FFT Stages

For radix-2 FFT:

Number of stages:

[
\log_2 N
]

Example:

| N    | Stages |
| ---- | ------ |
| 8    | 3      |
| 16   | 4      |
| 1024 | 10     |

---

# PART 13 — Example: 8-Point FFT

Input:

[
[x_0,x_1,x_2,x_3,x_4,x_5,x_6,x_7]
]

---

# Stage 1

Butterflies between:

* neighboring samples

---

# Stage 2

Butterflies between:

* groups of 4

---

# Stage 3

Butterflies between:

* groups of 8

Final outputs:

* FFT bins.

---

# PART 14 — Bit Reversal

This confuses many students.

FFT rearranges indices into bit-reversed order.

---

# Example

For (N=8):

| Index | Binary | Reversed | New |
| ----- | ------ | -------- | --- |
| 0     | 000    | 000      | 0   |
| 1     | 001    | 100      | 4   |
| 2     | 010    | 010      | 2   |
| 3     | 011    | 110      | 6   |
| 4     | 100    | 001      | 1   |

This ordering makes in-place FFT efficient.

---

# PART 15 — Why Bit Reversal Happens

Because recursive decomposition changes traversal order.

Bit reversal naturally emerges from:

* recursive splitting
* binary decomposition.

---

# PART 16 — In-Place FFT

FFT often:

* overwrites memory directly.

Advantages:

* lower RAM
* faster cache access
* embedded efficiency

Important in:

* ESP32
* DSP chips
* FPGA

---

# PART 17 — Decimation in Time (DIT)

The FFT we derived is:

# DIT FFT

because:

* input sequence gets divided.

---

# Another Variant

# DIF FFT

(Decimation in Frequency)

Instead:

* output frequencies are recursively split.

Both compute same FFT.

---

# PART 18 — Why FFT Complexity is (N\log N)

At each stage:

* total operations ≈ (N)

Number of stages:

[
\log_2N
]

So:

[
N\log_2N
]

---

# Compare Growth

| N         | DFT       | FFT         |
| --------- | --------- | ----------- |
| 1024      | 1,048,576 | 10,240      |
| 1,000,000 | (10^{12}) | ~20 million |

Massive difference.

---

# PART 19 — FFT as Matrix Factorization

DFT:

[
X=Wx
]

FFT factorizes matrix (W) into sparse butterfly matrices.

This is why:

* many computations disappear.

Advanced but important viewpoint.

---

# PART 20 — Physical Interpretation

FFT is:

* many rotating frequency detectors

organized efficiently.

Instead of independently computing every detector:

* FFT shares intermediate computations.

---

# PART 21 — FFT and Frequency Detection

Each FFT bin corresponds to:

[
f_k=\frac{kf_s}{N}
]

FFT efficiently computes:

* correlation with all sinusoidal basis functions.

---

# PART 22 — Real FFT Optimization

For real signals:

* half the spectrum is redundant.

Libraries exploit symmetry:

* reducing computation further.

Used heavily in audio DSP.

---

# PART 23 — Numerical Stability

FFT is numerically stable.

But issues include:

* floating-point precision
* quantization
* phase wrapping

Important in:

* beamforming
* MUSIC
* localization

---

# PART 24 — FFT Libraries

Most systems use optimized FFT libraries:

---

## FFTW

Very famous CPU FFT library.

---

## KissFFT

Simple embedded FFT.

---

## cuFFT

NVIDIA GPU FFT.

---

## CMSIS-DSP

ARM microcontroller FFT.

Important for ESP32-like systems.

---

# PART 25 — Deepest Intuition

The FFT is basically:

> recursive frequency decomposition using shared computations.

Instead of computing each frequency independently:

* smaller frequency analyses are reused.

This is the genius of FFT.

---

# PART 26 — Most Important Concepts to Master

Before moving ahead, deeply understand:

---

## Essential FFT Concepts

### 1. Even/Odd decomposition

### 2. Recursive splitting

### 3. Butterfly operation

### 4. Twiddle factors

### 5. Bit reversal

### 6. Frequency bins

### 7. Complex rotation

### 8. Radix-2 structure

### 9. Computational complexity

### 10. Phase rotation

---

# PART 27 — Why FFT Matters for YOUR Project

For sound localization:

* microphone signals are transformed using FFT
* phase differences are extracted
* localization algorithms work frequency-wise

FFT is the foundation for:

* GCC-PHAT
* Beamforming
* MUSIC
* SRP-PHAT
* DOA estimation

Everything ahead depends on this.

---

# NEXT TOPIC

The next critical topic is:

# Windowing (Hamming/Hann)

because real FFT systems suffer from:

* spectral leakage
* edge discontinuities

and windowing is essential before:

* STFT
* spectrograms
* GCC-PHAT
* MUSIC.



# PART 3 — Windowing (Hamming/Hann)

This is one of the most important practical DSP concepts.

Without understanding windowing:

* FFT results look confusing
* spectral leakage becomes severe
* localization quality drops
* GCC-PHAT becomes noisy
* spectrograms become messy

Windowing is absolutely fundamental in:

* audio DSP
* speech processing
* radar
* sonar
* beamforming
* MUSIC

---

# PART 1 — Why Windowing Exists

The FFT assumes:

> the signal repeats infinitely and periodically.

This assumption is extremely important.

Suppose you take only a small chunk of audio:

```text id="j2l7k2"
Recorded signal chunk:
|------------------|
```

FFT assumes this chunk repeats forever:

```text id="o4l1qz"
|----chunk----|----chunk----|----chunk----|
```

---

# Problem

If the signal edges do NOT connect smoothly:

```text id="wl87xj"
End jumps suddenly to beginning
```

then FFT sees a discontinuity.

That discontinuity introduces:

* fake frequencies
* spectral spreading
* noise in spectrum

This is called:

# Spectral Leakage

---

# PART 2 — Spectral Leakage Deeply

Suppose actual signal frequency:

* 1000.3 Hz

But FFT bins are:

* 1000 Hz
* 1015.6 Hz
* etc.

The signal does NOT perfectly fit inside FFT window.

Result:

* energy spreads into neighboring bins.

Instead of:

```text id="01u3pa"
Single sharp peak
```

you get:

```text id="2q3ewz"
Wide smeared peak
```

This is leakage.

---

# Why Leakage Happens

Because truncating a signal suddenly is equivalent to:

* multiplying by a rectangular window.

Sharp edges create high-frequency components.

---

# PART 3 — Rectangular Window

Without windowing, FFT automatically uses:

# Rectangular Window

Meaning:

[
w[n]=1
]

inside interval and 0 outside.

Graphically:

```text id="xy0qcl"
 ________
|        |
|        |
|________|
```

This creates sharp discontinuities at edges.

---

# PART 4 — Windowing Idea

Windowing means:

> smoothly reducing signal amplitude near edges.

Instead of abrupt cut:

```text id="tkfww8"
Sharp edges
```

we use smooth tapering:

```text id="m7s53o"
   /\ 
  /  \
 /    \
```

This reduces discontinuities.

---

# Mathematical Form

Windowed signal:

[
x_w[n]
======

x[n]w[n]
]

where:

* (x[n])=signal
* (w[n])=window function

---

# PART 5 — Important Tradeoff

Windowing:

* reduces leakage

BUT:

* reduces frequency resolution

This is a fundamental tradeoff.

---

# Leakage vs Resolution

| Better Leakage    | Worse Resolution |
| ----------------- | ---------------- |
| Better Resolution | Worse Leakage    |

No perfect window exists.

---

# PART 6 — Main Window Types

Most important:

1. Rectangular
2. Hann
3. Hamming
4. Blackman
5. Kaiser

For audio DSP:

* Hann and Hamming are most common.

---

# PART 7 — Hann Window

Very common in STFT and spectrograms.

Formula:

[
w[n]
====

0.5
\left(
1-
\cos\left(
\frac{2\pi n}{N-1}
\right)
\right)
]

---

# Shape

```text id="hqxqqm"
    /\
   /  \
  /    \
_/      \_
```

Edges smoothly go to zero.

---

# Properties

Advantages:

* good leakage reduction
* smooth spectrum
* good for audio

Disadvantages:

* slightly wider main lobe

Used heavily in:

* STFT
* speech
* spectrograms

---

# PART 8 — Hamming Window

Very similar to Hann.

Formula:

[
w[n]
====

## 0.54

0.46
\cos\left(
\frac{2\pi n}{N-1}
\right)
]

---

# Shape

Similar but edges do NOT fully reach zero.

---

# Why Different?

Hamming minimizes nearest side lobes better.

So:

* less leakage near main frequency.

---

# Hann vs Hamming

| Property   | Hann           | Hamming                |
| ---------- | -------------- | ---------------------- |
| Edge value | 0              | small nonzero          |
| Leakage    | Very good      | Slightly better nearby |
| Resolution | Slightly worse | Slightly better        |
| STFT usage | Very common    | Very common            |

---

# PART 9 — Main Lobe and Side Lobes

Critical concept.

Window spectrum contains:

---

## Main Lobe

Central frequency peak.

Controls:

* frequency resolution

Narrower main lobe:

* better separation of close frequencies.

---

## Side Lobes

Smaller peaks around main lobe.

Cause:

* leakage.

Lower side lobes:

* better leakage suppression.

---

# Tradeoff

You cannot simultaneously have:

* extremely narrow main lobe
* extremely low side lobes

Fundamental DSP limitation.

---

# PART 10 — Frequency-Domain Interpretation

Multiplication in time domain:

[
x[n]w[n]
]

becomes convolution in frequency domain.

Window spectrum smears frequency components.

This is why window affects spectral shape.

---

# PART 11 — Leakage Visualization

Without window:

```text id="7cx6b3"
Tall peak + many side ripples
```

With Hann:

```text id="e1pkl0"
Smoother peak + smaller ripples
```

---

# PART 12 — Why Windowing Matters for Audio

Audio signals are NOT periodic inside FFT frames.

Speech changes continuously.

Without windowing:

* strong FFT artifacts appear.

Windowing makes spectra physically meaningful.

---

# PART 13 — Windowing in STFT

In STFT:

* signal divided into small frames.

Each frame:

1. apply window
2. FFT
3. move forward

Without windowing:

* severe edge artifacts.

---

# PART 14 — Overlap

Because windows attenuate edges:

* information near boundaries weakens.

Solution:

* overlap adjacent windows.

Common:

* 50%
* 75%

Example:

```text id="w7wdnd"
Frame1: |------|
Frame2:    |------|
Frame3:       |------|
```

---

# PART 15 — Constant Overlap-Add (COLA)

Important STFT property.

Windows chosen so overlapping frames reconstruct signal properly.

Hann window with 50% overlap:

* commonly satisfies COLA.

---

# PART 16 — Window Length Tradeoff

Large window:

* better frequency resolution
* worse time resolution

Small window:

* better time localization
* poorer frequency precision

Critical for:

* spectrograms
* localization
* speech analysis

---

# PART 17 — Time-Frequency Tradeoff

Fundamental DSP principle.

Cannot simultaneously know:

* exact time
* exact frequency

Similar to uncertainty principle.

---

# PART 18 — Windowing in Sound Localization

Very important for your project.

---

# Why?

Localization often uses:

* phase information
* cross-spectrum
* FFT frames

Leakage corrupts phase estimation.

Bad phase:

* bad localization.

---

# Windowing Improves

* phase stability
* spectral estimation
* GCC-PHAT robustness
* beamforming quality

---

# PART 19 — Windowing and Phase

Windowing affects:

* magnitude strongly
* phase slightly

Good windows preserve phase consistency better.

Important for:

* GCC-PHAT
* MUSIC.

---

# PART 20 — Practical Audio Pipeline

Typical DSP pipeline:

```text id="6z5t1t"
Audio
→ Frame splitting
→ Windowing
→ FFT
→ Spectral processing
```

This is used almost everywhere.

---

# PART 21 — Why Hann is Extremely Popular

Hann provides:

* good leakage suppression
* smooth overlap-add
* computational simplicity

That’s why:

* librosa
* speech systems
* STFT pipelines

often default to Hann.

---

# PART 22 — Why Hamming is Popular

Hamming:

* better nearby side-lobe suppression
* slightly sharper spectral peaks

Used often in:

* speech recognition
* filter design

---

# PART 23 — Window Functions Are Frequency Filters

Deep interpretation:

Applying a window means:

* filtering the spectrum shape.

Different windows emphasize:

* different spectral behaviors.

---

# PART 24 — Important Practical Concepts

---

## Zero Padding + Windowing

Often combined.

Window:

* reduces leakage

Zero-padding:

* interpolates FFT bins

---

## Window Normalization

Need proper scaling:

* preserve amplitude
* preserve energy

Important in scientific measurements.

---

# PART 25 — DSP Engineer Intuition

Think of windowing as:

> smoothly observing a short signal segment without introducing sharp artificial edges.

---

# PART 26 — Most Important Concepts to Master

You should deeply understand:

---

## Essential Windowing Concepts

### 1. Spectral leakage

### 2. FFT periodicity assumption

### 3. Edge discontinuity

### 4. Main lobe

### 5. Side lobes

### 6. Leakage-resolution tradeoff

### 7. Hann window

### 8. Hamming window

### 9. Overlap

### 10. Time-frequency tradeoff

---

# PART 27 — Most Important Intuition

Windowing solves this problem:

```text id="w7s2n9"
FFT assumes repetition.
Edges don't match.
Discontinuity creates fake frequencies.
```

Windowing smooths edges to reduce those fake frequencies.

---

# NEXT TOPIC

Now we are ready for:

# Spectrograms and STFT (Short-Time Fourier Transform)

This is where:

* FFT
* windowing
* overlap

all combine together.

And this becomes the foundation for:

* speech recognition
* audio AI
* GCC-PHAT
* MUSIC
* sound localization systems.



# PART 4 — Spectrograms and STFT (Short-Time Fourier Transform)

Now we combine everything:

* DFT
* FFT
* Windowing
* Overlapping

into one of the most important tools in signal processing:

# STFT

and its visualization:

# Spectrogram

This is foundational for:

* speech recognition
* audio AI
* sound localization
* radar
* sonar
* music analysis
* beamforming
* GCC-PHAT
* MUSIC

---

# PART 1 — Why Ordinary FFT is Not Enough

Suppose you record speech:

```text id="t71n3q"
"Hello"
```

Speech changes over time.

Different frequencies appear at different moments.

---

# Problem with Normal FFT

If you FFT the entire signal:

[
x[n]
\rightarrow
X[k]
]

you only get:

* overall frequency content

You LOSE:

* timing information.

---

# Example

Suppose:

* 500 Hz occurs first
* 2000 Hz occurs later

Ordinary FFT cannot tell:

* when frequencies occurred.

---

# Need Time + Frequency Together

We want:

| Time           | Frequency                |
| -------------- | ------------------------ |
| At this moment | Which frequencies exist? |

This is exactly what STFT solves.

---

# PART 2 — Core Idea of STFT

Instead of FFTing the whole signal:

1. Take small chunk
2. Apply window
3. FFT
4. Slide window
5. Repeat

So we analyze:

* local frequencies over time.

---

# Visual Intuition

```text id="c2ow8f"
Signal:
|------------------------------|

Frame1:
|----|

Frame2:
    |----|

Frame3:
        |----|
```

Each frame:

* gets windowed
* transformed using FFT.

---

# PART 3 — STFT Mathematical Formula

STFT:

[
X(m,\omega)
===========

\sum_{n=-\infty}^{\infty}
x[n]w[n-m]e^{-j\omega n}
]

---

# Meaning of Symbols

---

## (x[n])

Input signal.

---

## (w[n-m])

Window centered at position (m).

Extracts local region.

---

## (e^{-j\omega n})

Frequency analysis basis.

---

## (X(m,\omega))

Frequency content at:

* time (m)
* frequency (\omega)

This creates:

* time-frequency representation.

---

# PART 4 — What STFT Actually Produces

STFT output is:

# A 2D representation

Axes:

| Axis      | Meaning        |
| --------- | -------------- |
| Time      | Frame position |
| Frequency | FFT bins       |

Values:

* magnitude
* phase

---

# PART 5 — Spectrogram

A spectrogram is:

[
|X(m,\omega)|^2
]

Usually:

* magnitude squared
* log-scaled

displayed as image.

---

# Spectrogram Axes

| Axis   | Meaning   |
| ------ | --------- |
| X-axis | Time      |
| Y-axis | Frequency |
| Color  | Energy    |

---

# Visual Example

```text id="17ohd5"
Bright areas = strong frequencies
Dark areas = weak frequencies
```

---

# PART 6 — Why Spectrograms are Powerful

They show:

* how frequencies evolve over time.

Speech:

* changing formants

Music:

* harmonics changing

Localization:

* frequency-dependent delays

---

# PART 7 — STFT Processing Pipeline

The full pipeline:

```text id="ljmjlwm"
Signal
→ Frame segmentation
→ Windowing
→ FFT
→ Magnitude/Phase
→ Spectrogram
```

---

# PART 8 — Frame Length

Critical parameter.

Suppose:

* sample rate = 16000 Hz
* frame size = 1024

Frame duration:

[
\frac{1024}{16000}
==================

64\text{ ms}
]

---

# PART 9 — Hop Length

Window shift amount.

Example:

* frame = 1024
* hop = 512

Means:

* 50% overlap.

---

# Why Overlap?

Window attenuates edges.

Without overlap:

* information lost.

Overlap improves:

* smoothness
* continuity
* reconstruction.

---

# PART 10 — Time-Frequency Tradeoff

One of the deepest DSP concepts.

---

# Large Window

Advantages:

* better frequency resolution

Disadvantages:

* poor time precision

---

# Small Window

Advantages:

* better timing precision

Disadvantages:

* poor frequency precision

---

# Fundamental Limitation

Cannot know:

* exact frequency
  and
* exact timing

simultaneously.

Similar to quantum uncertainty principle.

---

# PART 11 — Frequency Resolution in STFT

Resolution:

[
\Delta f
========

\frac{f_s}{N}
]

Large (N):

* finer frequency detail.

---

# PART 12 — Time Resolution

Approximate time precision:

[
\Delta t
========

\frac{N}{f_s}
]

Small windows:

* better time localization.

---

# PART 13 — Choosing Window Size

---

## Speech

Common:

* 20–40 ms

because speech changes rapidly.

---

## Music

Larger windows often used:

* better harmonic resolution.

---

## Localization

Depends on:

* latency
* frequency accuracy
* phase stability.

---

# PART 14 — Why Windowing is Essential in STFT

Without windowing:

* frame boundaries create discontinuities
* severe leakage occurs.

So every STFT uses:

* Hann
* Hamming
  or similar windows.

---

# PART 15 — STFT Magnitude and Phase

Each STFT bin contains:

[
X(m,k)
======

Re+jIm
]

---

# Magnitude

[
|X(m,k)|
]

Used for:

* spectrograms
* energy analysis.

---

# Phase

[
\angle X(m,k)
]

Used for:

* localization
* phase vocoders
* beamforming
* GCC-PHAT.

---

# PART 16 — Phase Evolution

As signal changes:

* phase evolves continuously.

Phase relationships across microphones:

* encode time delay.

This becomes crucial later.

---

# PART 17 — STFT and Convolution

STFT allows:

* frame-wise filtering
* spectral masking
* denoising

Widely used in AI speech enhancement.

---

# PART 18 — Spectrogram Interpretation

---

# Horizontal Lines

Constant frequencies.

Example:

* sustained musical note.

---

# Vertical Lines

Sudden broadband events.

Example:

* clap
* drum hit.

---

# Harmonics

Parallel frequency lines.

Example:

* speech vowels
* musical instruments.

---

# PART 19 — Mel Spectrograms

Speech systems often convert:

* linear frequency
  → mel scale.

Because human hearing is nonlinear.

Used in:

* speech AI
* Whisper
* voice assistants.

---

# PART 20 — Inverse STFT (ISTFT)

We can reconstruct signal.

Process:

1. inverse FFT
2. overlap-add frames

If windows satisfy COLA:

* accurate reconstruction possible.

---

# PART 21 — Overlap-Add Method

Each frame reconstructed:

```text id="zkh9aq"
Frame1
   + Frame2
       + Frame3
```

All frames summed together.

---

# PART 22 — Why STFT is Critical for Localization

Now VERY important for your project.

---

# Multi-Microphone Signals

Each microphone gets:

* slightly delayed version.

STFT converts signals into:

* frequency-domain frames.

Then localization algorithms compare:

* phase differences
* cross spectra.

---

# STFT Enables

* GCC-PHAT
* beamforming
* MUSIC
* SRP-PHAT

Almost all modern localization systems use STFT.

---

# PART 23 — Why Frequency Domain Helps

Time-domain localization:

* noisy
* unstable

Frequency-domain localization:

* phase-aware
* more robust
* easier filtering.

---

# PART 24 — STFT in Deep Learning

Modern audio AI uses:

* spectrograms
* mel spectrograms

as image-like inputs.

Examples:

* Whisper
* speaker recognition
* sound classification.

---

# PART 25 — Practical DSP Parameters

Common audio settings:

| Parameter   | Typical         |
| ----------- | --------------- |
| Sample Rate | 16kHz / 44.1kHz |
| FFT Size    | 512–2048        |
| Window      | Hann            |
| Overlap     | 50–75%          |

---

# PART 26 — Deep Intuition

STFT is basically:

> a moving localized FFT.

Instead of asking:

* “Which frequencies exist overall?”

STFT asks:

* “Which frequencies exist RIGHT NOW?”

---

# PART 27 — Most Important Concepts to Master

Before continuing, deeply understand:

---

## Essential STFT Concepts

### 1. Sliding windows

### 2. Frame segmentation

### 3. Overlap

### 4. Time-frequency tradeoff

### 5. Spectrogram interpretation

### 6. Phase evolution

### 7. Windowed FFT

### 8. Hop size

### 9. Frequency resolution

### 10. Time resolution

---

# PART 28 — Most Important Intuition

Think of STFT like this:

```text id="x8ot8o"
Ordinary FFT:
"What frequencies exist?"

STFT:
"When do those frequencies exist?"
```

---

# NEXT TOPIC

Now we are finally ready for:

# Cross-Correlation

This is the first direct localization-related concept.

Cross-correlation is how systems estimate:

* time delays
* alignment between microphones
* direction of arrival.

And GCC-PHAT is an advanced frequency-domain version of it.



Perfect. Now we enter the actual localization part.

We’ll go step-by-step and build the real microphone-array pipeline carefully.

The order will be:

1. Cross-Correlation
2. GCC-PHAT
3. TDOA Geometry
4. Microphone Array Geometry
5. Beamforming
6. MUSIC Algorithm

---

# First Topic:

# Cross-Correlation

This is the foundation of sound localization.

Before GCC-PHAT, beamforming, or MUSIC, you must deeply understand:

> how to estimate delay between two microphone signals.

That is exactly what cross-correlation does.

---

# PART 1 — Core Idea

Suppose:

* same sound reaches two microphones
* one microphone receives it slightly later

Example:

```text id="w5yypr"
Mic 1:  ----wave----
Mic 2:      ----wave----
```

Mic 2 signal is delayed.

Cross-correlation estimates:

* how much delay exists.

This delay is called:

# TDOA

(Time Difference of Arrival)

---

# PART 2 — Why Delay Matters

Sound direction is determined from delay.

If sound comes from left:

* left mic hears earlier.

If sound comes from right:

* right mic hears earlier.

Delay contains direction information.

---

# PART 3 — What Correlation Means

Correlation measures:

> similarity between two signals.

If signals align well:

* correlation becomes large.

If signals do not align:

* correlation becomes small.

---

# PART 4 — Basic Intuition

Suppose:

```text id="q81xlo"
x[n] = original signal
y[n] = delayed version
```

We:

1. slide one signal over another
2. measure similarity at each shift

The shift giving:

* maximum similarity
  = estimated delay.

---

# PART 5 — Cross-Correlation Formula

Discrete cross-correlation:

[
R_{xy}[\tau]
============

\sum_{n}
x[n]y[n-\tau]
]

---

# Meaning

---

## (x[n])

Signal from microphone 1.

---

## (y[n])

Signal from microphone 2.

---

## (\tau)

Shift (lag/delay).

---

# What Happens

For each possible delay:

1. shift signal
2. multiply samples
3. sum products

If signals align:

* large positive sum.

---

# PART 6 — Geometric Interpretation

Cross-correlation is basically:

# Inner Product

between:

* one signal
* shifted version of another.

If vectors align:

* large result.

If not:

* cancellation occurs.

---

# PART 7 — Correlation Peak

Suppose:

```text id="p5kx8s"
Mic1:  [1 2 3 4]
Mic2:      [1 2 3 4]
```

When shifted correctly:

* peaks overlap
* correlation maximum occurs.

Peak location gives delay.

---

# PART 8 — Positive and Negative Delays

Very important.

---

## Positive Delay

[
\tau > 0
]

means:

* second signal delayed.

---

## Negative Delay

[
\tau < 0
]

means:

* first signal delayed.

This tells:

* sound direction.

---

# PART 9 — Autocorrelation vs Cross-Correlation

---

## Autocorrelation

Signal correlated with itself.

[
R_{xx}[\tau]
]

Used for:

* pitch detection
* periodicity analysis

---

## Cross-Correlation

Two different signals.

[
R_{xy}[\tau]
]

Used for:

* localization
* delay estimation

---

# PART 10 — Example Physically

Suppose:

* microphones separated by 10 cm
* sound comes from left

Mic1 receives:

* first

Mic2 receives:

* slightly later.

Cross-correlation finds:

* tiny delay difference.

---

# PART 11 — Delay and Speed of Sound

Speed of sound:

[
c \approx 343\text{ m/s}
]

If microphones separated by:

[
d=0.1\text{ m}
]

Maximum delay:

[
\tau_{max}
==========

# \frac{d}{c}

0.29\text{ ms}
]

Very tiny.

This is why precise DSP is required.

---

# PART 12 — Correlation Output Shape

Correlation produces:

* a curve.

Peak location:

* estimated delay.

Example:

```text id="w6gfoz"
          /\
         /  \
________/    \_______
```

Peak center:

* best alignment.

---

# PART 13 — Noise Effects

Real signals contain:

* noise
* reverberation
* echoes

These distort correlation peaks.

Problems:

* multiple peaks
* blurred peaks
* unstable delay estimation

This leads to GCC-PHAT later.

---

# PART 14 — FFT-Based Correlation

Direct correlation:

* expensive.

Using Fourier transform:

[
R_{xy}
======

\mathcal{F}^{-1}
(X(f)Y^*(f))
]

where:

* (X(f))=FFT of signal 1
* (Y^*(f))=complex conjugate

This is MUCH faster.

---

# PART 15 — Why Conjugate Appears

Cross-spectrum:

[
X(f)Y^*(f)
]

extracts:

* phase difference
* frequency alignment

Very important later.

---

# PART 16 — Correlation and Delay

Delay in time domain becomes:

# Linear phase shift

in frequency domain:

[
Y(f)
====

X(f)e^{-j2\pi f\tau}
]

This relation is foundational for GCC-PHAT.

---

# PART 17 — Sample Delay

Estimated lag gives:

* sample delay.

Convert to seconds:

[
\tau
====

\frac{\text{lag}}{f_s}
]

where:

* (f_s)=sampling rate.

---

# Example

If:

* lag = 4 samples
* (f_s=16000)

then:

[
\tau
====

# \frac{4}{16000}

0.25\text{ ms}
]

---

# PART 18 — Correlation Resolution

Higher sampling rate:

* finer delay precision.

Important for localization accuracy.

---

# PART 19 — Subsample Delays

Real delays are not exact integers.

Need:

* interpolation
* phase estimation

GCC-PHAT helps greatly here.

---

# PART 20 — Multi-Microphone Systems

For many microphones:

* correlate each microphone pair.

Example:

* 4 microphones
  → multiple TDOA estimates.

Then combine geometrically.

---

# PART 21 — Correlation Problems in Real Rooms

Major challenges:

---

## Reverberation

Echoes create false peaks.

---

## Noise

Weakens correlation.

---

## Multiple Sources

Creates ambiguous peaks.

---

## Broadband Signals

Different frequencies behave differently.

---

# PART 22 — Why Ordinary Correlation is Often Insufficient

Simple correlation works poorly in:

* noisy rooms
* echoes
* multiple reflections

This is why:

# GCC-PHAT exists.

It improves:

* robustness
* peak sharpness
* phase reliability.

---

# PART 23 — Practical Localization Pipeline

Simple localization:

```text id="x2m5qc"
Mic1 + Mic2
→ Cross-correlation
→ Delay estimate
→ Convert delay to angle
```

This is the simplest DOA system.

---

# PART 24 — Deepest Intuition

Cross-correlation asks:

> “How much must I shift one signal so both align best?”

That shift equals:

* propagation delay.

Propagation delay contains:

* directional information.

---

# PART 25 — Most Important Concepts to Master

Before moving ahead, deeply understand:

---

## Essential Cross-Correlation Concepts

### 1. Signal alignment

### 2. Lag/shift

### 3. Correlation peak

### 4. Positive vs negative delay

### 5. Delay estimation

### 6. FFT-based correlation

### 7. Cross-spectrum

### 8. Time delay estimation (TDE)

### 9. TDOA

### 10. Noise/reverb effects

---

# PART 26 — Most Important Intuition

Think of cross-correlation like this:

```text id="c4rydb"
Slide one microphone signal
across the other
until they match best.
```

The amount of shift tells:

* which mic heard first
* how much earlier
* therefore sound direction.

---

# NEXT TOPIC

Next we should do:

# GCC-PHAT

This is the practical, robust, real-world version of correlation used in modern sound localization systems.



# PART 27 — GCC-PHAT

# (Generalized Cross Correlation with PHAT)

Now we move to the MOST important practical localization method for microphone arrays.

This is heavily used in:

* smart speakers
* robots
* drones
* conference systems
* voice assistants

because ordinary cross-correlation fails badly in:

* noise
* reverberation
* echoes

GCC-PHAT fixes many of those problems.

---

# PART 1 — Why Ordinary Correlation Fails

Suppose:

```text id="t2ehg5"
Mic1 → direct sound
Mic2 → delayed + echoes + noise
```

Ordinary correlation produces:

```text id="iuxjff"
multiple messy peaks
```

instead of:

* one sharp peak.

Problems:

* reverberation
* reflected waves
* frequency coloration
* microphone response differences

make localization unstable.

---

# PART 2 — Core Idea of GCC

Instead of correlating signals directly in time domain:

GCC works in:

# Frequency Domain

using FFT/STFT.

---

# Why Frequency Domain?

Because:

* delays become phase shifts
* phase is easier to analyze
* weighting becomes possible

---

# PART 3 — Cross-Power Spectrum

Suppose:

* (x[n])=mic1
* (y[n])=mic2

Take FFT:

[
X(f),Y(f)
]

Now compute:

[
G_{xy}(f)
=========

X(f)Y^*(f)
]

called:

# Cross-Power Spectrum

---

# Meaning

---

## (X(f))

Spectrum of mic1.

---

## (Y^*(f))

Complex conjugate of mic2 spectrum.

---

# What Does This Capture?

Cross-spectrum captures:

* frequency alignment
* phase difference
* delay information

between microphones.

---

# PART 4 — Delay as Phase Shift

Suppose:

[
y(t)=x(t-\tau)
]

In frequency domain:

[
Y(f)
====

X(f)e^{-j2\pi f\tau}
]

Then:

[
X(f)Y^*(f)
==========

|X(f)|^2e^{j2\pi f\tau}
]

Notice:

* delay encoded in phase.

This is the key insight behind GCC-PHAT.

---

# PART 5 — Generalized Cross Correlation (GCC)

General form:

[
R_{xy}(\tau)
============

\int
\Psi(f)
G_{xy}(f)
e^{j2\pi f\tau}
df
]

where:

* (\Psi(f))=weighting function

This weighting changes correlation behavior.

---

# PART 6 — PHAT Weighting

PHAT means:

# Phase Transform

Weighting:

[
\Psi(f)
=======

\frac{1}{|G_{xy}(f)|}
]

So GCC-PHAT becomes:

[
R_{PHAT}(\tau)
==============

\mathcal{F}^{-1}
\left(
\frac{X(f)Y^*(f)}
{|X(f)Y^*(f)|}
\right)
]

---

# PART 7 — What PHAT Actually Does

This is the most important intuition.

PHAT removes:

* magnitude information

and keeps only:

* phase information.

---

# Why?

Magnitude gets corrupted by:

* reverberation
* reflections
* room response
* source amplitude
* microphone gain

But delay information mainly exists in:

# phase differences.

---

# PART 8 — Result of PHAT

Without PHAT:

```text id="m2e6lr"
wide blurry peaks
```

With PHAT:

```text id="iq12gt"
sharp narrow peak
```

This makes delay estimation much more robust.

---

# PART 9 — Deep Physical Interpretation

Different frequencies may have:

* different amplitudes
* reflections
* attenuation

PHAT says:

> “Ignore amplitude. Trust only phase alignment.”

This greatly improves TDOA estimation.

---

# PART 10 — GCC-PHAT Pipeline

Practical pipeline:

```text id="owiy4e"
Mic signals
→ Window/STFT
→ FFT
→ Cross-spectrum
→ PHAT normalization
→ Inverse FFT
→ Correlation peak
→ Delay estimate
```

This is the standard real-world system.

---

# PART 11 — Why Inverse FFT Appears

After PHAT weighting:

[
\frac{X(f)Y^*(f)}
{|X(f)Y^*(f)|}
]

we perform inverse FFT.

Why?

Because:

* we want correlation as function of delay.

IFFT converts:

* frequency-domain phase relation
  → time-domain delay peak.

---

# PART 12 — Correlation Peak in GCC-PHAT

After IFFT:

```text id="5v14wa"
      /\
_____/  \_____
```

Peak location:

* estimated TDOA.

Peak becomes:

* sharper
* cleaner
  than ordinary correlation.

---

# PART 13 — Why GCC-PHAT Works Well for Speech

Speech is:

* broadband
* noisy
* reverberant

PHAT emphasizes:

* consistent phase relationships

across frequencies.

This improves speech localization greatly.

---

# PART 14 — Subsample Precision

Huge advantage.

GCC-PHAT can estimate:

* fractional sample delays

because phase changes continuously.

This gives:

* higher angular precision.

---

# PART 15 — Delay Resolution

Maximum theoretical delay:

[
\tau_{max}
==========

\frac{d}{c}
]

where:

* (d)=mic spacing
* (c)=speed of sound

GCC-PHAT estimates delays within this range.

---

# PART 16 — Why Multiple Frequencies Help

Single-frequency localization:

* ambiguous

Broadband signals:

* much better

because:

* phase patterns across frequencies become unique.

Speech works well because it is broadband.

---

# PART 17 — FFT Size Effects

Larger FFT:

* better frequency resolution
* better phase estimation

BUT:

* larger latency.

Tradeoff important in real-time systems.

---

# PART 18 — Windowing Importance

GCC-PHAT relies heavily on:

* accurate phase.

Without proper windowing:

* spectral leakage corrupts phase.

Usually:

* Hann window used.

---

# PART 19 — Noise Robustness

PHAT improves robustness against:

* colored noise
* room response
* amplitude distortion

But:

* very low SNR still difficult.

---

# PART 20 — Reverberation Effects

Reflections create:

* extra peaks.

PHAT suppresses many reflection effects because:

* reflections distort amplitude more than phase consistency.

---

# PART 21 — Multi-Microphone Arrays

With many microphones:

Compute GCC-PHAT for:

* every microphone pair.

Example:

* 4 microphones
  → 6 microphone pairs.

Then combine delays.

---

# PART 22 — Converting Delay to Direction

After delay estimate:

[
\tau
]

convert to angle:

[
\theta
======

\sin^{-1}
\left(
\frac{c\tau}{d}
\right)
]

where:

* (c)=speed of sound
* (d)=mic spacing.

This gives DOA.

---

# PART 23 — Practical Problems

Even GCC-PHAT has issues:

---

## Multiple Sources

Multiple peaks appear.

---

## Strong Reverberation

Still difficult indoors.

---

## Spatial Aliasing

Large mic spacing causes ambiguity.

---

## Synchronization Errors

Microphones must be synchronized precisely.

---

# PART 24 — Why Phase Is So Important

The entire localization problem is fundamentally about:

* measuring phase differences.

Because:

* propagation delay
  → phase shift.

This becomes even more important in:

* beamforming
* MUSIC.

---

# PART 25 — STFT + GCC-PHAT

Modern systems usually:

1. frame signal
2. apply STFT
3. GCC-PHAT per frame
4. average results

This improves stability.

---

# PART 26 — Deepest Intuition

Ordinary correlation asks:

> “Which alignment gives largest similarity?”

GCC-PHAT asks:

> “Which alignment gives most consistent phase relationship across frequencies?”

That is much more robust.

---

# PART 27 — Most Important Concepts to Master

Before moving ahead, deeply understand:

---

## Essential GCC-PHAT Concepts

### 1. Cross-power spectrum

### 2. Complex conjugate

### 3. Delay → phase shift

### 4. Phase-only weighting

### 5. PHAT normalization

### 6. IFFT correlation recovery

### 7. Correlation peaks

### 8. TDOA estimation

### 9. Broadband localization

### 10. Reverberation robustness

---

# PART 28 — Most Important Intuition

Think of GCC-PHAT like this:

```text id="rn7hqv"
Ignore loudness.
Ignore amplitude.
Only trust phase consistency.
```

That is why it localizes sound much better than ordinary correlation.

---

# NEXT TOPIC

Next we should do:

# TDOA Geometry + Converting Delay to Angle

This is where localization becomes actual:

* direction estimation
* angle computation
* geometric sound localization.



# PART 29 — TDOA Geometry

# (Time Difference of Arrival → Direction of Arrival)

Now we finally convert:

```text
Delay Estimate
      ↓
Sound Direction
```

This is where localization becomes an actual angle.

---

# PART 1 — What We Already Have

Using GCC-PHAT we estimated:

[
\tau
]

where:

[
\tau = t_2 - t_1
]

This is the arrival time difference between microphones.

Now we must answer:

> Which direction did the sound come from?

---

# PART 2 — Simplest Microphone Array

Consider 2 microphones:

```text
Mic1 -------- d -------- Mic2
```

where:

[
d
=

\text{microphone spacing}
]

Example:

[
d=0.1m
]

(10 cm)

---

# PART 3 — Sound from Front

Suppose sound comes directly from front:

```text
      Source
         |
         |
Mic1 -------- Mic2
```

Distance to both microphones is equal.

Therefore:

[
\tau=0
]

Both microphones hear sound simultaneously.

---

# Result

Direction:

[
\theta = 0^\circ
]

(front)

---

# PART 4 — Sound from Left

Now sound comes from left:

```text
Source →

Mic1 -------- Mic2
```

Mic1 hears first.

Mic2 hears later.

Therefore:

[
\tau > 0
]

---

# Physical Meaning

The sound must travel extra distance before reaching Mic2.

Extra distance creates delay.

---

# PART 5 — Sound from Right

```text
← Source

Mic1 -------- Mic2
```

Mic2 hears first.

Mic1 hears later.

Therefore:

[
\tau < 0
]

---

# Sign of Delay

Very important.

| Delay    | Meaning                 |
| -------- | ----------------------- |
| Positive | Source on one side      |
| Negative | Source on opposite side |
| Zero     | Source in front         |

---

# PART 6 — Path Difference

Key concept:

Sound does NOT travel the same distance to each microphone.

Difference in travel distance:

[
\Delta L
]

called:

# Path Difference

---

# PART 7 — Relationship Between Distance and Delay

Sound speed:

[
c \approx 343 m/s
]

Distance traveled:

[
\Delta L
========

c\tau
]

This is extremely important.

---

# Example

Suppose:

[
\tau=0.0002s
]

Then:

[
\Delta L
========

# 343 \times 0.0002

0.0686m
]

6.86 cm path difference.

---

# PART 8 — Geometry of Arrival Angle

Assume sound source is far away.

This is called:

# Far-Field Assumption

Wavefronts become approximately parallel.

```text
/////////
/////////
/////////

Mic1 ----- Mic2
```

This assumption simplifies geometry enormously.

---

# PART 9 — Arrival Angle

Define:

[
\theta
]

as sound direction relative to array normal.

```text
        Front
          |
          |
          |
Mic1------Mic2
```

---

# PART 10 — Deriving Path Difference

From geometry:

[
\Delta L
========

d\sin\theta
]

This is the fundamental localization equation.

Why?

Because projected distance onto propagation direction equals:

[
d\sin\theta
]

---

# Visual Intuition

```text
         /
        /
       / θ
      /
Mic1------Mic2
```

The angled wave reaches one microphone earlier.

---

# PART 11 — Combining Equations

We already know:

[
\Delta L=c\tau
]

and

[
\Delta L=d\sin\theta
]

Equating:

[
c\tau
=====

d\sin\theta
]

---

# Final DOA Formula

[
\boxed{
\theta
======

\sin^{-1}
\left(
\frac{c\tau}{d}
\right)
}
]

This is one of the most important equations in sound localization.

\theta=\sin^{-1}\left(\frac{c\tau}{d}\right)

---

# PART 12 — Example Calculation

Suppose:

Mic spacing:

[
d=0.1m
]

Delay:

[
\tau=0.0001s
]

Speed of sound:

[
c=343m/s
]

Then:

[
\theta
======

\sin^{-1}
\left(
\frac{343\times0.0001}{0.1}
\right)
]

# [

\sin^{-1}(0.343)
]

[
\approx20^\circ
]

Source is roughly 20° off-center.

---

# PART 13 — Maximum Possible Delay

Important physical constraint.

Maximum path difference:

[
\Delta L_{max}=d
]

Therefore:

[
\tau_{max}
==========

\frac{d}{c}
]

---

# Example

For:

[
d=0.1m
]

[
\tau_{max}
==========

\frac{0.1}{343}
]

# [

0.000291s
]

# [

291\mu s
]

Tiny delay!

This explains why localization is hard.

---

# PART 14 — Delay in Samples

Suppose:

[
f_s=16000Hz
]

Then:

[
291\mu s
\times
16000
=====

4.66
]

Only about 5 samples.

This is why GCC-PHAT and phase methods are needed.

---

# PART 15 — Front-Back Ambiguity

Huge limitation of 2 microphones.

Suppose:

```text
Source A
    ↘

Mic1------Mic2

    ↗
Source B
```

Both can produce identical delay.

Therefore:

2 microphones cannot distinguish:

* front
* back

This is called:

# Front-Back Ambiguity

---

# PART 16 — How to Solve Ambiguity

Need:

* 3 microphones
* 4 microphones
* circular array

More geometry gives unique solutions.

---

# PART 17 — Hyperbolic Localization

For position estimation:

Instead of angle only,

each TDOA defines:

# Hyperbola

Possible source locations:

```text
      )
    )
Mic1      Mic2
    (
      (
```

Source must lie somewhere on that curve.

---

# PART 18 — Multiple Microphones

Example:

4 microphones.

```text
M1 ---- M2
|        |
|        |
M3 ---- M4
```

Now compute multiple TDOAs.

Intersection of constraints gives source direction.

---

# PART 19 — Why More Microphones Help

Benefits:

* less ambiguity
* more robustness
* better noise rejection
* better accuracy

This is why smart speakers use:

* 4–8 microphones

---

# PART 20 — Far-Field vs Near-Field

---

## Far Field

Source very far away.

Assume:

[
distance \gg array\ size
]

Wavefronts:

```text
///////////
///////////
```

Parallel.

Most DOA algorithms assume this.

---

## Near Field

Source close.

Wavefronts:

```text
  )
 )
)
```

Curved.

More complicated geometry.

---

# PART 21 — Practical Limits

Localization accuracy depends on:

---

### Mic spacing

Larger spacing:

* larger delays
* easier estimation

BUT:

can cause spatial aliasing.

---

### Sampling rate

Higher:

* finer delay resolution

---

### Noise

More noise:

* poorer TDOA estimates

---

### Reverberation

Creates false delays.

---

# PART 22 — What Happens After TDOA?

Real pipeline:

```text
Microphones
↓
STFT
↓
GCC-PHAT
↓
Delay Estimate τ
↓
DOA Equation
↓
Angle θ
```

This alone can already build a basic direction finder.

---

# PART 23 — Why Beamforming Comes Next

TDOA gives:

> "Where is the sound?"

Beamforming answers:

> "Can I listen only in that direction?"

That's why the next topic is:

# Microphone Array Geometry

followed immediately by

# Beamforming

because array shape strongly affects localization performance.




# PART 30 — Microphone Array Geometry

Before beamforming or MUSIC, you must understand:

> How microphone placement affects localization accuracy.

Many localization problems are actually caused by poor microphone geometry, not poor algorithms.

---

# PART 1 — What is a Microphone Array?

A microphone array is simply:

```text
Multiple microphones
with known positions.
```

Example:

```text
Mic1    Mic2
  •------•
```

or

```text
Mic1    Mic2
  •------•
  |      |
  •------•
Mic3    Mic4
```

The geometry determines:

* which delays are measurable
* localization accuracy
* ambiguity
* maximum detectable frequency

---

# PART 2 — Why Geometry Matters

Suppose two arrays:

### Array A

```text
•-•
```

spacing = 2 cm

### Array B

```text
•---------•
```

spacing = 20 cm

For the same sound:

Array B produces:

* larger delay
* easier estimation

Array A produces:

* tiny delay
* harder estimation

---

# PART 3 — Linear Array

Most common beginner setup.

```text
M1 ---- M2 ---- M3 ---- M4
```

Advantages:

* simple
* easy math
* easy wiring

Used in:

* smart speakers
* soundbars

---

# Problem

Cannot uniquely distinguish:

```text
Front
```

from

```text
Back
```

This is called:

# Front-Back Ambiguity

---

# PART 4 — Circular Array

Example:

```text
      M1

 M4         M2

      M3
```

Advantages:

* 360° coverage
* removes front-back ambiguity
* good for DOA estimation

Used in:

* conference systems
* robots

---

# PART 5 — Planar Array

2D arrangement.

```text
M1 ---- M2

M3 ---- M4
```

Can estimate:

* azimuth
* elevation

Useful for 3D localization.

---

# PART 6 — Volumetric Array

3D microphone placement.

```text
      M1

 M2        M3

      M4
```

Used in:

* advanced acoustic research
* 3D source localization

---

# PART 7 — Array Aperture

Very important term.

Array aperture = total array size.

Example:

```text
M1-------------M4
```

Distance between extreme microphones.

---

# Why Important?

Larger aperture:

* larger measurable delays
* better angular resolution

But also introduces new problems.

---

# PART 8 — Speed of Sound

Always remember:

[
c \approx 343 m/s
]

Every geometry calculation depends on this.

---

# PART 9 — Wavelength

Critical concept.

[
\lambda = \frac{c}{f}
]

where:

* (c) = speed of sound
* (f) = frequency

Example:

1000 Hz:

[
\lambda
=======

# \frac{343}{1000}

0.343m
]

34.3 cm.

---

# PART 10 — Spatial Sampling

This is the microphone-array equivalent of Nyquist sampling.

For microphones:

We sample sound in space.

Not time.

---

# PART 11 — Spatial Aliasing

One of the biggest array-design problems.

Suppose spacing is too large.

```text
M1----------------M2
```

Different directions can produce identical phase differences.

Then localization becomes ambiguous.

---

# PART 12 — Spatial Nyquist Rule

To avoid aliasing:

[
d \le \frac{\lambda_{min}}{2}
]

where:

* (d) = microphone spacing
* (\lambda_{min}) = shortest wavelength

This is one of the most important array-design formulas.

d\leq\frac{\lambda_{min}}{2}

---

# PART 13 — Example

Suppose maximum frequency:

[
f_{max}=8000Hz
]

Then:

[
\lambda_{min}
=============

# \frac{343}{8000}

0.0429m
]

4.29 cm.

Therefore:

[
d
<
2.15cm
]

to avoid aliasing completely.

---

# PART 14 — Real Systems

Many systems choose:

2–5 cm spacing.

Why?

Balances:

* delay sensitivity
* aliasing risk

---

# PART 15 — Tradeoff

### Small Spacing

Advantages:

* less aliasing

Disadvantages:

* tiny delays
* harder estimation

---

### Large Spacing

Advantages:

* larger delays
* better sensitivity

Disadvantages:

* spatial aliasing

---

# PART 16 — Pair Count

Suppose:

N microphones.

Number of unique pairs:

[
\frac{N(N-1)}{2}
]

Example:

4 microphones:

[
6
]

pairs.

---

# Why Useful?

More pairs:

* more TDOA estimates
* better averaging
* more robustness

---

# PART 17 — Steering Direction

Every sound direction produces:

* unique delay pattern
* unique phase pattern

across microphones.

This pattern is called:

# Steering Vector

We'll use it heavily in beamforming and MUSIC.

---

# PART 18 — Example Delay Pattern

4-mic linear array:

```text
M1----M2----M3----M4
```

Sound from left:

```text
M1 first
M2 later
M3 later
M4 last
```

Creates delay sequence:

```text
0
τ
2τ
3τ
```

This pattern identifies direction.

---

# PART 19 — Why More Mics Help

Two microphones:

```text
•------•
```

Only one delay estimate.

Four microphones:

```text
•--•--•--•
```

Many delay estimates.

More information.

Better localization.

---

# PART 20 — What Geometry Should YOU Use?

For your ESP32 + multiple-mic project:

### 2 microphones

Good for:

* learning
* basic angle estimation

### 4 microphones

Recommended.

Can:

* remove ambiguity
* improve accuracy

### Circular 6-mic array

Excellent.

Used in many commercial products.

---

# PART 21 — What Beamforming Adds

Right now we can:

```text
Microphones
↓
GCC-PHAT
↓
TDOA
↓
Direction
```

Beamforming adds:

```text
Microphones
↓
Focus listening toward a direction
↓
Suppress other directions
```

Think of it as:

> A camera lens for sound.

---

# Most Important Concepts from Array Geometry

Understand these deeply:

1. Linear array
2. Circular array
3. Array aperture
4. Wavelength
5. Spatial sampling
6. Spatial aliasing
7. Mic spacing
8. Pair count
9. Delay pattern
10. Steering vectors

---

# Next Topic

The next major topic is:

# Beamforming

This is where microphones stop being independent sensors and start acting like a **single directional acoustic antenna**. This is one of the coolest concepts in array signal processing.

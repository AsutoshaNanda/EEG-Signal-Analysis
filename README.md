## PHASE-1

## Introduction

Epilepsy is a common neurological disorder that affects approximately 50 million people worldwide. It is characterized by sudden seizures that can be life-threatening. EEG (Electroencephalography) is commonly used to diagnose epilepsy by monitoring brain activity. However, EEG recordings require expert analysis, making the process slow and tedious.

This study examines different representations of EEG signals—**time-domain** and **frequency-domain**—to determine which is more effective for seizure detection. Two major EEG databases were used:

* **Freiburg Database** (Intracranial EEG)
* **CHB-MIT Database** (Scalp EEG)
 
---

### About Seizures

A seizure is an abnormal burst of electrical activity in the brain, which can lead to changes in behavior, movements, feelings, or consciousness. Seizures can vary in severity and duration, ranging from brief lapses in awareness to prolonged convulsions. For individuals with epilepsy, predicting seizures can make a world of difference by enabling timely interventions, such as administering medication or moving to a safe environment.



Epilepsy affects millions of people worldwide, and despite advancements in treatment, many patients continue to experience seizures. The unpredictability of seizures is one of the most challenging aspects of epilepsy, underscoring the importance of accurate and reliable prediction methods.

---

## Materials and Methods

### 1.Dataset Description

Two publicly available datasets were analyzed:

* **Freiburg Database**: Contains intracranial EEG (iEEG) data from 21 epilepsy patients. Electrodes were placed inside the brain, resulting in high-quality signals with minimal noise.

* **CHB-MIT Database**: Contains scalp EEG (sEEG) recordings from 23 children with epilepsy. Electrodes were placed on the scalp, making it a non-invasive method but with higher noise interference.

> In this project, I am using the **Preprocessed CHB-MIT Scalp EEG Database**.

Both datasets were used to classify EEG signals into three states:

1. **Ictal** – During a seizure
2. **Preictal** – Just before a seizure
3. **Interictal** – Between seizures

---

### 2.Time and Frequency Domain Signals

* **Time-domain signals** represent EEG activity over time.

* **Frequency-domain signals** show how signal components are distributed in different frequency bands, obtained using **Fast Fourier Transform (FFT)**. Frequency-domain signals often highlight patterns that are difficult to detect in time-domain signals.

---

### 3.Performance Evaluation

The study used three evaluation metrics:

* **Accuracy (ACC)**: Measures overall correctness.
* **Sensitivity (SEN)**: Measures how well seizures are detected.
* **Specificity (SPE)**: Measures how well non-seizure states are identified.

> ##### I am using the "Preprocessed CHB-MIT Scalp EEG dataset" because it provides a structured and balanced set of preictal and ictal EEG data, making it ideal for machine learning and deep learning models in epileptic seizure detection. With 23 retained EEG channels and an Outcome column for classification, it simplifies data handling while maintaining crucial seizure patterns.

🔗 [**Preprocessed CHB-MIT Scalp EEG Dataset**](https://ieee-dataport.org/open-access/preprocessed-chb-mit-scalp-eeg-database)

---

## PHASE-2
### Feature Extraction : Frequency Features
---
### Power Spectral Density (PSD) 

**Power Spectral Density (PSD)** represents the distribution of power across different frequency components in a signal. It provides insight into how the power of an EEG signal is distributed over frequency, making it a crucial tool for analyzing brain activity.

---

### Why PSD is Used in EEG?

* **Feature Extraction** – Helps identify dominant frequency bands (Delta, Theta, Alpha, Beta, Gamma) related to cognitive states.
* **Seizure Detection** – Highlights spectral patterns distinguishing normal and abnormal brain activity.
* **Signal Characterization** – Provides a compact and informative representation of EEG signals.

---

### EEG Frequency Bands and Their Significance:

* **Delta (0.5–4 Hz)** – Deep sleep, unconscious states
* **Theta (4–8 Hz)** – Drowsiness, relaxation
* **Alpha (8–12 Hz)** – Calm, resting state
* **Beta (12–30 Hz)** – Active thinking, problem-solving
* **Gamma (30–100 Hz)** – Cognitive processing, memory functions

---

### Welch’s Method

We will be using **Welch’s Method**, which is a technique used in EEG analysis to estimate the Power Spectral Density (PSD) more accurately.

Instead of analyzing the entire EEG signal at once (which can be noisy), Welch’s Method breaks the signal into smaller overlapping segments. For each segment, it calculates a power estimate, then averages all these estimates together. This reduces noise and gives a smoother and more reliable PSD result.

---


## Dominant Frequency 

**Dominant Frequency** refers to the most prominent (i.e., highest power) frequency component within a given EEG signal segment. In other words, it's the frequency at which the brain's electrical activity is most active over a specific period and region.

##  Significance of Dominant Frequency

* **Quantifies the core oscillatory activity** of each brain region.
* **Fast way to summarize brain activity** without diving into full PSD analysis.
* Useful for both **clinical diagnostics** and **cognitive research**.
* Can track **brain state transitions** in real-time EEG recordings.

---

##  Welch’s Method in Dominant Frequency

The **Welch method** is used to estimate the **Power Spectral Density (PSD)** of EEG signals. This is key to finding the dominant frequency.

###  Why Welch’s Method?

*  Reduces noise in the spectrum
*  Gives a smooth estimate of the PSD
*  Well-suited for EEG signals which are noisy and non-stationary

### 🔧 How It Works :

1. Split the EEG signal into overlapping segments
2. Apply a window function (like Hamming)
3. Compute FFT for each segment
4. Average the power spectra

From this, the **frequency with the highest PSD value** is extracted — that’s your **dominant frequency**.

---

## Entropy

## What is Entropy in EEG?

Entropy is a mathematical measure of randomness or uncertainty in a signal. In the context of EEG analysis, entropy helps quantify how complex or unpredictable brain activity is over time.

An EEG signal with:
- **Low entropy** indicates regular, predictable patterns (e.g., sleep, unconsciousness)
- **High entropy** reflects irregular, complex patterns (e.g., alertness, cognitive engagement)

Entropy metrics are particularly valuable in neuroscience because they capture dynamic brain behaviors that traditional frequency-based methods (like Fourier transforms) may overlook.

---

## Why Is Entropy Used in EEG Analysis?

Entropy is used in EEG research and clinical applications to assess brain function and identify abnormalities. Some key use cases include:

- **Sleep staging**: Differentiating REM and non-REM stages based on signal complexity.
- **Seizure detection**: Entropy often drops before and during epileptic seizures.
- **Cognitive workload monitoring**: Increased mental activity typically correlates with higher entropy.
- **Neurodegenerative disorders**: Diseases like Alzheimer's often show reduced signal complexity.

Because entropy captures subtle non-linear characteristics of brain signals, it provides insight beyond conventional power spectral or amplitude-based measures.

---

## Significance of Entropy in EEG

Entropy-based analysis is significant for several reasons:

1. **Non-linear insight**: EEG signals are non-stationary and often non-linear. Entropy effectively captures this complexity.
2. **Robust to noise**: Entropy measures are more resilient to artifacts than raw amplitude or power analysis.
3. **Channel-wise comparison**: Entropy can be computed independently for each EEG channel, enabling spatial brain mapping.
4. **Real-time use**: Entropy can be computed on-the-fly for applications in brain-computer interfaces and alertness monitoring.

---

## Shannon Entropy

### What is Shannon Entropy?

Shannon Entropy quantifies the average amount of information or uncertainty in a signal. For a discrete probability distribution of values in a signal, it is defined as: 
`H = -Σ (p_i * log2(p_i))`

---
## Band Power 

## What is Band Power in EEG?

**Band power** refers to the total amount of energy (or power) present in an EEG signal within a specific frequency range (or band). EEG signals are made up of different frequency components, and these are grouped into **standard brainwave bands**:

| Band  | Frequency Range (Hz) | Associated Mental State          |
| ----- | -------------------- | -------------------------------- |
| Delta | 0.5 – 4              | Deep sleep                       |
| Theta | 4 – 8                | Drowsiness, meditation           |
| Alpha | 8 – 13               | Relaxed wakefulness, eyes closed |
| Beta  | 13 – 30              | Alertness, concentration         |
| Gamma | 30 – 100             | High-level cognition, attention  |

**Band power analysis** computes how much power is concentrated in each of these bands, helping you understand the dominant mental state or activity of the brain.

---

## Why is Band Power Analysis Important in EEG?

Band power is one of the **most practical and interpretable features** in EEG analysis. Here's why it's commonly used:

1. **Quick summary of mental state**:
   Instead of analyzing the entire raw EEG waveform, we extract meaningful features that relate to known cognitive or physiological states.

2. **Used in medical and research settings**:

   * Sleep staging
   * Seizure detection
   * Brain-computer interfaces (BCIs)
   * Meditation and neurofeedback training
   * Detecting cognitive load or attention changes

3. **Foundational for machine learning and diagnostics**:
   Band power values are frequently used as **input features** for classification tasks (e.g., predicting alertness or mental fatigue).

---

## How is Band Power Computed?

We use the following general steps for **each EEG channel**:

1. **Compute PSD** using Welch’s method.
2. **For each frequency band (e.g., Theta 4–8 Hz)**:

   * Integrate the PSD within that band.
   * This gives you the **average power** in that frequency range.

This process is repeated across all bands and all channels, resulting in a matrix of values:
**\[Channel × Frequency Band] = Power**

---

## Welch’s Method

To compute the Power Spectral Density (PSD), we use **Welch’s method**, which is a common and reliable technique.

### Why Welch's Method?

* Reduces noise by averaging over segments
* Produces smooth, reliable power estimates
* Works well with non-stationary signals like EEG

### Summary of Welch's Method:

* EEG signal is split into overlapping segments
* Each segment is windowed (e.g., with a Hamming window)
* FFT is applied to each segment
* The power spectra are averaged

Then the power values within each EEG band are **integrated (summed or averaged)** to get the **band power**.

---

## Wavelet Transform 

## What is Wavelet Transform in EEG?

A **wavelet transform** is a mathematical technique that breaks a signal down into both **time** and **frequency** components. Unlike traditional Fourier-based methods (like PSD), which only show *what frequencies are present*, wavelet transforms also tell you **when** those frequencies occur.

This is crucial in EEG analysis because EEG signals are **non-stationary** — their frequency content **changes over time**. For example, a burst of alpha activity may only last for a few seconds during a recording, and we want to detect exactly *when* and *where* it happens.

---

## Why Use Wavelet Transform in EEG?

Wavelet transforms are widely used in EEG because they:

1. **Handle non-stationary signals well**
   EEG signals often contain short-lived events (e.g., spikes, bursts, artifacts). Wavelets can detect these because they provide **time-localized frequency information**.

2. **Capture both time and frequency**
   Unlike PSD (which gives global frequency info), wavelets give **localized power over time** — i.e., frequency vs. time maps.

3. **Enable event-based analysis**
   Especially useful for:

   * Detecting seizures
   * Monitoring brain responses to stimuli
   * Real-time analysis of dynamic brain states

4. **Provide multiresolution analysis**
   Low frequencies are analyzed with high temporal width, and high frequencies with fine time precision — a perfect match for EEG’s structure.

---

## How Wavelet Transform Works 

Wavelet transform breaks down a signal using small wave-like functions (called wavelets) that are **scaled and shifted** over the signal.

There are two main types:

* **DWT (Discrete Wavelet Transform)**: Breaks signal into approximation and detail coefficients at various levels.
* **CWT (Continuous Wavelet Transform)**: Produces a full time-frequency representation, ideal for visualization.

For EEG, you typically:

* Choose a wavelet (e.g., `db4`, `sym5`, `morl`)
* Decompose the EEG signal into levels
* Analyze or plot the energy at each level (each corresponds to a frequency range)

---
### Feature Extraction : Time Features
---
### Statistical Features
1. **Mean**: Represents the average amplitude of the EEG signal over a specific time window.
2. **Standard Deviation (SD)**: Measures the variability or dispersion of the signal amplitudes.
3. **Variance (var)**: Quantifies the spread of the signal amplitudes.
4. **Maximum (max)**: The highest amplitude value in the signal.
5. **Minimum (min)**: The lowest amplitude value in the signal.
6. **Peak-to-Peak (ptp)**: Difference between the maximum and minimum values.
7. **Skewness (skew)**: Measures the asymmetry of the signal distribution.
8. **Kurtosis (kurt)**: Indicates the "tailedness" of the signal distribution.
9. **Zero Crossings (zcross)**: Counts the number of times the signal crosses zero.
10. **Energy**: Represents the total power of the signal.
11. **Root Mean Square (RMS)**: A measure of the signal's magnitude.

### Hjorth Parameters
12. **Activity**: Represents the variance of the signal, indicating signal power.
13. **Mobility**: Measures the frequency content of the signal by comparing the variance of the first derivative to the original signal.
14. **Complexity**: Indicates the structural complexity of the signal by comparing second and first derivative mobilities.

### Temporal Features
15. **Line Length**: Sum of absolute differences between consecutive points, representing signal variability.

---
### EEG Channels
Features are extracted for the following channels:
- **FP1-F7, C3-P3, C4-P4, CZ-PZ, F3-C3, F4-C4, F7-T7, F8-T8, FP1-F3, FP2-F4, FP2-F8, FT10-T8, FT9-FT10, FZ-CZ, P3-O1, P4-O2, P7-O1, P7-T7, P8-O2, T7-FT9, T7-P7, T8-P8-0, T8-P8-1**

For each channel, the above features are computed and used for analysis.

## Time Series Analysis
EEG signals are inherently time-series data, capturing temporal patterns of brain activity. The analysis of time series involves:

- **Segmentation**: Dividing the continuous EEG signals into smaller time windows.
- **Feature Computation**: Calculating statistical features (mean, SD, variance, etc.) for each segment.
- **Sequence Construction**: Representing the EEG data as a sequence of statistical features over time.

This approach helps in identifying patterns that could predict seizures.

---

## PHASE-3
### Models Used
---
To classify and predict seizures, multiple machine learning models are employed. Each model is trained on features extracted from both the time and frequency domains, leveraging different characteristics of the EEG signal for improved performance.

#### K-Nearest Neighbors (KNN)
* **Simple and effective** for classifying EEG patterns, especially with small or low-dimensional datasets.
* **Non-parametric**, so it doesn’t assume any distribution of the data.

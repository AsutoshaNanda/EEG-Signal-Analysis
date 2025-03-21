## PHASE-1

## Introduction

Epilepsy is a common neurological disorder that affects approximately 50 million people worldwide. It is characterized by sudden seizures that can be life-threatening. EEG (Electroencephalography) is commonly used to diagnose epilepsy by monitoring brain activity. However, EEG recordings require expert analysis, making the process slow and tedious.

This study examines different representations of EEG signals—time-domain and frequency-domain—to determine which is more effective for seizure detection. Two major EEG databases were used:

• Freiburg Database (Intracranial EEG). 

• CHB-MIT Database (Scalp EEG).

## Materials and Methods

### Dataset Description

Two publicly available datasets were analyzed:

Freiburg Database: Contains intracranial EEG (iEEG) data from 21 epilepsy patients. Electrodes were placed inside the brain, resulting in high-quality signals with minimal noise.

CHB-MIT Database: Contains scalp EEG (sEEG) recordings from 23 children with epilepsy. Electrodes were placed on the scalp, making it a non-invasive method but with higher noise interference.

In this project , I am using Preprocessed CHB-MIT Scalp EEG Database.

Both datasets were used to classify EEG signals into three states:

Ictal – During a seizure.

Preictal – Just before a seizure.

Interictal – Between seizures.

### Time and Frequency Domain Signals

Time-domain signals represent EEG activity over time.

Frequency-domain signals show how signal components are distributed in different frequency bands, obtained using Fast Fourier Transform (FFT).Frequency-domain signals often highlight patterns that are difficult to detect in time-domain signals.

### Performance Evaluation

The study used three evaluation metrics:

• Accuracy (ACC): Measures overall correctness.

• Sensitivity (SEN): Measures how well seizures are detected.

• Specificity (SPE): Measures how well non-seizure states are identified.

##### I am using the "Preprocessed CHB-MIT Scalp EEG dataset" because it provides a structured and balanced set of preictal and ictal EEG data, making it ideal for machine learning and deep learning models in epileptic seizure detection. With 23 retained EEG channels and an Outcome column for classification, it simplifies data handling while maintaining crucial seizure patterns. 

The Preprocessed CHB-MIT Scalp EEG dataset link : [Preprocessed CHB-MIT Scalp EEG dataset](https://ieee-dataport.org/open-access/preprocessed-chb-mit-scalp-eeg-database)

## PHASE-2

## Power Spectral Density (PSD) in EEG Analysis

Power Spectral Density (PSD) represents the distribution of power across different frequency components in a signal. It provides insight into how the power of an EEG signal is distributed over frequency, making it a crucial tool for analyzing brain activity.

Why PSD is Used in EEG?

• Feature Extraction – Helps identify dominant frequency bands (Delta, Theta, Alpha, Beta, Gamma) related to cognitive states.

• Seizure Detection – Highlights spectral patterns distinguishing normal and abnormal brain activity.

• Signal Characterization – Provides a compact and informative representation of EEG signals.

EEG Frequency Bands and Their Significance:

•Delta (0.5–4 Hz) – Deep sleep, unconscious states.

•Theta (4–8 Hz) – Drowsiness, relaxation. 

•Alpha (8–12 Hz) – Calm, resting state.

•Beta (12–30 Hz) – Active thinking, problem-solving.

•Gamma (30–100 Hz) – Cognitive processing, memory functions.

We will be using "Welch’s Method" which is a technique used in EEG analysis to estimate the Power Spectral Density (PSD) more accurately. Instead of analyzing the entire EEG signal at once (which can be noisy), Welch’s Method breaks the signal into smaller overlapping segments. For each segment, it calculates a power estimate, then averages all these estimates together. This reduces noise and gives a smoother and more reliable PSD result.

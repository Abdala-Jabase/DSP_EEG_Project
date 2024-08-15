# Digital Signal Processing EEG Project

## Overview

This repository contains the code and documentation for a project conducted as part of the CSCE 363/3611 – Digital Signal Processing course. The project focuses on classifying Steady-State Visual Evoked Potentials (SSVEPs) using EEG data to advance Brain-Computer Interface (BCI) technology. It involves preprocessing EEG signals with Common Average Reference (CAR) filtering, analyzing frequency-domain features, and applying K-Nearest Neighbors (KNN) classification to predict stimuli responses accurately. The work contributes to enhancing non-invasive neural interfaces for Human-Computer Interaction (HCI).


## Data Preprocessing

The project begins with preprocessing EEG data and stimulus information from two subjects. The main steps include:

1. **Data Import**: 
   - The data is loaded using libraries such as `pandas`, `numpy`, and `matplotlib.pyplot`, along with modules from `scipy` and `sklearn`.
   - EEG and stimulus data for two subjects are imported from CSV files into `pandas` DataFrames.

2. **Identifying Stimulus Ranges**: 
   - The code identifies time ranges during which the stimulus is active for both subjects by iterating through the stimulus data and marking the start and end points of each stimulus period.

3. **Average Reference Calculation**: 
   - The average reference of the EEG data is computed across all electrodes to be used for Common Average Referencing (CAR).

4. **Applying CAR**: 
   - The CAR is applied to the EEG data by subtracting the average reference from each electrode's signal for both subjects.

5. **FFT Computation**: 
   - A function `compute_fft` is defined to compute the Fast Fourier Transform (FFT) of an electrode signal, returning the frequency and amplitude components.

6. **Extracting Electrode Data**: 
   - Specific electrode data (O1 and O2) are extracted before and after CAR for both subjects, and the average of these signals is computed.

7. **Frequency and Amplitude Analysis**: 
   - FFT is performed on the extracted electrode data for the identified stimulus ranges, both before and after CAR, and the frequency and amplitude information is stored.

8. **Visualization**: 
   - Plots are generated to visualize the frequency and amplitude of the EEG signals before and after CAR for each trial and electrode, with results displayed in a set of subplots for comparison.

## Method 1: Signal Processing and Analysis

### Approach

1. **Cleaning Data**:
   - The stimulus CSV was used to determine the indices of the 125 trials in each subject's CSV.
   - CAR was applied to each subject by calculating the average of each electrode and subtracting it from all electrodes for each trial.
   - The combined O1 & O2 signals were computed, and FFT was applied to each trial for both subjects.

2. **Methodology**:
   - The spectrums for each trial were analyzed by identifying frequency bins close to the ideal frequencies (6.66, 7.5, 8.57, 10, and 12 Hz).
   - The stimulus with the largest average in the identified frequency bins was chosen as the guess for the trial.

### Outputs

- **Subject 1**:
  - Electrode O1: 56.80% accuracy
  - Electrode O2: 71.20% accuracy
  - Combined O1 & O2: 64.00% accuracy
- **Subject 2**:
  - Electrode O1: 52.80% accuracy
  - Electrode O2: 77.60% accuracy
  - Combined O1 & O2: 70.40% accuracy

## Method 2: K-Nearest Neighbors Classification

### Approach

1. **Feature Extraction**:
   - Frequency amplitude data for each electrode (O1 and O2) was sliced from index 20 to 120.
   - Features were averaged across electrodes to create combined feature sets.

2. **Data Preparation**:
   - Features were prepared by averaging the data from both electrodes (O1 and O2) and by concatenating data from all electrodes.

3. **Classification Using K-Nearest Neighbors (KNN)**:
   - The KNN classifier was trained and evaluated using Leave-One-Out (LOO) cross-validation.
   - The classifier was trained with a range of K values from 1 to 30, and the best K for each scenario was identified.

### Outputs

- **Subject 1**:
  - Electrode O1: Best K = 4 with 56.8% accuracy
  - Electrode O2: Best K = 7 with 90.4% accuracy
  - Combined O1 & O2: Best K = 8 with 84.0% accuracy
  - All electrodes: Best K = 29 with 79.2% accuracy

- **Subject 2**:
  - Electrode O1: Best K = 21 with 46.4% accuracy
  - Electrode O2: Best K = 7 with 92.8% accuracy
  - Combined O1 & O2: Best K = 1 with 88.0% accuracy
  - All electrodes: Best K = 25 with 68.8% accuracy


## Project Members

- **Abdala Jabase**
- **Mohanad Abouserie**
- **Kareem Sayed**
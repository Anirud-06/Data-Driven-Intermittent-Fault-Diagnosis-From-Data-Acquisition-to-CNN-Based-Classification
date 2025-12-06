Data-Driven Intermittent Fault Diagnosis in Synchronous Generators
This repository contains the implementation of a deep learning framework designed to detect intermittent inter-turn short circuits in synchronous generators. By utilizing a custom Fault Injection Unit (FIU) and 1D Convolutional Neural Networks (1D-CNN), this system identifies transient fault precursors before they lead to permanent machine failure.

Project Background
Condition monitoring is essential for maintaining the reliability of electrical machinery, particularly synchronous generators used in power production and maritime applications. A significant issue in these machines is stator inter-turn defects, which often begin as "intermittent faults"—short circuits lasting only a fraction of a second (0.1s to 0.5s).
Existing protection systems often fail to register these brief anomalies. However, if left undetected, these intermittent faults cause efficiency decline and eventually lead to catastrophic breakdown. This project focuses on capturing these early-stage events using high-frequency data acquisition and advanced signal processing.

Technical Approach
We approach the detection process as a time-series classification problem. The pipeline consists of three main stages:
Data Acquisition: We utilize a custom 5 kVA synchronous generator connected to a National Instruments PXI system. A programmed Fault Injection Unit (NI 2514) introduces controlled short circuits at specific time intervals.
Signal Processing:
FFT Analysis: Used to analyze harmonic ripple content at the third harmonic (150 Hz).
Wavelet Denoising: We apply Discrete Wavelet Transform (using db4, sym4, and BIOR2.2 wavelets) to isolate fault signatures in short-duration signals.
Deep Learning Model: The processed signals are fed into a 1D Convolutional Neural Network (1D-CNN). The network comprises multiple convolutional layers with decreasing filter sizes to capture hierarchical transient spikes.
Performance Results
We evaluated the model on intermittent faults with durations of 0.5s, 0.2s, and 0.1s. While standard frequency domain analysis (FFT) struggled with shorter faults, wavelet-based preprocessing significantly improved detection rates.

Prerequisites
Python 3.8+

TensorFlow 2.x (for 1D-CNN implementation)

NumPy, SciPy

PyWavelets (for wavelet denoising)

NI-DAQmx (if interfacing with hardware)

The repository contains a sample of Faulty, Healthy and Intermittent fault data used.

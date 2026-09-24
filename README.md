# xai-wave

Minimal experiment for studying waveform reconstruction as a measurement variable in perturbation-based Audio XAI.

## Experimental pipeline

The classifier operates on log-mel spectrograms:

waveform -> STFT -> power spectrogram -> mel filterbank -> log compression -> CNN

LIME defines perturbations directly in the log-mel representation used by the classifier.

Perturbed log-mel features are then mapped back to an STFT magnitude through:

log-mel -> inverse log -> mel inversion -> target STFT magnitude

The same target magnitude is reconstructed using three conditions:

- **OP**: original phase + one iSTFT
- **GL_ORIG64**: Griffin-Lim, 64 iterations, initialized with the original phase
- **GL_RAND64**: Griffin-Lim, 64 iterations, initialized with random phase

The reconstructed waveform is passed again through the complete log-mel frontend and the frozen CNN.

## Main measurements

The experiment measures:

- perturbation response of the classifier;
- log-mel realization error;
- STFT magnitude realization error;
- waveform differences between reconstruction operators;
- paired AUC differences across perturbation budgets.

## Notebooks

1. CNN training and LIME explanation in log-mel space
2. Log-mel perturbation, feature inversion, and waveform reconstruction
3. Paired statistical analysis

## Scope

This repository contains a minimal methodological experiment. It is intended to isolate reconstruction effects before extending the analysis to larger bioacoustic datasets and models.

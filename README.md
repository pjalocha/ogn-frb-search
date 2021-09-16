# Search for Fast Radio Bursts (FRBs) with the Open Glider Network (OGN).

## Introduction
The concept is inspired by the paper published on arXiv.org https://arxiv.org/abs/1701.01475 - reading it is already a very good introduction to the subject and the detection/measurement basics.

The Open Glider Network (OGN0 is a network of ground receivers tuned to (Europe and Africa) the 868MHz ISM band.
This network should be sensitive enough to detect Fast Radio Bursts coming from our Galaxy.

This project attempts to perform such a search; at this moment data from about 20 OGN ground receivers is being collected and stored for futher analysis.

## How to join
If you already have an OGN receiver, install the software provided here and enable the FRB in the config file, otherwise install an OGN receiver first.

## FRB reception

### OGN receiver characteristics

| Characteristics | Value/description |
|-----|-----|
| Frequency | 868.8MHz |
| Bandwidth | 2MHz, some 1MHz |
| Duty cycle | 85% possibly 100% |
| Antenna type | vertical collinear |
| Antenna gain | 5-8dBi |
| Beam, horizontal | omni-directional |
| Beam, vertical | 10-15 degrees towards the horizon |
| Receiver | RTLSDR, possibly with LNA and/or filter |
| Noise Figure | 1dB (with LNA) 4dB (without LNA) |
| Timing accuracy | some miliseconds, to be possibly improved |
| Demodulators | GFSK and LoRa, filtered envelope for the FRB |

### Data processing for the FRB signal

An OGN receiver normally detects and demodulates GFSK and LoRa signals of bandwidths 100-250kHz.
For the purpose of FRB one needs to introduce a dedicated processing element which is sensitive to wideband pulses while being insensitive to the narrowband signals.

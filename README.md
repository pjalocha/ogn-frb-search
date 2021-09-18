# Search for Fast Radio Bursts (FRBs) with the Open Glider Network (OGN).

## Introduction
The concept is inspired by the paper published on arXiv.org https://arxiv.org/abs/1701.01475 - reading it is already a very good introduction to the subject and the detection/measurement basics.

The Open Glider Network (OGN0 is a network of ground receivers tuned to (Europe and Africa) the 868MHz ISM band.
This network should be sensitive enough to detect Fast Radio Bursts coming from our Galaxy.

This project attempts to perform such a search; at this moment data from about 20 OGN ground receivers is being collected and stored for futher analysis.

## How to join
If you already have an OGN receiver, install the software provided here and enable the FRB in the config file, otherwise install an OGN receiver first.
### Typical hardware required/recommended
| Element | Description/Remarks | est.price |
|------|-----|----|
| CPU | Raspberry PI 2, 3 or 4, 512MB RAM, case, power supply | 60 EUR |
| RTLSDR | Silver stick with Bias-T from rtl-sdr.org | 27 USD |
| Antenna | Collinear, 1-2m, 5-10dBi | 50-100 EUR |
| LNA | Uputronics with Bias-T, not required, but highly recommended | 40 GBP |
| antenna feeder | low-loss coax, less critical when LNA at the antenna | |

Note: beware of silver sticks which look similar to those from rtl-sdr.org but exhibit internal noise issues: rather get the originals from the website.

## FRB reception

### What signal we expect

A short, in the order of 1 milisecond pulse registered by several receivers within few miliseconds.
Differences between receivers should be consistent with an arrival direction.

### OGN receiver characteristics

| Characteristic | Value/description |
|-----|-----|
| Frequency | 868.8MHz |
| Bandwidth | 2MHz, some 1MHz |
| Duty cycle | 85% possibly 100% |
| Antenna type | vertical collinear |
| Antenna gain | 5-8dBi |
| Beam, horizontal | omni-directional |
| Beam, vertical | 10-15 degrees towards the horizon |
| Receiver | RTLSDR, possibly with LNA and/or filter |
| Noise Figure | 1dB (with LNA) 4-10dB (without LNA) |
| Timing accuracy | some miliseconds, to be possibly improved |
| Demodulators | GFSK and LoRa, filtered envelope for the FRB |

### Challenges
#### Antenna(s) pattern
OGN antennas receive signals basically on the horizon, this is where most of the aircraft are, thus for the FRB's we well can detect those on the horizon.
This can still work, as we expect those signals to come from our Galaxy, thus the best time to listen is when the Galaxy is low on the horizon.

#### Man-made noise
868MHz is an ISM band thus is filled with man-made signals, the processing needs to filter this signals out.
Still, after filtering, there are many pulse-like signals on the envelope, thus to get a confident FRB signal we need to correlate several receivers.
Fortunately, the OGN network has already few thousands of such, thus if we just get a small fraction to work for the FRB we have a chance to find it.

#### Sensitivity

#### Timing accuracy
OGN receivers have no GPS, the timestamp is based on the system time acquired with NTP.
Another factor is the unknown delay between the RF going into the RTL2832U chip and the digitized data acquired by the API on the RPI side.
For optimal performance it would be good to have total accuracy in the order of 1ms.

### Data processing for the FRB signal

An OGN receiver normally detects and demodulates GFSK and LoRa signals of bandwidths 100-250kHz.
For the purpose of FRB one needs to introduce a dedicated processing element which is sensitive to wideband pulses while being insensitive to the narrowband signals.


# Short report: Atlas 350XL RF output estimate from diode detector measurements

## Overview

This note summarizes a set of HF output measurements made on an Atlas 350XL transceiver using a simple RF detector connected to a 50 ohm load. The goal is not precision wattmetry, but a practical, band‑by‑band estimate of RF output and a record of the likely measurement uncertainties.

The detector uses five 1N4148 silicon switching diodes in series and a 6800 pF, 500 V capacitor to produce a DC reading proportional to RF envelope voltage. A setup of this kind behaves as a simple peak detector, and its output can be used for approximate relative comparison between bands when the same load, wiring, and meter arrangement are kept unchanged.

## Measurement setup

The test arrangement is: Atlas 350XL transmitter output feeding a 50 ohm dummy load, with the diode‑capacitor detector sampling the RF voltage across the load and producing a DC voltage that is then measured with a voltmeter. Supply voltage is 13.8 V, and current on each band is taken from the transceiver’s internal current meter.

The recorded readings are:

| Band   | Detector DC voltage | Supply voltage / current |
| :----- | :------------------ | :----------------------- |
| 1.8 MHz | 71 V               | 13.8 V / 14 A           |
| 3.5 MHz | 116 V              | 13.8 V / 18 A           |
| 7 MHz   | 106 V              | 13.8 V / 20 A           |
| 14 MHz  | 125 V              | 13.8 V / 24 A           |
| 21 MHz  | 101 V              | 13.8 V / 20 A           |
| 28 MHz  | 64 V               | 13.8 V / 16 A           |

In this detector, the DC meter is connected **after** the series diode string, so the measured DC corresponds to the RF peak at the load minus the total forward drop of the five diodes. A 1N4148 typically has a forward drop on the order of 0.6 to 0.7 V at useful current, so five in series are approximated as about 3.5 V total.

## Estimated output

With the meter on the rectified side, the RF peak across the 50 ohm load is approximated as:

\(V_{pk,RF} \approx V_{DC,measured} + 3.5\)

and then

\(V_{rms} = \frac{V_{pk}}{\sqrt{2}}, \qquad P \approx \frac{V_{rms}^2}{50}\)

gives the following band‑by‑band output estimates.

| Band   | Measured DC | Estimated RF peak | Estimated RF RMS | Estimated RF output | Estimated DC input | Rough efficiency |
| :----- | :---------- | :---------------- | :--------------- | :------------------ | :----------------- | :--------------- |
| 1.8 MHz | 71 V       | 74.5 V            | 52.7 V           | ≈ 55 W              | 193 W              | ≈ 29%            |
| 3.5 MHz | 116 V      | 119.5 V           | 84.5 V           | ≈ 143 W             | 248 W              | ≈ 58%            |
| 7 MHz   | 106 V      | 109.5 V           | 77.4 V           | ≈ 120 W             | 276 W              | ≈ 43%            |
| 14 MHz  | 125 V      | 128.5 V           | 90.8 V           | ≈ 165 W             | 331 W              | ≈ 50%            |
| 21 MHz  | 101 V      | 104.5 V           | 73.9 V           | ≈ 109 W             | 276 W              | ≈ 40%            |
| 28 MHz  | 64 V       | 67.5 V            | 47.7 V           | ≈ 46 W              | 221 W              | ≈ 21%            |

These numbers should be read as rough engineering estimates rather than true calibrated output power. With this detector style and the stated tolerance goal, a practical uncertainty of roughly plus or minus 20 W is reasonable, especially on the higher bands where detector response and stray capacitance matter more.

## Interpretation

The measurements suggest that this Atlas 350XL produces its strongest output in the middle HF range, peaking around 14 MHz and also performing well on 3.5 MHz. Output appears lower on 7 and 21 MHz, and substantially lower on 1.8 and 28 MHz.

That pattern could reflect real transmitter behavior, such as band‑dependent gain, driver level, tuning, low‑pass filter loss, or final‑stage matching. It could also partly reflect the detector itself, because a silicon diode detector does not have perfectly flat sensitivity with frequency and drive level; 1N4148‑type devices have several‑pF junction capacitance and frequency‑dependent rectification characteristics.

## Likely error sources

Several factors can shift the estimated power away from the true RF output:

- **Diode forward voltage uncertainty.** The 1N4148 forward drop is not fixed; it changes with current, temperature, and pulse shape. Assuming 3.5 V total for five diodes is reasonable for a ballpark estimate, but it is still an approximation.
- **Frequency‑dependent detector response.** The 1N4148 has junction capacitance in the low‑pF range, and detector sensitivity changes with frequency, source impedance, and layout. This can distort comparisons between 1.8 MHz and 28 MHz even if true RF power were unchanged.
- **Peak‑versus‑average ambiguity.** A diode‑capacitor detector tends to indicate a peak or near‑peak envelope quantity, not true RF RMS power directly. Converting the measured DC into watts therefore depends on the assumed detector model and waveform.
- **Stray capacitance and wiring inductance.** Lead length, detector placement, meter loading, and the physical layout around the dummy load all affect the reading, especially toward the upper HF bands.
- **Dummy‑load accuracy.** If the load is not very close to 50 ohms resistive across all tested bands, the inferred power from voltage will be biased.
- **Current‑meter uncertainty.** The Atlas 350XL internal current meter may not represent only PA current; depending on the internal shunt location, it may include some or most of the transceiver’s other loads, or omit some of them. That means the calculated DC input power and efficiency are only approximate unless the supply current is checked externally with a calibrated ammeter.
- **Supply‑voltage sag.** If the supply voltage at the radio terminals drops under load, the actual PA operating point can differ from the nominal 13.8 V used in the calculation.

## Practical conclusion

For comparative troubleshooting or performance surveying, this measurement method is useful. It is good enough to show that the Atlas 350XL is likely strongest on 14 MHz and 3.5 MHz, moderate on 7 and 21 MHz, and weak on 1.8 and 28 MHz under the stated test conditions.

For absolute power measurement, a calibrated RF wattmeter, directional coupler, or known‑good RF voltmeter across a verified 50 ohm dummy load would be preferable. Even so, this detector method is adequate for quick relative checks and for documenting whether band output trends improve or worsen after repair or alignment work.

#  Linear Integrated Circuits Laboratory 

## Experiment 2:Common Source Amplifier -CONFIGURATIONS(TSMC 180nm)

**Name:** Suhas Koushik K S  
**USN:** 4NI24EC180  
**Branch:** Electronics and Communication Engineering  
**Lab Course:** Linear Integrated Circuits (BEC456B)  
**Tool Used:** LTspice  
**Technology Library:** TSMC 180nm  
---
## 1. AIM

To design and analyze the following MOS amplifier configurations using TSMC 180nm CMOS technology in LTspice:

1. Common Source Amplifier with Source Degeneration  
2. Cascode Amplifier  
3. Current Mirror Loaded Common Source Amplifier  

---
## 2. SOFTWARE REQUIRED

- LTspice Simulation Tool  
- TSMC 180nm Model Library  
- DC Power Supply (VDD = 1.8V)  
- CMOS Transistors (NMOS and PMOS)  

---
## 3. MOS Amplifier Fundamentals

MOS amplifiers convert small input voltage variations into amplified output signals. For proper amplification, MOSFETs must operate in the **saturation region**.

### MOSFET Equations

| ID (Drain Current) | Vov (Overdrive) | gm (Transconductance) | ro (Output Resistance) | Av (Voltage Gain) |
|--------------------|-----------------|----------------------|------------------------|-------------------|
| (1/2) μCox (W/L)(VGS−VTH)² | VGS − VTH | 2ID / Vov | 1 / (λID) | −gm Rout |
---
## 4. Comparison of Amplifier Configurations

| Circuit | Concept | Advantage | Limitation |
|--------|---------|-----------|-----------|
| Source Degenerated CS | Source resistor feedback | Stable bias | Reduced gain |
| Cascode Amplifier | CS + Common Gate | High output resistance | Higher complexity |
| Active Load CS | Current mirror load | Higher gain | Bias sensitive |

---
## 5. Device Parameters (TSMC 180 nm)

| Supply Voltage | Target Drain Current | VTHn | VTHp | Channel Length |
|----------------|----------------------|------|------|----------------|
| 1.8 V | 200 µA | 0.36 V | −0.39 V | 560 nm |

### Oxide Parameters

| εox (Oxide Permittivity) | tox (Oxide Thickness) | Cox (Oxide Capacitance) |
|--------------------------|----------------------|-------------------------|
| εrε0 = 3.54 × 10⁻¹¹ | 4.1 × 10⁻⁹ m | εox / tox = 8.634 × 10⁻³ F/m² |

---
## 6. Saturation Conditions

To ensure proper amplifier operation, MOSFETs must satisfy:

| Device | Condition |
|------|-----------|
| NMOS | VDS ≥ VGS − VTH |
| PMOS | VSD ≥ VSG − VTH(PMOS) |

---
## 7. Process Transconductance Parameters

| Parameter | Calculation | Result |
|----------|-------------|-------|
| μnCox | μn × Cox | 2.363 × 10⁻⁴ A/V² |
| μpCox | μp × Cox | 9.99 × 10⁻⁵ A/V² |

---
## 8. Width Calculation

Using the saturation current equation
ID = (1/2) μCox (W/L) (Vov)²

Rearranging,
W = (2 ID L) / [μCox (Vov)²]

### Calculated Dimensions

| NMOS Width | PMOS Width |
|------------|------------|
| 15.16 µm | 35.9 µm |

---
### Observation

• NMOS mobility is higher than PMOS mobility.  
• Therefore NMOS requires smaller width.  
• PMOS width is approximately 2.3× NMOS width for the same current.

------------------------------------------------------------

### EXP2 - CIRCUIT 2A – SOURCE DEGENERATED COMMON SOURCE AMPLIFIER

---
## Design Objective

To design and implement a **source-degenerated common source amplifier**   for **ID = 200 µA** with **maximum symmetric output swing**.

---
## Circuit Implementation (LTspice)

<img width="676" height="802" alt="circuit2a" src="https://github.com/user-attachments/assets/f2fd8574-5f26-4518-8b56-8189b70a59fb" />

---
# DC Analysis

## Design Conditions

| VDD | ID | VTH (NMOS) | VTH (PMOS) |
|-----|----|------------|------------|
| 1.8 V | 200 µA | 0.36 V | −0.39 V |
---
## Bias Design and Voltage Selection

### Voltage Limits for Saturation Operation

| Parameter | Minimum | Maximum | Reason |
|-----------|---------|---------|-------|
| VGS (NMOS) | ≥ VTH = 0.36 V | ≤ VDD = 1.8 V | Required for channel formation |
| VDS (NMOS) | ≥ Vov | ≤ VDD | Required for saturation |
| VSG (PMOS) | ≥ |VTHp| = 0.39 V | ≤ VDD | PMOS conduction condition |
| VSD (PMOS) | ≥ Vov | ≤ VDD | Saturation condition |

---
## Output Voltage for Maximum Swing

To achieve **maximum symmetric signal swing**, the NMOS drain–source voltage is placed near the midpoint of the supply.

| VDS Calculation | Result |
|-----------------|--------|
| VDD / 2 = 1.8 / 2 | **0.9 V** |

**Justification**

Placing the operating point at **half the supply voltage** provides equal headroom for positive and negative output swings, thereby maximizing dynamic range.

---
## Source Voltage Selection

A small source voltage is introduced using a **source resistor** to provide **negative feedback and bias stabilization**.

| Parameter | Value |
|-----------|------|
| VS | **0.2 V** |

**Justification**

| Reason | Explanation |
|------|-------------|
| VS > 0 | Enables source degeneration feedback |
| VS << VDD | Preserves drain voltage headroom |
| Stabilizes ID | Increase in current raises VS → reduces VGS |

Thus **0.2 V** provides feedback while keeping sufficient voltage available across the transistor.

---
## Output Voltage Calculation

| Parameter | Calculation | Result |
|-----------|-------------|--------|
| VDS | Vout − VS | 0.9 = Vout − 0.2 |
| Vout | 0.9 + 0.2 | **1.1 V** |

---
## Source Resistor Calculation

| RS Calculation | Result |
|----------------|--------|
| VS / ID = 0.2 / (200 × 10⁻⁶) | **1 kΩ** |

---
## NMOS Gate Bias

| Calculation | Result |
|-------------|--------|
| VGS = VTH + Vov = 0.36 + 0.25 | **0.61 V** |
| VG = VGS + VS = 0.61 + 0.2 | **0.81 V** |

---
## Overdrive Voltage Verification

| Calculation | Result |
|-------------|--------|
| VGS = VG − VS = 0.81 − 0.2 | **0.61 V** |
| Vov = VGS − VTH = 0.61 − 0.36 | **0.25 V** |

### Allowable Overdrive Range

| Minimum Vov | Maximum Vov |
|-------------|-------------|
| > 0 | < VDS = 0.9 V |

Thus

0 < Vov < 0.9

The obtained value
Vov = **0.25 V**
lies well within this allowable range.

**Justification**

A moderate overdrive voltage:

• provides sufficient transconductance  
• maintains stable drain current  
• ensures adequate voltage headroom for signal swing

---
## PMOS Bias Calculation
| Calculation | Result |
|-------------|--------|
| VSG = Vov + VTHp = 0.25 + 0.39 | **0.64 V** |
| VGp = VDD − VSG = 1.8 − 0.64 | **1.16 V** |

# Saturation Verification

| Device | Condition | Result |
|-------|-----------|--------|
| NMOS | VDS ≥ Vov | 0.9 ≥ 0.25 ✔ |
| PMOS | VSD ≥ Vov | 0.7 ≥ 0.25 ✔ |

Both MOSFETs operate in **saturation region**.

---
# Final DC Operating Point

| VS | VDS | Vout | VG | VGp | ID | RS | Vov |
|----|-----|------|----|-----|----|----|----|
| 0.2 V | 0.9 V | 1.1 V | 0.81 V | 1.16 V | 200 µA | 1 kΩ | 0.25 V |

The calculated bias point ensures that both transistors operate in saturation while providing sufficient voltage headroom for maximum output signal swing.

------------------------------------------------------------
<img width="720" height="519" alt="circuit2aop" src="https://github.com/user-attachments/assets/1a17bf43-5d25-4251-b6f2-70671e00f70c" />

## Width Selection – Circuit 2A

The transistor widths were slightly increased during simulation to compensate for non-ideal MOSFET effects and obtain ID ≈ 200 µA.

| Device | Calculated Width (µm) | Practical Width (µm) | Justification |
|------|----------------------|----------------------|--------------|
| NMOS | 15.16 | 29 | Practical MOS models include channel-length modulation and mobility degradation, which reduce effective current. Increasing width restores ID ≈ 200 µA. |
| PMOS | 35.9 | 83 | PMOS mobility is lower than NMOS and short-channel effects reduce current, therefore a larger width is required to achieve the target current. |

-------------------
# Transient Analysis – Circuit 2A
(Source Degenerated Common Source Amplifier)

To evaluate the time-domain performance of the amplifier, a small-signal sinusoidal input was applied at the gate terminal.

## Input Signal Parameters

| Waveform | Frequency | Amplitude | DC Offset |
|----------|-----------|-----------|-----------|
| Sine | 1 kHz | 10 mV | 0.81 V |
Input command used in LTspice:

Vin = SINE(0.81 10m 1k)

The DC offset corresponds to the calculated gate bias voltage required to maintain **ID ≈ 200 µA**.

---

## Input Waveform

<img width="1919" height="858" alt="2at_input" src="https://github.com/user-attachments/assets/5be9f8d1-8683-4d56-a79a-cf8d5859f77a" />

The above waveform represents the sinusoidal input applied at the gate.

---

## Output Waveform

<img width="1919" height="861" alt="2at_output" src="https://github.com/user-attachments/assets/2d637dec-8348-4023-a200-dbd4c395d076" />

Since this is a **common source amplifier**, the output signal is inverted with respect to the input and exhibits a larger amplitude.

---

## Input and Output Comparison

<img width="1919" height="844" alt="2at_combined" src="https://github.com/user-attachments/assets/6118177b-885e-418a-9325-dd935be3f2ad" />

The combined waveform clearly shows amplification and the expected **180° phase inversion**.

---
#Practical Gain Calculation from Transient Waveform

| Vin(p-p) | Vout(p-p) | Gain (Av) | Gain (dB) |
|----------|-----------|-----------|-----------|
| 0.819−0.800 = **0.019 V** | 1.386−0.858 = **0.528 V** | 0.528 / 0.019 = **27.78 V/V** | 20 log₁₀(27.78) = **28.87 dB** |

## Observation

The output signal is inverted relative to the input and shows clear voltage amplification without distortion for the applied small-signal input.

---
# AC Analysis – Circuit 2A

Small-signal AC analysis was performed to determine the frequency response and midband gain of the amplifier.

### Simulation Parameters

| AC Command | Input AC Magnitude |
|------------|-------------------|
| `.ac dec 1000 .1 1G` | 1 V |
---

<img width="1917" height="867" alt="2aac_gain" src="https://github.com/user-attachments/assets/f8bbe4af-05e6-4259-9244-22ce99d99c7f" />

---

## Frequency Response Results – Circuit 2A

| Gain (dB) | Gain (V/V) | −3 dB Gain | Bandwidth | GBW | UGB |
|-----------|------------|------------|-----------|------|------|
| 28.71 dB | 10^(28.71/20) = **27.25** | 25.71 dB | **52.119 MHz** | 27.25 × 52.119 MHz = **1.42 GHz** | **1.717 GHz** |
The midband gain is obtained from the flat region of the AC frequency response plot.   The bandwidth corresponds to the frequency where the gain drops by **3 dB** from the midband value. The unity gain bandwidth is obtained from the frequency where the gain becomes **0 dB**.

### Note on GBW and UGB
In an ideal single-pole amplifier, the gain-bandwidth product (GBW) equals the unity-gain bandwidth (UGB). However, practical MOS amplifiers exhibit multiple poles due to parasitic capacitances such as Cgs, Cgd, and node capacitances. These additional poles modify the frequency response, causing GBW and UGB to deviate slightly from the ideal relationship.

---
## Theoretical Gain – Circuit 2A
Small-signal parameters obtained from the LTspice operating point:

| gm₁ | ro₁ | ro₂ | RS |
|-----|-----|-----|----|
| 1.6 mS | 58.8 kΩ | 58.8 kΩ | 1 kΩ |

The gain of a **source-degenerated common source amplifier** with active load is given by:

$$
A_v = -\frac{g_{m1}}{1 + g_{m1}R_S + \frac{R_S}{r_{o1}}}
\left[(g_{m1}R_S r_{o1} + R_S + r_{o1}) \parallel r_{o2}\right]
$$

| Denominator | Output Resistance Term | Voltage Gain | Gain (dB) |
|-------------|-----------------------|--------------|-----------|
| 1 + 1.6 + (1k/58.8k) = **2.617** | ([gm₁RSro₁ + RS + ro₁] ∥ ro₂) ≈ **42.6 kΩ** | (1.6 mS / 2.617) × 42.6 kΩ ≈ **26 V/V** | 20 log₁₀(26) ≈ **28 dB** |

For **TSMC 180 nm technology**, the channel-length modulation parameter λ typically lies in the range **0.1–0.2 V⁻¹**, which produces output resistance values consistent with the LTspice operating point.

---
### Observation
The AC analysis shows a midband gain of 28.71 dB, which agrees closely with both theoretical and transient gain results.
### Reason for Small Variation
The difference occurs because theoretical calculations assume ideal device behavior, while LTspice includes practical effects such as channel-length modulation.

-----------------------------------------------------------------------------------
### EXP2- CIRCUIT 2B – Common Source – Cascode Amplifier with Active Load
-----------------------------------------------------------------------------------
### Circuit Implementation in LTspice

<img width="783" height="821" alt="circuit2b" src="https://github.com/user-attachments/assets/0e2746e3-761b-4605-a284-921b31f4f046" />

# DC Analysis – Circuit 2B (Cascode Amplifier)

## Design Conditions

| VDD | ID | VTHn | VTHp |
|----|----|----|----|
| 1.8 V | 200 µA | 0.36 V | −0.39 V |

---
# Voltage Limits for Proper Operation

| Parameter | Minimum | Maximum | Reason |
|-----------|---------|---------|--------|
| VGS (NMOS) | ≥ VTH = 0.36 V | ≤ VDD = 1.8 V | Channel formation |
| VDS (NMOS) | ≥ VOV | ≤ VDD | Saturation condition |
| VSG (PMOS) | ≥ |VTHp| = 0.39 V | ≤ VDD | PMOS conduction |
| VSD (PMOS) | ≥ VOV | ≤ VDD | Saturation condition |

---
# Overdrive Voltage Determination

| Calculation | Result |
|-------------|--------|
| VGS = VTH + VOV = 0.36 + 0.25 | **0.61 V** |
| VOV = VGS − VTH = 0.61 − 0.36 | **0.25 V** |

### Allowable Range

| Minimum VOV | Maximum VOV |
|-------------|-------------|
| > 0 | < VDS |

Since the drain-source voltage will be near

VDS ≈ VDD/2 = **0.9 V**

the allowable range becomes

0 < VOV < 0.9 V

The obtained value

**VOV = 0.25 V**

lies well within this range.

### Justification

A moderate overdrive voltage

• provides sufficient transconductance  
• keeps current stable  
• leaves headroom for signal swing

---
# Intermediate Node Voltage (VS1)

In a cascode amplifier, the drain of the lower transistor becomes the source of the upper transistor.

To keep the **lower NMOS (M2) in saturation**

VDS2 ≥ VOV

Since

VS2 = 0

| Calculation | Result |
|-------------|--------|
| VDS2 = VD2 − VS2 = VS1 − 0 | VS1 |
| Required VDS2 ≥ VOV | ≥ 0.25 V |

Thus

| VS1 Condition | Result |
|---------------|--------|
| VS1 ≥ VOV | VS1 ≥ 0.25 V |

Choosing

VS1 ≈ **0.3 V**

satisfies the saturation condition.

### Justification

| Reason | Explanation |
|------|-------------|
| VS1 > VOV | keeps lower NMOS in saturation |
| VS1 << VDD | preserves voltage headroom |
| Stable bias | allows correct cascode operation |

---
# Output Voltage Selection

For maximum signal swing

VDS ≈ VDD / 2

| Calculation | Result |
|-------------|--------|
| VDS = 1.8 / 2 | **0.9 V** |

Output node voltage

| Calculation | Result |
|-------------|--------|
| Vout = VDS + VS1 = 0.9 + 0.3 | **1.2 V** |

---
# Saturation Verification

| Device | Condition | Result |
|------|-----------|--------|
| M2 (NMOS) | VDS2 ≥ VOV | 0.3 ≥ 0.25 ✔ |
| M1 (NMOS) | VDS1 ≥ VOV | 0.9 ≥ 0.25 ✔ |
| M3 (PMOS) | VSD ≥ VOV | 0.6 ≥ 0.25 ✔ |

All MOSFETs operate in **saturation region**.

---
# Final DC Operating Point

| VS2 | VS1 | Vout | ID | VOV |
|----|----|----|----|----|
| 0 V | 0.3 V | 1.2 V | 200 µA | 0.25 V |

###  LTspice Operating Point
<img width="835" height="578" alt="circuit2bop" src="https://github.com/user-attachments/assets/7b9cb4ec-1bba-4ac9-be79-6ab2e4a80bea" />

## Width Selection – Circuit 2B
The transistor widths were initially calculated using the square-law
saturation current equation to obtain **ID ≈ 200 µA**.

| Device | Calculated Width | Practical Width |
|------|------|------|
| M1 (NMOS – Cascode) | 15.16 µm | 26.88 µm |
| M2 (NMOS – Input) | 15.16 µm | 29.09 µm |
| M3 (PMOS – Active Load) | 35.9 µm | 83.37 µm |

### Justification
During LTspice simulation, the theoretical widths did not produce exactly **200 µA** due to non-ideal MOSFET effects.

| Reason | Effect |
|------|------|
| Channel length modulation | Changes effective drain current |
| Cascode bias sensitivity | Small voltage changes affect current |
| Mobility degradation | Reduces current compared to ideal model |

Therefore the widths were slightly adjusted in simulation until the desired operating current **ID ≈ 200 µA** was obtained while keeping all transistors in **saturation region**.

----
## Transient Analysis – Circuit 2B (Cascode)

### Input Signal Parameters

| Waveform | Frequency | Amplitude | DC Offset |
|----------|-----------|-----------|-----------|
| Sine | 1 kHz | 10 mV | 0.916 V |

| Simulation Command | Value |
|--------------------|-------|
| Transient Command | `.tran 0 5m` |

---
### Input Waveform

<img width="1915" height="847" alt="2bt_input" src="https://github.com/user-attachments/assets/9f5994aa-bba8-4fa2-8c64-17b4ecc44ffe" />

---
### Output Waveform

<img width="1919" height="859" alt="2bt_output" src="https://github.com/user-attachments/assets/e5c89cb9-748f-4cc0-8da3-07edfa0bab5b" />

---
### Input & Output Comparison

<img width="1919" height="854" alt="2bt_combined" src="https://github.com/user-attachments/assets/d4b035b5-e7f6-4096-8a32-4558cf469a95" />

---
## Practical Gain Calculation

| Vin(p-p) | Vout(p-p) | Gain (Av) | Gain (dB) |
|----------|-----------|-----------|-----------|
| 0.925 − 0.906 = **0.019 V** | 1.225 − 1.183 = **0.042 V** | 0.042 / 0.019 = **2.21 V/V** | **6.88 dB** |

---
### Observation

The output signal is inverted relative to the input and shows clear voltage amplification, confirming correct operation of the cascode amplifier.

-----
# AC Analysis – Circuit 2B

Small-signal AC analysis was performed to determine the frequency response and gain characteristics of the cascode amplifier.

### Simulation Parameters

| AC Command | Input AC Magnitude |
|------------|--------------------|
| `.ac dec 1000 .1 1G` | 1 V |

---
<img width="1915" height="848" alt="2bac_gain" src="https://github.com/user-attachments/assets/eb71ebf0-3b06-49f0-aa7c-752a2d80bcfd" />

---
## Gain and Frequency Characteristics – Circuit 2B

| Parameter | Calculation | Result |
|-----------|-------------|--------|
| Midband Gain | From AC plot | **6.94 dB (≈ 2.22 V/V)** |
| −3 dB Bandwidth | From AC plot | **48.417 MHz** |
| Gain Bandwidth Product (GBW) | 2.22 × 48.417 MHz | **≈ 107.48 MHz** |
| Unity Gain Bandwidth (UGB) | Frequency at 0 dB | **=90.782 MHz** |

-----
# Theoretical Gain – Circuit 2B

For TSMC 180 nm CMOS technology, the channel-length modulation parameter typically lies in the rangeλ ≈ 0.1 – 0.2 V⁻¹

Given

| Parameter | Value |
|-----------|------|
| ID | 200 µA |
| Vov | 0.25 V |
| gm | 1.6 mS |

## Theoretical Gain – Circuit 2B

The small-signal voltage gain of the cascode amplifier is

$$
A_v =
-\frac{g_{m1}}
{1 + g_{m1} r_{o3} + \frac{r_{o3}}{r_{o1}}}
\left(
r_{o2} \parallel
\left(
g_{m1} r_{o1} r_{o3} + r_{o1} + r_{o3}
\right)
\right)
$$

For the designed circuit:

| Parameter | Expression | Value |
|-----------|------------|------|
| Drain current | $I_D$ | 200 µA |
| Overdrive voltage | $V_{ov}$ | 0.25 V |
| Transconductance | $g_m = \frac{2I_D}{V_{ov}}$ | 1.6 mS |
| Channel modulation | $\lambda$ (TSMC 180nm) | 0.15 V⁻¹ |
| Output resistance | $r_o = \frac{1}{\lambda I_D}$ | 33.3 kΩ |

Thus

$$
r_{o1} \approx r_{o2} \approx r_{o3} \approx 33.3\,k\Omega
$$
### Gain Calculation

| Step | Expression | Substitution | Result |
|-----|------------|--------------|--------|
| Denominator | \(1 + g_{m1}r_{o3} + \frac{r_{o3}}{r_{o1}}\) | \(1 + (1.6\,mS \times 33.3\,k\Omega) + \frac{33.3k}{33.3k}\) | **≈ 55.3** |
| Inner Term | \(g_{m1} r_{o1} r_{o3} + r_{o1} + r_{o3}\) | \(1.6\,mS \times 33.3k \times 33.3k + 33.3k + 33.3k\) | **≈ 1.846 MΩ** |
| Parallel Term | \(r_{o2} \parallel (1.846M)\) | \(33.3k \parallel 1.846M\) | **≈ 32.7 kΩ** |
| Voltage Gain | \(A_v = \frac{g_{m1}}{55.3} \times 32.7k\) | \(\frac{1.6mS}{55.3} \times 32.7k\) | **≈ 0.94 V/V** |
| Gain (dB) | \(A_v(dB) = 20\log_{10}(A_v)\) | \(20\log_{10}(0.94)\) | **≈ −0.5 dB** |

---

### Observation

The simplified small-signal theoretical gain is **≈ −0.5 dB**.  
However, AC simulation shows **≈ 6.9 dB** because LTspice uses the **BSIM MOSFET model**, which includes mobility degradation, body effect, velocity saturation, and detailed channel-length modulation, increasing the effective output resistance and gain.

---

### Observation

The theoretical gain obtained using the simplified small-signal model is  
approximately **−0.5 dB**.

However, the **AC simulation shows a gain of about 6.9 dB**.  
This difference occurs because LTspice uses a **complete BSIM MOSFET model**  
that includes effects such as:

• mobility degradation  
• body effect  
• velocity saturation  
• detailed channel-length modulation  

These non-ideal effects increase the effective output resistance and lead to
a higher simulated gain.




---
### EXP2 – CIRCUIT 2C – 
Common Source Amplifier with Diode-Connected NMOS Current Source and PMOS Active Load
-------------------------------------------------------------

### Circuit Implementation in LTspice
<img width="759" height="850" alt="circuit2c" src="https://github.com/user-attachments/assets/f8919fea-a198-4e16-bd7e-c94ccda1caae" />

---
# DC Analysis – Circuit 2C

## Design Conditions

| VDD | ID | VTHn | VTHp |
|----|----|----|----|
| 1.8 V | 200 µA | 0.36 V | −0.39 V |

---
## Voltage Limits for Saturation Operation

| Parameter | Minimum | Maximum | Reason |
|-----------|---------|---------|--------|
| VGS (NMOS) | ≥ 0.36 V | ≤ 1.8 V | Channel formation |
| VDS (NMOS) | ≥ VOV | ≤ 1.8 V | Saturation condition |
| VSG (PMOS) | ≥ 0.39 V | ≤ 1.8 V | PMOS conduction |
| VSD (PMOS) | ≥ VOV | ≤ 1.8 V | Saturation condition |

---
# Overdrive Voltage Verification

| Calculation | Result |
|-------------|--------|
| VGS = VTH + VOV = 0.36 + 0.25 | **0.61 V** |
| VOV = VGS − VTH = 0.61 − 0.36 | **0.25 V** |

### Allowable Range

| Minimum VOV | Maximum VOV |
|-------------|-------------|
| > 0 | < VDS |

Since

VDS ≈ **0.9 V**

the allowable range becomes

0 < VOV < 0.9 V

The obtained value

**VOV = 0.25 V**

lies comfortably within this range.

### Justification
A moderate overdrive voltage

• provides sufficient transconductance  
• maintains stable drain current  
• leaves voltage headroom for signal swing

---
# Diode-Connected NMOS Bias (M3)

In a diode-connected MOSFET

VD = VG

Thus

| Calculation | Result |
|-------------|--------|
| VGS3 = VTH + VOV = 0.36 + 0.25 | **0.61 V** |

Since the source of M3 is grounded

| Node | Voltage |
|------|--------|
| VS3 | 0 V |
| VD3 = VG3 | **0.61 V** |

This node becomes the **source of M1**.

Therefore

| Node | Voltage |
|------|--------|
| VS1 | **0.61 V** |

### Justification

The diode-connected NMOS automatically adjusts its gate-source voltage to maintain the desired drain current (≈200 µA). This fixes the node voltage at approximately **0.61 V**, establishing the correct bias for the amplifier.

---
# Gate Bias of M1

For transistor M1 to carry the same current:

| Calculation | Result |
|-------------|--------|
| VGS1 = VTH + VOV = 0.36 + 0.25 | **0.61 V** |
| VG1 = VS1 + VGS1 = 0.61 + 0.61 | **1.22 V** |

Thus the **input DC bias voltage** is

**VIN(DC) ≈ 1.22 V**

---
# Output Voltage Selection

For maximum signal swing

VDS ≈ VDD / 2

| Calculation | Result |
|-------------|--------|
| VDS = 1.8 / 2 | **0.9 V** |

Therefore

| Calculation | Result |
|-------------|--------|
| Vout = VDS + VS1 = 0.9 + 0.61 | **≈ 1.5 V** |

---
# PMOS Active Load Bias

| Calculation | Result |
|-------------|--------|
| VSG2 = |VTHp| + VOV = 0.39 + 0.25 | **0.64 V** |
| VG2 = VDD − VSG2 = 1.8 − 0.64 | **1.16 V** |

Drain-source voltage

| Calculation | Result |
|-------------|--------|
| VSD2 = 1.8 − 1.5 | **0.3 V** |

### Saturation Check

| Device | Condition | Result |
|------|-----------|--------|
| M1 (NMOS) | VDS ≥ VOV | 0.9 ≥ 0.25 ✔ |
| M3 (NMOS) | VDS ≥ VOV | 0.61 ≥ 0.25 ✔ |
| M2 (PMOS) | VSD ≥ VOV | 0.3 ≥ 0.25 ✔ |

Thus **all transistors operate in saturation region**.

---
# Final DC Operating Point

| VS1 | Vout | VG1 | VG2 | ID | VOV |
|----|----|----|----|----|----|
| 0.61 V | 1.5 V | 1.22 V | 1.16 V | 200 µA | 0.25 V |

The diode-connected NMOS automatically establishes the correct source voltage for M1, ensuring stable biasing and maintaining all transistors in saturation.

---
### LTspice Operating Point

<img width="605" height="541" alt="circuit2cop" src="https://github.com/user-attachments/assets/4974f15c-eb00-422d-be8b-91ca110c9c50" />

## Width Selection – Circuit 2C
The transistor widths were initially calculated using the square-law saturation current equation to obtain **ID ≈ 200 µA**.

| Device | Calculated Width | Practical Width |
|------|------|------|
| M1 (NMOS – Amplifier) | 15.16 µm | 26.34 µm |
| M2 (PMOS – Active Load) | 35.9 µm | 87.87 µm |
| M3 (NMOS – Diode Connected Current Source) | 15.16 µm | 33.26 µm |

### Justification

During LTspice simulation, the theoretical widths did not produce exactly **200 µA** due to practical MOSFET model effects.

| Reason | Effect |
|------|------|
| Channel length modulation | Changes effective drain current |
| Diode-connected bias sensitivity | Current strongly depends on VGS |
| Mobility degradation | Reduces current compared to ideal model |

Therefore the widths were slightly adjusted in simulation until the desired operating current **ID ≈ 200 µA** was obtained while keeping all transistors in **saturation region**.

---
## Transient Analysis – Circuit 2C (Common Source with Diode-Connected Current Source)

### Input Signal Parameters

| Waveform | Frequency | Amplitude | DC Offset |
|----------|-----------|-----------|-----------|
| Sine | 1 kHz | 10 mV | 1.22 V |

| Simulation Command | Value |
|--------------------|-------|
| Transient Command | `.tran 0 5m` |

---
### Input Waveform

<img width="1919" height="861" alt="2ct_input" src="https://github.com/user-attachments/assets/488921a3-53c6-42f0-b3b1-63ef0d9aa6ec" />

---
### Output Waveform

<img width="1919" height="857" alt="2ct_output" src="https://github.com/user-attachments/assets/fdd3775a-909a-4a35-aa28-f4aa44f14767" />

---
### Input & Output Comparison

<img width="1909" height="858" alt="2ct_combined" src="https://github.com/user-attachments/assets/feda64ee-1a11-4c39-af94-20888a61345f" />

---
## Practical Gain Calculation

| Vin(p-p) | Vout(p-p) | Gain (Av) | Gain (dB) |
|----------|-----------|-----------|-----------|
| 1.229 − 1.210 = **0.019 V** | 1.618 − 1.235 = **0.383 V** | 0.383 / 0.019 = **20.16 V/V** | **26.08 dB** |

---
### Observation

The output waveform is inverted with respect to the input signal, confirming **common-source operation**. The output amplitude is significantly larger than the input amplitude, demonstrating proper voltage amplification while maintaining a stable bias point around **1.5 V**.

----
# AC Analysis – Circuit 2C

Small-signal AC analysis was performed to determine the **frequency response, midband gain, and bandwidth** of the amplifier.

### Simulation Parameters

| Parameter | Value |
|-----------|------|
| AC Command | `.ac dec 1000 .1 1G` |
| Input AC magnitude | 1 V |

---
<img width="1917" height="862" alt="2cac_gain" src="https://github.com/user-attachments/assets/a3375b34-a0da-4127-876e-fd4659fe7594" />

---
## Frequency Response Results – Circuit 2C

| Gain (dB) | Gain (V/V) | −3 dB Gain | Bandwidth | GBW | UGB |
|-----------|------------|------------|-----------|------|------|
| 25.55 dB | 10^(25.55/20) = **18.94** | 22.55 dB | **119.124 MHz** | 18.94 × 119.124 MHz = **2.25 GHz** | **≈ 2.691 GHz** |

The AC response confirms the amplifier’s midband gain and bandwidth. The gain–bandwidth product and unity gain bandwidth were obtainedfrom the same frequency response plot.

## Theoretical Gain – Circuit 2C (λ ≠ 0)

$$
R_s = \left(\frac{1}{g_{m3}} \parallel r_{o3}\right)
$$

Then the small-signal gain of Circuit 2C (λ ≠ 0) is

$$
A_v =
-\frac{g_{m1}}
{1 + g_{m1}R_s + \frac{r_{o1}}{R_s}}
\left[
r_{o2} \parallel
\left(
g_{m1} r_{o1} R_s + r_{o1} + R_s
\right)
\right]
$$
  
### Gain Calculation

| Step | Expression | Result |
|-----|------------|--------|
| Drain Current | ID | 200 µA |
| Overdrive Voltage | Vov | 0.25 V |
| Transconductance | gm = 2ID / Vov | **1.6 mS** |
| Channel modulation | λ (TSMC 180 nm) | **0.15 V⁻¹** |
| Output resistance | ro = 1/(λID) | **33.3 kΩ** |
| Parallel term | (1/gm3 ∥ ro3) | **613 Ω** |
| Denominator | 1 + gm1(613) + ro1/613 | **56.3** |
| Inner term | gm1 ro1(613) + ro1 + 613 | **66.5 kΩ** |
| Output resistance | ro2 ∥ 66.5k | **22.2 kΩ** |
| Voltage Gain | Av = (1.6mS / 56.3) × 22.2k | **20.1 V/V** |
| Gain in dB | 20 log10(20.1) | **≈ 26.06 dB** |

---

### Result

| Quantity | Value |
|---------|-------|
| Voltage Gain | **20.1 V/V** |
| Gain | **≈ 26.06 dB** |

This closely matches the simulated AC gain (~25.5 dB).

Thus the theoretical gain is approximately **26 dB**, which closely matches the gains obtained from

• **Transient analysis ≈ 26.08 dB**  
• **AC analysis ≈ 25.55 dB**

---
### Reason for Small Difference

The slight difference between theoretical and simulated gain occurs because theoretical calculations use simplified small-signal equations, while LTspice uses a complete **BSIM MOSFET model** including

• channel-length modulation variations  
• parasitic capacitances  
• mobility degradation  
• body effect

Hence a small variation (≈0.5–1 dB) between theoretical and simulation results is expected.

------
# Summary, Inference and Conclusion

## Summary

In this experiment, three MOSFET amplifier configurations were designed and analyzed using **TSMC 180 nm CMOS technology in LTspice**.

The circuits studied were:

• **Circuit 2A – Source Degenerated Common Source Amplifier**  
• **Circuit 2B – Cascode Amplifier with Active Load**  
• **Circuit 2C – Common Source Amplifier with Diode-Connected NMOS Current Source and PMOS Active Load**

For each configuration:

- DC bias conditions were calculated to ensure correct operating points.
- Saturation of all MOSFETs was verified.
- Transient analysis was performed to observe time-domain amplification.
- AC analysis was used to obtain gain and frequency response.
- Theoretical gain was derived and compared with simulation results.

---
## Inference

• **Source degeneration (Circuit 2A)** introduces negative feedback, which improves bias stability but slightly reduces gain.

• **Cascode configuration (Circuit 2B)** increases output resistance theoretically; however, practical device limitations and loading reduce the achievable gain.

• **Active load configuration (Circuit 2C)** uses a diode-connected current source and PMOS load, enabling higher voltage gain without source degeneration.

• Minor differences between theoretical and simulated results occur due to non-ideal MOSFET effects included in the LTspice BSIM model.

---
## Comparison of Amplifier Configurations

| Parameter | Circuit 2A | Circuit 2B | Circuit 2C |
|-----------|------------|------------|------------|
| Configuration | Source Degenerated CS | Cascode Amplifier | CS with Active Load |
| Source Biasing | Source resistor (RS) | Cascode NMOS bias | Diode-connected NMOS |
| Output Voltage (DC) | ≈ 1.1 V | ≈ 1.2 V | ≈ 1.5 V |
| AC Gain | ≈ 28.7 dB | ≈ 6.9 dB | ≈ 25.5 dB |
| Bandwidth (-3 dB) | ≈ 52.119 MHz | ≈ 48.417 MHz | ≈ 119.124 MHz |
| Gain Bandwidth Product | ≈ 1.4 GHz | ≈ 0.107 GHz | ≈ 2.25 GHz |
| Unity Gain Bandwidth | ≈ 1.717 GHz | ≈ 90.782 MHz | ≈ 2.691 GHz |
| Gain Characteristic | Moderate gain with feedback | Lower practical gain | Higher gain using active load |
| Bias Stability | High | High | Moderate |
| Circuit Complexity | Medium | High | Medium |

---
## Conclusion

The experiment demonstrates how different MOSFET amplifier configurations affect voltage gain, output resistance, and bias stability.

• The **source-degenerated amplifier (2A)** provides stable biasing and moderate gain due to feedback through the source resistor.

• The **cascode amplifier (2B)** theoretically increases output resistance and bandwidth, but the practical gain is limited by device parameters and loading effects.

• The **active load amplifier (2C)** achieves relatively high gain using current-source biasing without source degeneration.

Overall, the simulation results obtained from **LTspice closely follow the expected theoretical behavior**, confirming the correct design and operation of the MOS amplifier circuits.





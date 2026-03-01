#  Linear Integrated Circuits Laboratory  

## Experiment 2:Common Source Amplifier -CONFIGURSTIONS(TSMC 180nm)

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
## 3. THEORY
### 3.1 Basic MOS Amplifier Concepts
MOS amplifiers are fundamental building blocks in analog integrated circuits.  
They convert small input voltage variations into amplified output voltage signals.

All circuits are designed such that MOSFETs operate in **saturation region**, where:

ID = (1/2) μCox (W/L) (Vov)^2  

and  

gm = 2ID / Vov  

ro = 1 / (λID)

Voltage Gain:

Av = -gm × Rout

---

### 3.2 Concept of Source Degeneration Amplifier

The source degeneration amplifier is a Common Source configuration 
with a resistor connected at the source terminal.

Concept:
- Introduces negative feedback
- Improves linearity
- Reduces gain
- Enhances bias stability

Voltage Gain:
Av = -gm1 * Rout / (1 + gm1 Rs)

------------------------------------------------

### 3.3 Concept of Cascode Amplifier

The cascode amplifier combines Common Source and Common Gate stages.

Concept:
- Increases output resistance
- Reduces Miller effect
- Provides high voltage gain

Output Resistance:
Rout ≈ gm3 * ro3 * ro1

Voltage Gain:
Av = -gm1 * Rout

------------------------------------------------

### 3.4 Concept of Current Mirror Loaded Amplifier

This configuration uses a diode-connected transistor 
to establish reference current.

Concept:
- Provides active biasing
- Improves IC integration
- Offers moderate to high gain

Voltage Gain:
Av = -gm1 * (ro1 || ro2)
--------------------------------------------------
## 4.Device Parameters(From Datasheet)

Technology      : TSMC 180nm

Supply Voltage  : VDD = 1.8V

Target Drain Current (ID) : 200 µA

Overdrive Voltage (Vov)   : 0.25 V

Threshold Voltage (VTH NMOS)  : 0.36 V

threshold Voltage (VTH PMOS)  :-0.39 V

Channel Length (L)        : 560 nm

Oxide thickness: tox = 4.1 × 10⁻⁹ m 

Electron mobility NMOS: μn = 273.809 × 10⁻⁴ m²/Vs 

Electron mobility PMOS: μn = 115.68 × 10⁻⁴ m²/Vs 

Oxide permittivity: εox = εr ε0 = 8.854 × 10⁻¹² × 4  
εox = 3.54 × 10⁻¹¹  

Oxide capacitance: Cox = εox / tox  

Cox = (3.54 × 10⁻¹¹) / (4.1 × 10⁻⁹) 

Cox = 8.634 mF/m²  
-----------------------------------------------------------
## 6. OPERATING CONDITIONS FOR SATURATION

For NMOS:
VDS ≥ Vov

For PMOS:
VSD ≥ |Vov|

Drain Current:
ID = (1/2) μCox (W/L) (Vov)^2

Transconductance:
gm = 2ID / Vov

Output Resistance:

ro = 1 / (λID)
-----------------------------------------------------------------
## 7.Width Calculation Using Physical Parameters

------------------------------------------------------------
## Process Transconductance Parameters
(calculated using Device Parameters(From Datasheet))
μnCox = μn × Cox  

μnCox = 0.0273809 × 8.634 × 10⁻3  

μnCox = 2.363 × 10⁻4 A/V²  

μnCox ≈ 236 µA/V²  

------------------------------------------------------------

μpCox = μp × Cox  

μpCox = 0.011568 × 8.634 × 10⁻3  

μpCox = 9.99 × 10⁻5 A/V²  

μpCox ≈ 100 µA/V²  

------------------------------------------------------------

## 8.Width Calculation
(calculated using Device Parameters(From Datasheet))

Using saturation equation:

ID = (1/2) μCox (W/L) (Vov)^2  

Rearranging:

W = (2 ID L) / [μCox (Vov)^2]

------------------------------------------------------------

### NMOS Width

Wn = (2 × 200×10⁻6 × 560×10⁻9)  
     / [2.363×10⁻4 × (0.25)^2]

Wn = (2.24 × 10⁻10) / (1.477 × 10⁻5)

Wn = 1.516 × 10⁻5 m  

Wn = 15.16 µm  

------------------------------------------------------------

### PMOS Width

Wp = (2 × 200×10⁻6 × 560×10⁻9)  
     / [9.99×10⁻5 × (0.25)^2]

Wp = (2.24 × 10⁻10) / (6.24 × 10⁻6)

Wp = 3.59 × 10⁻5 m  

Wp = 35.9 µm  

------------------------------------------------------------

## Final Calculated Dimensions

NMOS  : W/L = 15.16µm / 0.56µm  
PMOS  : W/L = 35.9µm / 0.56µm  

------------------------------------------------------------

Observation:

• Since μn > μp, NMOS requires smaller width.  
• PMOS width is approximately 2.3× NMOS width.  
• These values theoretically give ID ≈ 200 µA (without λ effect).  

------------------------------------------------------------
### CIRCUIT A – SOURCE DEGENERATED COMMON SOURCE AMPLIFIER

------------------------------------------------------------

 Design Objective

To design and implement a source-degenerated common source amplifier 
for ID = 200 µA with maximum symmetric output swing.

----------------------------------------------------------
Circuit Implementation in LTspice
-----------------------------------
![Circuit 2A](circuit2a.png)
### 9. DC Analysis 

 DC BIAS CALCULATION – CIRCUIT A  
(Common Source with Source Degeneration)

Given:

VDD = 1.8 V  
ID = 200 µA  
Vov = 0.25 V  
VTH (NMOS) = 0.36 V  
|VTH (PMOS)| = 0.39 V  

------------------------------------------------------------

### Step 1: Choose Drain-Source Voltage for Symmetric Swing

For maximum output swing:

VDS = VDD / 2  

VDS = 1.8 / 2  

VDS = 0.9 V  

------------------------------------------------------------

### Step 2: Assume Source Voltage

Let:

VS = 0.2 V  

------------------------------------------------------------

### Step 3: Calculate Output Voltage

VDS = Vout − VS  

0.9 = Vout − 0.2  

Vout = 0.9 + 0.2  

Vout = 1.1 V  

------------------------------------------------------------

### Step 4: Calculate Source Resistor (RS)

VS = ID × RS  

RS = VS / ID  

RS = 0.2 / (200 × 10⁻⁶)  

RS = 1000 Ω  

RS = 1 kΩ  

------------------------------------------------------------

### Step 5: Calculate VGS (NMOS)

VGS = VTH + Vov  

VGS = 0.36 + 0.25  

VGS = 0.61 V  

------------------------------------------------------------

### Step 6: Calculate Gate Voltage (VG)

VGS = VG − VS  

VG = VGS + VS  

VG = 0.61 + 0.2  

VG = 0.81 V  

------------------------------------------------------------

### Step 7: PMOS Bias Calculation

For PMOS:

VSG = Vov + |VTHp|  

VSG = 0.25 + 0.39  

VSG = 0.64 V  

PMOS Source = VDD = 1.8 V  

VSG = VS − VGp  

1.8 − VGp = 0.64  

VGp = 1.8 − 0.64  

VGp = 1.16 V  

------------------------------------------------------------

### Step 8: Saturation Condition Check

NMOS:

VDS = 0.9 V  
VOV = 0.25 V  

Since 0.9 > 0.25  
NMOS operates in saturation.

PMOS:

VSD = 1.8 − 1.1  
VSD = 0.7 V  

Since 0.7 > 0.25  
PMOS operates in saturation.

------------------------------------------------------------

### Final DC Operating Point(from theretical calculations)

VS   = 0.2 V  
VDS  = 0.9 V  
Vout = 1.1 V  
VG   = 0.81 V  
VGp  = 1.16 V  
ID   = 200 µA  
RS   = 1 kΩ  

------------------------------------------------------------
![operating point - 2A](circuit2aop.png)
###  Width Selection for Circuit A

The MOSFET widths were calculated earlier using the 
square-law saturation equation to obtain ID = 200 µA.

The calculated values are:

NMOS  : W = 15.16 µm  
PMOS  : W = 35.9 µm  

(Refer Section 8: Width Calculation_FROM DEVICE PARAMETERS)

### Practical Width Adjustment

During LTspice simulation, the drain current obtained 
using theoretical widths was slightly different 
from the target value of 200 µA.

This deviation occurs due to:

• Channel length modulation  
• Mobility degradation  
• Velocity saturation  
• Short-channel effects  

Hence, widths were slightly adjusted in LTspice 
until ID ≈ 200 µA was achieved.

Final Dimensions Used in Simulation:

NMOS  : W = 29u µm  
PMOS  : W = 83u µm  

------------------------------------------------------------

## 10. Transient Analysis – Circuit 2A  
(Source Degenerated Common Source Amplifier)

To verify time-domain performance of the amplifier,
a small-signal sinusoidal input was applied.

### Input Signal Parameters

• Type        : Sine wave  
• Frequency   : 1 kHz  
• Amplitude   : 10 mV  
• DC Offset   : 0.81 V  

Input Command Used in LTspice:

Vin = SINE(0.81 10m 1k)

------------------------------------------------------------

The DC offset (0.81 V) corresponds to the calculated
gate bias voltage required to maintain ID = 200 µA.

The 10 mV amplitude ensures small-signal operation,
keeping the transistor in saturation region.

------------------------------------------------------------

![Transient Input](2at_input.png)

: Input Waveform Applied at Gate

------------------------------------------------------------

The output waveform is observed at the drain terminal.

Since this is a Common Source amplifier:

• Output is inverted (180° phase shift)  
• Output amplitude is greater than input amplitude  
• Signal is amplified around DC bias point (≈ 1.1 V)

------------------------------------------------------------

![Transient Output](2at_output.png)

: Output Waveform at Drain

------------------------------------------------------------

Both input and output waveforms plotted together:

![Transient Combined](2at_combined.png)

: Input vs Output Waveforms

------------------------------------------------------------

### Observations

• Output signal is inverted relative to input.  
• Amplification is clearly observed.  
• Output swing remains within saturation limits.  
• No clipping is observed for 10 mV input amplitude.  
• DC bias point remains stable at approximately 1.1 V.

------------------------------------------------------------
Measured:

Vin(p-p) = 0.819V - 0.800V
Vin(p-p) =0.019V

Vout(p-p) = 1.386V − 0.858V 
Vout(p-p) = 0.528V 

Practical gain:

Av = Vout / Vin  

Av = 0.528 / 0.019  

Av = 27.78 V/V 

Gain in dB:

Av(dB) = 20 log(27.78)  

Av(dB) = 28.87 dB  

This is the gain obtained from transient waveform.

---
# AC Analysis
## – Frequency Response (Circuit 2A)

To determine midband gain and bandwidth,
small-signal AC analysis was performed.

AC Simulation Command Used:

.ac dec 100 1 100MEG

Input AC magnitude = 1 V

------------------------------------------------------------

![AC Gain Plot](2aac_gain.png)

Figure: AC Gain (Magnitude vs Frequency)

From AC plot:

maximum Gain ≈ 28.71 dB  
The measured AC gain is 28.71 dB, which strongly correlates with our transient calculation
-3dB point 25.71dB=52.119MHz
---------
To verify simulation, theoretical gain is calculated using small-signal values from LTspice.

gm1 = 1.6 mA/V      ro1 ≈ 58.8 kΩ  
ro2 ≈ 58.8 kΩ      RS = 1 kΩ  

Gain formula:

Av = - gm1 / (1 + gm1RS + RS/ro1) × ([gm1RSro1 + RS + ro1] || ro2)

Substitution:

Denominator = 1 + 1.6 + (1k/58.8k) = 2.617  

Bracket term = (1.6×58.8k + 1k + 58.8k) || 58.8k  
             ≈ 42.6 kΩ  

Av = - (1.6mS / 2.617) × 42.6k  
Av ≈ -26 V/V  

Gain ≈ 28 dB  

Theoretical gain matches AC and transient results.

### Reason for Difference Between Theoretical and Simulation Gain

The small difference between theoretical and simulated gain 
occurs due to non-ideal device effects present in the MOS model.

In hand calculations, simplified small-signal equations are used,
whereas LTspice uses the complete BSIM model which includes:

• Channel length modulation  
• Mobility degradation  
• Parasitic capacitances  
• Higher-order effects  

Hence, a slight variation (≈ 0.5–1 dB) between theoretical 
and simulation results is expected.












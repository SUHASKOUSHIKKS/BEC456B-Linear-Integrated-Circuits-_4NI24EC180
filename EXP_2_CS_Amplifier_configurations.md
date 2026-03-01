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
## 4.Device Parameters (From Datasheet)

Technology      : TSMC 180nm
Supply Voltage  : VDD = 1.8V
Target Drain Current (ID) : 200 µA
Overdrive Voltage (Vov)   : 0.25 V
Threshold Voltage (VTH NMOS)  : 0.36 V
threshold Voltage (VTH PMOS)  :-0.39 V
Channel Length (L)        : 560 nm
Oxide thickness: tox = 4.1 × 10⁻⁹ m  
Electron mobility: μn = 273.809 × 10⁻⁴ m²/Vs  
Oxide permittivity: εox = εr ε0 = 8.854 × 10⁻¹² × 3.9  
εox = 3.45 × 10⁻¹¹  
Oxide capacitance: Cox = εox / tox  
Cox = (3.45 × 10⁻¹¹) / (4.1 × 10⁻⁹)  
Cox = 8.414 mF/m²  
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







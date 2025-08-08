# Experiment 3 – H-Bridge Driver and Integration

## 🎯 Objective
To design and test an **H-Bridge driver circuit** as the output stage of a Class-D audio amplifier. The H-Bridge will be driven by PWM signals from the single-ended to differential converter and PWM modulator (Experiment 2) and used to drive a resistive load or speaker.

---

## 📚 Theory
The H-Bridge driver is the final stage of the Class-D amplifier. It uses **two half-bridge stages** to create a differential output (`VOUT_P` and `VOUT_N`).  
Each half-bridge consists of:
- **Qp (PNP transistor)** for the high-side
- **Qn (NPN transistor)** for the low-side  
Driven by CMOS inverters and a **non-overlapping clock generator** to avoid shoot-through currents.

**Key Points:**
- Open-collector outputs like LM339 require pull-up resistors.
- Base resistors limit transistor base current.
- RC low-pass filters are used for **waveform observation only**, not in the load path.

---

## ⚙️ Specifications
- Supply Voltage: **VDD = VIN = 5V**
- PWM Frequency: **5 kHz**
- Load: **32 Ω** (resistive or speaker)

---

## 🛠️ Components
- Comparators: **LM339**
- Inverters: **MC14069 / CD4069**
- NAND gates: **SN74AHC00N**
- Transistors: **2NXXXX series** (NPN and PNP)
- Resistors: Pull-up (10kΩ), Base resistors (few kΩ)
- RC filter: f<sub>c</sub> = 1–2 kHz (for observation)

---

## 🧪 Procedure

### 1️⃣ Simulation (Pre-Lab)
1. Build the complete Class-D amplifier circuit in LTspice using:
   - PWM outputs (`VPWM_P` and `VPWM_N`) from Experiment 2
   - Two half-bridge drivers (Figure 4 in lab manual)
   - Speaker model (Figure 6)
2. Verify:
   - Differential output (`VOUT_P - VOUT_N`)
   - Inductor current matches **average voltage / RL**

---

### 2️⃣ Hardware Steps
1. **Set Up**  
   - VDD = VIN = 5V  
   - Load = 32 Ω resistor (initial test)
   
2. **Apply Input**  
   - Function generator: 312.5 Hz sine wave  
   - Amplitude: Same as ramp peak-to-peak (1V) from Experiment 1  
   - Feed into single-ended to differential converter (Exp-2 output)

3. **Measure PWM at Driver Output**  
   - Observe `VOUT_P` and `VOUT_N` on oscilloscope  
   - Verify:
     - `VOUT_P` duty cycle follows `Vin_a+`
     - `VOUT_N` duty cycle is inverted (1–D)

4. **Observe Filtered Output**  
   - Add RC filters to `VOUT_P` and `VOUT_N` (cutoff = 1–2 kHz)  
   - Verify the filtered waveform matches `Vin_a+` and `Vin_a-` shape  
   - Keep the load connected directly between `VOUT_P` and `VOUT_N` (filters are only for measurement)

5. **Speaker Test**  
   - Replace resistor with 32 Ω speaker  
   - Repeat tests with input frequencies: 156.25 Hz, 312.5 Hz, 625 Hz, 937.5 Hz, 1.25 kHz  
   - Vary input amplitude and note change in sound level

---

## 📊 Expected Results
- **Differential PWM** at `VOUT_P` and `VOUT_N`
- Filtered outputs resembling input sine wave
- Audible output on speaker at given test frequencies

---

## 📷 Waveform Capture
Capture and save oscilloscope screenshots for:
- `VOUT_P` and `VOUT_N` PWM waveforms
- Filtered outputs for one test condition

---

## 📝 Observations
- Duty cycle changes according to input amplitude
- Filtered output matches input sine
- Speaker reproduces different tones clearly

---

## 📌 Notes
- Ensure proper transistor saturation by adjusting base resistors if needed
- Use non-overlapping clock generator to prevent shoot-through
- Keep analog and digital grounds clean to minimize noise

---

## 📄 References
- BS Analog Systems Lab Manual – Experiment 3
- LTspice simulation files for Class-D amplifier

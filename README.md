# CMOS Inverter Design with Cadence Virtuoso (AMS 0.35µm)

This project focuses on the **design, simulation, optimization, and layout** of a **CMOS inverter** using **Cadence Virtuoso** with the AMS 0.35µm (C35B4) technology.

The work includes schematic design, testbench setup, transient/DC simulations, parameter sweep optimization for transistor sizing, and final layout verification (DRC/LVS).

---

## 📌 Objectives
- Design a CMOS inverter using **NMOS** and **PMOS** transistors.  
- Perform **transient** and **DC sweep simulations** to characterize the circuit.  
- Optimize the **PMOS width (Wp)** to balance rise and fall times.  
- Create the **layout** of the inverter following design rules.  
- Verify the design using **DRC** and **LVS** checks.  

---

## ⚙️ Tools & Technology
- **Technology**: AMS 0.35µm (C35B4)  
- **CAD Tool**: Cadence Virtuoso + ADE (Analog Design Environment)  
- **Transistor Models**: `NMOS4` and `PMOS4` from the PRIMLIB library  

---

## 📝 Initial Schematic & Testbench
The first version of the inverter used identical dimensions for NMOS and PMOS:  
- L = 0.35µm  
- W = 0.35µm  


**Schematic and Testbench Cellviews:**  
<p align="center">

<img src="./DC%20Analysis/CMOS%20inverter%20cellview.png" alt="CMOS Inverter Schematic" width="500"/>
<img src="./DC%20Analysis/testbench%20cellview.png" alt="Testbench Schematic" width="500"/>
</p>
---

## 📊 Simulation Results (Before Optimization)

### Transient Response
The inverter was simulated with a 0V–3.3V square input. We can see that the output is inverted as expected.
<img src="./DC%20Analysis/chronongramme%20temporel.png" alt="Testbench Schematic" width="400"/>

### DC Sweep
The transfer characteristic shows a switching threshold around **1.2V**, lower than the ideal mid-supply (1.65V).  
<img src="./DC%20Analysis/DC%20caracteristics%20parameter%20sweep.png" alt="Testbench Schematic" width="400"/>

---

## 🔧 Parameter Sweep Optimization

To balance the switching threshold, a **parametric sweep of Wp** (PMOS width) was performed:  

- Range: **0.5µm → 2µm**  
- Objective: Find optimal Wp so that **Vth ≈ Vdd/2 ≈ 1.65V**  

**Sweep Setup:**  
<img src="./Optimization/variable%20wp%20settings.png" alt="Testbench Schematic" width="550"/>

**DC Sweep with Different Wp Values:**  
<img src="./Optimization/wp%20parameter%20sweep.png" alt="Testbench Schematic" width="600"/>

The optimal **Wp ≈ 1.6–1.7µm** balances the inverter, bringing the switching threshold close to 1.65V.

---

## 📊 Simulation Results (After Optimization)

### Optimized Inverter Schematic & Testbench


### Transient Response
The rise and fall times are now balanced after sizing optimization.  
<img src="./Optimization/chronogramme%20temporel%20plot.png" alt="Testbench Schematic" width="600"/>

### DC Transfer Characteristic
The switching point is closer to mid-supply, improving inverter symmetry.  

---

## 🖼️ Layout Design & Extraction

The final **layout** was designed with proper routing and shared diffusion regions.  
- Inputs/outputs routed in Metal1/2  
- Polysilicon gates vertical and shared between NMOS & PMOS  
- Common source/drain regions used  
- No DRC violations  

**Layout and Extracted Views:**  
<p align="center">

<img src="./Layout/Layout%20view.png" alt="Testbench Schematic" width="400"/> 
<img src="./Layout/av_extracted%20view.png" alt="Testbench Schematic" width="400"/>
</p>
---

## 📚 Theoretical Note: Why is PMOS Wider than NMOS?
Due to the **lower mobility of holes** compared to electrons, PMOS transistors must be wider than NMOS to achieve **balanced drive strength**.  
In this project, the optimal ratio was found to be:  

$\frac{W_p}{W_n} \approx 3.2$


This ensures that the inverter’s **switching threshold is centered**, giving symmetrical rise and fall times.

---

## ✅ Conclusion
- A **CMOS inverter** was successfully designed and optimized in **Cadence Virtuoso**.  
- Transistor sizing optimization (Wp ≈ 1.7µm) balanced the switching threshold.  
- The final layout passed **DRC** checks and is LVS clean.  
- The inverter is now ready to be used as a **standard cell** in digital design flows.  


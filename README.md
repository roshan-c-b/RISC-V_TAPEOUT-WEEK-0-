
# RISC-V Tapeout – Week 0

<details>
<summary><b>Digital VLSI SoC Flow (Summary)</b></summary>  
<br>

### **Stage O1 – Specification / Modeling**

* Capture chip intent in **C/C++/SystemC**.
* Use C testbench as the **golden functional reference**.
* **Deliverable:** Verified model + testbench.

---

### **Stage O2 – RTL Development**

* Translate spec into synthesizable **Verilog/VHDL/SystemVerilog**.
* Build processor core + peripherals (UART, GPIO, SPI, etc.).
* Simulate RTL against the C reference.
* **Deliverable:** RTL design validated against model.

---

### **Stage O3 – Synthesis / Netlist**

* Run **logic synthesis** with a standard-cell library.
* Generate **gate-level netlist**.
* Integrate macros (SRAM, ROM, PLL) and analog IP wrappers.
* **Deliverable:** SoC netlist + synthesis reports.

---

### **Stage O4 – Physical Implementation**

* Map netlist to silicon:

  * Floorplan → Place → CTS → Route → DRC/LVS.
* Export **GDSII** layout for fab.
* **Deliverable:** Sign-off GDS.

---

### **Stage O4b – Post-Silicon Validation**

* Bring up silicon on board.
* Reuse **C testbench** for validation.
* Verify performance/frequency, ensure functional match.
* **Deliverable:** Working SoC ready for integration.

---

### **Design Flow Overview**

```text
(O1) C Model → (O2) RTL → (O3) Netlist → (O4) GDS → (O4b) Silicon Validation
```

**Note:** Same functionality must hold from O1 through O4.

* **Soft IP = synthesizable RTL.**
* **Hard IP = fixed layout blocks (SRAM, PLL, ADC).**

</details>

---

<details>
<summary><b>Tool Setup Instructions</b></summary>  
<br>

### Requirements

* Ubuntu 20.04+ (or WSL2/VM)
* ≥ 4 cores, 6 GB RAM, 50 GB disk

---

#### **Yosys — Synthesis**

```bash
sudo apt install -y build-essential git bison flex libreadline-dev gawk \
  tcl-dev libffi-dev graphviz xdot
git clone https://github.com/YosysHQ/yosys.git && cd yosys
make -j$(nproc) && sudo make install
```

`![Yosys](C:/Users/rosha/OneDrive/Documents/vsd-tapeout/yosys.png)`

---

#### **Icarus Verilog — Simulation**

```bash
sudo apt install -y iverilog
iverilog -o sim.vvp tb.v && vvp sim.vvp
```

`![Icarus](C:/Users/rosha/OneDrive/Documents/vsd-tapeout/iverilog.png)`

---

#### **GTKWave — Waveform Viewer**

```bash
sudo apt install -y gtkwave
gtkwave dump.vcd
```

`![GTKWave](tools/img/gtkwave.png)`

---

#### **Ngspice — Analog / Mixed-Signal**

```bash
sudo apt install -y ngspice
```

`![Ngspice](C:/Users/rosha/OneDrive/Documents/vsd-tapeoutngspice.png)`

---

#### **Magic — Layout Editor**

```bash
sudo apt install -y m4 tcsh libx11-dev libtk-dev libcairo2-dev
git clone https://github.com/RTimothyEdwards/magic.git && cd magic
./configure && make -j$(nproc) && sudo make install
```

`![Magic](C:/Users/rosha/OneDrive/Documents/vsd-tapeout/magic.png)`

---

#### **OpenLane — RTL → GDS**

```bash
# Install Docker
sudo apt install -y docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER

# Fetch OpenLane
git clone https://github.com/The-OpenROAD-Project/OpenLane.git
cd OpenLane && make
```

`![OpenLane](tools/img/openlane.png)`

</details>



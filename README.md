
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
sudo apt-get update
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make build-essential clang bison flex \
libreadline-dev gawk tcl-dev libffi-dev git \
graphviz xdot pkg-config python3 libboost-system-dev \
libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make
sudo make install
```

`[![Yosys](C:/Users/rosha/OneDrive/Documents/vsd-tapeout/yosys.png)](https://github.com/roshan-c-b/RISC-V_TAPEOUT-WEEK-0-)`

---

#### **Icarus Verilog — Simulation**

```bash
sudo apt-get update
sudo apt-get install iverilog
```

`<img width="356" height="129" alt="Image" src="https://github.com/user-attachments/assets/aaf2ea64-f7c0-44ea-bf6a-83a1ed6b7fbe" />

`

---

#### **GTKWave — Waveform Viewer**

```bash
sudo apt-get update
sudo apt install gtkwave
```

`<img width="571" height="421" alt="Image" src="https://github.com/user-attachments/assets/9f33fff8-5386-4a0f-af7a-3a3cf656a5c5" />`

---

#### **Ngspice — Analog / Mixed-Signal**

```bash
$ sudo apt update
$ sudo apt install ngspice
```

`![Ngspice](C:/Users/rosha/OneDrive/Documents/vsd-tapeoutngspice.png)`

---

#### **Magic — Layout Editor**

```bash
# Install required dependencies
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev

# Clone Magic repository
git clone https://github.com/RTimothyEdwards/magic
cd magic

# Configure build
./configure

# Build Magic
make

# Install system-wide
sudo make install
```

`<img width="364" height="103" alt="Image" src="https://github.com/user-attachments/assets/4b18b7c7-c72c-4cc5-bc0a-e696ab934060" />`

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



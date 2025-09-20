
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

### **Stage O4-a – Physical Implementation**

* Map netlist to silicon:

  * Floorplan → Place → CTS → Route → DRC/LVS.
* Export **GDSII** layout for fab.
* **Deliverable:** Sign-off GDS.

---

### **Stage O4-b – Post-Silicon Validation**

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

Yosys: A framework for RTL synthesis supporting Verilog.

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

`<img width="374" height="301" alt="Image" src="https://github.com/user-attachments/assets/8075584b-4852-43fe-97cc-1cdad9de7d46" />

---

#### **Icarus Verilog — Simulation**

```bash
sudo apt-get update
sudo apt-get install iverilog
```

`<img width="356" height="129" alt="Image" src="https://github.com/user-attachments/assets/aaf2ea64-f7c0-44ea-bf6a-83a1ed6b7fbe" />



---

#### **GTKWave — Waveform Viewer**

GTKWave: A waveform viewer to visualize simulation outputs from Verilog/VHDL.

```bash
sudo apt-get update
sudo apt install gtkwave
```

`<img width="571" height="421" alt="Image" src="https://github.com/user-attachments/assets/9f33fff8-5386-4a0f-af7a-3a3cf656a5c5" />

---

#### **Ngspice — Analog / Mixed-Signal**

Ngspice: A mixed-level circuit simulator for analog/digital systems.

```bash
$ sudo apt update
$ sudo apt install ngspice
```

`<img width="364" height="103" alt="Image" src="https://github.com/user-attachments/assets/31f0222d-98f8-43c2-8704-b8fc0782bfcc" />

---

#### **Magic — Layout Editor**

Magic: A VLSI layout tool for editing and viewing IC layouts.

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

`<img width="1045" height="611" alt="Image" src="https://github.com/user-attachments/assets/46e4ee93-6672-41ee-926a-e305c5be8da7" />

---

#### **OpenLane — RTL → GDS**

OpenLane: An automated RTL-to-GDSII flow for digital ASIC design.

```bash
## 5. OpenLane

### Install Docker & Dependencies

```bash
# Update system
sudo apt-get update
sudo apt-get upgrade

# Install dependencies
sudo apt install -y build-essential python3 python3-venv python3-pip make git
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# Install Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io

# Verify Docker installation
sudo docker run hello-world

# Add user to Docker group
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot

# Verify again after reboot
docker run hello-world
Install OpenLane
bash
Copy code
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```

`<img width="541" height="35" alt="Image" src="https://github.com/user-attachments/assets/039289ac-7da0-48e0-a418-157c104dd831" />

</details>



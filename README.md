# Nexys4DDR-ddr2-mig
Design for using onboard DDR2 memory with Xilinx MIG IP on Nexys 4 DDR/Nexys A7 FPGA boards

# Nexys 4 DDR2 MIG Example Project

A comprehensive reference design demonstrating DDR2 memory usage with Xilinx Memory Interface Generator (MIG) IP on Nexys 4 DDR and Nexys A7 FPGA trainer boards.

 Quick Start

This project provides a working DDR2 memory controller implementation with:
- **Complete MIG IP configuration** for Nexys 4 DDR/A7 boards
- **Step-by-step setup guide** with detailed screenshots
- **Simulation testbench** with timing diagrams
- **Hardware-verified** memory read/write operations

Prerequisites

- **Hardware**: Nexys 4 DDR or Nexys A7 FPGA trainer board
- **Software**: Xilinx Vivado (2018.3.1+ recommended)
- **FPGA**: Artix-7 XC7A100T-1CSG324C
- **Memory**: MT47H64M16HR-25E DDR2 SDRAM (1Gb, x16)



 **Key Features**

- **300 MHz DDR2 operation** (3.33ns clock period)
- **16-bit data width** with data masking support
- **SRAM-like interface** for easy integration
- **Cross-clock domain synchronization** (CPU ↔ Memory clocks)
- **Comprehensive simulation** with waveform analysis
- **Hardware validation** with LED status indicators

 **Memory Interface Specifications**

| Parameter | Value |
|-----------|-------|
| Memory Type | DDR2 SDRAM |
| Memory Part | MT47H64M16HR-25E |
| Capacity | 1Gb (128MB) |
| Data Width | 16-bit |
| Operating Frequency | 300 MHz |
| PHY:Controller Ratio | 2:1 |
| Addressing | Byte-addressable |
| Supported Widths | 8, 16, 32, 64-bit transactions |

 **Getting Started**

### **1. Clone/Download Project**
git clone git clone git clone

In Vivado TCL Console
open_project mig_example.xpr

### **2. Open in Vivado**
In Vivado TCL Console
open_project mig_example.xpr

### **3. Generate Bitstream**
Synthesize and implement
launch_runs synth_1
wait_on_run synth_1
launch_runs impl_1 -to_step write_bitstream
wait_on_run impl_1

### **4. Program FPGA**
- Connect Nexys board via USB
- Power on and program with generated `.bit` file
- **LED[0]** will illuminate when memory test passes

##  **Memory Interface Signals**

// CPU Clock Domain Interface
input clk_cpu, // CPU clock (slower domain)
input [27:0] mem_addr, // Byte address
input [63:0] mem_d_to_ram, // Write data
output [63:0] mem_d_from_ram, // Read data
input [1:0] mem_transaction_width, // 0=8bit, 1=16bit, 2=32bit, 3=64bit
input mem_wstrobe, // Write strobe
input mem_rstrobe, // Read strobe
output mem_transaction_complete, // Operation complete
output mem_ready // Controller ready

text

## **Simulation Results**

The project includes comprehensive simulation showing:
- **MIG calibration sequence** (~65μs in simulation)
- **Write/Read transactions** with timing verification
- **Data integrity checking** via LFSR pattern matching
- **Cross-domain synchronization** behavior

### **Key Timing Characteristics:**
- **Memory training**: ~65μs (simulation) / ~10ms (hardware)
- **Transaction latency**: 3-8 clock cycles typical
- **Throughput**: Up to 600 MB/s (300MHz × 16-bit)

## ⚠ **Important Notes**

- **Clock Requirements**: Memory clock must be ≥3× CPU clock for cross-domain sync
- **Data Alignment**: Uses big-endian "left-justified" data alignment
- **Version Compatibility**: MIG IP configured for v4.2 (Vivado 2018.3.1)
- **Simulation Model**: Updated DDR2 model included (Xilinx default is outdated)



##  **Documentation**

- **[Complete Setup Guide](docs/Nexys-4-Onboard-DDR2-MIG-Configuration.pdf)**: Detailed MIG IP configuration walkthrough
- **Xilinx UG586**: 7 Series FPGAs Memory Interface Solutions User Guide
- **Board Reference Manual**: Nexys 4 DDR/A7 documentation

##  **Technical Deep Dive**

### **MIG IP Configuration Summary:**
- **Controller**: Strict ordering mode for predictable behavior
- **Clocking**: 200MHz input, 300MHz DDR2, 150MHz controller
- **Termination**: 50Ω internal termination
- **Banks**: Optimized for Nexys board pin layout
- **Debug**: ChipScope disabled for resource efficiency

### **Memory Map:**
- **Address Space**: 0x00000000 - 0x07FFFFFF (128MB)
- **Byte Addressing**: Full byte-level granularity
- **Burst Support**: Configurable transaction widths

##  **Contributing**

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Test thoroughly on hardware
4. Submit pull request with detailed description

[Nexys 4 Onboard DDR2 MIG Configuration.pdf](https://github.com/user-attachments/files/22323161/Nexys.4.Onboard.DDR2.MIG.Configuration.pdf)





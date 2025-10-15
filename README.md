# 7T SRAM Schematic Analysis

## Overview
This document provides a detailed analysis of the 7T (7-Transistor) SRAM cell schematic shown in the Virtuoso Schematic Editor.

## Circuit Architecture

### Basic Structure
The 7T SRAM cell is a modified version of the conventional 6T SRAM, featuring an additional transistor to improve read stability and reduce power consumption during read operations.

### Key Components Visible in Schematic

#### 1. **Storage Core (Cross-Coupled Inverters)**
- **Two PMOS transistors** (upper devices) forming the pull-up network
- **Two NMOS transistors** (lower devices) forming the pull-down network
- These four transistors create two back-to-back inverters that form a bistable latch
- Stores one bit of data (either '0' or '1')

#### 2. **Access Transistors**
- **Two NMOS access transistors** connected to bitlines (bl and bl̄)
- Controlled by wordline (wl) signal
- Enable read and write operations to the storage nodes

#### 3. **Additional 7th Transistor**
- The distinguishing feature of 7T SRAM
- Typically a separate read transistor or a buffer transistor
- Isolates the read path from the storage nodes
- Improves read stability by preventing read disturb issues

### Signal Connections

#### Power Supply
- **VDD**: Positive power supply rail (top)
- **VSS/GND**: Ground rail (bottom)

#### Control Signals
- **wl (Word Line)**: Activates the cell for read/write operations
- **wl2u**: Secondary control signal (possibly for the 7th transistor)

#### Data Lines
- **bl (Bit Line)**: Primary bitline for data transfer
- **bl̄ (Bit Line Bar)**: Complementary bitline
- **rbl (Read Bit Line)**: Dedicated read bitline (if separate read port exists)

#### Storage Nodes
- **nmos1, pmos1**: Internal storage nodes (left inverter output)
- **nmos1̄, pmos1̄**: Complementary storage nodes (right inverter output)

### Circuit Operation

#### Write Operation
1. Wordline (wl) is asserted HIGH
2. Access transistors turn ON
3. Bitlines (bl and bl̄) are driven with complementary data
4. Data is forced into storage nodes, overwriting previous content
5. Cross-coupled inverters latch the new data

#### Read Operation
1. Bitlines are precharged to VDD
2. Wordline is asserted
3. One bitline discharges through access transistor and storage node
4. Sense amplifier detects voltage difference between bl and bl̄
5. 7th transistor may provide buffered read path to prevent disturbing stored data

### Design Considerations

#### Advantages of 7T SRAM
- **Improved Read Stability**: Additional transistor prevents read disturb
- **Lower Read Power**: Separate read path reduces unnecessary toggling
- **Better Noise Margins**: Storage nodes less affected during reads

#### Critical Parameters
- **Cell Ratio (CR)**: Ratio of pull-down to access transistor width
- **Pull-up Ratio (PR)**: Ratio of pull-down to pull-up transistor width
- **Beta Ratio**: Overall strength ratio for write/read operations

### Schematic Properties (from Property Editor)
- **Library**: 7t_SRAM
- **Cell**: 7t_sram
- **View**: schematic
- **Mode**: editable
- **Last Saved**: Sat Apr 20
- **Units**: inch (display units)

## Design Flow Integration
This schematic represents the circuit-level design that will be:
1. Simulated for functionality and timing
2. Used to create the physical layout (shown in second image)
3. Verified through LVS (Layout vs Schematic) checks
4. Characterized for performance metrics

## Notes
- The schematic shows careful attention to symmetry for balanced operation
- Transistor sizing is critical for proper functionality
- All nodes are properly labeled for easy debugging and analysis

![WhatsApp Image 2025-10-13 at 10 59 28](https://github.com/user-attachments/assets/08761852-411e-472b-ae06-e4e3bb12607f)

# 7T SRAM Layout Analysis

## Overview
This document analyzes the physical layout implementation of the 7T SRAM cell in Cadence Virtuoso Layout Suite XL.

## Layout Structure

### Layer Organization (from Layers Panel)

#### Active Layers Visible
1. **Nwell (pin)** - Yellow highlight
   - N-type well for PMOS transistors
   - Houses the pull-up devices

2. **Pwell (pin)** - Layer for PMOS devices
   - P-type substrate/well for NMOS transistors

3. **Nwell (drw)** - Drawing layer for N-wells
4. **Oxide (drw)** - Field oxide regions
5. **Poly (drw)** - Polysilicon gates
6. **Nimp (drw)** - N+ implant regions
7. **Pimp (drw)** - P+ implant regions
8. **Cont (drw)** - Contact cuts
9. **Metal layers** - Interconnect routing

### Physical Layout Features

#### Main Cell Structure (Orange Boundary)
- **Rectangular cell boundary**: Defines the SRAM cell area
- **Compact layout**: Optimized for area efficiency
- **Symmetrical design**: Critical for balanced electrical characteristics

#### Transistor Layout
The layout shows:
- **Active regions** (blue/white rectangles): Define source/drain areas
- **Polysilicon gates** (vertical bars): Cross the active regions to form transistors
- **Contact cuts** (small squares): Connect different metal layers

#### Metal Routing
- **bl and bl̄ (bitlines)**: Vertical metal routes on left and right
- **Horizontal connections**: Link internal nodes
- **Power rails**: VDD (top) and VSS (bottom) typically run horizontally

### Layout Hierarchy

#### Current View Settings
- **Palette**: Tool palette for drawing and editing
- **Layers panel**: Shows all available process layers
- **Filter**: "Nwell pin" currently selected
- **Display mode**: Classic layout view
- **Grid**: Visible grid for alignment (gpdk180 technology)

### Design Rules and Constraints

#### Spacing and Width Rules
The layout must satisfy:
- Minimum transistor width/length ratios
- Metal-to-metal spacing requirements
- Via/contact enclosure rules
- N-well to active spacing
- Poly-to-active extension rules

#### Critical Dimensions
- **Cell height**: Determined by power rail spacing
- **Cell width**: Optimized for minimum area while meeting design rules
- **Transistor sizing**: Matches schematic W/L ratios

### Layer-by-Layer Breakdown

#### Bottom Layers (Substrate/Wells)
- **Substrate**: P-type silicon base
- **N-well**: Region for PMOS transistors (top half)
- **P-well/substrate**: Region for NMOS transistors (bottom half)

#### Active Device Layers
- **Active (OD)**: Defines transistor source/drain regions
- **Poly**: Forms transistor gates
- **Implants**: N+ for NMOS, P+ for PMOS regions

#### Contact and Via Layers
- **Contact (CO)**: Connects poly/active to Metal1
- **Via1**: Connects Metal1 to Metal2
- **Via2**: Connects Metal2 to Metal3 (if needed)

#### Metal Layers
- **Metal1**: Local interconnections, power rails
- **Metal2**: Bitlines, longer routes
- **Metal3+**: Global routing (if used)

### Layout Design Considerations

#### Area Optimization
- Transistors arranged for minimum cell area
- Shared source/drain regions where possible
- Efficient use of metal layers

#### Performance Optimization
- Short interconnect lengths for speed
- Wide power rails for low resistance
- Proper shielding of sensitive nodes

#### Manufacturability
- All design rules satisfied (DRC clean)
- Proper antenna ratios
- Correct layer overlaps and enclosures

### Verification Checks Required

#### Physical Verification
1. **DRC (Design Rule Check)**
   - Verifies all geometric rules
   - Checks spacing, width, enclosure
   - Ensures manufacturability

2. **LVS (Layout vs Schematic)**
   - Extracts netlist from layout
   - Compares with schematic netlist
   - Verifies circuit connectivity

3. **ERC (Electrical Rule Check)**
   - Checks for electrical issues
   - Verifies antenna rules
   - Checks well/substrate connections

#### Parasitic Extraction
- **RC extraction**: Captures resistance and capacitance
- **Back-annotation**: Used for accurate timing simulation
- **Post-layout simulation**: Verifies performance with parasitics

### Layout Coordinates
From status bar:
- **Current position**: X: 13.9650, Y: -6.6450
- **Selection**: Multiple objects selected (Select:0)
- **Units**: Layout units (typically microns or nanometers)

### Technology Information
- **Technology**: gpdk180 (180nm Generic PDK)
- **Grid**: Snap grid visible for alignment
- **Ruler markers**: For distance measurements

## Integration with Schematic

### Correspondence
Each element in the schematic has a physical representation:
- Schematic transistor → Layout active + poly gate
- Schematic wire → Layout metal trace
- Schematic pin → Layout pin with metal/text

### Instance Matching
The layout instance name must match the schematic for LVS:
- Property match between schematic and layout
- Pin names must be identical
- Device multipliers properly reflected

## Array Integration

### For Memory Array
This cell will be:
- **Replicated** in rows and columns
- **Abutted** with neighboring cells
- **Connected** to shared bitlines and wordlines
- **Optimized** for regular array structure

### Array-Level Considerations
- Power rail continuity across cells
- Bitline routing through cell
- Wordline connection points
- Well continuity for latch-up prevention

## Notes
- Layout is more compact than typical 6T SRAM due to optimized 7T design
- Layer colors in viewer may differ from actual fabrication layers
- Orange boundary indicates cell extent for array placement
- Symmetry is maintained for electrical balance

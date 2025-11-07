This document was created by GitHub A.I. Read with caution...

# BASIC Stamp Halloween Prop Controllers

A collection of PBASIC programs for controlling Halloween animatronics and special effects using Parallax BASIC Stamp microcontrollers, primarily with EFX-Tek Prop-1 controllers.

## Overview

This repository contains controller programs for various Halloween props and effects, ranging from simple sequencers to complex multi-prop coordination systems. The code is designed to run on BASIC Stamp modules (BS1, BS2) and interfaces with external devices like RC4 relay controllers, PIR sensors, and various output devices.

## Hardware Platforms

### BASIC Stamp Models
- **BS1** - BASIC Stamp 1 (most programs)
- **BS2** - BASIC Stamp 2 (select programs like Police.bs2)

### Common Hardware Interfaces
- **EFX-Tek Prop-1 Controller** - Primary platform for most programs
- **RC4 Relay Controllers** - 4-relay modules for high-current switching
- **PIR Motion Sensors** - Trigger inputs via PIN6/PIN7
- **Various Output Devices** - LEDs, solenoids, fog machines, lights

## Program Categories

### Core Sequencer Engines
- **`Sequencer.BS1`** - Basic single-sequence prop controller
- **`Dual-Sequencer-MaxOuts.BS1`** - Dual independent sequence controller
- **`Dual-Sequencer-MaxOuts-RC4.BS1`** - Dual sequencer with RC4 relay support
- **`MultiSequencer.bs1`** - Multi-tasking sequencer engine
- **`MultiSequencer-1.bs1`** - Enhanced multi-sequence controller

### Specialized Prop Controllers

#### Gas Chamber Effects
- **`GasChamber.BS1`** - Gas chamber lighting and fog effects
- **`GasChamber_old.BS1`** - Previous version of gas chamber controller
- **`MultiGasChamberNurse.bs1`** - Multi-prop gas chamber with nurse character
- **`MultiGasChamberPopUp.bs1`** - Gas chamber with popup scares (multiple versions)

#### Rat & Creature Effects  
- **`Rats.bs1`** - Rat animatronic controller
- **`RatSequencer.bs1`** - Sequenced rat movement controller
- **`MultiRats.BS1`** - Multiple rat coordination system

#### Other Specialized Effects
- **`Police.bs2`** - Police light flasher patterns (BS2)
- **`Barrel_Blast_Seq.BS1`** - Barrel explosion sequence
- **`DeskPopup.bs1`** - Desktop popup scare mechanism

### Test & Utility Programs
- **`RC4Test.bs1`** - RC4 relay controller test/diagnostic program
- **`RC4Lights.bs1`** - RC4-based lighting controller
- **`Test3in4Out.BS1`** - 3-input, 4-output test program
- **`ForNathaniel.bs1`** - Custom program (specific user request)

## Key Features

### Advanced Sequencing
- **EEPROM-Based Sequences** - Sequences stored in EEPROM tables
- **Dual Timer Support** - Simultaneous independent prop control
- **Multi-Tasking** - Multiple sequences running concurrently
- **Flexible Timing** - Configurable delay resolution (typically 100ms units)

### RC4 Relay Integration
Many programs support RC4 4-relay controllers for high-current switching:
```pbasic
SYMBOL  rc4Sio          = 5         ' RC4 control pin
SYMBOL  rc4Baud         = OT2400     ' Communication baud rate  
SYMBOL  rc4Addr         = %11        ' RC4 address (0-3)
```

### Trigger System
Programs typically use two trigger inputs:
```pbasic
SYMBOL  Trigger1        = PIN7       ' Primary trigger (usually PIR)
SYMBOL  Trigger2        = PIN6       ' Secondary trigger
```

### Sequence Table Format
EEPROM sequences use a standardized format:
```pbasic
EEPROM (output_pattern, timing_value)
' Bit 7 = End of sequence flag
' Bit 6 = RC4 control flag (when applicable)
' Bits 0-5 = Output pattern or RC4 relay states
```

## Programming Patterns

### Common Structure
Most programs follow this pattern:
1. **Header Section** - File info, author, revision history
2. **I/O Definitions** - Pin assignments and symbolic names
3. **Constants** - Timing values, addresses, flags
4. **Variables** - Memory allocation for sequencers
5. **EEPROM Data** - Sequence tables and configuration
6. **Initialization** - Setup pins and reset pointers
7. **Main Loop** - Trigger monitoring and sequence execution
8. **Subroutines** - RC4 communication, utility functions

### Timing System
```pbasic
SYMBOL  DelayRes        = 100       ' 100ms resolution
' Timer values in EEPROM are multiplied by DelayRes
' Example: value of 10 = 1000ms (1 second) delay
```

### Reset Behavior
```pbasic
SYMBOL  ResetDelay      = 50        ' 5-second reset period
' Prevents re-triggering immediately after sequence ends
```

## Development Evolution

### Version History Pattern
Programs include detailed revision histories:
- **Initial versions** - Basic sequencing functionality
- **RC4 Integration** - Added relay controller support (2005)
- **Multi-tasking** - Concurrent sequence capabilities
- **Optimization** - Code size and timing improvements

### Author Collaboration
- **Jon Williams (Parallax EFX)** - Original sequencer frameworks
- **Allen Huffman** - Extensions, RC4 integration, multi-tasking
- **EFX-Tek Community** - Testing and application feedback

## Hardware Configuration

### Typical Prop-1 Setup
```
PIN0-PIN5: Output pins for direct device control
PIN6: Trigger2 input (active low)
PIN7: Trigger1 input (active low) 
PIN5: RC4 serial communication (when used)
```

### RC4 Relay Controller
```
Address: Jumper-selectable (0-3)
Relays: 4 high-current SPDT relays
Control: Serial commands via RC4 protocol
```

## Usage Examples

### Basic Prop Control
1. Connect PIR sensor to PIN7 (Trigger1)
2. Connect prop outputs to PIN0-PIN5
3. Download appropriate sequencer program
4. Customize EEPROM sequence table for your prop timing

### RC4 Relay Control
1. Connect RC4 controller to PIN5 (serial)
2. Set RC4 address jumpers
3. Use RC4-compatible program
4. Set RC4 control bit (Bit 6) in sequence data

### Multi-Prop Coordination
1. Use MultiSequencer variants
2. Define separate sequences for each prop
3. Configure independent trigger inputs
4. Coordinate timing via shared sequence tables

## File Extensions
- **`.BS1`** - BASIC Stamp 1 source code
- **`.bs1`** - BASIC Stamp 1 source code (lowercase)
- **`.bs2`** - BASIC Stamp 2 source code  
- **`.TXT`** - Documentation or text versions of source

## Development Tools
- **BASIC Stamp Editor** - Parallax development environment
- **EFX-Tek Prop-1 Controller** - Target hardware platform
- **PIR Sensors** - Motion detection for triggers
- **RC4 Controllers** - Relay interface modules

---

*These programs represent practical Halloween automation solutions developed for the maker/haunter community, demonstrating embedded programming techniques for real-world animatronic and special effects control.*

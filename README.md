# VLSI RTL Design and Synthesis

This repository presents my practical work completed during the VLSI RTL Design and Synthesis training. The exercises cover the complete progression from Verilog RTL development to synthesized and technology-mapped hardware.

The training includes RTL coding, testbench development, functional simulation, waveform analysis, synthesis, Boolean optimization, sequential logic, timing libraries, hierarchical and flattened synthesis, standard-cell mapping, Gate-Level Simulation, RTL coding practices, latch inference, generate constructs, MUX/DEMUX design, and arithmetic hardware implementation.

## The practical flow gradually moves from simple RTL examples toward optimized, technology-specific hardware using open-source EDA tools and the SKY130 standard-cell library. The individual modules establish the foundation of RTL design, introduce technology-aware synthesis and sequential circuits, explore optimization techniques, verify synthesized designs through GLS, and finally examine how different RTL constructs influence the generated hardware.

# Module 1 – Verilog RTL Design, Simulation and Synthesis Fundamentals

Module 1 established the basic RTL development and verification flow using Verilog HDL. A 2-to-1 multiplexer was used as the main practical example to understand how a hardware design is described, tested, simulated, analyzed through waveforms, and synthesized into a hardware-oriented netlist.

## Work Completed

* Introduction to Verilog RTL design
* Understanding RTL modules and hardware descriptions
* Understanding the Design Under Test (DUT)
* Testbench creation
* Combinational logic implementation
* 2-to-1 multiplexer design
* MUX input-selection behavior
* Writing synthesizable Verilog RTL
* Applying simulation stimulus
* Functional simulation using Icarus Verilog
* VCD waveform generation
* Waveform inspection using GTKWave
* Verification of MUX functionality
* Introduction to RTL synthesis
* Yosys synthesis flow
* RTL parsing and synthesis
* Technology-independent logic representation
* Introduction to standard-cell libraries
* Liberty library usage
* ABC-based technology mapping
* SKY130 standard-cell mapping
* Synthesized netlist generation
* Structural netlist inspection
* Understanding RTL-to-hardware transformation

The practical flow followed in this module was:

```text
Verilog RTL
     |
     v
Testbench
     |
     v
Icarus Verilog
     |
     v
Simulation
     |
     v
VCD Generation
     |
     v
GTKWave
     |
     v
Waveform Verification
     |
     v
Yosys Synthesis
     |
     v
Technology Mapping
     |
     v
Synthesized Netlist
```

## The 2-to-1 MUX provided a simple starting point for understanding the relationship between RTL code, simulation results and the synthesized hardware representation. The module also established the basic tool flow used throughout the remaining training.

# Module 2 – Timing Libraries, Hierarchical Synthesis and Sequential Logic

Module 2 extended the basic RTL-to-netlist flow into technology-specific implementation. The work concentrated on the SKY130 standard-cell library, PVT operating conditions, hierarchical and flattened synthesis, flip-flop design, reset/set behavior, simulation and standard-cell mapping.

## Work Completed

* Study of SKY130 `.lib` timing libraries
* Understanding standard-cell characterization
* Process, Voltage and Temperature (PVT) corners
* Typical process conditions
* Supply-voltage information
* Temperature conditions
* Understanding timing-related library information
* Hierarchical synthesis
* Flattened synthesis
* Comparison of hierarchical and flattened designs
* Understanding design hierarchy and modularity
* D Flip-Flop implementation
* Positive-edge-triggered sequential logic
* Asynchronous reset
* Asynchronous set
* Synchronous reset
* Comparison of reset and set behavior
* Sequential RTL simulation
* Icarus Verilog simulation
* GTKWave waveform analysis
* Yosys synthesis
* `dfflibmap`
* ABC technology mapping
* Mapping RTL flip-flops to SKY130 cells
* Standard-cell netlist generation
* Synthesized design visualization

One of the timing libraries studied was:

```text
sky130_fd_sc_hd__tt_025C_1v80.lib
```

The library naming convention was examined to understand the operating corner:

```text
tt      → Typical process
025C    → 25°C
1v80    → 1.8 V supply
```

The module also compared hierarchical and flattened synthesis. Hierarchical synthesis retains the modular structure of the RTL, while flattened synthesis combines the design into a more unified representation for whole-design optimization.

Different flip-flop coding styles were implemented and analyzed, including asynchronous reset, asynchronous set and synchronous reset.

The technology-aware synthesis flow can be summarized as:

```text
RTL Description
      |
      v
Yosys Synthesis
      |
      v
Sequential Logic
      |
      v
dfflibmap
      |
      v
ABC Technology Mapping
      |
      v
SKY130 Standard Cells
      |
      v
Technology-Mapped Netlist
```

This module demonstrated how a technology-independent RTL flip-flop can ultimately become a specific standard-cell implementation through synthesis and library mapping.

---

# Module 3 – Combinational and Sequential Logic Optimization

Module 3 focused on how Yosys analyzes RTL and simplifies hardware while maintaining the required functionality. The work included both combinational and sequential optimization, Boolean simplification, constant propagation, redundant logic removal, register optimization and sequential dependency analysis.

## Work Completed

### Combinational Optimization

* Introduction to synthesis optimization
* Boolean logic analysis
* Combinational logic simplification
* Yosys optimization
* `opt` command
* Technology mapping
* SKY130 standard-cell implementation
* Multi-level logic optimization
* Analysis of `opt_check`
* Analysis of `opt_check2`
* Analysis of `opt_check3`
* Synthesized circuit visualization using `show`
* Comparison of RTL structure and optimized hardware

The `opt_check` example demonstrated a simple AND operation that could be mapped to a SKY130 AND2 standard cell.

The multi-level `opt_check3` example demonstrated that several RTL levels can be reduced by synthesis into an equivalent technology-specific implementation. In this case, the optimized logic was represented using a SKY130 AND3 cell.

The general combinational optimization process was:

```text
RTL Expression
      |
      v
Logic Analysis
      |
      v
Boolean Simplification
      |
      v
Optimization
      |
      v
Technology Mapping
      |
      v
Optimized Standard-Cell Logic
```

### Sequential Optimization

The sequential portion of the module studied:

* Constant propagation
* Constant-driven sequential logic
* Reset simplification
* Redundant flip-flop identification
* Register optimization
* Sequential dependency analysis
* `dff_const1`
* `dff_const2`
* `dff_const3`
* `dff_const4`
* `dff_const5`
* `opt_clean`
* `stat`
* `show`
* SKY130 technology mapping

The five sequential examples demonstrated different optimization situations. Some registers could become functionally redundant because their values were constant, while other registers had to remain because their clock-to-clock dependencies affected the behavior of the design.

The sequential optimization flow was:

```text
RTL Verilog
     |
     v
Read RTL
     |
     v
Yosys Synthesis
     |
     v
Sequential Analysis
     |
     v
Constant Propagation
     |
     v
Redundant Logic Removal
     |
     v
Register Optimization
     |
     v
Dependency Analysis
     |
     v
Technology Mapping
     |
     v
Optimized Netlist
```

A major lesson from this module was that synthesis does not simply reproduce the RTL structure. It analyzes the actual behavior and removes hardware that is unnecessary while preserving required state and timing relationships.

---

# Module 4 – Gate-Level Simulation and Synthesis-Simulation Analysis

Module 4 concentrated on post-synthesis verification through Gate-Level Simulation and examined how Verilog coding style can affect simulation behavior. The module compared RTL simulation with synthesized gate-level behavior and studied possible synthesis-simulation mismatches.

## Work Completed

* Introduction to Gate-Level Simulation (GLS)
* RTL versus gate-level simulation
* Synthesis-simulation mismatch analysis
* 2-to-1 MUX using the ternary operator
* SKY130 MUX standard-cell mapping
* RTL MUX simulation
* Gate-level netlist simulation
* RTL and GLS waveform comparison
* Incomplete sensitivity-list analysis
* Correct use of `always @(*)`
* Blocking assignment behavior
* Blocking assignment ordering
* Non-blocking assignments
* Procedural execution behavior
* Sequential RTL coding practices
* Technology-specific standard-cell analysis
* Post-synthesis verification

A ternary MUX was described using:

```verilog
assign y = sel ? i1 : i0;
```

After synthesis and technology mapping, the MUX could be represented using the SKY130 standard cell:

```text
sky130_fd_sc_hd__mux2_1
```

This demonstrated the transition from a compact RTL description to a technology-specific hardware implementation.

The Gate-Level Simulation flow was:

```text
RTL Design
     |
     v
RTL Simulation
     |
     v
Yosys Synthesis
     |
     v
Technology Mapping
     |
     v
Gate-Level Netlist
     |
     v
Gate-Level Simulation
     |
     v
Waveform Analysis
     |
     v
RTL vs GLS Comparison
     |
     v
Final Verification
```

The module also demonstrated how an incomplete sensitivity list can prevent a combinational block from responding to changes in all relevant inputs. Blocking-assignment ordering was studied as another source of unexpected simulation behavior.

The general RTL coding guideline studied was:

```text
Combinational Logic → Blocking =
Sequential Logic    → Non-blocking <=
```

This distinction helps maintain predictable simulation and synthesis behavior.

The central verification objective was:

```text
RTL Behavior
     |
     v
   MATCH
     |
     v
Gate-Level Behavior
```

The module therefore reinforced the importance of checking the synthesized implementation rather than relying only on pre-synthesis RTL simulation.

---

# Module 5 – RTL Constructs, Latch Inference and Hardware Generation

Module 5 examined how different Verilog constructs are interpreted as hardware during synthesis. The practical work covered `if`, `case`, `generate`, MUX and DEMUX structures, incomplete assignments, latch inference and Ripple Carry Adder construction.

## Work Completed

* Understanding combinational RTL constructs
* `if`-based logic
* `case`-based logic
* Case-based combinational synthesis
* MUX implementation
* DEMUX implementation
* `demux_case`
* Incomplete `if` statements
* Latch inference
* Analysis of incomplete assignments
* `incomp_if`
* `incomp_if2`
* Partial `case` assignment
* `partial_case_assign`
* MUX using `generate`
* Repeated hardware generation
* Scalable RTL structures
* `genvar` and generate concepts
* Ripple Carry Adder implementation
* Full-adder stage construction
* Carry propagation
* RTL simulation
* GTKWave waveform analysis
* Yosys synthesis
* SKY130 technology mapping
* Synthesized hardware inspection

The module demonstrated that `case` and `if` statements are hardware descriptions rather than software instructions. During synthesis, Yosys analyzes the conditions and converts them into corresponding combinational logic.

### Latch Inference

One of the important concepts was the relationship between incomplete combinational assignments and latch generation.

The process can be represented as:

```text
Incomplete Assignment
        |
        v
No New Output Value
        |
        v
Previous Value Must Be Retained
        |
        v
Storage Required
        |
        v
Latch Inference
```

The module also examined partial `case` assignments and showed how providing a default assignment can make the intended combinational behavior explicit.

### Generate-Based Hardware

The `generate` construct was studied as a method for describing repeated hardware structures.

```text
Generate Construct
        |
        v
Repeated RTL Structure
        |
        v
Multiple Hardware Instances
        |
        v
Scalable Hardware
```

This approach is useful for multi-bit circuits and other designs containing repeated logic.

### Ripple Carry Adder

The Ripple Carry Adder experiment demonstrated how a multi-bit arithmetic circuit can be assembled from individual full-adder stages.

```text
Full Adder
    |
    v
Multiple Full Adders
    |
    v
Carry Propagation
    |
    v
Ripple Carry Adder
    |
    v
Multi-bit Addition
```

Each full adder receives two data inputs and a carry input and generates a sum and carry output. The carry is then passed to the following stage.

The experiment demonstrated the usefulness of modular RTL design and reusable hardware blocks.

The overall Module 5 flow was:

```text
RTL Constructs
      |
      +----------+----------+
      |          |          |
      v          v          v
     IF         CASE     GENERATE
      |          |          |
      v          v          v
Combinational  MUX/DEMUX  Repeated
   Logic        Logic     Hardware
      |          |          |
      +----------+----------+
                 |
                 v
          RTL Simulation
                 |
                 v
             GTKWave
                 |
                 v
          Yosys Synthesis
                 |
                 v
        Technology Mapping
                 |
                 v
        Synthesized Hardware
```

This module reinforced the connection between RTL coding style and the hardware structure produced by synthesis.

---

# Overall Training Coverage

Across Modules 1–5, the training developed a progressive understanding of the RTL-to-hardware implementation process.

```text
RTL DESIGN
     |
     v
VERILOG CODING
     |
     v
TESTBENCH DEVELOPMENT
     |
     v
FUNCTIONAL SIMULATION
     |
     v
VCD GENERATION
     |
     v
GTKWAVE ANALYSIS
     |
     v
YOSYS SYNTHESIS
     |
     v
LOGIC OPTIMIZATION
     |
     v
SEQUENTIAL OPTIMIZATION
     |
     v
TECHNOLOGY MAPPING
     |
     v
SKY130 STANDARD CELLS
     |
     v
GATE-LEVEL NETLIST
     |
     v
GATE-LEVEL SIMULATION
     |
     v
RTL vs GLS VERIFICATION
```

The modules collectively progress from basic RTL design and simulation in Module 1, through technology libraries and sequential logic in Module 2, optimization in Module 3, post-synthesis verification and coding semantics in Module 4, and finally RTL construct interpretation, latch inference, generated hardware and arithmetic structures in Module 5.

---

# Key Tools and Technologies

**Verilog HDL** – Used for describing digital hardware at RTL level.

**Icarus Verilog** – Used for compiling and simulating RTL and, where applicable, gate-level designs.

**GTKWave** – Used to inspect VCD waveforms and analyze signal behavior.

**Yosys** – Used for RTL synthesis, optimization and synthesized circuit generation.

**ABC** – Used for logic optimization and technology mapping.

**SKY130 Standard-Cell Library** – Used as the target technology for mapping synthesized logic.

**Liberty `.lib` Files** – Used to provide standard-cell functionality and technology characterization information.

**Graphviz** – Used in the sequential optimization work to visualize synthesized circuits.

## The modules specifically use these tools as part of the practical RTL-to-hardware workflow.

# Overall Learning Outcomes

Through the completion of Modules 1–5, I developed practical knowledge of:

* Verilog RTL design
* Combinational logic
* Sequential logic
* RTL module structure
* Testbench development
* Functional simulation
* VCD waveform generation
* GTKWave analysis
* RTL-to-netlist conversion
* Yosys synthesis
* Liberty timing libraries
* PVT corner interpretation
* Hierarchical synthesis
* Flattened synthesis
* D Flip-Flop design
* Asynchronous reset
* Asynchronous set
* Synchronous reset
* Standard-cell mapping
* `dfflibmap`
* ABC technology mapping
* Boolean optimization
* Constant propagation
* Redundant logic removal
* Reset simplification
* Register optimization
* Sequential dependency analysis
* `opt_clean`
* `stat`
* `show`
* RTL coding semantics
* Sensitivity-list behavior
* Blocking assignments
* Non-blocking assignments
* Ternary MUX implementation
* Gate-Level Simulation
* RTL versus GLS verification
* Synthesis-simulation mismatch analysis
* `if` and `case` constructs
* MUX and DEMUX implementation
* Incomplete combinational assignments
* Latch inference
* Partial case assignments
* `generate` constructs
* Repeated hardware generation
* Ripple Carry Adder design
* Full-adder based modular design
* Synthesized hardware inspection

These concepts collectively demonstrate how RTL descriptions are analyzed, simulated, optimized and converted into technology-specific hardware.

---

# Final Summary

The Modules 1–5 training provided a practical foundation in the complete Verilog RTL-to-gate-level design process. The work began with fundamental combinational RTL design and simulation, then progressed toward technology-aware synthesis, timing libraries, sequential logic, optimization, coding semantics, Gate-Level Simulation and synthesis verification.

The final stages introduced more advanced RTL construction concepts, including incomplete assignments and latch inference, case-based MUX/DEMUX designs, generate-based repeated structures and Ripple Carry Adders.

The complete learning path can be summarized as:

```text
DESIGN
   ↓
CODE
   ↓
SIMULATE
   ↓
VERIFY
   ↓
SYNTHESIZE
   ↓
OPTIMIZE
   ↓
TECHNOLOGY MAP
   ↓
GENERATE NETLIST
   ↓
GATE-LEVEL SIMULATION
   ↓
COMPARE
   ↓
FINAL VERIFICATION
```

The major outcome of the training was an improved practical understanding of how a Verilog RTL description becomes synthesized hardware and how different coding decisions influence the resulting implementation.

The five modules collectively demonstrated that RTL design is not limited to writing functional code. A designer must also understand simulation semantics, synthesis transformations, optimization, standard-cell technology, sequential behavior, coding completeness and post-synthesis verification.

---

# Image Placement Recommendations

For the **main repository README**, it is better to use a small number of representative images rather than copying every figure from the five individual module READMEs.

### Module 1

Recommended images:

1. **2-to-1 MUX RTL/design diagram**
2. **GTKWave MUX waveform**
3. **Yosys synthesis or RTL-to-netlist flow**

The Module 1 README already contains dedicated locations for the overview, testbench, waveform, simulation flow and synthesis-flow images.

### Module 2

Recommended images:

1. **SKY130 Liberty/timing library screenshot**
2. **D Flip-Flop waveform**
3. **Yosys standard-cell mapping result**

These represent the major topics of timing libraries, sequential logic and technology mapping.

### Module 3

Recommended images:

1. **Combinational optimization schematic**
2. **Sequential optimization result**
3. **Optimized SKY130 netlist/schematic**

The strongest visual evidence is the comparison between the original RTL structure and the simplified synthesized structure.

### Module 4

Recommended images:

1. **RTL MUX waveform**
2. **Gate-Level Simulation waveform**
3. **RTL vs GLS comparison**

These images directly communicate the module's main objective of verifying synthesized hardware.

### Module 5

Recommended images:

1. **Case/MUX/DEMUX schematic**
2. **Latch inference result**
3. **Ripple Carry Adder schematic**

These provide a good visual representation of RTL constructs, synthesis behavior and arithmetic hardware.

### Recommended Overall README Image Count

For a clean GitHub repository README, I recommend approximately:

```text
Module 1 → 2 images
Module 2 → 2 images
Module 3 → 2 images
Module 4 → 2 images
Module 5 → 2 images

Total → 10 representative images
```

Keep the detailed screenshots inside the individual `Module 1`, `Module 2`, `Module 3`, `Module 4`, and `Module 5` README files, while the main repository README should show only the most important results.

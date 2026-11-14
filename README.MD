# Verilog HDL

This repository brings together concise explanations, synthesizable RTL examples, and simulation testbenches. It is intended as a growing reference for learning digital design, understanding RTL behavior, and practicing functional verification.

Verilog is a hardware description language (HDL) used to describe and model digital systems. It allows designers to express hardware at different abstraction levels without tying the RTL description to a specific fabrication technology. Designs can be simulated and verified before implementation, and synthesizable RTL can be mapped to hardware using appropriate design tools.

**What this reference covers**
- Verilog module structure, ports, nets, registers, and vectors.
- Behavioral, dataflow, structural, gate-level, and switch-level modeling concepts.
- Operators, procedural assignments, and testbench fundamentals.
- Combinational circuits such as adders, subtractors, and multiplexers (2:1, 4:1, 8:1, 16:1, and hierarchical MUX designs).
- Sequential circuits such as latches, flip-flops, flip-flop conversions, shift registers, and synchronous/asynchronous counters.
- Finite State Machines (FSMs) including sequence detectors, skip counters, electronic locks, and vending machine controllers.
- Testbenches and waveform dumping for simulation.

---

# Contents

## 1. Introduction
1.1 [Verilog Basic Modeling Structure](#11-verilog-basic-modeling-structure)  
1.2 [Verilog Data Types](#12-verilog-data-types)  
1.3 [Components of a Verilog Module](#13-components-of-a-verilog-module)  
1.4 [Levels of Abstraction](#14-levels-of-abstraction)  
1.5 [AND Gate: Modeling Style Examples](#15-and-gate-modeling-style-examples)  
1.6 [Verilog Operators — Quick Reference](#16-verilog-operators--quick-reference)  
1.7 [Sequential Logic: Latch vs Flip-Flop](#17-sequential-logic-latch-vs-flip-flop)  
1.8 [Blocking vs Non-Blocking Assignments](#18-blocking-vs-non-blocking-assignments)  
1.9 [Testbench Writing](#19-testbench-writing)  
1.10 [begin-end vs fork-join](#110-begin-end-vs-fork-join)  
1.11 [initial, $display and $monitor](#111-initial-display-and-monitor)  

## 2. Verilog Codes
2.1 [Half Adder](#21-half-adder)  
2.2 [Full Adder](#22-full-adder)  
    - 2.2.1 [Gate-Level Full Adder](#221-gate-level-full-adder)  
    - 2.2.2 [Structural Full Adder (Using Half Adders)](#222-structural-full-adder-using-half-adders)  
2.3 [4-Bit Ripple Carry Adder](#23-4-bit-ripple-carry-adder)  
2.4 [Half Subtractor](#24-half-subtractor)  
2.5 [Full Subtractor](#25-full-subtractor)  
2.6 [2:1 Multiplexer](#26-21-multiplexer)  
2.7 [4:1 Multiplexer](#27-41-multiplexer)  
    - 2.7.1 [Behavioral 4:1 Multiplexer](#271-behavioral-41-multiplexer)  
    - 2.7.2 [Structural 4:1 Multiplexer](#272-structural-41-multiplexer)  
2.8 [4:1 Multiplexer Using 2:1 Multiplexers](#28-41-multiplexer-using-21-multiplexers)  
2.9 [8:1 Multiplexer](#29-81-multiplexer)  
2.10 [16:1 Multiplexer (Using 4:1 Multiplexers)](#210-161-multiplexer-using-41-multiplexers)  
2.11 [Latches](#211-latches)  
    - 2.11.1 [SR Latch](#2111-sr-latch)  
    - 2.11.2 [Positive-Level-Sensitive D Latch](#2112-positive-level-sensitive-d-latch)  
    - 2.11.3 [Negative-Level-Sensitive D Latch](#2113-negative-level-sensitive-d-latch)  
    - 2.11.4 [D Latch Using 2:1 Multiplexer](#2114-d-latch-using-21-multiplexer)  
2.12 [D Flip-Flop](#212-d-flip-flop)  
    - 2.12.1 [Positive-Edge, Synchronous Active-Low Reset](#2121-positive-edge-synchronous-active-low-reset)  
    - 2.12.2 [Negative-Edge, Synchronous Active-Low Reset](#2122-negative-edge-synchronous-active-low-reset)  
    - 2.12.3 [Positive-Edge, Asynchronous Active-Low Reset](#2123-positive-edge-asynchronous-active-low-reset)  
    - 2.12.4 [Negative-Edge, Asynchronous Active-Low Reset](#2124-negative-edge-asynchronous-active-low-reset)  
    - 2.12.5 [Positive-Edge, Asynchronous Active-High Reset](#2125-positive-edge-asynchronous-active-high-reset)  
    - 2.12.6 [Negative-Edge, Asynchronous Active-High Reset](#2126-negative-edge-asynchronous-active-high-reset)  
    - 2.12.7 [Positive-Edge D Flip-Flop Using 2:1 Multiplexers](#2127-positive-edge-d-flip-flop-using-21-multiplexers)  
2.13 [JK Flip-Flop](#213-jk-flip-flop)  
    - 2.13.1 [Positive-Edge, Synchronous Active-Low Reset](#2131-positive-edge-synchronous-active-low-reset)  
    - 2.13.2 [Negative-Edge, Synchronous Active-Low Reset](#2132-negative-edge-synchronous-active-low-reset)  
2.14 [T Flip-Flop](#214-t-flip-flop)  
    - 2.14.1 [Positive-Edge, Synchronous Active-Low Reset](#2141-positive-edge-synchronous-active-low-reset)  
    - 2.14.2 [Negative-Edge, Synchronous Active-Low Reset](#2142-negative-edge-synchronous-active-low-reset)  
    - 2.14.3 [Negative-Edge, Asynchronous Active-Low Reset](#2143-negative-edge-asynchronous-active-low-reset)  
2.15 [Flip-Flop Conversions](#215-flip-flop-conversions)  
    - 2.15.1 [JK Flip-Flop Using D Flip-Flop](#2151-jk-flip-flop-using-d-flip-flop)  
    - 2.15.2 [JK Flip-Flop Using T Flip-Flop](#2152-jk-flip-flop-using-t-flip-flop)  
2.16 [Shift Registers & Counters](#216-shift-registers--counters)  
    - 2.16.1 [4-Bit Shift Register](#2161-4-bit-shift-register)  
    - 2.16.2 [8-Bit Ring Counter](#2162-8-bit-ring-counter)  
    - 2.16.3 [Synchronous Up/Down Counter (Parameterized)](#2163-synchronous-updown-counter-parameterized)  
    - 2.16.4 [2-Bit Asynchronous Up Counter](#2164-2-bit-asynchronous-up-counter)  
    - 2.16.5 [2-Bit Asynchronous Down Counter](#2165-2-bit-asynchronous-down-counter)  
2.17 [Finite State Machines (FSM)](#217-finite-state-machines-fsm)  
    - 2.17.1 [Moore Sequence Detector (1011 — Non-Overlapping)](#2171-moore-sequence-detector-1011--non-overlapping)  
    - 2.17.2 [Moore Sequence Detector (1011 — Overlapping)](#2172-moore-sequence-detector-1011--overlapping)  
    - 2.17.3 [Mealy Sequence Detector (1011 — Non-Overlapping)](#2173-mealy-sequence-detector-1011--non-overlapping)  
    - 2.17.4 [Mealy Sequence Detector (1011 — Overlapping)](#2174-mealy-sequence-detector-1011--overlapping)  
    - 2.17.5 [Skip Counter FSM (0-1-3-6-7)](#2175-skip-counter-fsm-0-1-3-6-7)  
    - 2.17.6 [Electronic Combination Lock (01011)](#2176-electronic-combination-lock-01011)  
    - 2.17.7 [Vending Machine Controller (15 Rupee Dispenser)](#2177-vending-machine-controller-15-rupee-dispenser)  

---

# 1. Introduction

## 1.1 Verilog Basic Modeling Structure

A Verilog design is described using modules. A module defines the interface of a hardware block and describes its functionality.

A typical module follows this structure:

```verilog
module module_name (port_list);

    // Port declarations
    input  a, b;
    output y;

    // Internal signal declarations
    wire w1;

    // Circuit functionality
    assign y = a & b;

endmodule
```

The RTL description focuses on the required hardware behavior rather than the details of the fabrication process. This makes it possible to simulate, verify, modify, and synthesize a design using different supported tools.

**Key characteristics of Verilog**
- It is a hardware description language used primarily for digital hardware design.
- It supports concurrent hardware descriptions.
- Synthesizable RTL can be translated into hardware.
- It is case-sensitive: `data`, `Data`, and `DATA` are different identifiers.
- It is supported by tools from different vendors, although tool support and flows may vary.
- Designs can be described at switch, gate, dataflow, structural, and behavioral levels.

## 1.2 Verilog Data Types

### `wire` (net)
- Represents a connection between components.
- Does not store a value by itself; it is driven by a continuous assignment or a module/primitive output.
- An input port is a net by default unless declared otherwise.

```verilog
wire a;
wire [7:0] data_bus;

assign a = b & c;
```

### `reg` (procedural variable)
- Can hold the last value assigned to it until it is assigned again.
- Commonly used for signals assigned inside `always` or `initial` procedural blocks.
- The Verilog type `reg` does not automatically mean that the synthesized hardware is a physical flip-flop; the behavior of the procedural block determines the hardware inferred.

```verilog
reg enable;
reg [3:0] count;

always @(posedge clk)
    count <= count + 1'b1;
```

### Vectors
A vector is a multi-bit net or variable. The range is written as `[MSB:LSB]`.

```verilog
wire [7:0] data_bus;  // 8-bit net
reg  [3:0] count;     // 4-bit variable

assign data_bus[3:0] = count;
```

**Useful rules**
- In a testbench, DUT inputs are commonly driven by `reg` variables and DUT outputs are commonly observed using `wire` nets.
- A signal assigned by a Verilog continuous `assign` statement is generally declared as a net such as `wire`.
- An output assigned inside a Verilog procedural block is commonly declared as `output reg`.
- Verilog-2001 permits input ports to be declared as net types; do not treat the word `reg` as a synonym for a physical register.

## 1.3 Components of a Verilog Module

A module may contain:
1. **Module name and port list** — identifies the design block and its interface.
2. **Port declarations** — declares inputs, outputs, and inouts.
3. **Internal declarations** — wires, regs, parameters, integers, and other variables.
4. **Dataflow statements** — continuous assignments using `assign`.
5. **Module or primitive instantiations** — connects lower-level blocks or built-in gates.
6. **Procedural blocks** — `always` and `initial` blocks.
7. **Tasks and functions** — reusable procedural descriptions.
8. **endmodule** — terminates the module definition.

### General syntax

```verilog
module module_name (port_list);

    // Declarations
    input  a;
    output y;
    wire internal_signal;

    // Functionality
    assign y = a;

endmodule
```

## 1.4 Levels of Abstraction

Verilog supports different ways to describe the same digital circuit.

| Modeling level | Description |
|---|---|
| **Behavioral** | Describes what the circuit does using procedural statements such as `if`, `case`, and `always`. |
| **Dataflow** | Describes the relationship between signals using Boolean expressions and continuous `assign` statements. |
| **Structural** | Builds a design by connecting smaller modules or components. |
| **Gate level** | Describes logic using built-in gate primitives such as `and`, `or`, `not`, and `xor`. |
| **Switch level** | Models circuits using transistor-level switch primitives. |

## 1.5 AND Gate: Modeling Style Examples

The same AND gate can be described using different modeling styles.

### Behavioral modeling

```verilog
module and_behav (a, b, c);
    input a, b;
    output reg c;

    always @(*) begin
        if (a == 1'b1 && b == 1'b1)
            c = 1'b1;
        else
            c = 1'b0;
    end
endmodule
```

### Dataflow modeling

```verilog
module and_df (a, b, c);
    input a, b;
    output c;

    assign c = a & b;
endmodule
```

### Gate-level modeling

```verilog
module and_gate_level (a, b, c);
    input a, b;
    output c;

    and (c, a, b);
endmodule
```

## 1.6 Verilog Operators — Quick Reference

| Category | Operators | Purpose |
|---|---|---|
| Arithmetic | `+`, `-`, `*`, `/`, `%`, `**` | Arithmetic operations |
| Relational | `>`, `<`, `>=`, `<=` | Magnitude comparison |
| Equality | `==`, `!=`, `===`, `!==` | Equality comparison; case equality also compares X and Z |
| Logical | `&&`, `||`, `!` | Logical operations |
| Bitwise | `&`, `|`, `~`, `^`, `~^` | Bit-by-bit operations |
| Shift | `<<`, `>>`, `<<<`, `>>>` | Shift operations |
| Reduction | `&a`, `|a`, `^a`, `~&a`, `~|a` | Reduces a vector to one bit |
| Concatenation | `{a,b}` | Joins signals |
| Replication | `{N{a}}` | Repeats a signal N times |
| Conditional | `condition ? true_value : false_value` | Selects between two expressions |

Examples:

```verilog
assign y = sel ? a : b;          // 2:1 mux expression
assign bus = {a[3:0], b[3:0]};   // concatenation
wire all_ones = &data_bus;       // reduction AND
```

## 1.7 Sequential Logic: Latch vs Flip-Flop

Both latches and flip-flops store state, but they respond to different clock/control behavior.

| Feature | Latch | Flip-flop |
|---|---|---|
| Sensitivity | Level-sensitive | Edge-triggered |
| Data capture | Follows input while enabled | Captures input at active clock edge |
| Typical use | Level-controlled storage | Registers, counters, and state machines |

- A **positive-level-sensitive latch** is transparent while its enable/clock is high.
- A **positive-edge-triggered flip-flop** captures data on the rising edge.
- A **negative-edge-triggered flip-flop** captures data on the falling edge.
- A **synchronous reset** is acted on only at the active clock edge.
- An **asynchronous reset** can reset the state independently of the clock.

## 1.8 Blocking vs Non-Blocking Assignments

| Feature | Blocking `=` | Non-blocking `<=` |
|---|---|---|
| Update behavior | Updates immediately in procedural order | Schedules the update for the end of the current time step |
| Typical use | Combinational procedural logic | Clocked sequential logic |
| Next statement | Sees the updated value | Usually evaluates using the old value |

### Blocking example

```verilog
always @(*) begin
    a = b;
    c = a;  // c sees the updated value of a
end
```

### Non-blocking example

```verilog
always @(posedge clk) begin
    a <= b;
    c <= a;  // c receives the previous value of a
end
```

## 1.9 Testbench Writing

A testbench is a simulation environment used to verify a Design Under Test (DUT). It applies input stimulus and observes the outputs.

Typical steps:
1. Declare a testbench module, usually without ports.
2. Declare DUT input-driving signals as `reg` and output-observation signals as `wire`.
3. Instantiate the DUT and connect its ports.
4. Initialize the input signals.
5. Apply test cases using delays or loops.
6. Observe results using `$display` or `$monitor`.
7. Optionally generate waveform files using `$dumpfile` and `$dumpvars`.
8. End the simulation using `$finish`.

```verilog
module example_tb;
    reg a, b;
    wire y;

    and_df dut (.a(a), .b(b), .c(y));

    initial begin
        $dumpfile("example_tb.vcd");
        $dumpvars(0, example_tb);

        a = 0; b = 0;
        #5 a = 0; b = 1;
        #5 a = 1; b = 0;
        #5 a = 1; b = 1;
        #5 $finish;
    end
endmodule
```

## 1.10 begin-end vs fork-join

- `begin ... end` groups statements that execute sequentially in the order written.
- `fork ... join` starts the statements in parallel and waits until all of them complete.

```verilog
// Sequential execution
initial begin
    #20 $display("First:  %0t", $time);
    #10 $display("Second: %0t", $time);
end

// Parallel execution
initial fork
    #20 $display("At time %0t", $time);
    #10 $display("At time %0t", $time);
join
```

In the first block, the delays are cumulative. In the second block, each delay is measured from the time the forked statement starts.

## 1.11 initial, $display and $monitor

### `initial`
- Starts at simulation time zero and executes once.
- Commonly used for testbench stimulus, initialization, and waveform setup.
- Generally not used for synthesizable RTL.

### `$display` and `$monitor`
- `$display` prints when the statement executes.
- `$monitor` prints when one or more of its arguments change, and remains active until replaced or disabled.

```verilog
initial begin
    $display("Simulation started at %0t", $time);
    $monitor("time=%0t a=%b b=%b", $time, a, b);
end
```

---

# 2. Verilog Codes

The following sections contain the RTL design and its corresponding testbench. Each heading is linked from the contents section for quick navigation.

## 2.1 Half Adder

A half adder adds two 1-bit inputs and produces Sum and Carry outputs.

### Design Code

```verilog
module half_adder(a, b, s, c);
    input a, b;
    output s, c;

    xor (s, a, b);
    and (c, a, b);
endmodule
```

### Testbench

```verilog
module half_adder_tb;
    wire t_s, t_c;
    reg t_a, t_b;

    half_adder my_gate(
        .a(t_a), .b(t_b), .s(t_s), .c(t_c)
    );

    initial begin
        $monitor("a=%b, b=%b, sum=%b, carry=%b", t_a, t_b, t_s, t_c);
        t_a = 1'b0; t_b = 1'b0;
        #5 t_a = 1'b0; t_b = 1'b1;
        #5 t_a = 1'b1; t_b = 1'b0;
        #5 t_a = 1'b1; t_b = 1'b1;
        #5 $finish;
    end
endmodule
```

## 2.2 Full Adder

A full adder adds `A`, `B`, and `Cin` and produces `Sum` and `Cout`.

### 2.2.1 Gate-Level Full Adder

### Design Code

```verilog
module fulladd1(A, B, Cin, s, Cout);
    input A, B, Cin;
    output s, Cout;
    wire w1, w2, w3;

    xor g1(w1, A, B);
    xor g2(s, w1, Cin);
    and g3(w2, w1, Cin);
    and g4(w3, A, B);
    or  g5(Cout, w2, w3);
endmodule
```

### Testbench

```verilog
module fulladd1_tb;
    wire t_s, t_cout;
    reg t_x, t_y, t_cin;

    fulladd1 my_gate(
        .A(t_x), .B(t_y), .Cin(t_cin),
        .s(t_s), .Cout(t_cout)
    );

    initial begin
        $dumpfile("fulladd1_tb.vcd");
        $dumpvars(1, fulladd1_tb);
        $monitor("time=%0t A=%b B=%b Cin=%b Sum=%b Cout=%b",
                 $time, t_x, t_y, t_cin, t_s, t_cout);

        t_x=0; t_y=0; t_cin=0;
        #5 t_x=0; t_y=0; t_cin=1;
        #5 t_x=0; t_y=1; t_cin=0;
        #5 t_x=0; t_y=1; t_cin=1;
        #5 t_x=1; t_y=0; t_cin=0;
        #5 t_x=1; t_y=0; t_cin=1;
        #5 t_x=1; t_y=1; t_cin=0;
        #5 t_x=1; t_y=1; t_cin=1;
        #5 $finish;
    end
endmodule
```

### 2.2.2 Structural Full Adder (Using Half Adders)

A full adder built hierarchically by instantiating two half-adder sub-modules and an OR gate.

### Design Code

```verilog
module ha_sub(input a, b, output cout, s);
    and (cout, a, b);
    xor (s, a, b);
endmodule

module fulladd_struct(input x, y, cin, output sum, co);
    wire w1, w2, w3;

    ha_sub HA1 (.a(x), .b(y), .cout(w1), .s(w2));
    ha_sub HA2 (.a(cin), .b(w2), .cout(w3), .s(sum));
    or (co, w1, w3);
endmodule
```

### Testbench

```verilog
module fulladd_struct_tb;
    reg x, y, cin;
    wire sum, co;
    integer i;

    fulladd_struct dut(.x(x), .y(y), .cin(cin), .sum(sum), .co(co));

    initial begin
        $monitor("time=%0t x=%b y=%b cin=%b sum=%b co=%b", $time, x, y, cin, sum, co);
        for (i = 0; i < 8; i = i + 1) begin
            {x, y, cin} = i;
            #5;
        end
        $finish;
    end
endmodule
```

## 2.3 4-Bit Ripple Carry Adder

A 4-bit ripple carry adder connects four full-adder stages. The carry output of each stage feeds the next stage.

### Design Code

```verilog
module RA_4bit(
    a0, a1, a2, a3,
    b0, b1, b2, b3,
    c0, s0, s1, s2, s3, c4
);
    input a0, a1, a2, a3;
    input b0, b1, b2, b3;
    input c0;
    output s0, s1, s2, s3, c4;
    wire c1, c2, c3;

    FA FA1(a0, b0, c0, s0, c1);
    FA FA2(a1, b1, c1, s1, c2);
    FA FA3(a2, b2, c2, s2, c3);
    FA FA4(a3, b3, c3, s3, c4);
endmodule

module FA(a, b, e, s, c);
    input a, b, e;
    output s, c;

    assign s = a ^ b ^ e;
    assign c = (a & b) | (e & (a ^ b));
endmodule
```

### Testbench

```verilog
module RA4bit_tb;
    reg ta0, ta1, ta2, ta3;
    reg tb0, tb1, tb2, tb3;
    reg tc0;
    wire ts0, ts1, ts2, ts3, tc4;
    integer i;

    RA_4bit G0(
        ta0, ta1, ta2, ta3,
        tb0, tb1, tb2, tb3,
        tc0, ts0, ts1, ts2, ts3, tc4
    );

    initial begin
        {ta0,ta1,ta2,ta3,tb0,tb1,tb2,tb3} = 8'b0;
        tc0 = 1'b0;
        $dumpfile("RA4bit_tb.vcd");
        $dumpvars(1, RA4bit_tb);
        $monitor("time=%0t A=%b%b%b%b B=%b%b%b%b Cin=%b Sum=%b%b%b%b Cout=%b",
                 $time,ta3,ta2,ta1,ta0,tb3,tb2,tb1,tb0,
                 tc0,ts3,ts2,ts1,ts0,tc4);

        for (i=0; i<256; i=i+1) begin
            #5 {ta0,ta1,ta2,ta3,tb0,tb1,tb2,tb3} = i;
        end
        #5 $finish;
    end
endmodule
```

## 2.4 Half Subtractor

A half subtractor subtracts B from A and produces Difference and Borrow outputs.

### Design Code

```verilog
module hs_df(a, b, borrow, diff);
    input a, b;
    output borrow, diff;

    assign diff   = a ^ b;
    assign borrow = ~a & b;
endmodule
```

### Testbench

```verilog
module hs_tb;
    reg t_x, t_y;
    wire t_b, t_d;

    hs_df my_gate(
        .a(t_x), .b(t_y), .borrow(t_b), .diff(t_d)
    );

    initial begin
        $dumpfile("hs_tb.vcd");
        $dumpvars(1, hs_tb);
        $display("The inputs and outputs are:");
        $monitor("time=%0d, x=%b, y=%b, borrow=%b, diff=%b",
                 $time, t_x, t_y, t_b, t_d);

        t_x = 1'b0; t_y = 1'b0;
        #5 t_x = 1'b0; t_y = 1'b1;
        #5 t_x = 1'b1; t_y = 1'b0;
        #5 t_x = 1'b1; t_y = 1'b1;
        #5 $finish;
    end
endmodule
```

## 2.5 Full Subtractor

A full subtractor subtracts `b` and `bin` (borrow-in) from `a` and produces `diff` (difference) and `bout` (borrow-out).

### Design Code

```verilog
module full_sub_df(
    input a, b, bin,
    output diff, bout
);
    assign diff = a ^ b ^ bin;
    assign bout = (~a & b) | (~(a ^ b) & bin);
endmodule
```

### Testbench

```verilog
module full_sub_tb;
    reg a, b, bin;
    wire diff, bout;
    integer i;

    full_sub_df dut(.a(a), .b(b), .bin(bin), .diff(diff), .bout(bout));

    initial begin
        $dumpfile("full_sub_tb.vcd");
        $dumpvars(1, full_sub_tb);
        $monitor("time=%0t a=%b b=%b bin=%b diff=%b bout=%b",
                 $time, a, b, bin, diff, bout);

        for (i = 0; i < 8; i = i + 1) begin
            {a, b, bin} = i;
            #5;
        end
        $finish;
    end
endmodule
```

## 2.6 2:1 Multiplexer

A 2:1 multiplexer selects one of two input bits according to the select signal `S`. When `S` is 0, `I[0]` is selected; when `S` is 1, `I[1]` is selected.

### Design Code

```verilog
module mux2to1(Y, S, I);
    output reg Y;
    input S;
    input [1:0] I;

    always @(*) begin
        if (S == 1'b0)
            Y = I[0];
        else
            Y = I[1];
    end
endmodule
```

### Testbench

```verilog
module mux2to1_tb;
    wire Y;
    reg [1:0] I;
    reg S;
    integer i;

    mux2to1 m(.Y(Y), .S(S), .I(I));

    initial begin
        {S, I} = 3'b000;
        $monitor("time=%0t S=%b I=%b Y=%b", $time, S, I, Y);

        for (i = 0; i < 8; i = i + 1) begin
            {S, I} = i;
            #5;
        end
        $finish;
    end
endmodule
```

## 2.7 4:1 Multiplexer

A 4:1 multiplexer selects one of four data inputs using two select lines.

### 2.7.1 Behavioral 4:1 Multiplexer

### Design Code

```verilog
module mux4(sel1, sel2, a, b, c, d, y);
    input sel1, sel2, a, b, c, d;
    output reg y;

    always @(*) begin
        case ({sel1, sel2})
            2'b00: y = a;
            2'b01: y = b;
            2'b10: y = c;
            2'b11: y = d;
            default: y = 1'b0;
        endcase
    end
endmodule
```

### Testbench

```verilog
module mux4_tb;
    wire t_y;
    reg t_a, t_b, t_c, t_d, t_sel1, t_sel2;
    integer i;

    mux4 my_gate(
        .a(t_a), .b(t_b), .c(t_c), .d(t_d),
        .y(t_y), .sel1(t_sel1), .sel2(t_sel2)
    );

    initial begin
        {t_a, t_b, t_c, t_d, t_sel1, t_sel2} = 6'b0;
        $dumpfile("mux4_tb.vcd");
        $dumpvars(1, mux4_tb);
        $monitor("time=%0t a=%b b=%b c=%b d=%b sel1=%b sel2=%b y=%b",
                 $time, t_a, t_b, t_c, t_d, t_sel1, t_sel2, t_y);

        for (i = 0; i < 10; i = i + 1) begin
            #1;
            t_a = $random;
            t_b = $random;
            t_c = $random;
            t_d = $random;
            t_sel1 = $random;
            t_sel2 = $random;
        end
        #1 $finish;
    end
endmodule
```

### 2.7.2 Structural 4:1 Multiplexer

A 4:1 multiplexer built structurally using user-defined 3-input AND and 4-input OR gate modules.

### Design Code

```verilog
module and1(output z, input w, x, y);
    assign z = w & x & y;
endmodule

module or1(output e, input a, b, c, d);
    assign e = a | b | c | d;
endmodule

module mux4_struct(
    input [1:0] sel,
    input [3:0] a,
    output y
);
    wire [5:0] w;

    not (w[0], sel[0]);
    not (w[1], sel[1]);
    and1 g1(w[2], w[1], w[0], a[0]);
    and1 g2(w[3], w[1], sel[0], a[1]);
    and1 g3(w[4], sel[1], w[0], a[2]);
    and1 g4(w[5], sel[1], sel[0], a[3]);
    or1  g5(y, w[2], w[3], w[4], w[5]);
endmodule
```

### Testbench

```verilog
module mux4_struct_tb;
    wire t_y;
    reg [3:0] t_a;
    reg [1:0] t_sel;
    integer i;

    mux4_struct dut(t_sel, t_a, t_y);

    initial begin
        {t_a, t_sel} = 6'b0;
        $monitor("time=%0t a=%b sel=%b y=%b", $time, t_a, t_sel, t_y);
        for (i = 0; i < 64; i = i + 1) begin
            {t_a, t_sel} = i;
            #5;
        end
        $finish;
    end
endmodule
```

## 2.8 4:1 Multiplexer Using 2:1 Multiplexers

A 4:1 multiplexer constructed hierarchically using three 2:1 multiplexer instances.

### Design Code

```verilog
module mux2_unit(input s, a, b, output y);
    assign y = (~s & a) | (s & b);
endmodule

module mux4_using_mux2(
    input [1:0] sel,
    input [3:0] a,
    output y
);
    wire w0, w1;

    mux2_unit m0(sel[0], a[0], a[1], w0);
    mux2_unit m1(sel[0], a[2], a[3], w1);
    mux2_unit m2(sel[1], w0,   w1,   y);
endmodule
```

### Testbench

```verilog
module mux4_using_mux2_tb;
    reg [3:0] a;
    reg [1:0] sel;
    wire y;
    integer i;

    mux4_using_mux2 dut(.sel(sel), .a(a), .y(y));

    initial begin
        a = 4'b1010;
        $monitor("time=%0t sel=%b a=%b y=%b", $time, sel, a, y);
        for (i = 0; i < 4; i = i + 1) begin
            sel = i;
            #5;
        end
        $finish;
    end
endmodule
```

## 2.9 8:1 Multiplexer

An 8:1 multiplexer selects one of eight data inputs using a 3-bit select line `sel`.

### Design Code

```verilog
module mux8to1(
    input [2:0] sel,
    input [7:0] a,
    output reg y
);
    always @(*) begin
        case (sel)
            3'b000: y = a[0];
            3'b001: y = a[1];
            3'b010: y = a[2];
            3'b011: y = a[3];
            3'b100: y = a[4];
            3'b101: y = a[5];
            3'b110: y = a[6];
            3'b111: y = a[7];
            default: y = 1'b0;
        endcase
    end
endmodule
```

### Testbench

```verilog
module mux8to1_tb;
    reg [7:0] a;
    reg [2:0] sel;
    wire y;
    integer i;

    mux8to1 dut(.sel(sel), .a(a), .y(y));

    initial begin
        a = 8'b1101_0101;
        $monitor("time=%0t sel=%b a=%b y=%b", $time, sel, a, y);
        for (i = 0; i < 8; i = i + 1) begin
            sel = i;
            #5;
        end
        $finish;
    end
endmodule
```

## 2.10 16:1 Multiplexer (Using 4:1 Multiplexers)

A 16:1 multiplexer built hierarchically using five 4:1 multiplexer sub-modules.

### Design Code

```verilog
module mux4_unit(input [1:0] sel, input [3:0] a, output y);
    assign y = a[sel];
endmodule

module mux16to1(
    input [3:0] sel,
    input [15:0] a,
    output y
);
    wire [3:0] w;

    mux4_unit m0(sel[1:0], a[3:0],   w[0]);
    mux4_unit m1(sel[1:0], a[7:4],   w[1]);
    mux4_unit m2(sel[1:0], a[11:8],  w[2]);
    mux4_unit m3(sel[1:0], a[15:12], w[3]);
    mux4_unit m4(sel[3:2], w[3:0],   y);
endmodule
```

### Testbench

```verilog
module mux16to1_tb;
    reg [15:0] a;
    reg [3:0] sel;
    wire y;
    integer i;

    mux16to1 dut(.sel(sel), .a(a), .y(y));

    initial begin
        a = 16'hA5C3;
        $monitor("time=%0t sel=%0d (%b) a=%h y=%b", $time, sel, sel, a, y);
        for (i = 0; i < 16; i = i + 1) begin
            sel = i;
            #5;
        end
        $finish;
    end
endmodule
```

## 2.11 Latches

This section covers cross-coupled NAND SR latches, positive/negative level-sensitive D latches, and MUX-based latch implementations.

### 2.11.1 SR Latch

An SR latch modeled using continuous `assign` statements representing cross-coupled NAND gates.

### Design Code

```verilog
module sr_latch(output Q, Qn, input S, R);
    assign Q  = ~(R & Qn);
    assign Qn = ~(S & Q);
endmodule
```

### Testbench

```verilog
module sr_latch_tb;
    reg S, R;
    wire Q, Qn;

    sr_latch dut(Q, Qn, S, R);

    initial begin
        $monitor("time=%0t S=%b R=%b Q=%b Qn=%b", $time, S, R, Q, Qn);
        S = 1'b0; R = 1'b1;
        #5 S = 1'b1; R = 1'b1;
        #5 S = 1'b1; R = 1'b0;
        #5 S = 1'b1; R = 1'b1;
        #5 S = 1'b0; R = 1'b0;
        #5 S = 1'b1; R = 1'b1;
        #5 $finish;
    end
endmodule
```

### 2.11.2 Positive-Level-Sensitive D Latch

A positive-level-sensitive D latch is transparent when `clk` is high. The active-low reset `rstn` clears the output when it is low.

### Design Code

```verilog
module d_latch_pos(
    input d, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(clk or rstn or d) begin
        if (!rstn)
            q <= 1'b0;
        else if (clk)
            q <= d;
    end
endmodule
```

### Testbench

```verilog
module d_latch_pos_tb;
    reg d, clk, rstn;
    wire q, qb;

    d_latch_pos dl0(.d(d), .clk(clk), .rstn(rstn), .q(q), .qb(qb));

    always #5 clk = ~clk;

    initial begin
        $dumpfile("d_latch_pos_tb.vcd");
        $dumpvars(1, d_latch_pos_tb);
        {clk, rstn, d} = 3'b000;

        #10 rstn = 1;
        #8 d = 1;
        #8 d = 0;
        #8 d = 1;
        #8 d = 0;
        #2 rstn = 0;
        #8 d = 1;
        #8 d = 0;
        #2 rstn = 1;
        #8 d = 1;
        #8 d = 0;
        #2 $finish;
    end
endmodule
```

### 2.11.3 Negative-Level-Sensitive D Latch

A negative-level-sensitive D latch is transparent when `clk` is low (`!clk`).

### Design Code

```verilog
module d_latch_neg(
    input d, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(clk or rstn or d) begin
        if (!rstn)
            q <= 1'b0;
        else if (!clk)
            q <= d;
    end
endmodule
```

### Testbench

```verilog
module d_latch_neg_tb;
    reg d, clk, rstn;
    wire q, qb;

    d_latch_neg dl0(.d(d), .clk(clk), .rstn(rstn), .q(q), .qb(qb));

    always #5 clk = ~clk;

    initial begin
        $dumpfile("d_latch_neg_tb.vcd");
        $dumpvars(1, d_latch_neg_tb);
        {clk, rstn, d} = 3'b000;

        #10 rstn = 1;
        #8 d = 1;
        #8 d = 0;
        #8 d = 1;
        #8 d = 0;
        #2 rstn = 0;
        #8 d = 1;
        #8 d = 0;
        #2 rstn = 1;
        #8 d = 1;
        #8 d = 0;
        #2 $finish;
    end
endmodule
```

### 2.11.4 D Latch Using 2:1 Multiplexer

A positive level-sensitive D latch implemented by feeding the output of a 2:1 multiplexer back to its `0` input terminal.

### Design Code

```verilog
module mux2_latch_sub(input s, a, b, output reg y);
    always @(s, a, b) begin
        case (s)
            1'b0: y <= a;
            1'b1: y <= b;
            default: y <= 1'b0;
        endcase
    end
endmodule

module d_latch_mux(input d, clk, output q, qb);
    wire w1;

    mux2_latch_sub m1(clk, w1, d, w1);
    assign q  = w1;
    assign qb = ~q;
endmodule
```

### Testbench

```verilog
module d_latch_mux_tb;
    reg d, clk;
    wire q, qb;

    d_latch_mux dut(.d(d), .clk(clk), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $monitor("time=%0t clk=%b d=%b q=%b qb=%b", $time, clk, d, q, qb);
        clk = 1; d = 0;
        #7 d = 1;
        #6 d = 0;
        #6 d = 1;
        #10 $finish;
    end
endmodule
```

## 2.12 D Flip-Flop

This section covers D flip-flop implementations with different clock edges, reset configurations, and master-slave MUX structures.

### 2.12.1 Positive-Edge, Synchronous Active-Low Reset

The D flip-flop captures D on the rising edge of clk. The active-low reset is checked only at that clock edge.

### Design Code

```verilog
module dff_pos_sync_n(
    input d, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(posedge clk) begin
        if (!rstn)
            q <= 1'b0;
        else
            q <= d;
    end
endmodule
```

### Testbench

```verilog
module dff_pos_sync_n_tb;
    reg d, clk, rstn;
    wire q, qb;

    dff_pos_sync_n dut(.d(d), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("dff_pos_sync_n_tb.vcd");
        $dumpvars(1, dff_pos_sync_n_tb);
        {clk, rstn, d} = 3'b000;
        #10 rstn = 1;
        #8 d = 1; #8 d = 0;
        #8 d = 1; #8 d = 0;
        #8 d = 1; #8 d = 0;
        #4 rstn = 0;
        #8 d = 1; #8 d = 0;
        #2 $finish;
    end
endmodule
```

### 2.12.2 Negative-Edge, Synchronous Active-Low Reset

This version captures D on the falling edge of clk. The active-low reset is sampled at that edge.

### Design Code

```verilog
module dff_neg_sync_n(
    input d, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(negedge clk) begin
        if (!rstn)
            q <= 1'b0;
        else
            q <= d;
    end
endmodule
```

### Testbench

```verilog
module dff_neg_sync_n_tb;
    reg d, clk, rstn;
    wire q, qb;

    dff_neg_sync_n dut(.d(d), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("dff_neg_sync_n_tb.vcd");
        $dumpvars(1, dff_neg_sync_n_tb);
        {clk, rstn, d} = 3'b000;
        #10 rstn = 1;
        #8 d = 1; #8 d = 0;
        #8 d = 1; #8 d = 0;
        #8 d = 1; #8 d = 0;
        #4 rstn = 0;
        #8 d = 1; #8 d = 0;
        #2 $finish;
    end
endmodule
```

### 2.12.3 Positive-Edge, Asynchronous Active-Low Reset

The flip-flop captures D on the rising clock edge. When rstn goes low, q is cleared immediately, without waiting for a clock edge.

### Design Code

```verilog
module dff_pos_async_n(
    input d, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(posedge clk or negedge rstn) begin
        if (!rstn)
            q <= 1'b0;
        else
            q <= d;
    end
endmodule
```

### Testbench

```verilog
module dff_pos_async_n_tb;
    reg d, clk, rstn;
    wire q, qb;

    dff_pos_async_n dut(.d(d), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("dff_pos_async_n_tb.vcd");
        $dumpvars(1, dff_pos_async_n_tb);
        {clk, rstn, d} = 3'b000;
        #10 rstn = 1;
        #8 d = 1; #8 d = 0;
        #8 d = 1; #8 d = 0;
        #8 d = 1;
        #1 rstn = 0;
        #8 d = 0;
        #2 $finish;
    end
endmodule
```

### 2.12.4 Negative-Edge, Asynchronous Active-Low Reset

This version captures D on the falling clock edge and clears q immediately when rstn goes low.

### Design Code

```verilog
module dff_neg_async_n(
    input d, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(negedge clk or negedge rstn) begin
        if (!rstn)
            q <= 1'b0;
        else
            q <= d;
    end
endmodule
```

### Testbench

```verilog
module dff_neg_async_n_tb;
    reg d, clk, rstn;
    wire q, qb;

    dff_neg_async_n dut(.d(d), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("dff_neg_async_n_tb.vcd");
        $dumpvars(1, dff_neg_async_n_tb);
        {clk, rstn, d} = 3'b000;
        #10 rstn = 1;
        #8 d = 1; #8 d = 0;
        #8 d = 1; #8 d = 0;
        #8 d = 1;
        #1 rstn = 0;
        #8 d = 0;
        #2 $finish;
    end
endmodule
```

### 2.12.5 Positive-Edge, Asynchronous Active-High Reset

This version uses an active-high asynchronous reset. A rising edge on rst clears q immediately; otherwise D is captured on the rising edge of clk.

### Design Code

```verilog
module dff_pos_async(
    input d, clk, rst,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(posedge clk or posedge rst) begin
        if (rst)
            q <= 1'b0;
        else
            q <= d;
    end
endmodule
```

### Testbench

```verilog
module dff_pos_async_tb;
    reg d, clk, rst;
    wire q, qb;

    dff_pos_async dut(.d(d), .clk(clk), .rst(rst), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("dff_pos_async_tb.vcd");
        $dumpvars(1, dff_pos_async_tb);
        {clk, d} = 2'b00;
        rst = 1'b1;
        #10 rst = 1'b0;
        #8 d = 1; #8 d = 0;
        #8 d = 1; #8 d = 0;
        #8 d = 1;
        #1 rst = 1;
        #8 d = 0;
        #2 $finish;
    end
endmodule
```

### 2.12.6 Negative-Edge, Asynchronous Active-High Reset

This version captures D on the falling clock edge and responds immediately to a rising edge on rst.

### Design Code

```verilog
module dff_neg_async(
    input d, clk, rst,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(negedge clk or posedge rst) begin
        if (rst)
            q <= 1'b0;
        else
            q <= d;
    end
endmodule
```

### Testbench

```verilog
module dff_neg_async_tb;
    reg d, clk, rst;
    wire q, qb;

    dff_neg_async dut(.d(d), .clk(clk), .rst(rst), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("dff_neg_async_tb.vcd");
        $dumpvars(1, dff_neg_async_tb);
        {clk, d} = 2'b00;
        rst = 1'b1;
        #10 rst = 1'b0;
        #8 d = 1; #8 d = 0;
        #8 d = 1; #8 d = 0;
        #8 d = 1;
        #1 rst = 1;
        #8 d = 0;
        #2 $finish;
    end
endmodule
```

### 2.12.7 Positive-Edge D Flip-Flop Using 2:1 Multiplexers

A master-slave positive-edge-triggered D flip-flop built using two 2:1 multiplexers configured as positive level-sensitive latches.

### Design Code

```verilog
module dff_mux_pos(
    input d, clk,
    output q, qb
);
    wire w1, w2;

    mux2_latch_sub m1(~clk, w1, d,  w1);
    mux2_latch_sub m2( clk, w2, w1, w2);

    assign q  = w2;
    assign qb = ~q;
endmodule
```

### Testbench

```verilog
module dff_mux_pos_tb;
    reg d, clk;
    wire q, qb;

    dff_mux_pos dut(.d(d), .clk(clk), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $monitor("time=%0t clk=%b d=%b q=%b qb=%b", $time, clk, d, q, qb);
        clk = 0; d = 0;
        #3 d = 1;
        #8 d = 0;
        #8 d = 1;
        #10 $finish;
    end
endmodule
```

## 2.13 JK Flip-Flop

This section contains positive-edge and negative-edge JK flip-flop implementations.

### 2.13.1 Positive-Edge, Synchronous Active-Low Reset

The JK flip-flop updates on the rising clock edge. J and K determine whether the output holds, resets, sets, or toggles.

| J | K | Next state |
|---|---|---|
| 0 | 0 | Hold |
| 0 | 1 | Reset |
| 1 | 0 | Set |
| 1 | 1 | Toggle |

### Design Code

```verilog
module jkff_pos_sync_n(
    input j, k, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(posedge clk) begin
        if (!rstn)
            q <= 1'b0;
        else begin
            case ({j, k})
                2'b00: q <= q;
                2'b01: q <= 1'b0;
                2'b10: q <= 1'b1;
                2'b11: q <= ~q;
            endcase
        end
    end
endmodule
```

### Testbench

```verilog
module jkff_pos_sync_n_tb;
    reg j, k, clk, rstn;
    wire q, qb;

    jkff_pos_sync_n dut(.j(j), .k(k), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("jkff_pos_sync_n_tb.vcd");
        $dumpvars(1, jkff_pos_sync_n_tb);
        {clk, rstn, j, k} = 4'b0000;
        #10 rstn = 1;
        #8 j=0; k=1;
        #8 j=0; k=0;
        #8 j=1; k=0;
        #8 j=0; k=0;
        #6 j=1; k=1;
        #8 j=0; k=0;
        #8 j=1; k=0;
        #4 rstn=0;
        #10 $finish;
    end
endmodule
```

### 2.13.2 Negative-Edge, Synchronous Active-Low Reset

This version performs the JK operation on the falling edge of clk. Reset is synchronous and active-low.

### Design Code

```verilog
module jkff_neg_sync_n(
    input j, k, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(negedge clk) begin
        if (!rstn)
            q <= 1'b0;
        else begin
            case ({j, k})
                2'b00: q <= q;
                2'b01: q <= 1'b0;
                2'b10: q <= 1'b1;
                2'b11: q <= ~q;
            endcase
        end
    end
endmodule
```

### Testbench

```verilog
module jkff_neg_sync_n_tb;
    reg j, k, clk, rstn;
    wire q, qb;

    jkff_neg_sync_n dut(.j(j), .k(k), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("jkff_neg_sync_n_tb.vcd");
        $dumpvars(1, jkff_neg_sync_n_tb);
        {clk, rstn, j, k} = 4'b0000;
        #10 rstn = 1;
        #8 j=0; k=1;
        #8 j=0; k=0;
        #8 j=1; k=0;
        #8 j=0; k=0;
        #6 j=1; k=1;
        #8 j=0; k=0;
        #8 j=1; k=0;
        #4 rstn=0;
        #10 $finish;
    end
endmodule
```

## 2.14 T Flip-Flop

This section contains T flip-flop implementations with different clock-edge and reset configurations.

### 2.14.1 Positive-Edge, Synchronous Active-Low Reset

A T flip-flop toggles its output when T is high and holds its current state when T is low. Reset is synchronous and active-low.

### Design Code

```verilog
module tff_pos_sync_n(
    input t, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(posedge clk) begin
        if (!rstn)
            q <= 1'b0;
        else if (t)
            q <= ~q;
    end
endmodule
```

### Testbench

```verilog
module tff_pos_sync_n_tb;
    reg t, clk, rstn;
    wire q, qb;

    tff_pos_sync_n dut(.t(t), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("tff_pos_sync_n_tb.vcd");
        $dumpvars(1, tff_pos_sync_n_tb);
        {clk, rstn, t} = 3'b000;
        #10 rstn = 1;
        #8 t=1; #8 t=0;
        #8 t=1; #8 t=0;
        #8 t=1; #8 t=0;
        #4 rstn=0;
        #8 t=1; #8 t=0;
        #2 $finish;
    end
endmodule
```

### 2.14.2 Negative-Edge, Synchronous Active-Low Reset

This version toggles or holds its state on the falling edge of clk. Reset is sampled synchronously at that edge.

### Design Code

```verilog
module tff_neg_sync_n(
    input t, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(negedge clk) begin
        if (!rstn)
            q <= 1'b0;
        else if (t)
            q <= ~q;
    end
endmodule
```

### Testbench

```verilog
module tff_neg_sync_n_tb;
    reg t, clk, rstn;
    wire q, qb;

    tff_neg_sync_n dut(.t(t), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("tff_neg_sync_n_tb.vcd");
        $dumpvars(1, tff_neg_sync_n_tb);
        {clk, rstn, t} = 3'b000;
        #10 rstn = 1;
        #8 t=1; #8 t=0;
        #8 t=1; #8 t=0;
        #8 t=1; #8 t=0;
        #4 rstn=0;
        #8 t=1; #8 t=0;
        #2 $finish;
    end
endmodule
```

### 2.14.3 Negative-Edge, Asynchronous Active-Low Reset

This T flip-flop responds to the falling edge of clk. When rstn goes low, q is cleared immediately. When T is high at the active clock edge, q toggles.

### Design Code

```verilog
module tff_neg_async_n(
    input t, clk, rstn,
    output reg q,
    output qb
);
    assign qb = ~q;

    always @(negedge clk or negedge rstn) begin
        if (!rstn)
            q <= 1'b0;
        else if (t)
            q <= ~q;
    end
endmodule
```

### Testbench

```verilog
module tff_neg_async_n_tb;
    reg t, clk, rstn;
    wire q, qb;

    tff_neg_async_n dut(.t(t), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $dumpfile("tff_neg_async_n_tb.vcd");
        $dumpvars(1, tff_neg_async_n_tb);
        {clk, rstn, t} = 3'b000;
        #10 rstn = 1;
        #8 t=1; #8 t=0;
        #8 t=1; #8 t=0;
        #8 t=1; #8 t=0;
        #4 rstn=0;
        #8 t=1; #8 t=0;
        #2 $finish;
    end
endmodule
```

## 2.15 Flip-Flop Conversions

This section demonstrates how to build a JK flip-flop using a D flip-flop or a T flip-flop by deriving the appropriate excitation logic.

### 2.15.1 JK Flip-Flop Using D Flip-Flop

Uses the excitation equation $D = J \cdot \overline{Q} + \overline{K} \cdot Q$ to drive a positive-edge D flip-flop.

### Design Code

```verilog
module jk_using_dff(
    input j, k, clk, rstn,
    output q, qb
);
    wire d;
    assign qb = ~q;
    assign d  = (j & ~q) | (~k & q);

    dff_pos_sync_n d0(.d(d), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
endmodule
```

### Testbench

```verilog
module jk_using_dff_tb;
    reg j, k, clk, rstn;
    wire q, qb;

    jk_using_dff dut(.j(j), .k(k), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $monitor("time=%0t rstn=%b j=%b k=%b q=%b qb=%b", $time, rstn, j, k, q, qb);
        {clk, rstn, j, k} = 4'b0000;
        #10 rstn = 1;
        #8 j = 1; k = 0;
        #8 j = 0; k = 0;
        #8 j = 0; k = 1;
        #8 j = 1; k = 1;
        #10 $finish;
    end
endmodule
```

### 2.15.2 JK Flip-Flop Using T Flip-Flop

Uses the excitation equation $T = J \cdot \overline{Q} + K \cdot Q$ to drive a positive-edge T flip-flop.

### Design Code

```verilog
module jk_using_tff(
    input j, k, clk, rstn,
    output q, qb
);
    wire t;
    assign qb = ~q;
    assign t  = (j & ~q) | (k & q);

    tff_pos_sync_n t0(.t(t), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
endmodule
```

### Testbench

```verilog
module jk_using_tff_tb;
    reg j, k, clk, rstn;
    wire q, qb;

    jk_using_tff dut(.j(j), .k(k), .clk(clk), .rstn(rstn), .q(q), .qb(qb));
    always #5 clk = ~clk;

    initial begin
        $monitor("time=%0t rstn=%b j=%b k=%b q=%b qb=%b", $time, rstn, j, k, q, qb);
        {clk, rstn, j, k} = 4'b0000;
        #10 rstn = 1;
        #8 j = 1; k = 0;
        #8 j = 0; k = 0;
        #8 j = 0; k = 1;
        #8 j = 1; k = 1;
        #10 $finish;
    end
endmodule
```

## 2.16 Shift Registers & Counters

This section covers serial shift registers, ring counters, parameterized synchronous up/down counters, and asynchronous ripple counters.

### 2.16.1 4-Bit Shift Register

A 4-bit serial-in serial-out (SISO) shift register using non-blocking assignments.

### Design Code

```verilog
module shiftreg_4bit(
    input clock, clear, A,
    output reg E
);
    reg B, C, D;

    always @(posedge clock or posedge clear) begin
        if (clear) begin
            B <= 1'b0; C <= 1'b0; D <= 1'b0; E <= 1'b0;
        end else begin
            B <= A;
            C <= B;
            D <= C;
            E <= D;
        end
    end
endmodule
```

### Testbench

```verilog
module shiftreg_4bit_tb;
    reg clock, clear, A;
    wire E;

    shiftreg_4bit sr(.clock(clock), .clear(clear), .A(A), .E(E));
    always #5 clock = ~clock;

    initial begin
        $monitor("[%0t] clear=%b A=%b E=%b", $time, clear, A, E);
        clock = 0; clear = 1; A = 1;
        #7 clear = 0;
        #60 $finish;
    end
endmodule
```

### 2.16.2 8-Bit Ring Counter

An 8-bit ring counter that circulates a single `1` bit across the register on each rising clock edge.

### Design Code

```verilog
module ring_cntr(
    input clk, init,
    output reg [7:0] count
);
    always @(posedge clk) begin
        if (init)
            count <= 8'b1000_0000;
        else begin
            count <= count << 1;
            count[0] <= count[7];
        end
    end
endmodule
```

### Testbench

```verilog
module ring_counter_tb;
    reg clk, init;
    wire [7:0] count;

    ring_cntr rc(.clk(clk), .init(init), .count(count));
    always #5 clk = ~clk;

    initial begin
        clk = 0; init = 1;
        $monitor("[%0t] init=%0b count=%b", $time, init, count);
        #7 init = 0;
        #50 $finish;
    end
endmodule
```

### 2.16.3 Synchronous Up/Down Counter (Parameterized)

A parameterized synchronous counter that counts up when `mode = 1` and counts down when `mode = 0`.

### Design Code

```verilog
module sync_counter #(parameter N = 3) (
    input mode, clr, clk,
    output reg [N:0] count
);
    always @(posedge clk) begin
        if (clr)
            count <= 0;
        else if (mode)
            count <= count + 1'b1;
        else
            count <= count - 1'b1;
    end
endmodule
```

### Testbench

```verilog
module sync_counter_tb;
    parameter N = 3;
    reg mode, clr, clk;
    wire [N:0] count;

    sync_counter #(N) c1(.mode(mode), .clr(clr), .clk(clk), .count(count));
    always #5 clk = ~clk;

    initial begin
        clk = 0; clr = 1; mode = 1;
        $dumpfile("sync_counter_tb.vcd");
        $dumpvars(1, sync_counter_tb);
        $monitor("[%0t] mode=%0b clr=%0b clk=%b count=%b", $time, mode, clr, clk, count);
        #7 clr = 0;
        #80 mode = 0;
        #80 $finish;
    end
endmodule
```

### 2.16.4 2-Bit Asynchronous Up Counter

A 2-bit ripple up counter built using negative-edge-triggered T flip-flops where `q[0]` clocks the second stage.

### Design Code

```verilog
module cntr_up_asynch(
    input clk, rstn,
    output [1:0] y
);
    wire [1:0] q, qb;

    tff_neg_async_n tf0(1'b1, clk,  rstn, q[0], qb[0]);
    tff_neg_async_n tf1(1'b1, q[0], rstn, q[1], qb[1]);

    assign y = q;
endmodule
```

### Testbench

```verilog
module cntr_up_asynch_tb;
    reg clk, rstn;
    wire [1:0] y;

    cntr_up_asynch dut(.clk(clk), .rstn(rstn), .y(y));
    always #5 clk = ~clk;

    initial begin
        $monitor("[%0t] rstn=%b y=%b (%0d)", $time, rstn, y, y);
        clk = 0; rstn = 0;
        #10 rstn = 1;
        #50 $finish;
    end
endmodule
```

### 2.16.5 2-Bit Asynchronous Down Counter

A 2-bit ripple down counter built using negative-edge-triggered T flip-flops where `qb[0]` clocks the second stage.

### Design Code

```verilog
module cntr_down_asynch(
    input clk, rstn,
    output [1:0] y
);
    wire [1:0] q, qb;

    tff_neg_async_n tf0(1'b1, clk,   rstn, q[0], qb[0]);
    tff_neg_async_n tf1(1'b1, qb[0], rstn, q[1], qb[1]);

    assign y = q;
endmodule
```

### Testbench

```verilog
module cntr_down_asynch_tb;
    reg clk, rstn;
    wire [1:0] y;

    cntr_down_asynch dut(.clk(clk), .rstn(rstn), .y(y));
    always #5 clk = ~clk;

    initial begin
        $monitor("[%0t] rstn=%b y=%b (%0d)", $time, rstn, y, y);
        clk = 0; rstn = 0;
        #10 rstn = 1;
        #50 $finish;
    end
endmodule
```

## 2.17 Finite State Machines (FSM)

This section covers Moore and Mealy sequence detectors (both overlapping and non-overlapping), custom sequence counters, an electronic combination lock, and a vending machine controller.

### 2.17.1 Moore Sequence Detector (1011 — Non-Overlapping)

Detects the bit pattern `1011` using a 5-state Moore machine without overlapping sequences.

### Design Code

```verilog
module det_1011_moore_non_overlap(
    input clk, rstn, in,
    output out
);
    parameter S0 = 0, S1 = 1, S10 = 2, S101 = 3, S1011 = 4;
    reg [2:0] cur_state, next_state;

    assign out = (cur_state == S1011) ? 1'b1 : 1'b0;

    always @(posedge clk) begin
        if (!rstn) cur_state <= S0;
        else       cur_state <= next_state;
    end

    always @(cur_state or in) begin
        case (cur_state)
            S0:      next_state = in ? S1    : S0;
            S1:      next_state = in ? S1    : S10;
            S10:     next_state = in ? S101  : S0;
            S101:    next_state = in ? S1011 : S10;
            S1011:   next_state = in ? S1    : S0;
            default: next_state = S0;
        endcase
    end
endmodule
```

### Testbench

```verilog
module det_1011_moore_non_overlap_tb;
    reg clk, in, rstn;
    wire out;
    integer i;
    reg [15:0] data;

    always #10 clk = ~clk;

    det_1011_moore_non_overlap u0(.clk(clk), .rstn(rstn), .in(in), .out(out));

    initial begin
        $monitor("Time=%0t rstn=%b in=%b out=%b", $time, rstn, in, out);
        clk = 0; rstn = 0; in = 0;
        data = 16'b1110_1011_0110_1110;
        i = 0;
        #50 rstn = 1;
        #350 $finish;
    end

    always @(posedge clk) begin
        if (rstn && i < 16) begin
            in <= data[i];
            i  <= i + 1;
        end
    end
endmodule
```

### 2.17.2 Moore Sequence Detector (1011 — Overlapping)

Detects the bit pattern `1011` using a 5-state Moore machine allowing overlapping sequences (`S1011` transitions to `S10` when `in = 0`).

### Design Code

```verilog
module det_1011_moore_overlap(
    input clk, rstn, in,
    output out
);
    parameter S0 = 0, S1 = 1, S10 = 2, S101 = 3, S1011 = 4;
    reg [2:0] cur_state, next_state;

    assign out = (cur_state == S1011) ? 1'b1 : 1'b0;

    always @(posedge clk) begin
        if (!rstn) cur_state <= S0;
        else       cur_state <= next_state;
    end

    always @(cur_state or in) begin
        case (cur_state)
            S0:      next_state = in ? S1    : S0;
            S1:      next_state = in ? S1    : S10;
            S10:     next_state = in ? S101  : S0;
            S101:    next_state = in ? S1011 : S10;
            S1011:   next_state = in ? S1    : S10;
            default: next_state = S0;
        endcase
    end
endmodule
```

### Testbench

```verilog
module det_1011_moore_overlap_tb;
    reg clk, in, rstn;
    wire out;
    integer i;
    reg [15:0] data;

    always #10 clk = ~clk;

    det_1011_moore_overlap u0(.clk(clk), .rstn(rstn), .in(in), .out(out));

    initial begin
        $monitor("Time=%0t rstn=%b in=%b out=%b", $time, rstn, in, out);
        clk = 0; rstn = 0; in = 0;
        data = 16'b1110_1011_0111_1011;
        i = 0;
        #50 rstn = 1;
        #350 $finish;
    end

    always @(posedge clk) begin
        if (rstn && i < 16) begin
            in <= data[i];
            i  <= i + 1;
        end
    end
endmodule
```

### 2.17.3 Mealy Sequence Detector (1011 — Non-Overlapping)

Detects the bit pattern `1011` using a 4-state Mealy machine without overlapping sequences.

### Design Code

```verilog
module det_1011_mealy_non_overlap(
    input clk, rstn, in,
    output reg out
);
    parameter S0 = 0, S1 = 1, S10 = 2, S101 = 3;
    reg [1:0] cur_state, next_state;

    always @(posedge clk) begin
        if (!rstn) cur_state <= S0;
        else       cur_state <= next_state;
    end

    always @(cur_state or in) begin
        case (cur_state)
            S0:      begin next_state = in ? S1   : S0;  out = 1'b0; end
            S1:      begin next_state = in ? S1   : S10; out = 1'b0; end
            S10:     begin next_state = in ? S101 : S0;  out = 1'b0; end
            S101:    begin next_state = in ? S0   : S10; out = in ? 1'b1 : 1'b0; end
            default: begin next_state = S0; out = 1'b0; end
        endcase
    end
endmodule
```

### Testbench

```verilog
module det_1011_mealy_non_overlap_tb;
    reg clk, in, rstn;
    wire out;
    integer i;
    reg [15:0] data;

    always #10 clk = ~clk;

    det_1011_mealy_non_overlap u0(.clk(clk), .rstn(rstn), .in(in), .out(out));

    initial begin
        $monitor("Time=%0t rstn=%b in=%b out=%b", $time, rstn, in, out);
        clk = 0; rstn = 0; in = 0;
        data = 16'b1110_1101_1011_1011;
        i = 0;
        #50 rstn = 1;
        #350 $finish;
    end

    always @(posedge clk) begin
        if (rstn && i < 16) begin
            in <= data[i];
            i  <= i + 1;
        end
    end
endmodule
```

### 2.17.4 Mealy Sequence Detector (1011 — Overlapping)

Detects the bit pattern `1011` using a 4-state Mealy machine allowing overlapping sequences (`S101` transitions to `S1` when `in = 1`).

### Design Code

```verilog
module det_1011_mealy_overlap(
    input clk, rstn, in,
    output reg out
);
    parameter S0 = 0, S1 = 1, S10 = 2, S101 = 3;
    reg [1:0] cur_state, next_state;

    always @(posedge clk) begin
        if (!rstn) cur_state <= S0;
        else       cur_state <= next_state;
    end

    always @(cur_state or in) begin
        case (cur_state)
            S0:      begin next_state = in ? S1   : S0;  out = 1'b0; end
            S1:      begin next_state = in ? S1   : S10; out = 1'b0; end
            S10:     begin next_state = in ? S101 : S0;  out = 1'b0; end
            S101:    begin next_state = in ? S1   : S10; out = in ? 1'b1 : 1'b0; end
            default: begin next_state = S0; out = 1'b0; end
        endcase
    end
endmodule
```

### Testbench

```verilog
module det_1011_mealy_overlap_tb;
    reg clk, in, rstn;
    wire out;
    integer i;
    reg [15:0] data;

    always #10 clk = ~clk;

    det_1011_mealy_overlap u0(.clk(clk), .rstn(rstn), .in(in), .out(out));

    initial begin
        $monitor("Time=%0t rstn=%b in=%b out=%b", $time, rstn, in, out);
        clk = 0; rstn = 0; in = 0;
        data = 16'b1110_1011_0110_1110;
        i = 0;
        #50 rstn = 1;
        #350 $finish;
    end

    always @(posedge clk) begin
        if (rstn && i < 16) begin
            in <= data[i];
            i  <= i + 1;
        end
    end
endmodule
```

### 2.17.5 Skip Counter FSM (0-1-3-6-7)

A Moore FSM that counts the non-sequential pattern `0 -> 1 -> 3 -> 6 -> 7 -> 0` when `x_in` is high, holds its count when `x_in` is low, and asserts `y_out = 1` when the count reaches `7`.

### Design Code

```verilog
module skip_counter_fsm(
    output y_out,
    output [2:0] st,
    input x_in, clock, reset
);
    reg [2:0] state;
    parameter S0 = 3'b000, S1 = 3'b001, S2 = 3'b011, S3 = 3'b110, S4 = 3'b111;

    always @(posedge clock) begin
        if (reset == 1'b0)
            state <= S0;
        else begin
            case (state)
                S0: if (x_in) state <= S1; else state <= S0;
                S1: if (x_in) state <= S2; else state <= S1;
                S2: if (x_in) state <= S3; else state <= S2;
                S3: if (x_in) state <= S4; else state <= S3;
                S4: if (x_in) state <= S0; else state <= S4;
                default: state <= S0;
            endcase
        end
    end

    assign y_out = (state == S4);
    assign st    = state;
endmodule
```

### Testbench

```verilog
module skip_counter_fsm_tb;
    wire [2:0] t_st;
    wire t_y_out;
    reg t_x_in, t_clock, t_reset;

    skip_counter_fsm M1(t_y_out, t_st, t_x_in, t_clock, t_reset);
    always #5 t_clock = ~t_clock;

    initial begin
        $dumpfile("skip_counter_fsm_tb.vcd");
        $dumpvars(1, skip_counter_fsm_tb);
        $monitor("[%0t] reset=%b x_in=%b state=%0d (%b) y_out=%b",
                 $time, t_reset, t_x_in, t_st, t_st, t_y_out);

        t_reset = 0; t_clock = 0; t_x_in = 1;
        fork
            #7   t_reset = 1;
            #82  t_x_in  = 0;
            #107 t_reset = 0;
        join
        #150 $finish;
    end
endmodule
```

### 2.17.6 Electronic Combination Lock (01011)

An electronic combination lock with a `reset` button, two number buttons (`b0` for 0 and `b1` for 1), and an `unlock` output that asserts when the sequence `01011` is entered.

### Design Code

```verilog
module lock(
    input clk, reset, b0, b1,
    output unlock
);
    parameter S_RESET = 0, S_0 = 1, S_01 = 2, S_010 = 3, S_0101 = 4, S_01011 = 5;
    reg [2:0] state, next_state;

    always @(*) begin
        if (reset)
            next_state = S_RESET;
        else begin
            case (state)
                S_RESET: next_state = b0 ? S_0   : (b1 ? S_RESET : state);
                S_0:     next_state = b0 ? S_0   : (b1 ? S_01    : state);
                S_01:    next_state = b0 ? S_010 : (b1 ? S_RESET : state);
                S_010:   next_state = b0 ? S_0   : (b1 ? S_0101  : state);
                S_0101:  next_state = b0 ? S_010 : (b1 ? S_01011 : state);
                S_01011: next_state = b0 ? S_0   : (b1 ? S_RESET : state);
                default: next_state = S_RESET;
            endcase
        end
    end

    always @(posedge clk)
        state <= next_state;

    assign unlock = (state == S_01011) ? 1'b1 : 1'b0;
endmodule
```

### Testbench

```verilog
module lock_tb;
    reg clk, b0, b1, reset;
    wire unlock;
    integer i;
    reg [4:0] data;

    always #10 clk = ~clk;

    lock u0(clk, reset, b0, b1, unlock);

    initial begin
        $monitor("Time=%0t reset=%b b0=%b b1=%b unlock=%b", $time, reset, b0, b1, unlock);
        $dumpfile("lock_tb.vcd");
        $dumpvars(1, lock_tb);
        clk = 0; reset = 1; b0 = 0; b1 = 0;
        #50 reset = 0;
        data = 5'b01011;
        i = 4;
        #130 $finish;
    end

    always @(posedge clk) begin
        if (!reset && i >= 0) begin
            b0 <= ~data[i];
            b1 <=  data[i];
            i  <= i - 1;
        end
    end
endmodule
```

### 2.17.7 Vending Machine Controller (15 Rupee Dispenser)

A vending machine FSM that accepts 5-rupee (`2'b01`) and 10-rupee (`2'b10`) coins and asserts `can_despatch = 1` when the accumulated total reaches or exceeds 15 rupees.

### Design Code

```verilog
module vending_machine(
    output can_despatch,
    input clk,
    input [1:0] coin,
    input rst
);
    reg [1:0] state, next_state;
    parameter s0 = 0, s5 = 1, s10 = 2, s15 = 3;

    always @(posedge clk) begin
        if (rst)
            state <= s0;
        else
            state <= next_state;
    end

    always @(state, coin) begin
        case (state)
            s0: begin
                if (coin == 2'b00)      next_state = s0;
                else if (coin == 2'b01) next_state = s5;
                else if (coin == 2'b10) next_state = s10;
                else                    next_state = s0;
            end
            s5: begin
                if (coin == 2'b00)      next_state = s5;
                else if (coin == 2'b01) next_state = s10;
                else if (coin == 2'b10) next_state = s15;
                else                    next_state = s5;
            end
            s10: begin
                if (coin == 2'b00)      next_state = s10;
                else if (coin == 2'b01) next_state = s15;
                else if (coin == 2'b10) next_state = s15;
                else                    next_state = s10;
            end
            s15: begin
                if (coin == 2'b00)      next_state = s0;
                else if (coin == 2'b01) next_state = s5;
                else if (coin == 2'b10) next_state = s10;
                else                    next_state = s0;
            end
            default: next_state = s0;
        endcase
    end

    assign can_despatch = (state == s15) ? 1'b1 : 1'b0;
endmodule
```

### Testbench

```verilog
module vending_machine_tb;
    reg clk, rst;
    wire can_despatch;
    integer i;
    reg [1:0] coin_stack [0:5], coin;

    always #10 clk = ~clk;

    vending_machine u0(can_despatch, clk, coin, rst);

    initial begin
        $monitor("Time=%0t reset=%b coin=%b can_despatched=%b", $time, rst, coin, can_despatch);
        $dumpfile("vending_machine_tb.vcd");
        $dumpvars(1, vending_machine_tb);
        clk = 0; rst = 1; coin = 2'b00;
        #50 rst = 0;

        coin_stack[0] = 2'b00; // 0 rupee
        coin_stack[1] = 2'b01; // 5 rupee
        coin_stack[2] = 2'b10; // 10 rupee -> dispenses
        coin_stack[3] = 2'b01; // 5 rupee
        coin_stack[4] = 2'b10; // 10 rupee -> dispenses
        coin_stack[5] = 2'b00; // 0 rupee
        i = 0;
        #130 $finish;
    end

    always @(posedge clk) begin
        if (!rst && i < 6) begin
            coin <= coin_stack[i];
            i    <= i + 1;
        end
    end
endmodule
```

---


# Verilog HDL: Introduction, Quick Reference & Code Library

A practical learning reference for Verilog HDL, from fundamental language concepts to combinational and sequential circuit implementations. This repository brings together concise explanations, synthesizable RTL examples, and simulation testbenches. It is intended as a growing reference for learning digital design, understanding RTL behavior, and practicing functional verification.

Verilog is a hardware description language (HDL) used to describe and model digital systems. It allows designers to express hardware at different abstraction levels without tying the RTL description to a specific fabrication technology. Designs can be simulated and verified before implementation, and synthesizable RTL can be mapped to hardware using appropriate design tools.

**What this reference covers**
- Verilog module structure, ports, nets, registers, and vectors.
- Behavioral, dataflow, structural, gate-level, and switch-level modeling concepts.
- Operators, procedural assignments, and testbench fundamentals.
- Combinational circuits such as adders, subtractors, and multiplexers.
- Sequential circuits such as latches and flip-flops.
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
2.2 [Half Subtractor](#22-half-subtractor)  
2.3 [2:1 Multiplexer](#23-21-multiplexer)  
2.4 [4:1 Multiplexer](#24-41-multiplexer)  
2.5 [Full Adder](#25-full-adder)  
2.6 [4-Bit Ripple Carry Adder](#26-4-bit-ripple-carry-adder)  
2.7 [Positive-Level-Sensitive D Latch](#27-positive-level-sensitive-d-latch)  
2.8 [D Flip-Flop: Positive-Edge, Synchronous Active-Low Reset](#28-d-flip-flop-positive-edge-synchronous-active-low-reset)  
2.9 [D Flip-Flop: Negative-Edge, Synchronous Active-Low Reset](#29-d-flip-flop-negative-edge-synchronous-active-low-reset)  
2.10 [D Flip-Flop: Positive-Edge, Asynchronous Active-Low Reset](#210-d-flip-flop-positive-edge-asynchronous-active-low-reset)  
2.11 [D Flip-Flop: Negative-Edge, Asynchronous Active-Low Reset](#211-d-flip-flop-negative-edge-asynchronous-active-low-reset)  
2.12 [D Flip-Flop: Positive-Edge, Asynchronous Active-High Reset](#212-d-flip-flop-positive-edge-asynchronous-active-high-reset)  
2.13 [D Flip-Flop: Negative-Edge, Asynchronous Active-High Reset](#213-d-flip-flop-negative-edge-asynchronous-active-high-reset)  
2.14 [JK Flip-Flop: Positive-Edge, Synchronous Active-Low Reset](#214-jk-flip-flop-positive-edge-synchronous-active-low-reset)  
2.15 [JK Flip-Flop: Negative-Edge, Synchronous Active-Low Reset](#215-jk-flip-flop-negative-edge-synchronous-active-low-reset)  
2.16 [T Flip-Flop: Positive-Edge, Synchronous Active-Low Reset](#216-t-flip-flop-positive-edge-synchronous-active-low-reset)  
2.17 [T Flip-Flop: Negative-Edge, Synchronous Active-Low Reset](#217-t-flip-flop-negative-edge-synchronous-active-low-reset)  
2.18 [T Flip-Flop: Negative-Edge, Asynchronous Active-Low Reset](#218-t-flip-flop-negative-edge-asynchronous-active-low-reset)  

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

## 2.2 Half Subtractor

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

## 2.3 2:1 Multiplexer

A 2:1 multiplexer selects one of two input bits according to the select signal S. When S is 0, I[0] is selected; when S is 1, I[1] is selected.

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

## 2.4 4:1 Multiplexer

A 4:1 multiplexer selects one of four data inputs using two select lines.

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

## 2.5 Full Adder

A full adder adds A, B, and Carry-in and produces Sum and Carry-out.

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

## 2.6 4-Bit Ripple Carry Adder

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

## 2.7 Positive-Level-Sensitive D Latch

A positive-level-sensitive D latch is transparent when clk is high. The active-low reset rstn clears the output when it is low.

### Design Code

```verilog
module d_latch(
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
module d_latch_tb;
    reg d, clk, rstn;
    wire q, qb;

    d_latch dl0(.d(d), .clk(clk), .rstn(rstn), .q(q), .qb(qb));

    always #5 clk = ~clk;

    initial begin
        $dumpfile("d_latch_tb.vcd");
        $dumpvars(1, d_latch_tb);
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

## 2.8 D Flip-Flop: Positive-Edge, Synchronous Active-Low Reset

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

## 2.9 D Flip-Flop: Negative-Edge, Synchronous Active-Low Reset

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

## 2.10 D Flip-Flop: Positive-Edge, Asynchronous Active-Low Reset

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

## 2.11 D Flip-Flop: Negative-Edge, Asynchronous Active-Low Reset

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

## 2.12 D Flip-Flop: Positive-Edge, Asynchronous Active-High Reset

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

## 2.13 D Flip-Flop: Negative-Edge, Asynchronous Active-High Reset

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

## 2.14 JK Flip-Flop: Positive-Edge, Synchronous Active-Low Reset

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

## 2.15 JK Flip-Flop: Negative-Edge, Synchronous Active-Low Reset

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

## 2.16 T Flip-Flop: Positive-Edge, Synchronous Active-Low Reset

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

## 2.17 T Flip-Flop: Negative-Edge, Synchronous Active-Low Reset

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

## 2.18 T Flip-Flop: Negative-Edge, Asynchronous Active-Low Reset

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

---

## Notes

- Each code section contains a design module and a separate testbench.
- Testbench module names are unique so multiple examples can be kept in the same repository without module-name collisions.
- The D flip-flop examples distinguish clock edge, reset polarity, and synchronous/asynchronous reset behavior.
- The repeated positive-edge asynchronous active-low DFF example from the supplied notes has been included once.
- The active-high asynchronous reset examples use `posedge rst` and `if (rst)`, so the reset behavior matches the active-high description.
- The testbenches are simulation examples; run each with its corresponding DUT and check the waveform/output before using it in a larger design.

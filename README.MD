# Verilog HDL Codes

A collection of Verilog HDL designs and their testbenches, covering basic combinational logic circuits. Each section includes the design code and a corresponding testbench for simulation.

## Contents

Click a design below to jump directly to its Verilog code and testbench.

1. [Half Adder](#1-half-adder)
2. [Half Subtractor](#2-half-subtractor)
3. [4:1 Multiplexer](#3-41-multiplexer)
4. [Full Adder](#4-full-adder)
5. [4-Bit Ripple Carry Adder](#5-4-bit-ripple-carry-adder)

---

## 1. Half Adder

A half adder adds two 1-bit inputs and produces a Sum and Carry output.

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
        .a(t_a),
        .b(t_b),
        .s(t_s),
        .c(t_c)
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

---

## 2. Half Subtractor

A half subtractor subtracts input B from input A and produces Difference and Borrow outputs.

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
        .a(t_x),
        .b(t_y),
        .borrow(t_b),
        .diff(t_d)
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

---

## 3. 4:1 Multiplexer

A 4:1 multiplexer selects one of four data inputs based on the two select lines.

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
        .a(t_a),
        .b(t_b),
        .c(t_c),
        .d(t_d),
        .y(t_y),
        .sel1(t_sel1),
        .sel2(t_sel2)
    );

    initial begin
        {t_a, t_b, t_c, t_d, t_sel1, t_sel2} = 6'b0;

        $dumpfile("mux4_tb.vcd");
        $dumpvars(1, mux4_tb);

        $display("The inputs and outputs are:");
        $monitor("time=%0d, a=%b, b=%b, c=%b, d=%b, sel1=%b, sel2=%b, y=%b",
                 $time, t_a, t_b, t_c, t_d, t_sel1, t_sel2, t_y);

        for (i = 0; i < 10; i = i + 1) begin
            #1;
            t_a    = $random;
            t_b    = $random;
            t_c    = $random;
            t_d    = $random;
            t_sel1 = $random;
            t_sel2 = $random;
        end

        #1 $finish;
    end

endmodule
```

---

## 4. Full Adder

A full adder adds three 1-bit inputs (A, B, and Carry-in) and produces Sum and Carry-out outputs.

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
        .A(t_x),
        .B(t_y),
        .Cin(t_cin),
        .s(t_s),
        .Cout(t_cout)
    );

    initial begin
        $dumpfile("fulladd1_tb.vcd");
        $dumpvars(1, fulladd1_tb);

        $display("The inputs and outputs are:");
        $monitor("time=%0d, A=%b, B=%b, Cin=%b, Sum=%b, Cout=%b",
                 $time, t_x, t_y, t_cin, t_s, t_cout);

        t_x = 1'b0; t_y = 1'b0; t_cin = 1'b0;
        #5 t_x = 1'b0; t_y = 1'b0; t_cin = 1'b1;
        #5 t_x = 1'b0; t_y = 1'b1; t_cin = 1'b0;
        #5 t_x = 1'b0; t_y = 1'b1; t_cin = 1'b1;
        #5 t_x = 1'b1; t_y = 1'b0; t_cin = 1'b0;
        #5 t_x = 1'b1; t_y = 1'b0; t_cin = 1'b1;
        #5 t_x = 1'b1; t_y = 1'b1; t_cin = 1'b0;
        #5 t_x = 1'b1; t_y = 1'b1; t_cin = 1'b1;
        #5 $finish;
    end

endmodule
```

---

## 5. 4-Bit Ripple Carry Adder

A 4-bit ripple carry adder uses four full adders connected in series. The carry output of each stage is passed to the next stage.

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
        {ta0, ta1, ta2, ta3, tb0, tb1, tb2, tb3} = 8'b0;
        tc0 = 1'b0;

        $dumpfile("RA4bit_tb.vcd");
        $dumpvars(1, RA4bit_tb);

        $display("The inputs and outputs are:");
        $monitor("time=%0d, a0=%b, a1=%b, a2=%b, a3=%b, b0=%b, b1=%b, b2=%b, b3=%b, Cin=%b, s0=%b, s1=%b, s2=%b, s3=%b, Cout=%b",
                 $time, ta0, ta1, ta2, ta3, tb0, tb1, tb2, tb3,
                 tc0, ts0, ts1, ts2, ts3, tc4);

        for (i = 0; i < 256; i = i + 1) begin
            #5;
            {ta0, ta1, ta2, ta3, tb0, tb1, tb2, tb3} = i;
        end

        #5 $finish;
    end

endmodule
```

---

## Notes

- Each testbench instantiates its corresponding design module and applies input combinations.
- The testbenches use simulation delays to observe output changes.
- VCD files are generated in the testbenches that include `$dumpfile` and `$dumpvars`.

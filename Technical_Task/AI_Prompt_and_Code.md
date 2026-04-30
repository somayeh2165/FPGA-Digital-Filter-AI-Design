module tb_security_filter();
    reg clk, rst;
    reg [7:0] x;
    wire [7:0] y;
    wire alarm;

    // uut: Unit Under Test
    security_fir_filter uut (
        .clk(clk), .rst(rst), .x(x), .y(y), .alarm(alarm)
    );

    // Clock: 10 units period
    always #5 clk = ~clk;

    initial begin
        $dumpfile("dump.vcd"); 
        $dumpvars(0, tb_security_filter);
        
        clk = 0; rst = 0; x = 0;
        #10 rst = 1; // Release reset

        // Scenario 1: Normal values
        #10 x = 8'h05;
        #10 x = 8'h0A;
        
        // Scenario 2: Attack/Anomaly (High input)
        #20 x = 8'h45; // Output will exceed 8'h30
        
        #40 $finish;
    end
endmodule
module security_fir_filter(
    input clk,
    input rst,
    input [7:0] x,
    output reg [7:0] y,
    output reg alarm
);
    // Coefficients in Q3.4 format
    parameter c0 = 8'h08; // 0.5
    parameter c1 = 8'h10; // 1.0
    parameter c2 = 8'h08; 
    parameter c3 = 8'h04;

    reg [7:0] x1, x2, x3;
    wire [15:0] p0, p1, p2, p3;
    wire [15:0] sum;

    // Shift register for input samples
    always @(posedge clk or negedge rst) begin
        if (!rst) begin
            x1 <= 0; x2 <= 0; x3 <= 0;
        end else begin
            x1 <= x; x2 <= x1; x3 <= x2;
        end
    end

    // Multiplication and Summation
    assign p0 = x * c0;
    assign p1 = x1 * c1;
    assign p2 = x2 * c2;
    assign p3 = x3 * c3;
    assign sum = (p0 + p1 + p2 + p3) >> 4; 

    // Output and Anomaly Detection Alarm
    always @(posedge clk or negedge rst) begin
        if (!rst) begin
            y <= 0;
            alarm <= 0;
        end else begin
            y <= sum[7:0];
            // If output > 8'h30 (Dec 48), trigger alarm
            if (sum[7:0] > 8'h30) 
                alarm <= 1;
            else
                alarm <= 0;
        end
    end
endmodule

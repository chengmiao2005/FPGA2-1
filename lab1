module counter (
    input        sys_clk,    
    input        sys_rst_n,  
    output reg   led_out     
);


parameter CNT_MAX = 24;  

reg [27:0] cnt;  

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (!sys_rst_n) begin  
        cnt <= 28'd0;
        led_out <= 1'b1;
    end else begin
        if (cnt == CNT_MAX) begin  
            cnt <= 28'd0;
            led_out <= ~led_out;
        end else begin  
            cnt <= cnt + 1'b1;
        end
    end
end

endmodule




`timescale 1ns/1ps

module tb_counter ();

reg        sys_clk;
reg        sys_rst_n;
wire       led_out;
wire [27:0] cnt;  
counter u_counter (
    .sys_clk    (sys_clk),
    .sys_rst_n  (sys_rst_n),
    .led_out    (led_out)
);

assign cnt = u_counter.cnt;  
initial begin
    sys_clk = 1'b0;
    forever #10 sys_clk = ~sys_clk;
end
initial begin
    sys_rst_n = 1'b0;
    #20;         
    sys_rst_n = 1'b1;
    #1000;       
    $stop;       
end
initial begin
    $monitor("Time = %t, cnt = %d, led_out = %b", $time, cnt, led_out);
end

endmodule

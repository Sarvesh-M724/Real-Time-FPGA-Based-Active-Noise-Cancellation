// Simple LMS Filter Core for ANC
module lms_filter (
    input clk,
    input rst_n,
    input signed [15:0] x_n, // Reference noise
    input signed [15:0] d_n, // Desired signal (Noise + Audio)
    output reg signed [15:0] y_n // Anti-noise output
);
    parameter MU = 8'h01; // Step size (convergence rate)
    reg signed [15:0] w;     // Filter weight (simplified 1-tap)
    wire signed [15:0] e_n;  // Error signal

    assign e_n = d_n - y_n; // Error calculation [cite: 55]

    always @(posedge clk or negedge rst_n) begin
        if (!rst_n) begin
            w <= 16'h0000;
            y_n <= 16'h0000;
        end else begin
            // Adaptive Weight Update: w(n+1) = w(n) + mu * e(n) * x(n)
            w <= w + (MU * e_n * x_n >>> 8); 
            y_n <= (w * x_n) >>> 15; // Generate anti-noise [cite: 41]
        end
    end
endmodule

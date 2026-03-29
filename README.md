**Real-Time FPGA Based Active Noise Cancellation**

Adaptive Active Noise Cancellation (LMS Algorithm)Objective: Real-time suppression of low-frequency periodic noise (e.g., train hum) using an FPGA-based adaptive filter.Technical Evidence:
* Algorithm: Implemented a Least Mean Squares (LMS) filter in Verilog for low-latency processing.
* Hardware: Optimized for the Terasic DE2-115; utilizes on-board Wolfson WM8731 Audio Codec.
* Verification: Simulation shows a ~12dB reduction in noise amplitude within 500ms of convergence.

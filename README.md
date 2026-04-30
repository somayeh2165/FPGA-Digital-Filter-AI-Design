FPGA-Digital-Filter-AI-Design
Course: Advanced FPGA Design and Applications (ELEG 6341)

Institution: Prairie View A&M University

Student: Somayeh Soroush (PhD Student in Electrical Engineering)

Collaborator: AI Assistant (Gemini)

1. Project Introduction & Abstract (Step 6)
This project demonstrates an AI-enhanced design workflow for digital filtering, specifically tailored for Smart Grid Security applications. In modern power systems, sensor data must be filtered in real-time to detect cyber-physical anomalies.

In this repository, we utilize a Human-in-the-Loop approach to design an FIR filter with an integrated anomaly detection alarm on the Xilinx Zynq-7000 FPGA. By providing architectural constraints to a Large Language Model (LLM), we generate RTL code, verify its functionality, and evaluate its hardware efficiency compared to manual designs documented in previous laboratory reports.

2. Environment Setup (Step 1)
To ensure the reproducibility of this AI-driven hardware design, the following environment is used:

Hardware Specifications:

Target Device: Xilinx Zynq-7000 SoC (xc7z020clg400-1)

Platform: Zybo Z7-20 Development Board

Software Toolchain:

Vivado Design Suite (v2023.1): For RTL simulation, synthesis, and implementation.

Vitis HLS: For C++ based algorithmic validation.

MobaXterm: For serial interaction with the FPGA terminal.

AI Methodology:

Method: RTLLM-inspired feedback loop.

AI Tool: Gemini 1.5 Pro / ChatGPT.

3. Technical Task: AI-Generated Security Filter (Steps 2-5)
The core technical contribution of this project is the development of a Verilog-based FIR filter that monitors signal amplitudes. If the input exceeds a predefined safety threshold (suggesting a potential sensor spoofing attack), the system triggers an alarm bit.

The Workflow:

Initial Prompting: Describing the filter specifications to the AI.

RTL Generation: Reviewing the AI-produced Verilog code for synthesis errors.

Verification: Running testbenches to confirm the alarm logic.

4. Hardware Implementation Results
Based on the synthesis results in Vivado, the design achieves the following (referenced from our baseline lab experiments):

Worst Negative Slack (WNS): Optimized for high-frequency operation (>100 MHz).

Resource Utilization: Minimal LUT and DSP usage for parallel processing.# FPGA-Digital-Filter-AI-Design
AI-Assisted design of a digital filter for Smart Grid security on Zynq-7000 FPGA.

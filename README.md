# Phase-Modulation-using-NumPy-and-Matplotlib-
__Aim:__ 
To implement and analyze phase modulation (PM) using Python's NumPy and Matplotlib libraries. 

__Apparatus Required:__ 
1. Software: Python with NumPy and Matplotlib libraries 
2. Hardware: Personal Computer

   __Theory:__
   Phase Modulation (PM) is a technique where the phase of the carrier wave is varied in proportion to the 
instantaneous amplitude of the input signal (message signal). Unlike frequency modulation, where the frequency 
is varied, in phase modulation, the phase angle of the carrier wave changes with the amplitude of the message 
signal.

__Algorithm:__

  1   Initialize Parameters:
     Set values for carrier amplitude (Ac), carrier frequency (fc), message frequency (fm), sampling frequency,and phase deviation sensitivity (kpk).   
   
  2. Generate Time Axis: 
   Create a time vector for the signal duration based on the sampling frequency.
   
 3. Generate Message Signal: 
   Define the message signal as a cosine wave.
   
 4. Generate PM Signal: 
   Apply the PM modulation formula to obtain the modulated signal.
   
 5. Plot the Signals: 
   Use Matplotlib to plot the message signal, carrier signal, and phase-modulated signal.

__Program:__ 

```
clc;
clear;
close;

fs = 50000;                       // Sampling frequency
t = 0:1/fs:0.01;                  // Time duration
N = 5;                            // Number of channels

// Baseband message frequencies
msg_freq = [120, 240, 340, 500, 800];

// Carrier frequencies for FDM
carrier_freq = [3000, 6000, 9000, 12000, 15000];

messages = zeros(N, length(t));
carriers = zeros(N, length(t));
modulated = zeros(N, length(t));

// Generate message and carrier signals
for i = 1:N
    messages(i, :) = sin(2 * %pi * msg_freq(i) * t);
    carriers(i, :) = cos(2 * %pi * carrier_freq(i) * t);
    modulated(i, :) = messages(i, :) .* carriers(i, :); 
end

// FDM composite signal
fdm_signal = sum(modulated, "r");

// Demodulation
demodulated = zeros(N, length(t));

for i = 1:N
    demodulated(i, :) = fdm_signal .* carriers(i, :);  // Multiply by same carrier
end

// Plotting section

// Original messages
scf(1);
for i = 1:N
    subplot(N,1,i);
    plot(t, messages(i,:));
    xtitle("Original Message Signal " + string(i));
    ylabel("Amplitude");
    if i == N then xlabel("Time (s)"); end
end

// FDM Composite Signal
scf(2);
plot(t, fdm_signal);
xtitle("FDM Composite Signal");
xlabel("Time (s)");
ylabel("Amplitude");

// Demodulated Signals
scf(3);
for i = 1:N
    subplot(N,1,i);
    plot(t, demodulated(i,:));
    xtitle("Demodulated Signal " + string(i));
    ylabel("Amplitude");
    if i == N then xlabel("Time (s)"); end
end
```



__Output:__ 


<img width="1086" height="868" alt="image" src="https://github.com/user-attachments/assets/d2e04554-1f4f-4bce-8366-f8d3ace8b94b" />

<img width="1160" height="690" alt="image" src="https://github.com/user-attachments/assets/6c210117-50a5-477e-be95-fbdb304fa5e4" />

<img width="1166" height="754" alt="image" src="https://github.com/user-attachments/assets/cfa3190b-b55c-4b9b-9c08-f36243914513" />


__Result:__

The Frequency Division Multiplexing (FDM) technique was successfully implemented using SCILAB. Five different message signals were modulated onto five separate carrier frequencies, combined to form a single FDM composite signal, and then individually recovered using demodulation.



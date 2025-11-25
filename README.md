# Frequency-Division-Multiplexing---Modulation-and-Demodulation-using-Python
### Aim:
To study Frequency Division Multiplexing (FDM) using SCILAB by modulating multiple message signals onto different carrier frequencies and recovering them using demodulation filters.
### Apparatus Required:
SCILAB software
### Theory:
Frequency Division Multiplexing (FDM) is a technique where multiple message signals are transmitted simultaneously over a single communication channel by assigning each message a unique carrier frequency.

Each message is modulated using amplitude modulation (AM/DSB-SC) with a different carrier.

These modulated signals occupy non-overlapping frequency bands, allowing them to be added together to form a composite FDM signal.

At the receiver, band-pass filters are used to extract individual channels.

Each extracted signal is then demodulated to recover the original message.

FDM is widely used in radio broadcasting, cable TV, and telecommunication links.

### Algorithm
FDM Modulation Algorithm:
Input:

• 5 message signals: m1(t), m2(t), m3(t), m4(t), m5(t)
• Time vector t
• 5 different carrier frequencies

#### Steps:

Initialize the parameters such as sampling frequency, time duration, and number of channels.

Generate five message signals with different baseband frequencies.

Assign a unique carrier frequency to each message to avoid overlapping bands.

Modulate each message signal using its respective carrier signal (multiplication).

Add all modulated signals to obtain the FDM composite signal.

At the receiver, apply band-pass filters, each tuned to one carrier band.

Demodulate each extracted signal to recover the original messages.

Plot the original, modulated, composite, and recovered signals.

__Program:__ 

```
Fs = 56300;
t = 0:1/Fs:0.02;

m1 = sin(2*%pi*200*t);
m2 = sin(2*%pi*300*t);
m3 = sin(2*%pi*400*t);
m4 = sin(2*%pi*500*t);
m5 = sin(2*%pi*600*t);
m6 = sin(2*%pi*700*t);

c1 = 3000; c2 = 6000; c3 = 9000; c4 = 12000; c5 = 15000; c6 = 18000;

carrier1 = cos(2*%pi*c1*t);
carrier2 = cos(2*%pi*c2*t);
carrier3 = cos(2*%pi*c3*t);
carrier4 = cos(2*%pi*c4*t);
carrier5 = cos(2*%pi*c5*t);
carrier6 = cos(2*%pi*c6*t);

s1 = m1 .* carrier1;
s2 = m2 .* carrier2;
s3 = m3 .* carrier3;
s4 = m4 .* carrier4;
s5 = m5 .* carrier5;
s6 = m6 .* carrier6;

s_total = s1 + s2 + s3 + s4 + s5 + s6;

// Demultiplex: multiply by carriers to shift each band back to baseband
r1 = s_total .* carrier1;
r2 = s_total .* carrier2;
r3 = s_total .* carrier3;
r4 = s_total .* carrier4;
r5 = s_total .* carrier5;
r6 = s_total .* carrier6;

// Simple FFT-based ideal low-pass filter (avoids butter/toolbox issues)
function y = ideal_lowpass_fft(x, Fs, fc)
    N = length(x);
    X = fft(x);
    f = Fs*(0:N-1)/N;
    mask = (f <= fc) | (f >= Fs-fc);
    Y = X .* mask;
    y = real(ifft(Y));
endfunction

fc = 1000;
dm1 = ideal_lowpass_fft(r1, Fs, fc);
dm2 = ideal_lowpass_fft(r2, Fs, fc);
dm3 = ideal_lowpass_fft(r3, Fs, fc);
dm4 = ideal_lowpass_fft(r4, Fs, fc);
dm5 = ideal_lowpass_fft(r5, Fs, fc);
dm6 = ideal_lowpass_fft(r6, Fs, fc);

figure(1);
subplot(3,2,1); plot(t,m1); title("Message Signal 1");
subplot(3,2,2); plot(t,m2); title("Message Signal 2");
subplot(3,2,3); plot(t,m3); title("Message Signal 3");
subplot(3,2,4); plot(t,m4); title("Message Signal 4");
subplot(3,2,5); plot(t,m5); title("Message Signal 5");
subplot(3,2,6); plot(t,m6); title("Message Signal 6");

figure(2);
plot(t, s_total); title("Multiplexed FDM Signal");

figure(3);
subplot(3,2,1); plot(t,dm1); title("Recovered Signal 1");
subplot(3,2,2); plot(t,dm2); title("Recovered Signal 2");
subplot(3,2,3); plot(t,dm3); title("Recovered Signal 3");
subplot(3,2,4); plot(t,dm4); title("Recovered Signal 4");
subplot(3,2,5); plot(t,dm5); title("Recovered Signal 5");
subplot(3,2,6); plot(t,dm6); title("Recovered Signal 6");
```

__Output:__ 

![WhatsApp Image 2025-11-25 at 10 51 40_a6cf0d20](https://github.com/user-attachments/assets/10ded3e6-bba6-4d91-be67-78f047795e45)

![WhatsApp Image 2025-11-25 at 10 52 02_a81e373f](https://github.com/user-attachments/assets/ef5f5c3f-bd00-4b61-9d0c-3dddeab6c109)

![WhatsApp Image 2025-11-25 at 10 52 41_9d1c9183](https://github.com/user-attachments/assets/f516db7e-fba5-4757-b152-f679d680b3f0)


__Result:__

The Frequency Division Multiplexing (FDM) technique was successfully implemented using SCILAB. Five different message signals were modulated onto five separate carrier frequencies, combined to form a single FDM composite signal, and then individually recovered using demodulation.



# FREQUENCY-DIVISIN-MULTIPLEXING
AIM

To implement Frequency Division Multiplexing (FDM) for six different message signals using Scilab, generate the multiplexed signal, and perform demultiplexing to recover all the original message signals. The experiment also includes plotting the message signals, multiplexed signal, and demultiplexed signals.

APPARATUS REQUIRED

Computer System

Scilab Software

ALGORITHM

Set sampling frequency, time duration, and time vector.

Generate six message signals with different frequencies.

Assign six different carrier frequencies.

Perform DSB-SC modulation by multiplying each message with its carrier.

Add all modulated signals to form the multiplexed FDM signal.

For each channel, multiply the multiplexed signal with the same carrier (demodulation).

Apply a low-pass filter to extract the recovered message.

Plot message signals, multiplexed signal, and recovered s ignals.

THEORY

Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a different carrier frequency. 

Each message modulates its own carrier, and all modulated signals are added to form the multiplexed signal. Since the carrier frequencies are well separated, the signals do not overlap in the frequency domain.

At the receiver, each signal is recovered by multiplying the multiplexed signal with the corresponding carrier (coherent demodulation) and passing it through a low-pass filter to extract the original baseband message. FDM is widely used in radio broadcasting, telephone systems, and cable TV.

PROGRAM
~~~
Fs = 50000;
t = 0:1/Fs:0.02;

m1 = 3.6 * sin(2*%pi*250*t);
m2 = 3.8 * sin(2*%pi*350*t);
m3 = 4.1 * sin(2*%pi*450*t);
m4 = 4.2 * sin(2*%pi*550*t);
m5 = 4.4 * sin(2*%pi*650*t);
m6 = 4.6 * sin(2*%pi*750*t);

c1 = 4000; 
c2 = 8000; 
c3 = 12000; 
c4 = 16000; 
c5 = 20000; 
c6 = 24000;

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

r1 = s_total .* carrier1;
r2 = s_total .* carrier2;
r3 = s_total .* carrier3;
r4 = s_total .* carrier4;
r5 = s_total .* carrier5;
r6 = s_total .* carrier6;

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
~~~
OUTPUT WAVEFORM
<img width="1920" height="1200" alt="Screenshot (133)" src="https://github.com/user-attachments/assets/9ea995cd-e29e-4757-bbc5-dc26b4fa6b46" />
<img width="1920" height="1200" alt="Screenshot (131)" src="https://github.com/user-attachments/assets/ba27f164-02cd-4b43-b35c-a6f91b84bae1" />
<img width="1920" height="1200" alt="Screenshot (132)" src="https://github.com/user-attachments/assets/e92589f2-92cc-40de-ae45-67ef485ab583" />

CALCULATION

![WhatsApp Image 2025-11-29 at 14 13 18](https://github.com/user-attachments/assets/0d84a207-aae9-4bb6-ab6e-97948ed39c1c)


RESULT

Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.

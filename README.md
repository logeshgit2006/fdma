clc; clear all; close all; 
 
% Step 1: Parameters 
Fs = 10000;               % Sampling frequency (Hz) 
t = 0:1/Fs:0.01;          % Time vector (10 ms) 
 
% Step 2: Define baseband user signals 
u1 = sin(2*pi*50*t);        
u2 = sin(2*pi*100*t);      
u3 = sin(2*pi*150*t);      
u4 = sin(2*pi*200*t);      
u5 = sin(2*pi*250*t);      
 
% Step 3: Carrier frequencies 
f1 = 1000; f2 = 2000; f3 = 3000; f4 = 4000; f5 = 5000; 
 
% Step 4: Modulation 
y1 = u1 .* cos(2*pi*f1*t); 
y2 = u2 .* cos(2*pi*f2*t); 
y3 = u3 .* cos(2*pi*f3*t); 
y4 = u4 .* cos(2*pi*f4*t); 
y5 = u5 .* cos(2*pi*f5*t); 
 
% Step 5: Composite FDMA signal 
composite = y1 + y2 + y3 + y4 + y5; 
 
% Plot composite signal 
figure; 
plot(t, composite, 'LineWidth',1.2); 
title('Composite FDMA Signal'); 
xlabel('Time (s)'); ylabel('Amplitude'); 
 
% Step 6: Receiver side (down-conversion) 
r1 = composite .* cos(2*pi*f1*t) * 2; 
r2 = composite .* cos(2*pi*f2*t) * 2; 
r3 = composite .* cos(2*pi*f3*t) * 2; 
r4 = composite .* cos(2*pi*f4*t) * 2; 
r5 = composite .* cos(2*pi*f5*t) * 2; 
 
% Step 7: Low-pass filter 
rec1 = lowpass(r1, 300, Fs); 
rec2 = lowpass(r2, 300, Fs); 
rec3 = lowpass(r3, 300, Fs); 
rec4 = lowpass(r4, 300, Fs); 
rec5 = lowpass(r5, 300, Fs); 
% Plot input signals 
figure; 
subplot(5,1,1); plot(t,u1); title('Input User 1 (50 Hz)'); 
subplot(5,1,2); plot(t,u2); title('Input User 2 (100 Hz)'); 
subplot(5,1,3); plot(t,u3); title('Input User 3 (150 Hz)'); 
subplot(5,1,4); plot(t,u4); title('Input User 4 (200 Hz)'); 
subplot(5,1,5); plot(t,u5); title('Input User 5 (250 Hz)'); 
% Plot recovered signals 
figure; 
subplot(5,1,1); plot(t,rec1); title('Recovered User 1'); 
subplot(5,1,2); plot(t,rec2); title('Recovered User 2'); 
subplot(5,1,3); plot(t,rec3); title('Recovered User 3'); 
subplot(5,1,4); plot(t,rec4); title('Recovered User 4'); 
subplot(5,1,5); plot(t,rec5); title('Recovered User 5');

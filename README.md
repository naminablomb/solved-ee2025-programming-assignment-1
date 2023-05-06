Download Link: https://assignmentchef.com/product/solved-ee2025-programming-assignment-1
<br>
<strong>Programming Language: </strong>You can use Matlab, Python or any other tool for this programming assignment.

<strong>The Problem: </strong>You will implement digital modulation and demodulation to communicate a binary image file across an additive white Gaussian noise channel. The image file binary image is included with this assignment in numpy and Matlab formats. This is a 110×100 array, where each element is a 0 or a 1. Here, a 0 represents a black pixel and 1 is a white pixel. You can load and render the image in python and Matlab as follows. Do not copy-paste these commands, but manually type them in the command window or terminal.

Python:

import numpy as np

from matplotlib import pyplot as plt MonaLisa = np.load(‘binary image.npy’) plt.imshow(MonaLisa,‘gray’), plt.show()

Matlab:

load binary image.mat imshow(MonaLisa, [0 1])

The image, in all, contains 110 × 100 = 11000 information bits. You will modulate and transmit them using 4-QAM modulation scheme with carrier frequency 2 MHz and symbol duration 1 micro sec, i.e., 2 bits are transmitted per micro second. The receiver will use the optimal demodulator, i.e., the maximum-likelihood detector or the minimum distance detector.

You will simulate the communication for 4 values of E<em><sub>b</sub>/N<sub>o</sub></em>: −10<em>,</em>−5<em>,</em>0<em>,</em>5 dB. For each of these scenarios, you will plot the received image (which will be noisy) and report the number of pixels that were wrongly demodulated. These four figures and the corresponding number of wrong pixels must be reported in a single pdf file.

<strong>Channel model and modulation scheme: </strong>The carrier frequency <em>f<sub>c </sub></em>= 2 MHz and symbol duration <em>T </em>= 1<em>µ </em>sec. Since each symbol carries 2 bits, the overall communication duration is 11000 × <em>T/</em>2 = 5<em>.</em>5 msec. The transmitted waveform <em>s</em>(<em>t</em>) for duration 0 ≤ <em>t &lt; </em>0<em>.</em>0055 is determined as follows. We first order the pixels or information bits in a sequence <em>b</em><sub>1</sub><em>,…,b</em><sub>11000</sub>. For each <em>i </em>= 1<em>,…,</em>5500, we transmit one 4-QAM symbol in the time window (<em>i </em>− 1)<em>T </em>≤ <em>t &lt; iT </em>that modulates the bits <em>b</em><sub>2<em>i</em>−1 </sub>and <em>b</em><sub>2<em>i</em></sub>. The transmitted waveform in this interval is given by

<em>s</em>(<em>t</em>) = <em>x</em><sub>2<em>i</em>−1 </sub>cos(2<em>πf<sub>c</sub>t</em>) + <em>x</em><sub>2<em>i </em></sub>sin(2<em>πf<sub>c</sub>t</em>)<em>, </em>for (<em>i </em>− 1)<em>T </em>≤ <em>t &lt; iT,</em>

where <em>x<sub>j </sub></em>= +1 if <em>b<sub>j </sub></em>= 0 and <em>x<sub>j </sub></em>= −1 if <em>b<sub>j </sub></em>= 1. Given this modulation scheme, you must calculate the energy per information bit E<em><sub>b</sub></em>. This will be required to determine the value of noise power spectral density <em>N<sub>o</sub>/</em>2.

The noise <em>w</em>(<em>t</em>) is modelled as a Gaussian random process with power spectral density equal to <em>N<sub>o</sub>/</em>2 across all frequencies. For a given value of E<em><sub>b</sub>/N<sub>o</sub></em>, you can calculate <em>N<sub>o </sub></em>since E<em><sub>b </sub></em>is already known. The received waveform is

<em>r</em>(<em>t</em>) = <em>s</em>(<em>t</em>) + <em>w</em>(<em>t</em>) for 0 ≤ <em>t &lt; </em>0<em>.</em>0055<em>.</em>

1

<strong>The Discrete-Time Model: </strong>Since we need to simulate the communication scheme using Matlab/python, we need to discretize the channel model. We will use a sampling rate of <em>f<sub>s </sub></em>= 50 MHz. We will assume that the received waveform <em>r</em>(<em>t</em>) is first passed through an ideal low-pass filter with bandwidth −<em>f<sub>s</sub>/</em>2 <em>&lt; f &lt; f<sub>s</sub>/</em>2, and then sampled at rate <em>f<sub>s </sub></em>samples per second. The total number of samples of <em>r</em>(<em>t</em>) will be <em>f<sub>s </sub></em>×0<em>.</em>0055 = 275000, since the communication duration is 5<em>.</em>5 msec. We will make the simplifying assumption that the low pass filtering operation does not distort the transmitted waveform <em>s</em>(<em>t</em>). Under this assumption, the <em>n</em><sup>th </sup>sample is

<em>r</em>[<em>n</em>] = <em>s</em>[<em>n</em>] + <em>w</em>[<em>n</em>] = <em>r</em>(<em>nT<sub>s</sub></em>) = <em>s</em>(<em>nT<sub>s</sub></em>) + <em>w</em>(<em>nT<sub>s</sub></em>)<em>, </em>for <em>n </em>= 0<em>,</em>1<em>,…,</em>274999<em>,</em>

where <em>T<sub>s </sub></em>= 1<em>/f<sub>s</sub></em>. The transmitted signal is captured by the sequence <em>s</em>[<em>n</em>] = <em>s</em>(<em>nT<sub>s</sub></em>) and noise by <em>w</em>[<em>n</em>]. The noise signal <em>w</em>[<em>n</em>] is modelled as composed of independent and identically distributed Gaussian random variables with mean zero and variance <em>f<sub>s </sub></em>× <em>N<sub>o</sub>/</em>2.

Note that the number of samples per QAM symbol is <em>f<sub>s </sub></em>× <em>T </em>= 50, i.e., samples <em>r</em>[0]<em>,…,r</em>[49] correspond to bits <em>b</em><sub>1 </sub>and <em>b</em><sub>2</sub>; the next 50 samples correspond to bits <em>b</em><sub>3 </sub>and <em>b</em><sub>4</sub>, and so on. The receiver uses minimum distance decoding on <em>r</em>[0]<em>,…,r</em>[49] to demodulate <em>b</em><sub>1 </sub>and <em>b</em><sub>2</sub>, and uses the next 50 samples to demodulate <em>b</em><sub>3 </sub>and <em>b</em><sub>4</sub>, and so on.

<strong>Verifying your simulation results: </strong>The bit error rate (BER) of 4-QAM modulation scheme is <em>Q</em>(<sup>p</sup>2E<em><sub>b</sub>/N<sub>o</sub></em>), where <em>Q </em>is the Gaussian tail function. Thus, the number of pixels that are wrongly demodulated will be approximately equal to 11000 × BER. You can use this rule-of-thumb to verify if your program is correct.

2
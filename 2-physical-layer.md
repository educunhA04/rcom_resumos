# PHYSICAL LAYER 

1. [Physical Layer](#physical-layer)
   - [Services Provided](#services-provided)
   - [Signal Transmission](#signal-transmission)
     - [Encoding and Modulation](#encoding-and-modulation)
   - [Bandwidth and Data Rate](#bandwidth-and-data-rate)
   - [Reconstructing the Signal at the Receiver](#reconstructing-the-signal-at-the-receiver)

2. [Types of Modulation](#types-of-modulation)

3. [Baseband vs Passband Transmission](#baseband-vs-passband-transmission)
   - [Baseband Transmission](#baseband-transmission)
     - [Common Baseband Codes](#common-baseband-codes)
     - [Advantages](#advantages-of-baseband-transmission)
     - [Disadvantages](#disadvantages)
     - [Common Applications](#common-applications)
   - [Passband Transmission](#passband-transmission)
     - [Advantages](#advantages-of-passband-transmission)
     - [Disadvantages](#disadvantages-of-passband-transmission)
     - [Common Applications](#common-applications-of-passband-transmission)
   - [Key Differences](#key-differences)

4. [Shannon’s Law](#shannons-law)

5. [Free Space Loss](#free-space-loss)



The Physical Layer is the foundation of the network stack, responsible for the actual transmission of raw data (bits) over a physical medium. It interfaces with the Data Link Layer and ensures the reliable delivery of data at the hardware level.


# Services Provided
- Acts as an **unreliable virtual bit pipe** for higher layers.
- Transmits and receives digital data over physical communication channels.
- Manages the **interfaces** required for data transmission and reception.


# Signal Transmission

- Dependendo do canal utilizado e das suas características físicas, pode-se obter resultados diferentes para um mesmo sinal. 

- Se enviar a mesma transmissão para o mesmo canal duas vezes, não se garante que o resultado seja o mesmo, visto que as características físicas do canal podem ter sido alteradas desde uma emissão para a outra. Ou seja, o canal pode ser `não estacionário` (**exemplos**: `sem fio` - mudanças de posição entre transmissor e recepto, `com fio` - degradação do material). 

- Se as características do canal não tiverem sido alteradas (canal `estacionário`), para uma mesma transmissão, o resultado será o mesmo.

## Encoding and Modulation
- **Encoding**: Converts digital data into an electrical, optical, or radio signal.
- **Modulation**: Alters a carrier signal (amplitude, frequency, or phase) to encode data:
  - **Amplitude Modulation (AM)**: Data encoded in signal amplitude.
  - **Frequency Modulation (FM)**: Data encoded in signal frequency.
  - **Phase Modulation (PM)**: Data encoded in signal phase.
  - **Quadrature Amplitude Modulation (QAM)**: Combines amplitude and phase changes for higher efficiency.

![alt text](/images/physical_layer_images/image-2.png)


1. **Transmitter `S`**:
   - Generates the input signal `s(t)`, representing the transmitted data.
   - Signal can be digital or analog, e.g., rectangular pulses.

2. **Channel `H`**:
   - The medium through which the signal propagates (e.g., wired, optical, or wireless).
   - Modifies `s(t)` due to:
     - **Attenuation**: Reduces the signal amplitude.
     - **Distortion**: Alters the shape of `s(t)` based on the channel's frequency response.
     - **Noise**: Adds unwanted interference.
   - The channel’s effect is represented mathematically by its impulse response `h(t)`.

3. **Receiver `R`**:
   - Receives the output signal `r(t)`, which is the convolution of `s(t)` and `h(t)`:
   - The receiver's goal is to recover the original transmitted data.

**R(f) = S(f) x H(f), f is frequency**


# Bandwidth and Data Rate
## Bandwidth-Limited Signals
- Signals have limited frequency ranges (bandwidth).
- Digital systems use sampling to reconstruct signals:

## Bitrate and Baudrate
- **Bitrate**: Number of bits transmitted per second.
- **Baudrate**: Number of signal changes per second (symbols).

# Reconstructing the Signal at the Receiver
During transmission, the signal \( s(t) \) is modified due to:
- **Attenuation**: Reduction in signal amplitude.
- **Distortion**: Change in signal shape due to the channel's limited bandwidth.
- **Noise**: Addition of random signals, such as thermal noise or electromagnetic interference.
- **Inter-Symbol Interference (ISI)**: Overlapping of adjacent symbols in time, making it harder to distinguish them.

The receiver must compensate for these effects to accurately reconstruct the original data.



## Nyquist’s Theorem**: 
- A signal with bandwidth `B` can be fully reconstructed if sampled at `2B` samples/second.

### Nyquist Sampling Rate
- **Example**:
  - If the channel's bandwidth is `3 kHz`, the minimum sampling rate is `6 kHz`.


### Sampling and Reconstruction
- The receiver measures `r(t)` at regular intervals (`t_1, t_2, t_3,...`).
- These samples are used to determine the transmitted bits.


## Examples of Reconstruction

### Basic Bitrate
- If the channel has a bandwidth `3 kHz` and the receiver samples at `6 kHz`:
  - Each sample represents **1 bit of information**, resulting in a bitrate of `6 kbit/s`.

### Multilevel Modulation
- If the transmitter uses `M = 4` levels to encode bits (e.g., -5 V, -2 V, 2 V, 5 V):
  - Each level carries `2 bits` of information (00, 01, 10, 11).
  - The bitrate `C` increases:
    `C = 2*B*log2(M)`
    - For `B = 3 kHz` and `M = 4`, `C = 12 kbit/s`.
# Types of Modulation
![alt text](/images/physical_layer_images/image-1.png)

# Baseband vs Passband Transmission

Baseband and passband transmissions are two fundamental methods for transmitting signals over communication channels. The choice between the two depends on the type of channel and the application requirements.



## **Baseband Transmission**
Baseband transmission refers to sending a signal that occupies a frequency range starting from near **zero** Hz up to a maximum frequency.

### Characteristics:
- **Frequency Range**: Signal frequencies are from `0` Hz up to `B` Hz (the bandwidth of the signal).
- **Typical Use**: Common for wired communication, such as Ethernet and LANs, where the medium directly supports low-frequency signals.
- **Signal Types**: Binary signals or multilevel digital signals.
- **Transmission Medium**: Usually used in cables (e.g., twisted pair, coaxial) where the signal does not need modulation to fit into a specific frequency band.

### Common Baseband Codes:
Baseband transmission often uses **line coding schemes** to represent data. Below are some of the most common baseband codes:

1. **NRZ-L (Non-Return to Zero-Level)**:
   - Binary `1` is represented by one level (e.g., +5V) and `0` by another level (e.g., 0V or -5V).
   - No transitions between bits unless the bit value changes.
   - **Disadvantage**: Long sequences of `0`s or `1`s make clock synchronization difficult.

2. **NRZ-I (Non-Return to Zero-Inverted)**:
   - A `1` is represented by a change in voltage level, while a `0` is represented by no change.
   - **Advantage**: Solves the problem of clock synchronization for sequences of `1`s.

3. **Manchester Code**:
   - Combines data and clock information in a single signal.
   - Transition in the middle of the bit:
     - `1`: Positive-to-negative transition.
     - `0`: Negative-to-positive transition.
   - **Used in Ethernet (IEEE 802.3)**.

4. **4B/5B Encoding**:
   - Maps groups of 4 data bits into 5 encoded bits to ensure enough transitions for clock recovery.
   - Often combined with physical-level codes like NRZI.
   - **Example Mapping**:
     ```
     Data:  0000 → Encoded: 11110
     Data:  0001 → Encoded: 01001
     Data:  1111 → Encoded: 11101
     ```



### Advantages of Baseband Transmission:
1. Simpler system design (no modulation required).
2. Efficient for short distances where low-frequency signals can propagate without significant attenuation.

### Disadvantages:
1. Limited to short-range communication due to high attenuation at low frequencies.
2. Cannot be used in shared or wireless channels, as signals must fit into specific frequency bands.

### Common Applications:
- Ethernet (e.g., IEEE 802.3 uses Manchester coding).
- Serial communication over twisted pair cables.
- Transmission in digital circuits.



## **Passband Transmission**
Passband transmission involves modulating a baseband signal to shift it to a specific frequency band (carrier frequency) for transmission.

### Characteristics:
- **Frequency Range**: Signal is shifted to a band centered around a carrier frequency `f_c` and spans from `f_c - B/2` to `f_c + B/2`.
- **Typical Use**: Required for wireless communication and systems where multiple signals share the same medium.
- **Signal Types**: Modulated signals (e.g., AM, FM, QAM).
- **Transmission Medium**: Commonly used in wireless, optical fiber, and radio communication, where modulation is necessary to fit into the channel.

### Advantages:
1. Enables multiple signals to coexist in the same medium (frequency-division multiplexing).
2. Suitable for long-distance communication.
3. Can utilize the properties of specific frequency bands (e.g., lower attenuation in higher frequencies for fiber optics).

### Disadvantages:
1. Requires modulation and demodulation, increasing system complexity.
2. Prone to noise in the passband frequency range.

### Common Applications:
- Wireless communication (e.g., cellular networks, Wi-Fi, satellite).
- Optical communication over fiber optics.
- Cable TV and broadband internet.

---

## 3. **Key Differences**

| Feature                | Baseband Transmission                  | Passband Transmission                 |
|------------------------|-----------------------------------------|---------------------------------------|
| **Frequency Range**    | From 0 Hz to the signal bandwidth B. | Around a carrier frequency f_c. |
| **Modulation**         | No modulation required.                | Requires modulation (e.g., AM, QAM).  |
| **Medium**             | Used in wired systems (e.g., cables).  | Used in wireless and shared mediums.  |
| **Applications**       | Ethernet, digital circuits.            | Wi-Fi, cellular, satellite, optical.  |
| **System Complexity**  | Simpler system design.                 | More complex due to modulation.       |
| **Multiplexing**       | Limited to one signal per channel.     | Supports multiple signals per channel.|

# Shannon’s Law
Defines the maximum theoretical capacity (`C`) of a communication channel:

## Noise imposes the limit on the number of levels M (bit/symbol)
- Noise high ➔ low M
- high Signal to Noise Ratio (SNR) ➔ high M

## Maximum theoretical capacity of a channel, C (bit/s)

`C = Bc * log2(1 + Pr / (N0*Bc))`

➔ Bc – bandwidth of the channel (Hz) (see last slide)
Bc = sampling rate

➔ Pr – signal power as seen by receiver (W)

➔ N0 – White noise; noise power per unit bandwidth (W/Hz)

➔ N0Bc – noise power within the bandwidth Bc
, as seen by receiver (W) 

# Free Space Loss

```
Pt/Pr = (4*pi*d)^2 / λ^2 = [(4*pi*d)^2 / λ^2] = [(4*pi*f*d)^2 / c^2], 

λ*f = c
```
- Pt = signal power at transmitting antenna
- Pr = signal power at receiving antenna
- λ = carrier wavelength
- d = propagation distance between antennas
- c = speed of light (3×108 m/s)

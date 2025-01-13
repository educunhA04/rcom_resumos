# PHYSICAL LAYER 

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


# Shannon’s Law
Defines the maximum theoretical capacity (`C`) of a communication channel:


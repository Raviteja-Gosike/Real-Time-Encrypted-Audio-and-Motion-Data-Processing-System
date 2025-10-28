# Encrypted Voice Transmission with Motion Sync  
**A Simulink-based Android application for secure real-time audio and motion data communication**

---

## Overview

This project demonstrates a real-time encrypted audio and motion data transmission system between two Android devices using Simulink Mobile. It integrates digital signal processing (DSP), frequency-domain encryption, and motion synchronization via sensors — showcasing a complete wireless communication framework that runs directly on smartphones.

Developed as part of a Digital Signal Processing application, the system consists of:
- **Sender (Phone A)** – Captures, encrypts, and transmits data.  
- **Receiver (Phone B)** – Decrypts, reconstructs, and plays back data.  

---

## System Architecture

The project is implemented using Simulink models:

| Component | File | Description |
|------------|------|-------------|
| **Sender System** | `sender1.slx` | Captures audio and motion data, encrypts in frequency domain, sends via UDP |
| **Receiver System** | `receiver1.slx` | Receives and decrypts the encrypted audio, synchronizes motion data, and plays sound output |

---

## Working Principle

### 1. Audio Capture and Encryption (Sender Side)
- Audio is recorded at 44.1 kHz using the Android device’s microphones.
- Data is processed in frames (4410×2) and converted to double precision.
- The signal undergoes FFT (Fast Fourier Transform) to move into the frequency domain.
- A frequency-domain scrambling technique is applied by multiplying with an invertible key matrix (P):
  \[
  Y = P \cdot X
  \]
  where **X** is the FFT of the signal, and **P** is the encryption key.
- The encrypted frequency-domain signal is transmitted using the UDP Send block.

### 2. Motion Data Synchronization
- Simultaneously, accelerometer and gyroscope readings (X, Y, Z axes) are collected.
- A frame counter ensures synchronization between audio and motion frames.
- Audio, motion data, and frame number are merged and sent together.

### 3. Decryption and Playback (Receiver Side)
- The receiver extracts the encrypted data stream.
- Frequency-domain descrambling is achieved using the inverse matrix (P⁻¹):
  \[
  X' = P^{-1} \cdot Y
  \]
- The decrypted signal is reconstructed using IFFT (Inverse FFT).
- The real part of the signal is converted to `int16` and played through the Android device’s speaker.
- Motion data is displayed in real-time for visualization.

---

## Technical Details

| Feature | Description |
|----------|-------------|
| **Platform** | Simulink Mobile (MATLAB) |
| **Protocol** | UDP (User Datagram Protocol) |
| **Audio Sampling Rate** | 44.1 kHz |
| **Frame Size** | 4410 × 2 |
| **Encryption Method** | Frequency-domain scrambling using matrix multiplication |
| **Sensors Used** | Accelerometer, Gyroscope |
| **Outputs** | Audio playback, motion display, frame synchronization |

---

## Key Concepts

- **Frequency-Domain Encryption** – Protects audio data by scrambling frequency components with a reversible matrix.  
- **UDP Communication** – Enables lightweight, low-latency real-time transmission.  
- **Motion Synchronization** – Integrates sensor data for future motion-based or interactive communication systems.  
- **Simulink Mobile Integration** – Demonstrates end-to-end DSP system prototyping on Android.

---

## Setup and Usage

1. Open the project in MATLAB/Simulink.  
2. Deploy `sender1.slx` on **Phone A (Sender)** and `receiver1.slx` on **Phone B (Receiver)** using the **Simulink Mobile app**.  
3. Configure the UDP blocks with matching IP addresses and ports on both devices.  
4. Ensure both phones are connected to the same Wi-Fi network.  
5. Run the models:  
   - The sender captures and encrypts voice and motion data.  
   - The receiver decrypts and plays the sound while showing motion activity.

---

## Results

- Successfully achieved real-time encrypted audio streaming with synchronized motion data.  
- Demonstrated frequency scrambling and descrambling with minimal delay.  
- Ensured system operation in a wireless mobile environment using Simulink blocks only.  

---

## Future Enhancements

- Implement dynamic key exchange for stronger encryption.  
- Introduce error correction for UDP packet loss.  
- Extend to multi-device or gesture-based control applications.  

---

## Authors

- **Govindu Vignesh**  
- **Gosike Raviteja**  
- **Bootla Sahasrith**

---

## License

This project is for educational and research purposes.  
Feel free to fork, modify, and build upon it with proper attribution.

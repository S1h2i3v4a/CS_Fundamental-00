# Module 08: Transmission Impairments & Signal Characteristics

## 1. Transmission Impairments ka Parichay
Jab koi analog ya digital signal kisi physical medium (copper cable, optical fiber, ya free space wireless) ke through travel karta hai, to medium ki imperfect physical properties ke karan signal degrade ho jata hai. Is degradation ko **Transmission Impairment** kehte hain.
Iske teen primary causes hote hain:
1. **Attenuation (Loss of signal energy)**
2. **Distortion (Shape deformation)**
3. **Noise (Unwanted external electrical energy)**

---

## 2. The 3 Impairments in Depth

### 2.1 Attenuation (Loss of Energy)
- Medium ki electrical resistance ke karan signal ki electrical/optical power distance ke sath kam hoti jati hai (heat dissipation).
- Agar signal bohot zyada attenuate ho jaye, to receiving antenna ya NIC use background noise se differentiate nahi kar pata.
- **Solution:** Regular intervals par **Amplifiers** (analog signals ke liye) ya **Repeaters** (digital bits regenerate karne ke liye) lagaye jate hain.
- **Decibel (dB) Measurement:**
  $$	ext{dB} = 10 \log_{10}\left(rac{P_2}{P_1}ight)$$
  - Jahan $P_1$ original input power hai aur $P_2$ attenuated output power hai.
  - Agar signal power **half** ho jaye ($P_2 = 0.5 P_1$):
    $$	ext{dB} = 10 \log_{10}(0.5) = 10 	imes (-0.301) pprox -3 	ext{ dB}$$
  - **Voltage Formula:**
    $$	ext{dB} = 20 \log_{10}\left(rac{V_2}{V_1}ight)$$
  - **dB Addition Advantage:** Cascaded systems me stages ko multiply karne ki jagah decibels ko directly add kiya jata hai:
    $$	ext{dB}_{	ext{total}} = 	ext{dB}_1 + 	ext{dB}_2 + 	ext{dB}_3$$

### 2.2 Distortion (Shape Alteration)
- Distortion sirf **Composite Signals** (jo multiple harmonic frequencies se milkar bante hain) me hota hai.
- Har frequency component ki medium me propagation speed thodi alag hoti hai ($v = \lambda f$).
- Iske karan alag-alag frequencies destination par alag-alag arrival phase (time delay) me pahunchti hain, jisse composite signal ka overall waveform distorted ho jata hai (**Delay Distortion / Phase Shift**).

### 2.3 Noise (External Corruption)
Medium me bahar se aane wali unwanted energy jo signal me add hokar bits ko corrupt kar deti hai.
- **4 Types of Noise:**
  1. **Thermal Noise (Johnson-Nyquist / White Noise):** Medium ke conductors me electrons ke random thermal motion ke karan create hota hai. Isse eliminate nahi kiya ja sakta ($N_0 = kTB$).
  2. **Induced Noise:** Motors, generators, fluorescent lights, aur AC transformers ke magnetic fields se induced hone wala noise.
  3. **Crosstalk:** Ek wire pair ka magnetic signal pass wali doosri wire pair me bleed ho jana (e.g., telephone call me doosron ki aawaz sunai dena). Twisted-pair cabling crosstalk kam karta hai.
  4. **Impulse Noise:** Sudden high-voltage spike (e.g., bijli girna / lightning, power surge, relay sparking). Yeh digital communications me burst error ka sabse bada kaaran hai!

---

## 3. Signal-to-Noise Ratio (SNR)
Signal power aur noise power ke ratio ko **SNR** kehte hain:
$$	ext{SNR} = rac{	ext{Average Signal Power}}{	ext{Average Noise Power}}$$
Decibels me represent karne ke liye:
$$	ext{SNR}_{	ext{dB}} = 10 \log_{10}(	ext{SNR})$$

- **High SNR (e.g., 30 dB):** Signal power noise power se 1000 guna zyada hai $\implies$ High quality clean link.
- **Low SNR (e.g., 0 dB):** Signal power aur noise power equal hain $\implies$ Data corrupt hone ke bohot high chances.

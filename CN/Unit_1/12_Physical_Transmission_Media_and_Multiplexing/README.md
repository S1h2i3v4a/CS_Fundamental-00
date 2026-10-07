# Module 12: Physical Transmission Media & Multiplexing

## 1. Transmission Media ka Master Classification
Transmission medium sender aur receiver ke beech physical communication path provide karta hai:
1. **Guided Media (Bounded / Wired Media):** Physical metallic wires ya glass fibers jo signal ko physically guide karti hain.
2. **Unguided Media (Unbounded / Wireless):** Electromagnetic waves jo free air, vacuum, ya water ke through propagate karti hain.

---

## 2. Guided Media in Depth

| Parameter | Twisted Pair Cable | Coaxial Cable | Optical Fiber Cable |
| :--- | :--- | :--- | :--- |
| **Material** | Insulated copper wires twisted in pairs | Center copper core + braided copper shield | Ultra-pure silica glass / plastic core |
| **Transmission Signal** | Electrical voltage signals | Electrical signals | Light pulses (Photons) |
| **Bandwidth Capacity** | Moderate (10 Mbps to 10 Gbps) | High (10 Mbps to 100 Mbps) | Extremely High (Gbps to Terabits/sec) |
| **EMI / Noise Immunity** | Low (STP has moderate immunity) | Good (Braided outer copper shield) | **100% Immune to EMI & RFI** |
| **Attenuation** | High (Repeaters every 100m) | Moderate (Repeaters every 1-2 km) | Lowest (Repeaters every 50-100 km) |
| **Installation & Cost** | Cheapest, very flexible, easy | Moderate cost & flexibility | Expensive, fragile, requires skilled splicing |
| **Standard Connectors** | RJ-45, RJ-11 | BNC, F-type | SC, ST, LC, MTP connectors |

### Optical Fiber ka Physics Principle: Total Internal Reflection (TIR)
Optical fiber glass ke do layers se bana hota hai:
1. **Core:** Inner optical conduit jiska refractive index $n_1$ high hota hai.
2. **Cladding:** Outer glass layer jiska refractive index $n_2$ kam hota hai ($n_2 < n_1$).

**Snell's Law:** Light ray tabhi core ke andar trapped rehti hai jab angle of incidence $	heta$ critical angle $	heta_c$ se bada ho:
$$	heta > 	heta_c = \sin^{-1}\left(rac{n_2}{n_1}ight)$$

---

## 3. Unguided Media (Wireless Transmission)
- **Radio Waves (3 kHz to 1 GHz):** Omnidirectional antenna (waves travel in all directions). Walls penetrate kar sakti hain. E.g., FM Radio, Cordless phones.
- **Microwaves (1 GHz to 300 GHz):** Unidirectional line-of-sight propagation. Waves straight line me travel karti hain aur obstacles se block ho jati hain. Highly focused parabolic dish antennas use hote hain. E.g., Cellular mobile networks, Satellite communication.
- **Infrared (300 GHz to 400 THz):** Short-range closed-room communication. Walls penetrate nahi kar sakti, isliye high security deti hai (padosi ke room me signal leak nahi hota). E.g., TV Remote controls.

---

## 4. Multiplexing Techniques
Multiplexing ek aisi technique hai jisme multiple input data streams ko combine karke single physical link ke through transmit kiya jata hai:

1. **FDM (Frequency Division Multiplexing - Analog):**
   - Channel ki total bandwidth ko multiple non-overlapping frequency bands me divide kiya jata hai.
   - Har sender ko ek dedicated frequency band milti hai.
   - Frequency overlap rokne ke liye adjacent channels ke beech **Guard Bands** rakhe jate hain.
   - *Example:* AM/FM radio, Cable TV.
2. **WDM (Wavelength Division Multiplexing - Optical):**
   - Optical fiber me FDM ka equivalent version.
   - Alag-alag wavelengths (light colors $\lambda_1, \lambda_2, \lambda_3$) ko prism ya diffraction grating se combine kiya jata hai.
   - **DWDM (Dense WDM):** Ek single fiber core par 80+ distinct wavelengths transmit kar sakta hai.
3. **TDM (Time Division Multiplexing - Digital):**
   - Sabhi sources link ki puri bandwidth share karte hain, par alag-alag **Time Slots** me:
     - **Synchronous TDM:** Har device ko fixed pre-assigned time slot milta hai. Agar kisi device ke paas data na ho, to uska time slot empty/waste jata hai.
     - **Statistical TDM (Asynchronous TDM):** Time slots dynamically allocate hote hain (sirf active devices ko). Idle slots eliminate ho jate hain $\implies$ Maximum link efficiency.

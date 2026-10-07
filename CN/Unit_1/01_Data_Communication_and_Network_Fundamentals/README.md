# Module 01: Data Communication & Network Fundamentals

## 1. Data Communication ke 5 Fundamental Components
Data communication do ya do se adhik devices ke beech transmission medium ke through data/information ka exchange hota hai. Is effective communication ke 5 core elements hote hain:

1. **Message (Data Payload):** Wo information ya data jise communicate kiya jana hai. Format text, numbers, images, audio, ya video ho sakta hai.
2. **Sender (Source Device):** Device jo data message generate aur transmit karta hai (e.g., Computer, Workstation, Smartphone, Video Camera).
3. **Receiver (Sink / Destination Device):** Device jo transmitted data message accept karta hai (e.g., Server, Printer, Television).
4. **Transmission Medium (Physical Path):** Physical channel jiske through message sender se receiver tak travel karta hai.
   - *Guided Media (Wired):* Twisted Pair, Coaxial Cable, Fiber Optic Cable.
   - *Unguided Media (Wireless):* Radio waves, Microwaves, Infrared.
5. **Protocol (Governing Rules):** Agreed set of rules jo data communication ko govern karta hai. Bina protocol ke devices physically connected ho sakti hain par communicate nahi kar sakti (jaise do log ek doosre ki bhasha na samajh sakein).

---

## 2. Data Flow & Transmission Modes

| Feature | Simplex Mode | Half-Duplex Mode | Full-Duplex Mode |
| :--- | :--- | :--- | :--- |
| **Directionality** | Unidirectional (Ek hi disha me) | Bidirectional (Dono dishao me, par ek samay me ek) | Bidirectional simultaneously (Ek sath dono dishao me) |
| **Channel Capacity** | Entire capacity used by 1 direction | Shared alternatively in time | Divided between both directions |
| **Performance** | Lowest utilization | Moderate | Highest throughput |
| **Hardware Complexity** | Simple | Moderate | Complex (Separate transmit/receive circuits or carrier splitting) |
| **Real-world Example** | Keyboard to CPU, Traditional TV/Radio | Walkie-Talkie ("Over"), Old Hub networks | Mobile Phone call, Modern Full-Duplex Switch |

---

## 3. Types of Connection: Point-to-Point vs Multipoint

### 3.1 Point-to-Point Connection (Dedicated Link)
- Do specific devices ke beech dedicated physical link hota hai.
- Channel ki entire capacity unhi do devices ke communication ke liye reserved hoti hai.
- *Examples:* TV Remote control and TV sensor, direct cable between two computers, microwave link between two towers.

### 3.2 Multipoint (Multi-drop Connection / Shared Link)
- Ek hi transmission link ko do se adhik devices share karti hain.
- Capacity sharing do tarike se hoti hai:
  - *Spatially Shared:* Agar devices link ko simultaneously use kar sakti hain.
  - *Time Shared (Timeshare):* Agar devices baari-baari (turn-by-turn) link access karti hain.
- *Examples:* Traditional Bus topology with coaxial backbone, Wi-Fi Access Point serving multiple client laptops.

```
Point-to-Point:   [Device A] <=========================> [Device B]  (100% Dedicated Channel)

Multipoint:       [Device A] ----+----------+----------+----- [Terminator]
                                 |          |          |
                              [Drop 1]   [Drop 2]   [Drop 3]  (Shared Channel Capacity)
```

---

## 4. Fundamental Effectiveness Criteria of Data Communication
AKTU exam me bar-bar poochha jane wala core concept:
1. **Delivery:** System ko data strictly intended destination par hi deliver karna chahiye.
2. **Accuracy:** System ko accurate data deliver karna chahiye (unaltered bits). Corrupted data unusable hota hai.
3. **Timeliness:** Data real-time aur bina excessive delay ke pahunchna chahiye (Audio/Video me packet delays intolerable hote hain).
4. **Jitter:** Packet arrival time ke variation ko Jitter kehte hain. High jitter voice/video quality degrade karta hai.

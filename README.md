# 🤖 Robotic Arm Torque & Servo Selection analysis

## task Description
This task involves evaluating a robotic arm with **three joints** (three servo motors) designed to carry a **1 kg payload**. Our objectives are:

### Task 1:
1. Calculate the **torque required at each joint** (for 1 kg payload).
2. Recommend the **best and most appropriate servo motor** for each joint.

### Task 2:
3. Evaluate: Can the **same motors** (selected for 1 kg) lift **2 kg** if we add gears?
4. Analyze the **specific drawbacks** we would face in that 2 kg case.
5. Propose **engineering alternatives** to overcome those specific drawbacks.

---

## Robotic Arm Measurements

| Segment | Length (cm) | Length (m) |
|---------|-------------|------------|
| L1      | 15          | 0.15       |
| L2      | 10          | 0.10       |
| L3      | 4           | 0.04       |

**Total Arm Reach from base to payload: 0.29 m**  
**Payload: 1 kg**  
**Gravity (g): 9.81 m/s²**

---

## 🧮 Torque Calculations — for 1 KG Payload

> **Force = Mass × Gravity = 1 × 9.81 = 9.81 N**

### 🔸 Joint 3 (Wrist)
- Load distance from joint: 0.04 m
- Torque = 9.81 × 0.04 = **0.39 Nm**
- With 1.5× safety margin = **0.59 Nm**

### 🔸 Joint 2 (Elbow)
- Load is 1 kg at 0.04 m + arm L3 (0.04 m from J2)
- Total distance = 0.04 m
- Torque = 9.81 × 0.04 = **0.39 Nm**
- With 1.5× safety margin = **0.59 Nm**

### 🔸 Joint 1 (Base)
- Load at total reach (L2 + L3) = 0.10 + 0.04 = 0.14 m
- Torque = 9.81 × 0.14 = **1.37 Nm**
- With 1.5× safety margin = **2.06 Nm**

| Joint | Load Distance | Torque (Nm) | With Safety Margin |
|-------|----------------|-------------|---------------------|
| J3 (Wrist) | 0.04 m         | 0.39 Nm     | **0.59 Nm**         |
| J2 (Elbow) | 0.04 m         | 0.39 Nm     | **0.59 Nm**         |
| J1 (Base)  | 0.14 m         | 1.37 Nm     | **2.06 Nm**         |

---

## Recommended Servo Motors (For 1 KG)

| Joint | Torque Needed | Servo Recommendation             | Rated Torque | Status        |
|-------|----------------|----------------------------------|--------------|----------------|
| J1    | 2.06 Nm        | **MG996R** or **Dynamixel AX-18A** | ~3–4 Nm     |  Safe         |
| J2    | 0.59 Nm        | **MG90S** or **MG996R**           | ~2–3 Nm     |  Overkill     |
| J3    | 0.59 Nm        | **SG90** or **MG90S**             | ~1–2 Nm     | Suitable     |

> These motors are selected assuming no gear ratios are used and based on the 1 kg payload scenario only.

---

# TASK 2: Can the Same Motors Carry 2 KG With Gears?

### New Load: 2 KG  
> Force = 2 × 9.81 = **19.62 N**

| Joint | Load Point | Required Torque (Nm) | Gear Ratio Needed (approx) |
|-------|------------|-----------------------|-----------------------------|
| J3    | 0.04 m     | 0.78 Nm               | 0.78 / 1.0 = **~0.8×**      |
| J2    | 0.04 m     | 0.78 Nm               | 0.78 / 2.0 = **~0.4×**      |
| J1    | 0.14 m     | 2.75 Nm               | 2.75 / 3.0 = **~0.92×**     |

 So: Yes, the same motors can carry 2 KG if modest gear ratios (1.1×–1.3×) are added where needed.

---

## ⚠️ Specific Cons of Using Gears to Lift 2 KG

| Problem            | Why It Happens (with 2kg)                                                                 |
|--------------------|------------------------------------------------------------------------------------------|
|  Overheating     | Motors work harder, gear friction adds heat                                             |
|  Slow Movement   | Gear reduction sacrifices speed for torque                                              |
|  Inaccuracy      | Gears introduce **backlash** — wobble and lag                                           |
|  Current Drain    | More torque → higher current = faster battery depletion                                |
|  Mechanical Stress | Heavier system and gear forces stress shafts and mounts                                |
| ⚙ Maintenance Need | More moving parts = higher chance of mechanical failure                                |

---

## Engineering Alternatives to Gearing

| Method                        | What It Solves                                                 |
|-------------------------------|------------------------------------------------------------------|
|  Use Higher Torque Servos   | Avoids need for gearing, less stress on components             |
|  Add Counterweights         | Balances torque, reducing motor strain                         |
|  Use Lightweight Materials   | Reduces overall required torque                                |
|  Redesign Arm Geometry      | Keeps center of mass closer to base                            |
|  Stepper Motors + Drivers   | Provide higher torque + precision without servo lag            |
|  Harmonic Drives            | Compact gear solution without backlash                         |
|  Limit Payload to 1.5 kg    | Stays within safe operating range of motors                    |

---

##  Conclusion

- For **1 kg payload**, the updated torque values based on correct arm geometry confirm smaller servos are sufficient.
- For **2 kg**, using minor gears or upgrading motor specs is necessary.
- Gearing adds drawbacks like heat, slow response, and wear.
- Preferred solutions: stronger motors, smarter geometry, or harmonic drives.

---

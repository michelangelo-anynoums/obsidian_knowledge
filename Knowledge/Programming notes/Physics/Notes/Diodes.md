![[Pasted image 20260720142537.png|416]]

# 4.5 Diodes

## **Diodes**

A **diode** is an electronic component that allows electric current to flow mainly in **one direction**.

A diode has two terminals:

- **Anode (+)** → positive side
    
- **Cathode (-)** → negative side
    

The diode works like a **one-way valve** for electric current.

**Example:**  
A water valve lets water pass only in one direction. A diode does the same with electric current.

**Symbol:**

```
A ----|>|---- K
     diode
```

The arrow-like side shows the direction of **conventional current flow**.

---

## **One-way current flow**

A diode allows current to pass when it is **forward biased**.

**Forward bias:**

- Anode is connected to positive voltage.
    
- Cathode is connected to negative voltage.
    
- Current flows through the diode.
    

A diode blocks current when it is **reverse biased**.

**Reverse bias:**

- Anode is connected to negative voltage.
    
- Cathode is connected to positive voltage.
    
- Almost no current flows.
    

A silicon diode usually needs about **0.7 V** before it starts conducting.

**Important idea:**

**Forward bias → current flows**  
**Reverse bias → current is blocked**

---

## **Rectification**

**Rectification** is the process of converting **alternating current (AC)** into **direct current (DC)**.

AC changes direction many times per second.  
DC flows only in one direction.

Diodes are used in **rectifier circuits** because they only allow current to move one way.

**Example:**

A phone charger uses diodes to convert:

```
AC from wall socket → DC for battery
```

A simple half-wave rectifier:

```
AC source ---->|---- Load
              diode
```

Only one half of the AC signal passes through.

---

## **Protection circuits**

Diodes can protect electronic components from **wrong voltage or wrong current direction**.

Common protection uses:

- **Reverse polarity protection** → prevents damage if a battery is connected incorrectly.
    
- **Voltage protection** → protects circuits from high voltage spikes.
    
- **Flyback diode** → protects circuits with motors or relays.
    

**Example:**

A motor can create a sudden voltage spike when it is switched off. A diode connected across the motor absorbs this spike and protects the circuit.

![[Pasted image 20260720143433.png|671]]

---

# Simple resolved examples

## **Example 1: Diode direction**

**Question:**  
A diode has its anode connected to +5 V and its cathode connected to 0 V. Does current flow?

**Solution:**

- Anode = positive
    
- Cathode = negative
    
- The diode is **forward biased**.
    

**Answer:**

Current flows through the diode.

---

## **Example 2: Diode voltage**

**Question:**  
A silicon diode has an input voltage of 5 V and a forward voltage of 0.7 V. What voltage reaches the resistor?

**Formula:**

V_resistor = V_input - V_diode

**Calculation:**

V_resistor = 5 V - 0.7 V

V_resistor = 4.3 V

**Answer:**

The resistor receives approximately **4.3 V**.

---

## **Example 3: Rectification**

**Question:**  
A diode is placed in an AC circuit. What happens during the negative half of the AC wave?

**Solution:**

During the negative half:

- The diode becomes **reverse biased**.
    
- Current cannot pass.
    

**Answer:**

Only the positive half of the AC signal passes, creating a pulsating DC output.

---

# Key ideas

- A **diode** allows current to flow mainly in **one direction**.
    
- **Forward bias** allows current flow.
    
- **Reverse bias** blocks current.
    
- Diodes are used for **rectification** and **circuit protection**.
    
- A silicon diode has a typical voltage drop of about **0.7 V**.
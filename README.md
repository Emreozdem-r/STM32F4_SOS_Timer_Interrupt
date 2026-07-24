# STM32F4 Non-Blocking S.O.S. Morse Code

This project implements an S.O.S. Morse code transmitter using **TIM2 Hardware Interrupt** on an STM32F4 Discovery board without using blocking delay functions like `HAL_Delay()`.

## 🛠 Features
- **Non-Blocking Architecture:** Uses a millisecond hardware timer interrupt (`ms_counter`) to handle timings, keeping the main loop (`while(1)`) completely unblocked.
- **Data-Driven Logic:** Uses an array and modulo arithmetic (`step % 2`) instead of long `if-else` chains.
- **Microsecond Precision:** Configured with STM32 internal clock settings.

## 📐 Timer Calculation
To achieve a **1 ms** hardware interrupt frequency ($1\text{ kHz}$) with a $16\text{ MHz}$ HSI clock:

$$\text{Interrupt Frequency} = \frac{16.000.000\text{ Hz}}{(PSC + 1) \times (ARR + 1)}$$

* **Prescaler (PSC):** $15$
* **Auto-Reload Register (ARR):** $999$
* **Result:** $\frac{16.000.000}{16 \times 1000} = 1000\text{ Hz} \rightarrow 1\text{ ms}$

## 🚀 S.O.S. Timing Sequence
* **Dot (.):** 250 ms ON, 250 ms OFF
* **Dash (-):** 750 ms ON, 250 ms OFF
* **Pause:** 1500 ms OFF after full S.O.S. transmission

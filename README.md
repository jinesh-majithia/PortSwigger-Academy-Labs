# PortSwigger Web Security Academy: Advanced Track
## Vulnerability Focus: Race Conditions & Multi-Endpoint Logic Flaws

Welcome to my security research and learning repository. As part of my transition from Data Operations into Cybersecurity, I am documenting my practical, hands-on labs from the **PortSwigger Web Security Academy**. This repository serves as a portfolio of my technical capabilities, analytical mindset, and commitment to continuous learning.

This specific module deep-dives into exploiting **sub-millisecond collision windows** via race conditions, moving past textbook theories to practical, multi-endpoint exploitation using advanced network synchronization techniques.

---

## 🛠️ Lab Demonstration: Single-Packet Attack Execution

Below is the walkthrough video demonstrating the successful exploitation of a race condition using the **single-packet attack technique**. 

> 💡 **Note for Reviewers / Recruiters:** If you have cloned this repository locally, the video file can be found at `assets/race-condition-exploit.mp4`.

![Race Condition Exploit Demonstration](assets/race-condition-exploit.mp4)

*If your markdown reader does not support native MP4 playback, you can view or download the raw file directly from the `/assets` directory of this repository.*

---

## 🧠 Key Technical Takeaways & Core Concepts

### 1. The Sub-Millisecond Collision Window
In standard multi-threaded web environments, application logic often operates under the false assumption of sequential execution (Step A $
ightarrow$ Step B $
ightarrow$ Step C). A race condition weaponizes the minuscule fraction of time between a state verification (e.g., checking if a discount code is valid) and a state modification (e.g., marking that code as consumed). If multiple requests hit that exact gap simultaneously, the logic collapses.

### 2. Overcoming Network Jitter (The Single-Packet Attack)
Traditionally, executing race conditions over the WAN was considered highly unreliable due to network jitter—natural variations in packet travel times across the internet. If Request 1 arrives even $1	ext{ms}$ before Request 2, the attack fails.

The **Single-Packet Attack technique** completely eliminates this limitation:
* **Connection Warm-Up:** The attacker sends initial TCP and HTTP protocol structures to warm up the connection path.
* **Request Pipelining:** Multiple requests are sent over a single HTTP/2 or HTTP/1.1 connection, but the final, critical bytes of each request are intentionally withheld.
* **The Release:** The final bytes of *all* distinct requests are packed into a **single TCP packet**. The upstream server receives and untangles them at the exact same microsecond, guaranteeing simultaneous processing and forcing a logic collision regardless of internet latency.

### 3. The Operations-to-Security Bridge
Coming from a Data Operations background, this lab was a massive paradigm shift. In production monitoring, we track unexpected spikes, latency shifts, and data anomalies as stability indicators. This research proved to me that those exact anomalies are often the systemic footprints of an attacker manipulating application state timing. Security and operations are fundamentally two sides of the same coin.

---

## 📈 Current Progress & Continuous Learning Commitment
* **Completed:** Race Conditions (Basic to Advanced Multi-Endpoint Labs)
* **In Progress:** Authentication Vulnerabilities & Business Logic Flaws
* **Objective:** Complete the entire PortSwigger Web Security Academy portfolio to build a robust, defensive engineering mindset.

---

## 🔗 Connected Write-ups
For a higher-level breakdown of my journey and how timing flaws intersect with enterprise data operations, read my featured article on Medium:
👉 [Beyond the Clock: What Web Security Academy Taught Me About the Hidden Chaos of Race Conditions](https://medium.com/@jineshcanada23/beyond-the-clock-what-web-security-academy-taught-me-about-the-hidden-chaos-of-race-conditions-607b55e96170)

---
*Looking to collaborate or discussing AppSec / SecOps roles? Feel free to open an issue or connect with me directly via LinkedIn!*

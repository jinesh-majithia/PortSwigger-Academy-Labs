# PortSwigger Web Security Academy: Portfolio & Lab Walkthroughs

Welcome to my security research and learning repository. As part of my transition from Data Operations into Cybersecurity, I am documenting my practical, hands-on labs from the **PortSwigger Web Security Academy**. This repository serves as a portfolio of my technical capabilities, analytical mindset, and commitment to continuous learning.

---

## 📈 Current Progress & Portfolio Index
* **Completed:** Race Conditions (Advanced Multi-Endpoint Tracks) & SQL Injection Fundamentals
* **In Progress:** Authentication Vulnerabilities & Business Logic Flaws
* **Objective:** Complete the PortSwigger Web Security Academy tracks to build a robust, defensive engineering mindset.

---

## 🏎️ Topic 1: Race Conditions

### Lab: Multi-Endpoint Race Conditions & The Single-Packet Attack
**Difficulty:** EXPERT / ADVANCED

This specific module deep-dives into exploiting **sub-millisecond collision windows** via race conditions, moving past textbook theories to practical, multi-endpoint exploitation using advanced network synchronization techniques.

#### 🛠️ Lab Demonstration
Below is the walkthrough video demonstrating the successful exploitation of a race condition using the **single-packet attack technique**. Click the image below to watch the full execution on YouTube:

[![Race Condition Exploit Demonstration](https://img.youtube.com/vi/KzBjZbQsIZY/0.jpg)](https://www.youtube.com/watch?v=KzBjZbQsIZY)

#### 🧠 Key Technical Takeaways & Core Concepts
* **The Sub-Millisecond Collision Window:** In standard multi-threaded web environments, application logic often operates under the false assumption of sequential execution. A race condition weaponizes the minuscule fraction of time between a state verification (e.g., checking if a discount code is valid) and a state modification (e.g., marking that code as consumed).
* **Overcoming Network Jitter:** Traditionally, executing race conditions over the WAN was considered highly unreliable due to network jitter. The **Single-Packet Attack technique** eliminates this by syncing requests over HTTP/2 or HTTP/1.1 pipelining, withholding the final critical bytes, and releasing them inside a **single TCP packet** so the upstream server processes them simultaneously.
* **The Operations-to-Security Bridge:** Coming from a Data Operations background, this was a massive paradigm shift. In production monitoring, we track unexpected spikes and latency shifts as stability indicators. This research proved that those exact anomalies are often the systemic footprints of an attacker manipulating application state timing.

#### 🔗 Connected Write-up
👉 [Beyond the Clock: What Web Security Academy Taught Me About the Hidden Chaos of Race Conditions](https://medium.com/@jineshcanada23/beyond-the-clock-what-web-security-academy-taught-me-about-the-hidden-chaos-of-race-conditions-607b55e96170)

---

## 💉 Topic 2: SQL Injection (SQLi)

### 1. Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
**Difficulty:** APPRENTICE

#### 🛠️ Lab Demonstration
Below is the walkthrough video demonstrating the successful manipulation of the application's SQL query constraints to uncover hidden, unreleased database records. Click the image below to watch the execution on YouTube:

[![SQLi Hidden Data Lab Walkthrough](https://img.youtube.com/vi/ic0IIMJwGNs/0.jpg)](https://youtu.be/ic0IIMJwGNs)

#### 🧠 Technical Summary
The application features a product category filter that directly concatenates user input into a SQL query (`SELECT * FROM products WHERE category = 'Gifts' AND released = 1`). By injecting a conditional override payload (`'+OR+1=1--`), the trailing logic is commented out and the query is forced to evaluate to true for all rows, dumping unreleased product data to the UI.

#### 🔗 Connected Write-up
👉 [Breaking the Filter: How I Unlocked Hidden Application Data via SQL Injection](https://medium.com/@jineshcanada23/breaking-the-filter-how-i-unlocked-hidden-application-data-via-sql-injection-2ea072a5fe96)

---

### 2. Lab: SQL injection vulnerability allowing login bypass
**Difficulty:** APPRENTICE

#### 🛠️ Lab Demonstration
Below is the walkthrough video demonstrating how a SQL injection flaw in a login form can be exploited to bypass authentication entirely and log in as the administrative user without knowing the password credential. Click the image below to watch the execution on YouTube:

[![SQLi Login Bypass Lab Walkthrough](https://img.youtube.com/vi/sDU4JxlWrnY/0.jpg)](https://www.youtube.com/watch?v=sDU4JxlWrnY)

#### 🧠 Technical Summary
The vulnerability exists in the username input field, which feeds directly into the login database query loop (`SELECT * FROM users WHERE username = 'USER_INPUT' AND password = 'USER_INPUT'`). By entering `administrator'--`, the query structure is truncated after the username validation, completely short-circuiting the password verification layer and granting full administrative access.

#### 🔗 Connected Write-up
👉 [Learning SQL Injection Through a Login Bypass Lab: PortSwigger Walkthrough](https://medium.com/@jineshcanada23/learning-sql-injection-through-a-login-bypass-lab-portswigger-walkthrough-af05059e5b42)

---

*Looking to collaborate or discussing AppSec / SecOps roles? Feel free to open an issue or connect with me directly via [LinkedIn](https://www.linkedin.com/in/jineshmajithia/)!*

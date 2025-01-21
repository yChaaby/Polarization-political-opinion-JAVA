# Distributed Opinion Interaction System  

## Project Overview  
This project simulates a distributed system where users, referred to as "agents," interact and share opinions on various topics. The system incorporates diverse user roles with specific behaviors and decision-making mechanisms, aiming to model social interactions, consensus-building, and opinion dynamics.  

The system operates using Java RMI (Remote Method Invocation) to enable distributed communication, ensuring seamless interaction between users.  

---

## Features  

### Roles of Agents  

1. **Users**  
   - Assign an opinion \( O_A(T) \) (a value between 0 and 1) to topics.  
   - Share opinions with other users.  

2. **Critical Thinkers (CTs)**  
   - Verify evidence before updating their opinion.  
   - Accept evidence \( x \) only if it meets predefined criteria (e.g., \( x \) is a multiple of 7).  

3. **Influencers**  
   - Broadcast opinions to multiple users.  
   - Resist changes to their opinions.  
   - Do not provide evidence when interacting.  

4. **Proposers**  
   - Introduce new topics for discussion.  
   - Notify all users about newly discussed topics.  

5. **Consensus Finders (CFs)**  
   - Facilitate consensus by averaging the opinions of two agents:  
     \[
     O_{\text{new}}(T) = \frac{O_A(T) + O_B(T)}{2}
     \]

6. **Polarimeters**  
   - Measure system polarization on a topic \( T \) at regular intervals using the Esteban and Ray formula:  
     \[
     P = K \sum_{i \in I} \sum_{j \in I} \pi_i^{1+\alpha} \pi_j |m_i - m_j|
     \]
     Where:  
     - \( K > 0 \) is a normalization constant,  
     - \( \pi_i \) is the number of agents in interval \( i \),  
     - \( m_i \) is the midpoint of interval \( i \),  
     - \( \alpha = 1.6 \).  

---

## Architecture  

1. **Central Server**  
   - Provides users with IP addresses and ports of intended recipients.  
   - Does not store opinions, influences, or topics.  

2. **Users**  
   - Communicate directly using Java RMI.  

---

## Non-Functional Requirements  

1. **Randomized Behavior**  
   - Random numbers determine opinions, influence degrees, evidence, and interaction frequencies.  

2. **Logging**  
   - Use Java Logging to track system events, including:  
     - Messages sent and received,  
     - Opinion updates,  
     - Evidence validation results.  

3. **Synchronization and Communication**  
   - Java RMI ensures distributed communication.  
   - Synchronize threads to handle delays or missing messages.  

---

## Usage  

1. **Run Proposer**  
   ```bash
   java Proposer --topic="Are vaccines good?"

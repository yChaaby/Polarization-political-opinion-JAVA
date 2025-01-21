# Distributed Opinion Interaction System

## Overview
This project is a distributed system where users (agents) interact and exchange opinions on various topics. The system models user behaviors, including opinion updates, critical thinking, broadcasting by influencers, proposing new topics, consensus finding, and measuring polarization.

## Team

Our team is composed of passionate students:

- **Youssef**: Team Lead and System Architect passionate about Software Engineering and Data-driven solutions.
- **Mazigh**: Developer and passionate about Data Engineering and Analysis.
- **Koceila**: Developer and passionate Data Science & Consulting.

We work collaboratively to ensure the success of this project, leveraging diverse skills and expertise.
## Features

### Opinion Update Formula
When agent **B** receives a message from agent **A**, **B**'s opinion on a topic **T** is updated using the following formula:

$O_B'(T) = O_B(T) + (O_A(T) - O_B(T)) \times i_{AB}$

- $O_B'(T)$: New opinion of **B** on topic **T**.
- $O_B(T)$: Current opinion of **B** on topic **T**.
- $O_A(T)$: Opinion of **A** on topic **T**.
- $i_{AB}$: Degree of influence of **A** on **B**, where $i_{AB} \in (0, 1]$.

### Consensus Formula
A Consensus Finder helps two agents, **A** and **B**, reach a consensus on a topic **T**. Their opinions are updated to the average:

$O_{new}(T) = \frac{O_A(T) + O_B(T)}{2}$

### Polarization Formula
The system's polarization on a topic **T** is measured using the Esteban and Ray formula:

$P = K \sum_{i \in I} \sum_{j \in I} \pi_i^{1+\alpha} \pi_j |m_i - m_j|$

- $K > 0$: Normalization constant.
- $\pi_i$: Number of agents in interval $i$.
- $m_i$: Midpoint of interval $i$.
- $\alpha = 1.6$: Parameter controlling sensitivity to polarization.

## Agent Roles
- **Critical Thinkers (CT):** Validate opinions by requesting evidence before updating their opinions. They do not update opinions based on messages from influencers.
- **Influencers:** Broadcast their opinions to multiple users but resist changing their own opinions and do not provide evidence.
- **Proposers:** Introduce new topics for discussion, which are announced to all users by the server.
- **Consensus Finders (CF):** Facilitate discussions between agents to reach a consensus on a topic.
- **Polarimeters:** Measure system polarization on a given topic at regular intervals.

## System Architecture
The system is built using Java RMI (Remote Method Invocation) with a client-server architecture. Users log in to a centralized server to obtain IP addresses and ports for communication. Communication between users is direct (point-to-point) after initial contact through the server.

## Non-Functional Requirements
- Random numbers are used to simulate behavior, such as initial opinions, degrees of influence, and evidence validation.
- ~~Java Logging is implemented to track events, including message arrivals, opinion updates, and evidence validation failures.~~
- Thread synchronization is carefully managed to ensure proper communication and avoid conflicts.

## Usage
Run agents with the following commands:
- Proposer:
    ```bash
  cd ./Client/src
  java Proposer
- Polarimeter:
    ```bash
  cd ./Client/src
  java Polarimeter
- Server:
  ```bash
  cd ./Server/src
  java Main #(you can rename it as needed; "server" would be a very good choice)

## License
None ...

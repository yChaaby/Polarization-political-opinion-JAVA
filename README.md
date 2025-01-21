# Distributed Opinion Interaction System

## Overview
This project is a distributed system where users (agents) interact and exchange opinions on various topics. The system models user behaviors, including opinion updates, critical thinking, broadcasting by influencers, proposing new topics, consensus finding, and measuring polarization.

## Features

### Opinion Update Formula
When agent **B** receives a message from agent **A**, **B**'s opinion on a topic **T** is updated using the following formula:

**O<sub>B</sub>'(T) = O<sub>B</sub>(T) + (O<sub>A</sub>(T) - O<sub>B</sub>(T)) × i<sub>AB</sub>**

- **O<sub>B</sub>'(T)**: New opinion of **B** on topic **T**.
- **O<sub>B</sub>(T)**: Current opinion of **B** on topic **T**.
- **O<sub>A</sub>(T)**: Opinion of **A** on topic **T**.
- **i<sub>AB</sub>**: Degree of influence of **A** on **B**, where **i<sub>AB</sub> ∈ (0, 1]**.

### Consensus Formula
A Consensus Finder helps two agents, **A** and **B**, reach a consensus on a topic **T**. Their opinions are updated to the average:

**O<sub>new</sub>(T) = (O<sub>A</sub>(T) + O<sub>B</sub>(T)) / 2**

### Polarization Formula
The system's polarization on a topic **T** is measured using the Esteban and Ray formula:

**P = K ∑<sub>i ∈ I</sub> ∑<sub>j ∈ I</sub> π<sub>i</sub><sup>1+α</sup> π<sub>j</sub> |m<sub>i</sub> - m<sub>j</sub>|**

- **K > 0**: Normalization constant.
- **π<sub>i</sub>**: Number of agents in interval **i**.
- **m<sub>i</sub>**: Midpoint of interval **i**.
- **α = 1.6**: Parameter controlling sensitivity to polarization.

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
- Java Logging is implemented to track events, including message arrivals, opinion updates, and evidence validation failures.
- Thread synchronization is carefully managed to ensure proper communication and avoid conflicts.

## Usage
Run agents with the following commands:
- Proposer: `java Proposer --topic="are vaccines good?"`
- Polarimeter: `java Polarimeter --delay=5000`

## License
This project is licensed under the MIT License.

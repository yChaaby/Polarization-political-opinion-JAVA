<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Distributed Opinion Interaction System</title>
</head>
<body>
    <h1>Distributed Opinion Interaction System</h1>
    
    <h2>Overview</h2>
    <p>
        This project is a distributed system where users (agents) interact and exchange opinions on various topics. 
        The system models user behaviors, including opinion updates, critical thinking, broadcasting by influencers, 
        proposing new topics, consensus finding, and measuring polarization.
    </p>
    
    <h2>Features</h2>

    <h3>Opinion Update Formula</h3>
    <p>
        When agent <em>B</em> receives a message from agent <em>A</em>, <em>B</em>'s opinion on a topic <em>T</em> 
        is updated using the following formula:
    </p>
    <p>
        <code>O<sub>B</sub>'(T) = O<sub>B</sub>(T) + (O<sub>A</sub>(T) - O<sub>B</sub>(T)) × i<sub>AB</sub></code>
    </p>
    <ul>
        <li><code>O<sub>B</sub>'(T)</code>: New opinion of <em>B</em> on topic <em>T</em>.</li>
        <li><code>O<sub>B</sub>(T)</code>: Current opinion of <em>B</em> on topic <em>T</em>.</li>
        <li><code>O<sub>A</sub>(T)</code>: Opinion of <em>A</em> on topic <em>T</em>.</li>
        <li><code>i<sub>AB</sub></code>: Degree of influence of <em>A</em> on <em>B</em>, where <code>i<sub>AB</sub> ∈ (0, 1]</code>.</li>
    </ul>

    <h3>Consensus Formula</h3>
    <p>
        A Consensus Finder helps two agents, <em>A</em> and <em>B</em>, reach a consensus on a topic <em>T</em>. Their opinions are updated to the average:
    </p>
    <p>
        <code>O<sub>new</sub>(T) = (O<sub>A</sub>(T) + O<sub>B</sub>(T)) / 2</code>
    </p>

    <h3>Polarization Formula</h3>
    <p>
        The system's polarization on a topic <em>T</em> is measured using the Esteban and Ray formula:
    </p>
    <p>
        <code>P = K ∑<sub>i ∈ I</sub> ∑<sub>j ∈ I</sub> π<sub>i</sub><sup>1+α</sup> π<sub>j</sub> |m<sub>i</sub> - m<sub>j</sub>|</code>
    </p>
    <ul>
        <li><code>K > 0</code>: Normalization constant.</li>
        <li><code>π<sub>i</sub></code>: Number of agents in interval <em>i</em>.</li>
        <li><code>m<sub>i</sub></code>: Midpoint of interval <em>i</em>.</li>
        <li><code>α = 1.6</code>: Parameter controlling sensitivity to polarization.</li>
    </ul>

    <h2>Agent Roles</h2>
    <ul>
        <li><strong>Critical Thinkers (CT):</strong> Validate opinions by requesting evidence before updating their opinions. They do not update opinions based on messages from influencers.</li>
        <li><strong>Influencers:</strong> Broadcast their opinions to multiple users but resist changing their own opinions and do not provide evidence.</li>
        <li><strong>Proposers:</strong> Introduce new topics for discussion, which are announced to all users by the server.</li>
        <li><strong>Consensus Finders (CF):</strong> Facilitate discussions between agents to reach a consensus on a topic.</li>
        <li><strong>Polarimeters:</strong> Measure system polarization on a given topic at regular intervals.</li>
    </ul>

    <h2>System Architecture</h2>
    <p>
        The system is built using Java RMI (Remote Method Invocation) with a client-server architecture. Users log in to a centralized server to obtain IP addresses and ports for communication. 
        Communication between users is direct (point-to-point) after initial contact through the server.
    </p>

    <h2>Non-Functional Requirements</h2>
    <ul>
        <li>Random numbers are used to simulate behavior, such as initial opinions, degrees of influence, and evidence validation.</li>
        <li>Java Logging is implemented to track events, including message arrivals, opinion updates, and evidence validation failures.</li>
        <li>Thread synchronization is carefully managed to ensure proper communication and avoid conflicts.</li>
    </ul>

    <h2>Usage</h2>
    <p>Run agents with the following commands:</p>
    <ul>
        <li>Proposer: <code>java Proposer --topic="are vaccines good?"</code></li>
        <li>Polarimeter: <code>java Polarimeter --delay=5000</code></li>
    </ul>

    <h2>License</h2>
    <p>This project is licensed under the MIT License.</p>
</body>
</html>

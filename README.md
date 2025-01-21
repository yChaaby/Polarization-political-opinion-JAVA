\documentclass[a4paper,12pt]{article}
\usepackage{amsmath}
\usepackage{hyperref}
\usepackage{geometry}

\geometry{margin=1in}

\title{Distributed Opinion Interaction System}
\author{}
\date{}

\begin{document}

\maketitle

\section*{Project Overview}
This project simulates a distributed system where users, referred to as "agents," interact and share opinions on various topics. The system incorporates diverse user roles with specific behaviors and decision-making mechanisms, aiming to model social interactions, consensus-building, and opinion dynamics.

The system operates using Java RMI (Remote Method Invocation) to enable distributed communication, ensuring seamless interaction between users.

\section*{Features}

\subsection*{Roles of Agents}

\begin{itemize}
    \item \textbf{Users}  
    \begin{itemize}
        \item Assign an opinion \( O_A(T) \) (a value between 0 and 1) to topics.  
        \item Share opinions with other users.  
    \end{itemize}

    \item \textbf{Critical Thinkers (CTs)}  
    \begin{itemize}
        \item Verify evidence before updating their opinion.  
        \item Accept evidence \( x \) only if it meets predefined criteria (e.g., \( x \) is a multiple of 7).  
    \end{itemize}

    \item \textbf{Influencers}  
    \begin{itemize}
        \item Broadcast opinions to multiple users.  
        \item Resist changes to their opinions.  
        \item Do not provide evidence when interacting.  
    \end{itemize}

    \item \textbf{Proposers}  
    \begin{itemize}
        \item Introduce new topics for discussion.  
        \item Notify all users about newly discussed topics.  
    \end{itemize}

    \item \textbf{Consensus Finders (CFs)}  
    \begin{itemize}
        \item Facilitate consensus by averaging the opinions of two agents:  
        \[
        O_{\text{new}}(T) = \frac{O_A(T) + O_B(T)}{2}
        \]
    \end{itemize}

    \item \textbf{Polarimeters}  
    \begin{itemize}
        \item Measure system polarization on a topic \( T \) at regular intervals using the Esteban and Ray formula:  
        \[
        P = K \sum_{i \in I} \sum_{j \in I} \pi_i^{1+\alpha} \pi_j |m_i - m_j|
        \]
        Where:  
        \begin{itemize}
            \item \( K > 0 \) is a normalization constant,  
            \item \( \pi_i \) is the number of agents in interval \( i \),  
            \item \( m_i \) is the midpoint of interval \( i \),  
            \item \( \alpha = 1.6 \).  
        \end{itemize}
    \end{itemize}
\end{itemize}

\section*{Architecture}

\subsection*{Central Server}
\begin{itemize}
    \item Provides users with IP addresses and ports of intended recipients.  
    \item Does not store opinions, influences, or topics.  
\end{itemize}

\subsection*{Users}
\begin{itemize}
    \item Communicate directly using Java RMI.  
\end{itemize}

\section*{Non-Functional Requirements}

\begin{enumerate}
    \item \textbf{Randomized Behavior}  
    Random numbers determine opinions, influence degrees, evidence, and interaction frequencies.

    \item \textbf{Logging}  
    Use Java Logging to track system events, including:  
    \begin{itemize}
        \item Messages sent and received,  
        \item Opinion updates,  
        \item Evidence validation results.  
    \end{itemize}

    \item \textbf{Synchronization and Communication}  
    Java RMI ensures distributed communication. Synchronize threads to handle delays or missing messages.
\end{enumerate}

\section*{Usage}

\subsection*{Run Proposer}
\begin{verbatim}
java Proposer --topic="Are vaccines good?"
\end{verbatim}

\subsection*{Run Polarimeter}
\begin{verbatim}
java Polarimeter --delay=5000
\end{verbatim}

\section*{Formula References}

\subsection*{Opinion Update Formula}
\[
O_B'(T) = O_B(T) + (O_A(T) - O_B(T)) \cdot i_{AB}
\]
Where \( i_{AB} \in (0, 1] \) is the influence of agent \( A \) on \( B \).

\end{document}

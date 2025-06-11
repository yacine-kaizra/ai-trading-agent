# ai-trading-agent
\documentclass[11pt]{article}
\usepackage{geometry}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage{listings}
\usepackage{color}
\usepackage{enumitem}

\geometry{margin=1in}
\title{\textbf{AI Trading Agent Using A* and Greedy Search}}
\author{Yacine Kaizra}


\begin{document}

\maketitle

\section*{Abstract}
This document describes the architecture and implementation of an AI trading agent that uses \textbf{A* search} and \textbf{Greedy Search} algorithms to simulate optimal investment decisions on historical stock data. The agent dynamically generates a state space of possible actions (buy/sell/hold) while respecting financial constraints (available funds, diversification limits). Heuristic scores guide the search toward maximizing portfolio value.

\section{Overview}
The trading agent operates on historical stock price data (e.g., 2023–2024) and simulates trades to maximize returns. It evaluates sequences of actions (buy/sell/hold) for a given set of stocks (e.g., \texttt{["AAPL", "MSFT", "TSLA"]}) and outputs the most profitable path based on heuristic-driven search algorithms.

\section{Workflow Summary}
\begin{enumerate}[label=\textbf{\arabic*.}]
    \item \textbf{Data Retrieval}: Fetch historical prices using \texttt{yfinance} (daily close prices for the specified period).
    \item \textbf{State Space Generation}: Construct a tree of valid actions (buy/sell/hold) for each stock.
    \item \textbf{Heuristic Design}: Assign scores to actions based on price trends, portfolio impact, and risk.
    \item \textbf{Search Algorithm}: Use A* or Greedy Search to find the optimal action sequence.
    \item \textbf{Portfolio Update}: Track cash, owned shares, and portfolio value after each trade.
\end{enumerate}

\section{Technical Details}
\subsection*{1. State Space Construction}
The agent builds a state space where each node represents a portfolio state (cash, owned shares). Actions branch into:

    
- \texttt{BUY <stock>}: Requires sufficient funds.
    
- \texttt{SELL <stock>}: Requires ownership of the stock.
    
- \texttt{HOLD}: No change to the portfolio.


Invalid nodes are pruned:

    
- No purchase if funds are insufficient.
    
- No sale if stock is not owned.
    
- No purchase if stock allocation exceeds 20\% of total portfolio value.


\subsection*{2. Heuristic Design}
Each action receives a heuristic score $ h \in [0.01, 1.0] $, normalized across stocks to ensure fairness. Scores are calculated 


\subsubsection*{Normalization}
Scores are scaled to $[0.01, 1.0]$ to prevent dominance by any single factor:

\subsection*{3. Search Algorithms}

    
- \textbf{A* Search and Greedy Search}}: Uses a max-heap priority queue to explore paths with the highest cumulative heuristic score.
    



\subsection*{4. Portfolio Management}
The \texttt{Stocks} class tracks:

    
- Current cash balance.
    
- Owned shares per stock.
    
- Portfolio value (cash + market value of shares).


Constraints:

    
- Diversification limit: No single stock > 20\% of total portfolio value.
    
- Transaction validation (e.g., no selling unowned shares).


\section{Code Structure}
\begin{lstlisting}[language=Python, caption=Example State Space Node]
{
    'symbol': 'AAPL',
    'action': 'BUY',
    'value': 125.00,
    'heuristic': 0.85
}
\end{lstlisting}

\section{Results}
 gives pretty good results between 115% to 160% sometimes even more
 on the inital capita given



\textbf{exampe results}
    \begin{figure}[ht]
    \centering
    \includegraphics[width=1.2\textwidth]{Capture d’écran 2025-06-11 122104}
    \caption{59 percent investment return}
    \label{fig:my_label}
    \end{figure}




\section{Conclusion}
This project demonstrates the application of classical AI search algorithms to financial decision-making. By combining heuristic scoring with real-world constraints, the agent balances exploration (A*) and exploitation (Greedy Search) to simulate profitable trading strategies.


\end{document}

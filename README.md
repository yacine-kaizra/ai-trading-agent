# AI Trading Agent Using A* and Greedy Search 

By Yacine Kaizra    



This document describes the architecture and implementation of an AI trading agent that uses A  search * and Greedy Search  algorithms to simulate optimal investment decisions on historical stock data. The agent dynamically generates a state space of possible actions (buy/sell/hold) while respecting financial constraints (available funds, diversification limits). Heuristic scores guide the search toward maximizing portfolio value.   
# Overview 

The trading agent operates on historical stock price data (e.g., 2023–2024) and simulates trades to maximize returns. It evaluates sequences of actions (buy/sell/hold) for a given set of stocks (e.g., ["AAPL", "MSFT", "TSLA"]) and outputs the most profitable path based on heuristic-driven search algorithms.   
Workflow Summary 

*  Data Retrieval : Fetch historical prices using yfinance (daily close prices for the specified period).  
* State Space Generation : Construct a tree of valid actions (buy/sell/hold) for each stock.  
*    Heuristic Design : Assign scores to actions based on price trends, portfolio impact, and risk.  
*    Search Algorithm : Use A* or Greedy Search to find the optimal action sequence.  
*    Portfolio Update : Track cash, owned shares, and portfolio value after each trade.
     

# Technical Details 
 # 1. State Space Construction 

The agent builds a state space where each node represents a portfolio state (cash, owned shares). Actions branch into:   

  *  BUY <stock>: Requires sufficient funds.  
   * SELL <stock>: Requires ownership of the stock.  
   * HOLD: No change to the portfolio.
     

Invalid nodes are pruned:   

 *   No purchase if funds are insufficient.  
 *   No sale if stock is not owned.  
   * No purchase if stock allocation exceeds 20% of total portfolio value.
     

# 2. Heuristic Design 

Each action receives a heuristic score h ∈ [0.01, 1.0], normalized across stocks to ensure fairness. Scores are calculated based on:   

*   Price trends  
*  Portfolio diversification impact  
* Risk-adjusted return potential
     
# 3. Search Algorithms 

A  Search and Greedy Search : Uses a max-heap priority queue to explore paths with the highest cumulative heuristic score.
{4. Portfolio Management 

The Stocks class tracks:   

 *   Current cash balance  
  *  Owned shares per stock  
  *  Portfolio value (cash + market value of shares)
     

Constraints:   

  *  Diversification limit: No single stock > 20% of total portfolio value.  
   * Transaction validation (e.g., no selling unowned shares).
     
     
{  
    'symbol': 'AAPL',  
    'action': 'BUY',  
    'value': 125.00,  
    'heuristic': 0.85  
}  
# Results 

Gives pretty good results between 115% to 160% , sometimes even more on the initial capital given.   
# Conclusion 

This project demonstrates the application of classical AI search algorithms to financial decision-making. By combining heuristic scoring with real-world constraints, the agent balances exploration (A*) and exploitation (Greedy Search) to simulate profitable trading strategies.   

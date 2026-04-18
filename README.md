# Supply Chain & Operations Analytics — Delta Sky Broadcasting

## Overview
This project presents a data-driven analysis of key operational processes 
at Delta Sky Broadcasting, a UK-based satellite television service provider. 
Using Microsoft Excel, four core operational areas were analysed: 
subscription call demand forecasting, satellite box inventory management, 
engineer job allocation, and vehicle servicing efficiency. The goal was 
to identify inefficiencies and provide practical, data-supported 
recommendations.

---

## What Was Done

### 1. Investigating Subscription Call Demand
A time series analysis was performed on 56 days of subscription call data 
(1st May to 25th June). A 7-day Centred Moving Average (CMA) was calculated 
to smooth out short-term fluctuations and reveal the underlying trend. 
The additive decomposition method was used to remove the trend and isolate 
seasonal patterns, as seasonal effects remained constant over time rather 
than growing with the trend.

A seasonal matrix was built by grouping detrended values by day of the week, 
and the median detrended value for each weekday was used to create a daily 
seasonal profile. Key finding: calls peak midweek, especially on Wednesdays, 
and are lowest on weekends, particularly Sundays. This indicates strong 
weekly seasonality in customer behaviour.

---

### 2. Forecasting Call Demand
Three seasonal forecasting models were tested using training data from 
1st May to 18th June, with a 7-day out-of-sample forecast (19th–25th June):

- **Seasonal Naïve** — uses the value from the same weekday of the 
  previous week
- **Seasonal Average** — uses the average calls for each weekday
- **Seasonal Exponential Smoothing** — uses Excel's FORECAST.ETS function, 
  which automatically selects the best smoothing parameter

Model accuracy was measured using three error metrics:

| Model | In-Sample MAE | In-Sample RMSE |
|---|---|---|
| Seasonal Naïve | Highest | Highest |
| Seasonal Average | Perfect ME (0.00) | Poor out-of-sample |
| Exponential Smoothing | **243.80** | **308.23** |

Exponential Smoothing was selected as the best model due to its lowest 
in-sample errors and strong adaptability to changing trends.

---

### 3. Inventory Simulation
Delta Sky Broadcasting uses a reorder point inventory system for satellite 
boxes. An order of 10 boxes is placed when inventory falls to 2 or fewer 
units, arriving the following morning. A 7-day simulation was run in Excel 
using random numbers seeded from the student ID.

Key cost variables:
- Holding cost: £10 per box per day
- Ordering cost: £500 per order
- Backorder cost: £20 per box per day

Results over 7 days:

| Cost Type | Amount |
|---|---|
| Holding Costs | £340 |
| Ordering Costs | £1,000 (2 orders placed) |
| Backorder Costs | £120 |
| **Total Cost** | **£1,460** |
| Average Daily Cost | £208.57 |

The simulation highlighted a trade-off between holding costs and backorder 
penalties. Increasing the reorder point slightly could reduce stockouts 
while keeping costs manageable.

---

### 4. Engineer Job Allocation (Linear Programming)
The existing manual approach for assigning engineers to installation jobs 
was evaluated and improved using a Linear Programming (LP) model in Excel 
Solver. Five engineers (Tom, Bob, Paul, Steve, and Lucas) were assigned 
to five customer jobs with the objective of minimising total travel distance.

- Binary decision variables (0 or 1) were used in a 5×5 assignment matrix
- SUMPRODUCT was used to calculate total distance
- Solver with the Simplex LP method was applied

Results:
- **Current manual approach:** 28 miles total
- **LP optimised approach:** 27 miles total
- **Saving:** 1 mile per assignment cycle

While the saving appears small here, scaling this across multiple hubs 
and hundreds of daily jobs would result in significant fuel and time savings.

---

### 5. Vehicle Servicing Queue Simulation
A queuing simulation was built in Excel to model the Saturday vehicle 
servicing process for 15 engineer vehicles, handled by 2 mechanics. 
Arrival times were simulated using a Poisson distribution (4 vehicles 
per hour) and service times using an exponential distribution 
(mean of 20 minutes).

Key results:

| Metric | Result |
|---|---|
| Total Wait Time | 208.27 minutes |
| Average Wait per Vehicle | 13.88 minutes |
| Maximum Wait Time | 41.73 minutes |
| Mechanic 1 Idle Time | 129.53 min (41%) |
| Mechanic 2 Idle Time | 103.83 min (33%) |

The high idle times suggest room for scheduling improvement. Adding a 
third mechanic during peak hours or implementing an appointment-based 
system could significantly reduce vehicle wait times and mechanic 
downtime.

---

## Key Takeaway
Excel-based analytical methods — including time series decomposition, 
exponential smoothing, inventory simulation, linear programming, and 
queuing simulation — can effectively identify inefficiencies in 
operations. For Delta Sky Broadcasting, the key recommendations are 
to raise the inventory reorder point, adopt LP-based engineer 
assignments, and improve vehicle servicing scheduling during peak 
demand periods.

---

## Tools Used
- **Microsoft Excel** — time series analysis, forecasting, inventory 
  simulation, linear programming (Solver), and queuing simulation

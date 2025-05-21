# U.S.-Domestic-Airline-Route-Optimization-Analysis

# ✈️ Identifying Optimal Routes for U.S. Domestic Airline Market Entry

## 🌟 Project Overview

Welcome to this exploration of the U.S. domestic airline market! This project dives into 2019 data to uncover potentially lucrative and operationally sound routes for a hypothetical new airline. The journey is guided by key business questions I formulated, aiming to pinpoint pathways to success by focusing on route busyness, profitability (before hefty aircraft investments!), and a commitment to punctuality. ⏱️

## 🎯 Project Context and Goals

For this personal project, I put on my strategic thinking cap! I envisioned a scenario where a new airline is looking to make a smart entry into the bustling U.S. domestic market. To chart a course, I defined the following business questions, imagining an initial fleet ready for 5 round trip routes and factoring in a planning estimate of ~$90 million for aircraft acquisition per route:

1.  **Busiest Routes?** busiest Which routes see the most take-offs and landings?
2.  **💰 Most Profitable Routes?** Which routes generate the highest operational profit (before new plane costs)?
3.  **🏆 Recommended Investment Routes?** Balancing profit, demand, and operations, which 5 routes are prime for investment?
4.  **📈 Breakeven Analysis:** For our top picks, how many round trips until that $90M aircraft investment pays off?
5.  **📊 Future Performance Tracking:** What Key Performance Indicators (KPIs) should be on our dashboard for sustained success?

This analysis is all about finding data-driven answers and actionable insights!

## 📚 Data Sources

The engine for this analysis is fueled by the following Q1 2019 datasets:
* **Flights.csv:** The logbook of flights – dates, origins, destinations, distances, and passenger loads.
* **Tickets.csv:** The passenger perspective – itinerary details, fares, and traveler counts.
* **Airport_Codes.csv:** The map legend – airport codes, locations, and sizes.
* **Airline_Challenge_Metadata.xlsx:** The guide to understanding the data.

## 🛠️ Methodology & Magic

Here's the flight plan for how this analysis got off the ground:

1.  **🚀 Initial Setup & Data Loading:**
    * Imported the trusty toolkit: Pandas, NumPy, Matplotlib, Seaborn, and Plotly.
    * Loaded the datasets into Pandas DataFrames, ready for inspection.

2.  **🧼 Data Quality Assessment & Cleaning:** (Sparkling clean data is happy data!)
    * **Flights Data (`df_flights_active`):**
        * Standardized airport codes (no rogue spaces!).
        * Handled missing `CANCELLED` flags (assumed cancelled).
        * Ensured `DISTANCE` and `OCCUPANCY_RATE` were numeric.
        * Filtered for active, valid flights (no ghost flights!).
        * Removed duplicates and ensured occupancy rates made sense.
    * **Tickets Data (`df_tickets`):**
        * Focused on roundtrip adventures (`ROUNDTRIP = 1`).
        * Ensured every `ITIN_ID` was a unique story.
        * Standardized airport codes.
        * Made sure `ITIN_FARE` was numeric and sensible.
        * Filtered out records with missing or invalid fare/passenger data.
    * **Airports Data (`df_airports`):**
        * Zoomed in on U.S. medium and large airports.
        * Ensured all had valid `IATA_CODE`s.
        * Kept it lean with just `IATA_CODE` and `AIRPORT_SIZE`.
    * Created a `valid_airports` list to keep everything consistent.

3.  **✨ Feature Engineering (Adding Extra Value!):**
    * **ROUTE_ID Creation:** Forged a universal `ROUTE_ID` (e.g., JFK-ORD) for easy tracking.
    * **Flight-Level Costs & Revenue Calculation (`df_flights_active`):**
        * Estimated `PASSENGERS` per flight.
        * Calculated `BAGGAGE_REVENUE` 🛍️.
        * Estimated operational costs: `FUEL_MAINT_COST`, `DEPREC_INS_COST`, `AIRPORT_FEE` ⛽️.
        * Accounted for `TOTAL_DELAY_COST` ⏳ (time is money!).
        * Summed it all up into `TOTAL_COST`.
    * **Directional Flight Counts:** Tallied flights for each direction of a route.
    * **Round Trip Calculation:** Smartly determined actual `ROUND_TRIPS` using the "Directional Minimum Count" method.

4.  **🔍 Data Aggregation & Analysis:**
    * **Route-Level Aggregation:** Rolled up flight data (passengers, costs, revenue) by `ROUTE_ID`.
    * **Ticket-Level Aggregation:** Calculated `AVG_FARE` per route.
    * **Combined Route Data (`df_routes`):** The grand merge!
        * Calculated `TICKET_REVENUE` and `TOTAL_REVENUE`.
        * Calculated `PROFIT` (Revenue - Cost).
        * Determined `PROFIT_PER_ROUND_TRIP`.
    * **Univariate Analysis:** Peaked into `OCCUPANCY_RATE` and `ITIN_FARE` distributions.
    * **Bivariate Analysis:** Explored connections: Profit vs. Round Trips, Delay Cost vs. Profit, etc.

5.  **💡 Answering the Big Questions:**
    * Identified the top 10 busiest and most profitable routes.
    * Curated a list of 5 recommended routes for investment.
    * Calculated breakeven points for these prime routes.
    * Proposed KPIs for a clear view of future performance.

## 💎 Key Findings & Recommendations

This is where the data truly shines and tells its story! Here are the key insights and recommendations derived from the Q1 2019 U.S. domestic airline analysis:

*  **Busiest Routes (2019):** 🚀 These are the highways of the sky, showing significant demand.
    * LAX-SFO: 4147 round trips
    * LAX-JFK: 2410 round trips
    * ORD-LAX: 2238 round trips
    * SFO-JFK: 2168 round trips
    * ORD-LGA: 2034 round trips
* **💰 Top 5 Most Profitable Routes (Q1 2019 - Operational Profit):** These routes show the best financial returns based on operational revenue versus costs (before considering initial aircraft purchase).
    * SFO-JFK: $11.77M profit
    * LAX-JFK: $11.08M profit
    * CLT-LGA: $6.26M profit
    * BOS-ORD: $5.63M profit
    * ORD-LGA: $5.01M profit

* **🏆 Recommended Routes for Investment (Top 5):** Based on a blend of high profit, substantial round trips, manageable delay costs, and achievable breakeven points, these 5 routes stand out as prime candidates for a new airline venture:
    * **Route 1: SFO-JFK** - **Why it Shines:** Highest operational profit, very high demand (top 4 busiest), indicating a robust market.
    * **Route 2: LAX-JFK** - **Why it Shines:** Second highest operational profit and second busiest route, showcasing strong, consistent returns.
    * **Route 3: CLT-LGA** - **Why it Shines:** Excellent profitability (top 3) combined with significant passenger volume (top 6 busiest).
    * **Route 4: BOS-ORD** - **Why it Shines:** Strong profit (top 4) and a high number of round trips, indicating a reliable and busy corridor.
    * **Route 5: ORD-LGA** - **Why it Shines:** Good profitability (top 5) and a very busy route (top 5 busiest), ensuring high utilization.
    

* **📈 Breakeven Analysis for Recommended Routes:** Here's an estimate of how many round trips would be needed for each recommended route to cover the initial $90 million aircraft acquisition cost:
    * SFO-JFK: Approx. 3313 round trips to soar into profit!
    * LAX-JFK: Approx. 3920 round trips to soar into profit!
    * CLT-LGA: Approx. 5370 round trips to soar into profit!
    * BOS-ORD: Approx. 5749 round trips to soar into profit!
    * ORD-LGA: Approx. 7184 round trips to soar into profit!
 

* **📊 Recommended KPIs for Future Tracking:** To navigate towards sustained success, these Key Performance Indicators should be on the dashboard:
    * **Profit Margin %:** `(Total Profit / Total Revenue) * 100%`
    * **Revenue per Passenger 🧑‍✈️:** `Total Revenue / Total Passengers`
    * **Cost per Passenger 💵:** `Total Operational Cost / Total Passengers`
    * **Cost per Mile ✈️:** `Total Operational Cost / Total Miles Flown`
    * **Breakeven Progress % 🎯:** `(Current Cumulative Profit / $90M Aircraft Cost) * 100%` (tracked per route)
  

## 💻 Technical Stack

* Python 🐍
* Pandas 🐼 (for data wrangling)
* NumPy (for numerical operations)
* Matplotlib & Seaborn 📊 (for classic visualizations)
* Plotly Express 📈 (for interactive charts)

## ▶️ How to Run the Analysis

1.  Ensure all data files (`Flights.csv`, `Tickets.csv`, `Airport_Codes.csv`, `Airline_Challenge_Metadata.xlsx`) are nestled in a `data/` subdirectory (or adjust paths in the notebook).
2.  Install the squadron of Python libraries:
    ```bash
    pip install pandas numpy matplotlib seaborn plotly
    ```
3.  Open and run the Jupyter Notebook `Task.ipynb` to see the analysis unfold! 🚀

## 🔮 Future Work Considerations (The Adventure Continues!)

This initial voyage was insightful, but there's always more sky to explore:
* **🕰️ Temporal Trends:** How does route performance change month-to-month or week-to-week?
* **✈️ Airport Size Impact:** Do large vs. medium airports significantly alter costs or delays?
* **🎟️ Ticket Price Deep Dive:** What stories can varying fare prices on the same route tell us?
* **⏳ Delay Pattern Discovery:** Which routes are chronic delay culprits? How can we mitigate this?

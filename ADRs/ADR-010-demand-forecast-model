
# TITLE

Demand Forecast per Zone Using ARIMAX with External Factors

# STATUS

Proposed

# CONTEXT

To plan both nightly rebalancing and daytime relocations, we need reliable short-term demand forecasts at a fine-grained resolution.

* Demand is influenced not only by historical booking patterns but also by external factors such as weather, holidays, and local events.
* Our in-house booking system contains the historical attempted bookings (including failed unlocks), which provide the best signal for true demand.
* A simple but interpretable model is sufficient at this stage; we need stability and explainability more than cutting-edge complexity.

# DECISION

We will implement a **per-zone ARIMAX forecast** to predict demand in 15-minute intervals.

* **Inputs:**

  * Historical attempted bookings from our booking system (main demand signal).
  * Exogenous features: weather conditions and forecasts, holidays, events.
* **Method:** ARIMAX (AutoRegressive Integrated Moving Average with Exogenous regressors).
* **Granularity:** Forecast demand for each node (zone) in **15-minute buckets**.
* **Horizon:** Up to several hours ahead (e.g., 6 hours), refreshed in a rolling fashion.

![Demand Forecast Model](../architecture/images/demand_forecast.png)  

**Pros**

* Simple, transparent, and interpretable.
* Easy to incorporate exogenous data like weather and holidays.
* Efficient to train and serve for many zones simultaneously.
* Provides granular per-zone, per-interval demand values.

**Cons**

* Limited ability to capture complex spatiotemporal correlations across zones.
* Forecast accuracy depends heavily on quality and coverage of exogenous data.
* May require frequent retraining for zones with high volatility or irregular demand.

# CONSEQUENCES

* Provides the **demand baseline** for nightly rebalancing and residual daytime optimization.
* 15-minute granularity supports time-sensitive relocation planning.
* Simple ARIMAX may underperform in highly dynamic contexts, but its interpretability supports operational adoption.
* As the system matures, we may upgrade to more advanced models (e.g., gradient boosting, spatiotemporal deep learning).

# COMPLIANCE

* Monitor forecast error metrics (MAE/MAPE) per zone and time slice.
* Validate that demand forecasts align with realized attempted bookings.
* Retrain ARIMAX models periodically and when drift is detected.
* Maintain feature contracts to ensure consistent input data from booking and external APIs.

# COMMENTS

* ARIMAX chosen as a baseline; future ADR may supersede this with a more advanced demand forecasting approach.
* This ADR links directly to **Nightly Reset ADR** and **Residual Optimization ADR**, as both depend on accurate demand predictions.

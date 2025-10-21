# AI-Enabled Use Cases for MobilityCorp

This document outlines five AI-driven use cases designed to improve operations, reliability, and customer experience for MobilityCorp.  
Each use case includes a short description, its importance, and critical questions focused on AI uncertainty, provider changes, and cost management.

1. **Demand Forecasting & Vehicle Placement**: Predicts demand to optimize vehicle availability and placement.
2. **Battery Health & Technician Scheduling**: Monitors battery health and plans efficient technician routes.
3. **Dynamic Pricing & Booking Suggestions**: Adjusts pricing dynamically and suggests bookings based on demand.
4. **Photo Validation for Vehicle Return**: Automates vehicle return checks using AI vision models.
5. **Personalization & Mobility Assistant**: Provides personalized travel recommendations and smart assistance.

---

## 1. AI Demand Forecasting & Vehicle Placement

### What it does
Predicts when and where customers will want vehicles (scooters, bikes, cars, vans).  
Helps the company move or rebalance vehicles before demand peaks — so users find vehicles where they expect.

### Why it matters
Reduces “no vehicle available” complaints and improves utilization.

### Critical Questions
- How accurate does the forecast need to be for it to be useful?
- What happens if the model is wrong — do we have a fallback (like a rule-based approach)?
- How often should the model be retrained as demand patterns change (e.g., events, holidays)?
- How do we swap AI models or providers easily if another service becomes cheaper or better?
- Can we control costs by using cheaper batch predictions instead of real-time AI calls?
- How do we verify and monitor that predictions stay reliable over time?

---

## 2. AI for Battery Health & Technician Scheduling

### What it does
Predicts which vehicles will soon run out of charge and plans the best routes for field staff to replace or charge batteries efficiently.

### Why it matters
Keeps the fleet available and reduces downtime and technician travel costs.

### Critical Questions
- How sure is the AI about battery life predictions — what if it’s wrong?
- Do we still have a backup plan (e.g., simple “battery < 20%” rule)?
- How do we retrain or replace the model if new vehicle types or batteries are added?
- Should we host the AI model ourselves or use a cloud AI service — what’s cheaper long-term?
- Can we monitor and measure the cost vs benefit of these AI optimizations?
- If the AI route planner fails or changes provider, can the system still create basic routes automatically?

---

## 3. AI Dynamic Pricing & Booking Suggestions

### What it does
Adjusts prices automatically based on demand, availability, and location.  
Suggests customers book vehicles in advance when AI predicts high demand.

### Why it matters
Improves revenue, keeps vehicles used evenly, and helps ensure availability.

### Critical Questions
- How do we explain AI pricing to customers so it’s transparent and fair?
- How do we control the AI so it doesn’t set prices too high or too low?
- Can we easily change or remove the AI pricing model if it becomes too costly or inaccurate?
- Should we run AI pricing in real time (expensive) or update hourly/daily (cheaper)?
- How do we handle different city rules — can the AI be tuned per location?
- How do we verify that AI pricing actually increases usage or revenue before rolling out widely?

---

## 4. AI Photo Validation for Vehicle Return

### What it does
Uses AI vision models (such as object detection and segmentation) to check that vehicles are properly parked and not damaged when returned; sensor data (e.g., location, battery status) complements image analysis to verify parking and detect issues.  
Detects if an eCar/eVan is plugged in correctly, notifies the user of immediate actions needed (such as repositioning the vehicle or reconnecting the charger), and flags potential issues to human reviewers.

### Why it matters
Reduces manual review work and speeds up trip closing and payments.

### Critical Questions
- How do we verify that the AI image checks are correct before trusting them?
- What happens if the AI mislabels damage or fails to detect issues?
- How do we keep AI image models updated if lighting, parking layouts, or vehicle types change?
- How do we switch to a new image AI provider if costs or accuracy change?
- How much processing can be done on-device (cheaper, faster) vs in the cloud (more expensive but powerful)?
- How do we make sure photo data is stored and deleted correctly under GDPR?

---

## 5. AI Personalization & Mobility Assistant

### What it does
Learns each customer’s travel habits (e.g., commute times, weekend trips) and gives personalized recommendations or reminders.  
Includes a smart chat assistant to help users during trips (e.g., if vehicle breaks down).

### Why it matters
Increases loyalty and frequency of use, and reduces support calls.

### Critical Questions
- How do we keep user data private and still personalize effectively?
- How do we update or replace the AI assistant if a better or cheaper language model becomes available?
- Can we run the AI assistant partly offline or with cached responses to save cost?
- How do we measure if AI personalization really increases repeat usage?
- What if the AI gives wrong or confusing advice — how do we hand off to a human smoothly?
- How do we design our system so we can plug in different AI providers easily in the future?

---

## Cross-Cutting AI Architecture Questions

These apply to all AI use cases:

- **AI Reliability:** How do we detect when an AI model’s predictions go bad?
- **Cost Management:** Can we use cheaper models or smaller inference schedules without hurting accuracy?
- **Model Replaceability:** Can we swap AI vendors easily (e.g., HuggingFace → OpenAI → local model)?
- **Validation:** How do we continuously test that AI results match business goals (availability, revenue, user satisfaction)?
- **Fallbacks:** What happens if the AI service is unavailable — do we have deterministic rules to continue operating?
- **Data Governance:** How do we ensure all AI data flows are GDPR-compliant and multilingual-ready?

---

*Prepared for the MobilityCorp AI Architecture Design Project.*

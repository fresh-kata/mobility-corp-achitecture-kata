# ADR: Why do we need Agentic AI?

# STATUS
**Accepted**
# CONTEXT
Planning trips is a complex task, and it needs to consider many dynamic factors:
* Users have varying preferences (fastest, cheapest, greenest).
* Weather and traffic conditions change frequently.
* Each country and city has different rules and restrictions.
* Vehicles are often not available when or where users need them.
* Users can’t always rely on our service for regular commutes.
* Supply teams need better demand forecasts.

The question is How can an Agentic AI help address these challenges effectively?
Is this the right approach to improve trip planning and fleet management?

As planning is and undeterministic problem with many variables and changing conditions, traditional static algorithms or simple rule-based systems are insufficient.
An Agentic AI can dynamically adapt to changing conditions, learn user preferences, and make complex decisions in real-time.


# DECISION
Agentic AI is chosen to handle the complexity of trip planning for MobilityCorp users.  
The Agentic AI will:
* Collect and analyze data from various sources (weather, traffic, fleet status, user habits).
* Create main and backup travel plans based on user preferences and real-time conditions.
* Send booking or supply requests when vehicle availability is low.
* Monitor ongoing trips and re-plan when needed.
* Continuously learn and improve its planning capabilities over time.
* Ensure compliance with local laws and regulations.

# CONSEQUENCES
It needs AI engineering expertise to build and maintain the Agentic AI system.
It may require significant computational resources for real-time data processing and decision-making.
There may be challenges in ensuring data privacy and security when handling user information.


# COMPLIANCE
Regular audits and monitoring will be conducted to ensure the Agentic AI adheres to compliance requirements.

# COMMENTS

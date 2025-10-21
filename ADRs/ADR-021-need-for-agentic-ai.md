# Need for agentic AI

**Author**: Marlon Ehrich<br />
**Status**: ACCEPTED<br />
**Type**: DESIGN<br />
**Created**: 2025-10-19<br />
**Post-history**:  

Agentic AI is essential for addressing the complexities of trip planning and fleet management, enabling dynamic adaptation to changing conditions, learning user preferences, and making real-time decisions.

# CONTEXT

Planning trips is a complex task that involves many dynamic factors:  
* Users have varying preferences (fastest, cheapest, greenest).  
* Weather and traffic conditions change frequently.  
* Each country and city has different rules and restrictions.  
* Vehicles are often not available when or where users need them.  
* Users can’t always rely on our service for regular commutes.  
* Supply teams need better demand forecasts.  

Traditional static algorithms or simple rule-based systems are insufficient for this undeterministic problem with many variables and changing conditions.  

# DECISION

In the context of improving trip planning and fleet management, facing the challenges of dynamic conditions, user preferences, and operational constraints, we decided to adopt Agentic AI and neglected traditional static algorithms or rule-based systems.  

The Agentic AI will:  
* Dynamically adapt to changing conditions.  
* Learn user preferences and make complex decisions in real-time.  
* Collect and analyze data from various sources (weather, traffic, fleet status, user habits).  
* Create main and backup travel plans based on user preferences and real-time conditions.  
* Send booking or supply requests when vehicle availability is low.  
* Monitor ongoing trips and re-plan when needed.  
* Continuously learn and improve its planning capabilities over time.  
* Ensure compliance with local laws and regulations.  

This decision aims to enhance system adaptability, user satisfaction, and operational efficiency, accepting the downsides of requiring significant computational resources and AI engineering expertise, because these trade-offs are necessary to address the complexity of trip planning effectively.  

# CONSEQUENCES

The impact of this decision includes:  
* The need for AI engineering expertise to build and maintain the Agentic AI system.  
* Significant computational resources for real-time data processing and decision-making.  
* Challenges in ensuring data privacy and security when handling user information.  

# COMPLIANCE

Regular audits and monitoring will be conducted to ensure the Agentic AI adheres to compliance requirements, including data privacy and security standards.  

# COMMENTS

None.  

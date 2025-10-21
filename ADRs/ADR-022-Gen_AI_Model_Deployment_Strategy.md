# Generative AI Model Deployment Strategy

**Author**: Bahram Jahanshahi<br />
**Status**: PROPOSED<br />
**Type**: INFRASTRUCTURE<br />
**Created**: 2023-10-05<br />
**Post-history**:  

Selection of a centralized hosting strategy for deploying Generative AI models at MobilityCorp, prioritizing data privacy, maintainability, and compliance, while accepting manageable latency due to predictable request loads.

# CONTEXT

MobilityCorp is evaluating deployment strategies for Generative AI models to balance performance, privacy, and maintainability. The following options were considered:  
1. **Centralized Model Hosting:** Host AI models on MobilityCorp servers for better control over data privacy and security, with manageable latency due to predictable request loads.  
2. **Edge Model Deployment:** Deploy models on user devices for reduced latency and offline functionality, but with challenges in privacy, updates, and consistency.  
3. **Third-Party AI Services:** Leverage external platforms for advanced capabilities but face compliance and data-sharing concerns.  
4. **Mixed Approach:** Combine centralized hosting with third-party services for a balance of performance and privacy, at the cost of added complexity.  

Key considerations include:  
- Predictable request loads due to fixed vehicle numbers in each region.  
- Privacy as a top priority, especially for sensitive trip-planning data.  
- Smaller models suffice for the Agentic AI, ensuring good performance without requiring large-scale LLMs.  
- Centralized hosting simplifies updates and ensures consistency.  
- Third-party services pose compliance risks, particularly with data residency and user consent.  

# DECISION

In the context of MobilityCorp's trip-planning use case, facing the need for high privacy and manageable latency, we decided for **Centralized Model Hosting** and neglected other options to achieve:  
- **System qualities:** Strong data privacy, consistent model updates, and maintainability.  
- **Desired consequences:** Efficient management of AI models and compliance with privacy regulations.  

We accept the downside of potential latency compared to edge deployments because the predictable request load makes this trade-off acceptable.  

# CONSEQUENCES

The decision to use centralized hosting has the following impacts:  
- **Trade-offs:** Slightly higher latency compared to edge deployments, but manageable due to predictable request patterns.  
- **Infrastructure needs:** Robust infrastructure to handle peak loads.  
- **Benefits:** Greater control over user data, simplified maintenance, and quicker model updates.  

Hiring AI engineering expertise is essential to build and maintain the centralized AI model hosting infrastructure.

# COMPLIANCE

To ensure compliance:  
- Adhere to data privacy regulations and user consent requirements.  
- Regularly audit the centralized system for security and performance.  
- Implement robust monitoring to handle peak loads effectively.  

# COMMENTS

Any comments or references.
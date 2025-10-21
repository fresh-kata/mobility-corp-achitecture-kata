# Generative AI Model Deployment Strategy

# STATUS
Proposed 

# CONTEXT
There are several AI model deployment options:
1. **Centralized Model Hosting:** Host the AI models on MobilityCorp servers. This allows for better control over data privacy and security, as well as easier updates and maintenance. However, it may introduce latency in responses due to network communication.
2. **Edge Model Deployment:** Deploy AI models on user devices (e.g., smartphones). This reduces latency and allows for offline functionality, but raises challenges in ensuring data privacy, model updates, and consistency across different devices.
3. **Third-Party AI Services:** Utilize third-party AI platforms (e.g., OpenAI, Google AI) to handle the AI processing. This can leverage advanced capabilities and reduce development time, but may involve data sharing with external entities and potential compliance issues.
4. **Mixed Approach:** Mix centralized with Third-Party services, where sensitive data is processed in-house while less sensitive tasks are offloaded to third-party services. This balances performance and privacy but adds complexity in managing multiple systems.

Which deployment strategy best aligns with MobilityCorp's goals for performance, privacy, and maintainability?

## Considerations:
- **Performance:** Response time and latency requirements for user interactions.
- **Privacy:** Ensuring user data is protected and compliant with regulations.
- **Maintainability:** Ease of updating models and managing deployments.

Here are some facts about the system that influence the decision:
- According to the requirements, it's said that there is fixed amount of vehicles in every region (country/city); 
Therefore, the amount of user's requests is somewhat predictable and can be managed with a centralized system without overwhelming the infrastructure.  
- When the number of requests for planning is predictable and limited, the latency introduced by centralized hosting is manageable.
- Privacy is a top priority, especially with sensitive user data involved in trip planning.
- The Agentic AI si supposed to plan and this does not need a big LLM. Even by using smaller models, the system can achieve good performance.
- Using third-party services may introduce compliance challenges, especially with data residency and user consent.
- Maintaining models centrally allows for easier updates and consistency across the user base.


# DECISION
Using a Centralized Model Hosting strategy is chosen for deploying Generative AI models at MobilityCorp.

This approach offers the best balance between performance, privacy, and maintainability given the predictable request load and the importance of data security. 
The centralized system allows for efficient management of AI models, ensuring that updates and improvements can be rolled out consistently across all users.

# CONSEQUENCES

The centralized hosting approach may introduce some latency compared to edge deployments, but this is acceptable given the predictable request load.
This strategy requires robust infrastructure to handle peak loads, but the predictable nature of requests makes this feasible.
By avoiding third-party services, MobilityCorp can maintain greater control over user data, ensuring compliance with privacy regulations.
The centralized model hosting will simplify maintenance and updates, allowing for quicker iterations and improvements to the AI models.

*It's highly needed to hire AI engineering expertise to build and maintain the centralized AI model hosting infrastructure.*

# COMPLIANCE


# COMMENTS
Any comments or references.
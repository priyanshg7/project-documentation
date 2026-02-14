# Requirements Document

## Introduction

HanumanAI is a *voice-first, multilingual, agentic AI platform* designed to function as a *“smart ally in the farmer’s pocket”* for Indian farmers. The platform supports *end-to-end agricultural decision-making*, from crop planning and disease control to market selling and government scheme access.
The system is grounded in *primary field research conducted with 30+ farmers and their families in Kanpur, Uttar Pradesh*, ensuring that all features reflect real farming challenges rather than theoretical assumptions.

HanumanAI directly addresses the following critical pain points:

- Missed sowing windows and incorrect crop selection due to lack of timely, localized guidance
- Overuse or imbalance of fertilizers and water due to lack of soil and irrigation insights
- Late or incorrect identification of pests and diseases
- Income loss due to volatile mandi prices, poor sell timing, and post-harvest weather damage
- Low adoption of government welfare schemes due to complex processes and low digital literacy
- Need for *short, spoken, actionable instructions* rather than long text-based explanations

The platform is designed to work *even in low-connectivity environments, supports **low digital literacy users, and prioritizes **voice-based interaction in local Indian languages*.

“All generative reasoning, planning, and agent coordination in HanumanAI is powered by Amazon Bedrock using large language models optimized for multilingual and contextual decision-making.”

## Glossary

- *HanumanAI_Platform* – A voice-first, multilingual, agentic AI web platform built from on-ground farmer research, designed to support Indian farmers in end-to-end agricultural decision-making—from crop planning and disease management to market selling and government scheme access—through a single, easy-to-use dashboard.
- *Voice_Interface* – The primary interaction layer of HanumanAI that enables farmers to navigate the platform, ask questions, and receive guidance using voice input and output in 22+ Indian languages, ensuring accessibility for low-literacy and first-time smartphone users.
- *Farm_Profile* – A digital representation of a farmer’s agricultural context, capturing land area, location, crops, soil type and composition, available irrigation methods, water source, and previously grown crops. This profile acts as the foundational context for all AI-driven recommendations across the platform.
- *AI_Agent* – Specialized, domain-focused intelligent agents (Crop Planner Agent, Disease Diagnosis Agent, Market Analysis Agent, Scheme Recommendation Agent, and Task Planner Agent) that work independently on their respective data and collaboratively combine insights to deliver accurate, context-aware, and actionable advice.oratively
- *Crop_Plan* – A personalized, day-by-day agricultural plan generated using Farm_Profile data, farmer crop preferences (if provided), soil health information, irrigation availability, weather forecasts, and historical patterns. The plan covers crop and variety selection, profit estimation, crop overview, best sowing windows, seed estimation and treatment, fertilizer and water recommendations, pest and disease prevention, and harvesting guidance—converted into simple weekly and daily actions.
- *Disease_Diagnosis* – A multi-modal AI system that allows farmers to upload crop images or describe symptoms via voice to identify the top likely pests or diseases. It provides disease names, reference images, confidence scores, tailored step-by-step cure plans (organic and inorganic), dosage adjusted to crop and farm size, nearby medicine shop details, and proactive alerts for early symptoms and prevention.
- *Mandi_Price* – Government-sourced, real-time agricultural market price data used to analyze crop prices across nearby mandis, helping farmers compare selling options, understand price trends, and make informed Sell/Hold decisions.
- *Government_Scheme* – Central and state government welfare schemes and subsidies relevant to farmers, matched using location, crop activity, and farmer profile data, and explained through simplified summaries and voice-based guidance.
- *Task_Reminder_Planner* – Voice-based and messaging-based (including planned WhatsApp alerts) reminders generated after a farmer finalizes or modifies a crop plan. These reminders translate AI recommendations into weekly targets, check-and-care schedules, and timely farming actions to ensure proper crop execution.
- *Multi_Modal_Input* – A flexible interaction mechanism that allows farmers to use voice commands, upload crop images, or use minimal touch inputs depending on convenience, with the system maintaining context across all input types.
- *Localized_Data* – Region-specific information including weather forecasts, soil characteristics, crop suitability, pest and disease patterns, irrigation feasibility, mandi prices, and applicable government schemes, ensuring all recommendations are practical and locally relevant.
- *Dashboard* – The main landing interface of HanumanAI where farmers start their journey. It provides a simple, icon-based and voice-navigable entry point to all core modules, including AI Crop Planner, Disease Diagnosis, Real-Time Market Analysis, Government Schemes, and Task Planner, designed for quick understanding and ease of use.

## Requirements

### Requirement 1: Voice-First Interface

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmers with low digital literacy or limited smartphone experience, farmers want to interact with HanumanAI primarily through voice in my local language, so that farmer can easily navigate the platform, understand recommendations, and take action without reading or typing.

#### Acceptance Criteria

1. WHEN a farmer interacts with the platform, THE Voice_Interface SHALL act as the primary and default mode of interaction across all modules, including navigation, data input, and receipt of recommendations.

2. WHEN a farmer speaks in their preferred local language, THE Voice_Interface SHALL accurately convert speech to text and interpret intent in the context of the active Farm_Profile and current module.

3. WHEN the system provides guidance or recommendations, THE Voice_Interface SHALL respond using short, clear, and actionable voice instructions in the farmer’s selected language, avoiding technical or complex terminology.

4. WHEN voice input is unclear, incomplete, or ambiguous, THE Voice_Interface SHALL request clarification using simple, farmer-friendly voice prompts, guiding the user step by step.

5. WHEN network connectivity is limited or unstable, THE Voice_Interface SHALL support basic offline voice commands for essential actions such as navigation, task reminders, and previously cached recommendations.

6. WHERE multilingual support is enabled, THE Voice_Interface SHALL support 22+ Indian languages, including Hindi and major regional languages, and allow farmers to change their preferred language using voice commands.

7. The Voice_Interface SHALL be implemented using AWS-native services such as Amazon Transcribe (speech-to-text), Amazon Polly (text-to-speech), and Amazon Translate to support multilingual, voice-first interaction.

### Requirement 2: Farm Profile Management

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmers want to create and manage a detailed digital profile of their farm, so that HanumanAI can understand their  real farming conditions and provide accurate, personalized, and location-specific recommendations across all features.

#### Acceptance Criteria

1. WHEN a farmer creates a Farm_Profile, THE HanumanAI_Platform SHALL collect and store essential farm context including location, preferred language, land area, crops, soil type and composition (if available), irrigation methods, water source, and previously grown crops.

2. WHEN soil health information is available, THE HanumanAI_Platform SHALL allow farmers to add soil composition data obtained from Soil Health Cards or Krishi Vigyan Kendra testing, which will be used for fertilizer and nutrient recommendations.

3. WHEN a farmer owns or manages multiple farms, THE HanumanAI_Platform SHALL support creation, selection, and switching between multiple Farm_Profile instances, with all recommendations generated using the currently active profile.

4. WHEN farm conditions change (such as crop selection, irrigation method, or soil updates), THE HanumanAI_Platform SHALL allow easy updates to Farm_Profile data, including voice-based updates, without requiring re-registration.

5. WHEN any AI-driven recommendation is generated, THE HanumanAI_Platform SHALL use the active Farm_Profile as the primary decision context, ensuring advice is tailored to the farmer’s actual land, resources, and history.

6. THE HanumanAI_Platform SHALL securely persist Farm_Profile data in the cloud, cache essential profile information locally for offline use, and automatically synchronize updates when connectivity is restored.

### Requirement 3: AI Crop Planning

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmers want a detailed, personalized, crop plan with Variety Recommendation, Crop Overview, Best date To Sow the crop in the area, Water Estimation of the Crop, Seed Treatment, Seed Estimation and Sourscing  , so that farmer can make the right decisions at the right time—from seed selection to harvest—while maximizing yield, minimizing cost, and reducing risk.

#### Acceptance Criteria

1. WHEN a farmer requests a crop plan, THE Crop Planning AI_Agent SHALL first fetch details from the active Farm_Profile and consider farmer preferences (if provided).

    - IF the farmer specifies a preferred crop, THE AI_Agent SHALL suggest suitable varieties for that crop based on location, weather conditions, soil characteristics, irrigation availability, and profit estimation.

    - IF the farmer does not specify a crop, THE AI_Agent SHALL recommend appropriate crops for the farm along with expected profit and risk levels.

2. WHEN crop or variety recommendations are generated, THE AI_Agent SHALL provide a clear crop overview, including expected duration, climatic suitability, major risks, and estimated profitability to support informed selection by the farmer.

3. WHEN a crop and variety are finalized, THE AI_Agent SHALL generate a personalized, day-by-day Crop_Plan covering the full crop lifecycle using soil data, weather forecasts, historical patterns, and available farm resources.

4. THE Crop_Plan SHALL include, at a minimum:

    - Best sowing windows with risk levels and crop insurance (PMFBY) eligibility indicators

    - Seed estimation based on land area and spacing norms, along with seed treatment steps, estimated cost, and nearby sourcing options

    - Water requirement estimation and irrigation scheduling based on crop stage, irrigation method, and weather, including pump usage and water-saving tips

    - Fertilizer recommendations using Soil Health Card data, weather, and previous crop history, offering organic and inorganic options with exact dosages, timing, application methods, and subsidy awareness

    - Pest and disease prevention guidance, including predicted risks based on crop, season, and location, with early symptoms and precautionary actions

    - Harvest timing guidance and post-harvest precautions

5. WHEN weather conditions or farm parameters change significantly, THE AI_Agent SHALL automatically update the Crop_Plan, notify the farmer via voice, and adjust upcoming actions to reduce risk or loss.

6. WHEN the farmer begins executing the plan, THE AI_Agent SHALL convert the Crop_Plan into weekly targets and daily or stage-wise actions, tracked through the Task Planner and delivered as voice-based reminders.

7. WHEN the farmer follows or modifies plan steps, THE AI_Agent SHALL monitor progress and adapt future recommendations based on execution, observed outcomes, and updated conditions.

8. ALL Crop_Plan guidance SHALL be delivered in simple, spoken, farmer-friendly language, avoiding technical jargon and ensuring the farmer clearly understands what to do, when to do it, and how much to use.

### Requirement 4: Real-Time Market Analysis with Ai crop Selling recommendation 

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmers want clear, real-time market intelligence and simple selling advice, so that farmer can decide whether to sell, hold, or urgently sell my produce, and where to sell it to maximize my actual take-home income.

#### Acceptance Criteria

1. WHEN a farmer requests market information, THE HanumanAI_Platform SHALL fetch government-sourced, real-time Mandi_Price data for the selected crop and nearby mandis relevant to the farmer’s location.

2. WHEN analyzing market conditions, THE Market Analysis AI_Agent SHALL combine current mandi prices, historical price trends, crop type, perishability, transport cost estimates, and local weather forecasts to generate a clear Sell / Hold / Sell Urgently recommendation.

3. WHEN providing selling advice, THE HanumanAI_Platform SHALL calculate and display the actual expected take-home profit, accounting for transport costs, mandi distance, and possible post-harvest spoilage risks.

4. WHEN multiple mandis are available, THE HanumanAI_Platform SHALL rank nearby mandis based on net profit after transport, highlighting the most profitable selling location for the farmer.

5. WHEN weather events such as rain or heatwaves are predicted, THE HanumanAI_Platform SHALL issue smart weather-based alerts (e.g., “Sell perishables before rain”) to help farmers avoid losses.

6. WHEN historical and seasonal data is analyzed, THE Market Analysis AI_Agent SHALL indicate whether the current price is a seasonal high or low, helping farmers judge if the price is fair.

7. WHEN mandi prices or influencing factors change, THE HanumanAI_Platform SHALL refresh market insights and recommendations at regular intervals and notify farmers of significant opportunities or risks via voice alerts.

### Requirement 5: Disease Diagnosis and Treatment

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmer want to quickly identify crop pests or diseases and receive clear, accurate treatment(Both Inorganic and Treatments) guidance with nearby shop recommendations, so that Farmer can take timely action, reduce crop loss, and avoid unnecessary or incorrect chemical use.

#### Acceptance Criteria

1. WHEN a farmer provides a crop image, THE Disease Diagnosis AI_Agent SHALL analyze the image and identify the top likely pests or diseases, using crop type, growth stage, and location as additional context.

2. WHEN a farmer describes symptoms using voice, THE Disease Diagnosis AI_Agent SHALL process the voice input and provide diagnostic suggestions, even when images are not available.

3. WHEN a diagnosis is generated, THE system SHALL present the top three probable diseases or pests, each with a confidence score, disease name (local and scientific where applicable), and reference images for visual confirmation.

4. WHEN a disease or pest is identified, THE Disease Diagnosis AI_Agent SHALL provide a simple, step-by-step cure plan, offering both organic and chemical treatment options, clearly explained in farmer-friendly language.

5. WHEN treatment recommendations are provided, THE system SHALL automatically adjust dosage, quantity, and application schedule based on the selected crop, farm size, and growth stage, ensuring safety, accuracy, and cost-effectiveness.

6. WHEN suggesting treatments, THE system SHALL consider local availability of medicines and provide an Instant Shop Locator, showing nearby agri-input shops with names, contact details, and map directions.

7. THE Disease Diagnosis AI_Agent SHALL maintain and use a localized disease knowledge base, covering common regional pests and diseases, their seasonal occurrence, early symptoms, and preventive measures.

8. WHEN risk patterns are detected, THE system SHALL issue proactive disease alerts, warning farmers about likely outbreaks in their area, early signs to watch for, and preventive actions to take.

9. ALL disease guidance SHALL be delivered in a fully multilingual, voice-first format, ensuring farmers clearly understand what the problem is, what to apply, how much to use, and when to act.

10. Image analysis SHALL be performed using AWS-native computer vision services (e.g., Amazon Rekognition) combined with domain-specific AI reasoning powered by Amazon Bedrock. 

### Requirement 6: Government Schemes Access

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmers want simple and reliable access to government welfare schemes and subsidies relevant to my farming activities, so that farmer can understand their eligibility, apply correctly, and receive benefits without confusion or dependency on middlemen.

#### Acceptance Criteria

1. WHEN a farmer searches or asks about government schemes, THE Scheme Recommendation AI_Agent SHALL identify and recommend relevant central and state Government_Scheme options based on the farmer’s location, crop activity, season, and active Farm_Profile.

2. WHEN schemes are presented, THE HanumanAI_Platform SHALL display them as simple, easy-to-understand scheme cards, clearly showing benefits, eligibility criteria, deadlines, required documents, and application mode, without technical or legal jargon.

3. WHEN a farmer wants to check eligibility, THE Scheme Recommendation AI_Agent SHALL assess the farmer’s qualification status using profile data and clearly explain why the farmer is eligible or not, along with the documents required.

4. WHEN a farmer asks questions about a scheme, THE HanumanAI_Platform SHALL provide a multilingual, voice-enabled AI helpdesk, allowing farmers to ask questions in their local language and receive step-by-step, spoken guidance on application procedures, fees (if any), and next steps.

5. WHEN new or time-sensitive schemes are announced, THE HanumanAI_Platform SHALL proactively notify eligible farmers, ensuring they do not miss deadlines due to lack of awareness.

6. THE HanumanAI_Platform SHALL integrate with trusted government data sources (such as data.gov.in) to ensure scheme information remains accurate, up-to-date, and location-specific.

### Requirement 7: Task Planning and Reminders

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmers want clear, voice-based weekly and daily farming tasks derived from my finalized crop plan, so that so farmer can correctly execute each step of cultivation on time without missing critical actions.

#### Acceptance Criteria

1. WHEN a farmer finalizes or modifies a Crop_Plan, THE Task Planning AI_Agent SHALL automatically convert the plan into a structured task schedule, including weekly targets, stage-wise activities, and check-and-care actions for the entire crop lifecycle.

2. WHEN tasks are generated, THE HanumanAI_Platform SHALL clearly explain what action is required, why it is important, how to do it, and what happens if it is delayed, using simple, spoken instructions in the farmer’s preferred language.

3. WHEN a task is due, THE HanumanAI_Platform SHALL deliver voice-based reminders and planned messaging alerts (e.g., WhatsApp notifications) at appropriate times based on crop stage, weather conditions, and urgency.

4. WHEN farmers complete or skip a task, THE HanumanAI_Platform SHALL allow voice-based confirmation or feedback, which is then used to update task status and inform future recommendations.

5. WHEN weather events or risk conditions change, THE Task Planning AI_Agent SHALL reschedule, reprioritize, or modify upcoming tasks, ensuring the farmer focuses on the most critical actions first.

6. WHEN multiple tasks overlap, THE system SHALL prioritize tasks based on crop risk, growth stage, and potential yield impact, rather than fixed calendar timing.

7. THE Task Planning system SHALL adapt over time, adjusting reminder frequency and timing based on farmer response behavior and preferences, without overwhelming the user.

### Requirement 8: Multi-Modal Input Processing

**User Story:** As from the farmer family and after consulting with 30+ famrers, Framer want to provide information through voice, images, or simple touch inputs, so that Farmer can communicate with the system in the most convenient way for each situation.

#### Acceptance Criteria

1. WHEN farmers provide input, THE HanumanAI_Platform SHALL accept voice commands, image uploads, and touch interactions
2. WHEN processing Multi_Modal_Input, THE HanumanAI_Platform SHALL combine different input types for comprehensive analysis
3. WHEN image quality is poor, THE HanumanAI_Platform SHALL request better images or alternative voice descriptions
4. WHEN voice input fails, THE HanumanAI_Platform SHALL provide simple visual alternatives for critical functions
5. THE HanumanAI_Platform SHALL maintain context across different input modalities within a single interaction session
6. The Voice_Interface SHALL be implemented using AWS-native services such as Amazon Transcribe (speech-to-text), Amazon Polly (text-to-speech), and Amazon Translate to support multilingual, voice-first interaction.

### Requirement 9: Multilingual Support and Language Accessibility

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmer want to use HanumanAI in my preferred local language, so that Farmer can easily understand recommendations, interact confidently with the platform, and take correct actions without language barriers.

#### Acceptance Criteria

1. WHEN a farmer uses the platform, THE HanumanAI_Platform SHALL support 22+ Indian languages, including Hindi and major regional languages, across all core modules.

2. WHEN a farmer selects or changes a language, THE HanumanAI_Platform SHALL apply the selected language consistently across the entire experience, including voice responses, text labels, notifications, and reminders.

3. WHEN delivering recommendations or guidance, THE system SHALL present information using simple, farmer-friendly language, avoiding technical jargon and complex policy terms.

4. WHEN farmers interact using voice, THE Voice_Interface SHALL accurately recognize and respond in the selected local language, including dialect-aware phrasing where feasible.

5. WHEN language is changed mid-session, THE HanumanAI_Platform SHALL retain context and continue the interaction without forcing the farmer to restart tasks or flows.

6. THE HanumanAI_Platform SHALL ensure that all critical actions—crop planning, disease diagnosis, market analysis, scheme guidance, and task reminders—are fully usable without reliance on English text.

7. The Voice_Interface SHALL be implemented using AWS-native services such as Amazon Transcribe (speech-to-text), Amazon Polly (text-to-speech), and Amazon Translate to support multilingual, voice-first interaction.

### Requirement 10: Localized Data Integration

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmer want recommendations based on my specific location and local conditions, so that the advice is relevant and actionable for my farming context.

#### Acceptance Criteria

1. WHEN providing recommendations, THE HanumanAI_Platform SHALL use Localized_Data including weather, soil conditions, and regional farming practices
2. WHEN accessing external data sources, THE HanumanAI_Platform SHALL integrate with Google Places API for location services and data.gov.in for government information
3. WHEN weather data is processed, THE HanumanAI_Platform SHALL use location-specific forecasts and historical climate patterns
4. WHEN market information is provided, THE HanumanAI_Platform SHALL prioritize nearby markets and transportation-accessible locations
5. THE HanumanAI_Platform SHALL integrate with Amazon Location Service for location, distance, and routing services, and data.gov.in and other trusted government sources for official agricultural and scheme information

### Requirement 11: Authentication and Data Security

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmer want my personal and farm data to be secure and accessible only to me, so that farmer can trust the platform with sensitive agricultural and financial information.

#### Acceptance Criteria

1. WHEN farmers register, THE HanumanAI_Platform SHALL provide secure authentication using phone numbers and OTP verification
2. WHEN storing farmer data, THE HanumanAI_Platform SHALL encrypt all personal and farm information using industry-standard encryption
3. WHEN accessing the platform, THE HanumanAI_Platform SHALL maintain secure sessions and automatic logout after inactivity
4. WHEN data is transmitted, THE HanumanAI_Platform SHALL use HTTPS encryption for all communications
5. THE HanumanAI_Platform SHALL comply with Indian data protection regulations and provide data deletion options upon request

### Requirement 12: Performance and Scalability

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmer want  fast response times and reliable service, so that Farmer can get timely agricultural guidance when needed.

#### Acceptance Criteria

1. WHEN farmers make voice queries, THE HanumanAI_Platform SHALL provide responses within 3 seconds for cached data and 10 seconds for AI-generated recommendations
2. WHEN multiple farmers access the system simultaneously, THE HanumanAI_Platform SHALL maintain performance with up to 10,000 concurrent users
3. WHEN system load increases, THE HanumanAI_Platform SHALL scale automatically to maintain response times
4. WHEN critical alerts are sent, THE HanumanAI_Platform SHALL deliver notifications within 1 minute of trigger events
5. THE HanumanAI_Platform SHALL maintain 99.5% uptime availability during peak farming seasons

### Requirement 13: Farmer-Friendly Dashboard and Navigation

**User Story:** As from the farmer family and after consulting with 30+ famrers, Farmer want a simple, clear dashboard that helps me easily understand what the platform can do and quickly access the right feature using voice or minimal taps, so that Farmer can confidently use HanumanAI without confusion.

#### Acceptance Criteria

1. WHEN a farmer opens the HanumanAI platform, THE system SHALL display a single, clean dashboard that acts as the entry point to all core modules, including AI Crop Planner, Disease Diagnosis, Real-Time Market Analysis, Government Schemes, and Task Planner.

2. WHEN the dashboard is presented, THE platform SHALL use icon-based, minimal-text design supported by voice prompts, ensuring usability for farmers with low digital literacy.

3. WHEN a farmer interacts with the dashboard, THE system SHALL allow voice-based navigation to any module (e.g., “Open Crop Planner”, “Check market price”, “Diagnose disease”) without requiring manual search or typing.

4. WHEN a farmer is a first-time user, THE dashboard SHALL guide them through Farm Profile creation using a step-by-step, voice-assisted flow before allowing access to personalized recommendations.

5. WHEN a farmer returns to the platform, THE dashboard SHALL surface relevant shortcuts and alerts, such as pending tasks, weather warnings, or important updates, based on the active Farm_Profile.

6. WHEN a farmer switches farms or language, THE dashboard SHALL immediately reflect the change and update all visible information accordingly.

7. THE dashboard SHALL be consistent across languages and devices, ensuring that all core actions remain accessible regardless of the farmer’s preferred language or screen size.
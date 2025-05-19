
![[ai-ml-gen-ai.png]]

## Artificial Intelligence

Use of technologies that can mimic cognitive functions of humans.

Includes being able to see, understand, and respond to spoken or written language, analyze data, make recommendations and more.

AI is an umbrella category that includes machine learning, robotics, expert systems and natural language processing, and generative AI.

## [[Machine Learning]]

Subset of AI that les machines learn from data without explicit programming.

Relies on models to analyze large amounts of data, learn from insights, and make predictions and informed decisions.

## [[Generative AI]]

Artificial intelligence that can produce new content including text, images, audio and synthetic data. [[Machine Learning#Deep Learning|Deep learning]] techniques are the engine behind generative AI.

### [[Generative AI#Foundation Models|Foundation Models]]
Powerful machine learning models trained on large datasets. They can be adapted to a wide range of tasks and applications.

## Secure AI
- Preventing harm being done by applications from malicious attacks and misuse
### Secure Model Lifecycle
#### Data Gathering
 - Secure data gathering - protecting data from unauthorized access and ensuring data integrity
 - Prevent data poisoning - attacks that inject malicious data into training datasets

#### Data Preparation
- Anonymize confidential or sensitive data present in training data
- Validate using integrity checks and anomaly detection to prevent poisoning
- Encrypted at rest and in use
- Logging and monitoring should also be performed

#### Training
- Safeguarding the training data and model parameters
- Prevent model theft

#### Model Management
- Staying up to date on latest security best practices
- Regularly patch and update vulnerabilities
- Monitor performance and outputs for anomalies or signs of tampering
- Regularly review access permissions

#### Deploy and Predict
- Control access to model in production
- Verify source of pre-built models, check for vulnerabilities

### Secure AI Framework (SAIF)
- Tools and best practices for building secure AI systems
- For more information, explore [Google's Secure AI Framework (SAIF)](https://safety.google/cybersecurity-advancements/saif/)

### Google Cloud Security Tools
- Use tools like [[Identity and Access Management (IAM)|IAM]] and [[Security Command Center]] and to protect data and model operations

## Responsible AI

AI should be
- socially beneficial
- avoid creating or reinforcing unfair bias
- build and tested for safety
- accountable to people
- incorporate privacy design principles
- uphold standards of scientific excellence
- made available for uses that accord with these principles

#### Transparency
- Users should understand how their information is used and how AI system works
#### Privacy
- Anonymizing and pseudonymizing data - models can sometimes leak information from training data

#### Data Quality, Bias, Fairness
- Ethical AI requires high quality data 
- Data should be collected consensually
- Consider if data perpetuates harmful biases
- Incorporate fairness as a core principle in AI development

#### Accountability and Explainability
- Makes decision making process of AI models transparent and understandable
- [[Vertex Explainable AI]] help understand model outputs and identify potential biases

#### Legal Implications
- AI increasingly governed by legal frameworks in areas like privacy, non-discrimination, intellectual property, and liability. Organizations must ensure compliance with these laws and regulations.
- Adherence to rules and limitations of AI models and compliance with licensing agreements and legal standards also important. 

## Explainable AI
Tools and frameworks to help understand and interpret predictions made by your machine learning models.

## AI Solutions
Google provides a set of solutions aimed to solve business needs. Some examples:

### Contact Center AI
Provides models for speaking with customers and assisting human agents. Increases operation efficiency, personalizes customer care.

### [[Document AI]]
Extract and classify information from unstructured documents such as invoices, receipts, forms, letters, reports.

### [[Product Discovery AI]]
Select optimal ordering of products on a retailer's e-commerce site when shoppers choose a category like winter jackets or kitchenware

### Cloud Talent Solution
Provides job search and talent acquisition capabilities, matches candidates to ideal jobs faster and allows employers to attract and convert higher quality candidates



## Considerations for Selecting AI and ML

### Speed to Production / Market
How quickly do you need something in production?

### Differentiation
How unique is your model? Or how unique does it need to be?

### Expertise Required
What roles are required? Data scientists, data engineers, machine learning engineers among others.

### Effort Required
How complex is the problem? How much data is available? How experienced is the team?


## Types of Learning

- Supervised - rely on labeled data - e.g. predicting house prices based on features like location, size, number of bedrooms
- Unsupervised - work with unlabeled data - e.g. clustering customers based on purchasing behavior to discover new segments
- Reinforcement - learn from interaction and feedback - e.g. self driving car

### Data
#### Labeled Data
- Has tags that assign meaning to data - name, type, number

#### Unlabeled Data
- Data that is not tagged in any way - raw unprocessed information without inherent meaning


### Google Cloud ML Examples

#### Predictive maintenance with [[Vertex AI]]
- Supervised learning
- Predict when equipment will fail and schedule maintenance to avoid downtime

#### Anomaly detection with [[BigQuery ML]]
- Unsupervised learning
- Identify unusual patterns in data that may indicate fraud or other issues

#### Product recommendations with [[Vertex AI]]
- Reinforcement learning
- Provide personalized recommendations to users based on their behavior and preferences


### Data Tools & Management for ML Workloads

#### Gathering data
- [[Pub Sub|Pub/Sub]] - real time streaming data processing
- [[Cloud Storage]] - suited for unstructured data
- [[Cloud SQL]] and [[Cloud Spanner]] used to manage unstructured data

#### Prepare data
- Cleaning and transforming data to be usable - formatting and labelling
- [[BigQuery]] - data analysis - filter data, correct inconsistencies, handle missing values
- [[Data Catalog]] - data governance - centralized repository to discover datasets in organization

#### Train your model
- [[Vertex AI]] - build and train machine learning models using prebuilt containers for popular frameworks, custom training jobs, tools for model evaluation.

#### Deploy and predict
- [[Vertex AI]] - tools to deploy trained models to make predictions, and scale to handle varying usage.

#### Monitor and manage
- Versioning - track model versions
- Performance tracking - review model metrics
- Drift monitory - detect changes in model accuracy over time
- Data management - [[Vertex AI#Feature Store|Vertex AI Feature Store]] to manage data features the model uses
- Storage - [[Vertex AI#Model Garden|Vertext AI Model Garden]] to store and manage models
- Automate - [[Vertex AI#Pipelines|Vertex AI Pipelines]] to automate machine learning tasks



## Choosing a Model

### Modality
- Type of data the model can process and generate - text, images, video, audio
- For single data type, choose model optimized for specific modality
- For multiple data types choose a multimodal model that can understand and synthesize information across different modalities
### Context Window
- Amount of information the model can consider at one time when generating a response
- Larger context window allows for more complex and nuanced interactions
- Larger context window also comes with increased computational costs
### Security
- Ensure model complies with relevant security standards and regulations for your industry
- Consider data encryption, access controls, vulnerability management
### Availability and Reliability
- Consider factors like uptime guarantees, redundancy, disaster recovery
### Cost
- Could be based on usage, compute time or other factors
- Match model to the task - bigger isn't always better
### Performance
- Evaluate model performance on relevant benchmarks and datasets
- Consider trade-offs between performance and cost
### Fine-tuning and Customization
- For specialized use cases, consider models that offer fine-tuning
- Often involves training the model on specific dataset related to your use case
### Ease of Integration
- Look for models with well-documented APIs and SDKs


## Model Limitations

### Data Dependency
- Require large datasets. Biases and incompleteness seep into outputs.
### Knowledge Cutoff
- Last date an AI model was trained on new information.
### Bias
- AI models can reflect and amplify biases present in training data.
### Fairness
- AI models can produce unfair outcomes for certain groups of people, even with perfectly balanced data.
### Hallucinations
- Outputs that aren't accurate or based on real information. 
### Edge Cases
- Rare and atypical scenarios that expose a model's weaknesses leading to errors, misinterpretations, and unexpected results.


## Overcoming Limitations

### Grounding
- Connecting AI model to verifiable sources of information.
- Reduces hallucinations and improves accuracy.
- Builds trust by providing citations and confidence scores.

#### Retrieval Augmented Generation (RAG)
- Grounding method that uses search to find relevant information from a knowledgebase giving LLM necessary context
- Retrieval - from question RAG uses search engine that understands semantic meaning of text to find relevant information
- Augmentation - retrieved information is added to the prompt given to the AI
- Generation - AI generates a response based on the augmented prompt together with existing knowledge

#### Prompt Engineering
- Rapid and straightforward approach to supplying background information to models
- Involves crafting precise prompts to guide models to desired outputs
- Limited by the model's existing knowledge

#### Fine-tuning
- Further training a pre-trained or foundation model on new dataset specific to task.
- Requires more time and resources than prompt engineering

#### Humans in the Loop (HITL)
- Integrate human input and feedback into the AI model's decision-making process.
- Good for
	- Content moderation - filter out harmful or inappropriate content that AI might miss
	- Sensitive applications - such as healthcare, legal, and finance - provide oversight and mitigate risk
	- High-risk decision making - safeguard when ML informs decisions with high consequences such as medical diagnosis or criminal justice assessments.
	- Pre-generation review - before deployment human experts review outputs for errors or bias 
	- Post-generation review - after deployment continuous human oversight to monitor AI outputs and provide feedback, enabling models to adapt to evolving contexts and user needs
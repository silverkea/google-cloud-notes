Vertex AI is Google Cloud's unified machine learning (ML) platform designed to streamline the entire ML workflow. It provides the infrastructure, tools, and pre-trained models you need to build, deploy, and manage your ML and generative AI solutions.

- Open and flexible - support s open frameworks allowing use of preferred models and tools without vendor lockin
- Powerful infrastructure - built on Google Cloud's infrastructure, providing high performance and scalability
- Pre-trained models - wide variety of pre-trained models
- Comprehensive tools - develop, deploy, manage models using integrated tools
- Customization - fine-tune and adapt models using built in IDE
- Easy integration via APIs


## MLOps Tools

Vertex AI also includes ML operations (MLOps) tools built in to help you orchestrate end-to-end ML workflows, perform feature engineering, run experiments, manage and iterate your models, track ML metadata, and monitor and evaluate model quality. 

MLOps helps automate, standardize, and manage the ML project lifecycle, enabling better collaboration and continuous improvement.

### Feature Store
Share, server and reuse ML features to maintain consistency and efficiency.

### Model Registry
Manage model versions, track changes, organize models throughout their lifecycle.

### Model Evaluation
Quickly evaluate and compare model performance to identify best model for use case.

### Workflow Orchestration
Automate ML workflows from data processing to deployment using Vertex AI Pipelines.

### Model Monitoring
Monitor models for performance degradation, detect input skew and drift, and trigger updates or retraining.


## Model Garden

Vertex AI Model Garden is a collection of pre-trained models and APIs that can be used to build and deploy machine learning applications. It includes a variety of models for different tasks, such as natural language processing, computer vision, and speech recognition.


### First-party Foundation Models

Leverage state-of-the-art models from Google including Gemini models and task-specific models for image generation, speech-to-text, and more. 

- Gemini Pro, Flash, and more. [View Gemini specs](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/models#gemini-models)
- Imagen for text-to-image. [View Imagen specs](https://cloud.google.com/vertex-ai/docs/generative-ai/image/overview)
- Veo for text-to-video and image-to-video. [View Veo specs](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/veo-video-generation?)
- Chirp 2.0 for speech-to-text. [View Chirp specs](https://cloud.google.com/vertex-ai/docs/generative-ai/speech/speech-to-text)

### First-party Pre-trained APIs

Build and deploy AI applications faster with our pre-trained APIs powered by the best Google AI research and technology.

- [View Speech-to-Text specs](https://cloud.google.com/speech-to-text) 
- [View Natural Language Processing (NLP) specs](https://cloud.google.com/natural-language)
- [View Translation specs](https://cloud.google.com/translate)
- [View Vision specs](https://cloud.google.com/vision)

### Open Models
Access a variety of enterprise-ready open models. 
- [View Gemma 2 specs](https://console.cloud.google.com/vertex-ai/publishers/google/model-garden/gemma2)
- [View CodeGemma specs](https://console.cloud.google.com/vertex-ai/publishers/google/model-garden/codegemma)
- [View PaliGemma specs](https://console.cloud.google.com/vertex-ai/publishers/google/model-garden/paligemma)
- [View Meta's Llama 3.1 specs](https://cloud.google.com/blog/products/ai-machine-learning/llama-3-1-on-vertex-ai) 
- [View Meta's Llama 3.2 specs](https://cloud.google.com/blog/products/ai-machine-learning/llama-3-2-metas-new-generation-models-vertex-ai)
- [View Mistral AI specs](https://cloud.google.com/blog/products/ai-machine-learning/codestral-and-mistral-large-v2-on-vertex-ai)
- [View Mistral AI21specs](https://console.cloud.google.com/vertex-ai/publishers/ai21/model-garden/jamba-1.5-large)[](https://www.tii.ae/)
- TII's Falcon BERT, FLAN-T5, ViT, EfficientNet. [View TII's Falcon specs](https://www.tii.ae/)

### Third-party Models
Model Garden supports third-party models from partners with foundation models.
[View Anthropic's Claude Model Family specs](https://console.cloud.google.com/vertex-ai/model-garden?pageState=%28%22galleryStateKey%22:%28%22f%22:%28%22g%22:%5B%22providers%22%5D,%22o%22:%5B%22ANTHROPIC%22%5D%29,%22s%22:%22%22%29%29)


## Building Models
Two options
- Fully custom using any ML framework - PyTorch, TensorFlow, scikit-learn, XFBoost
- Use [[AutoML]] to create and train models with minimal technical knowledge and effort



## AI on the Edge
Edge computing runs AI on devices or servers closer to the data source or point of need. 

### [[Lite Runtime]] (LiteRT)
- Platform that helps machine learning models work efficiently on your device. 
- Example model: [[Gemini Nano]]

### Edge Support in Vertex AI
Vertex AI provides tools and services to deploy and run AI models on edge devices, enabling real-time processing and reducing latency.

- Convert models - convert to run on [[Lite Runtime]] (LiteRT)
- Package and deploy - package models into containers for deployment on edge devices
- Manage and monitor - manage and monitor models on edge devices using Vertex AI tools

# AI Engineering: 10-Lesson Course

> Based on Chip Huyen's *AI Engineering: Building Applications with Foundation Models* (O'Reilly, 2025)  
> Target Audience: Learners interested in AI with no programming experience  
> Lesson Duration: 2 hours (1 hour concept + 1 hour hands-on)  
> Total Lessons: 10

## This Course Runs on Two Tracks

| Track | Material | Prerequisites | Notes |
|-------|----------|---------------|-------|
| **Concept track** | This document | Zero code, web tools only | Intuition-building on ChatGPT / Poe / AI Studio; every tool is free or has a free tier |
| **Code track** | `EN_Lesson_XX_*.ipynb` (English) / `Lesson_XX_*.ipynb` (Chinese) | Python + one API key | The same ideas reproduced in code; run `00_Environment_Setup.ipynb` first |

About the code track:
- Four providers are supported. **Switch by editing one line** at the top of any notebook:

  ```python
  PROVIDER = 'openai'   # 'openai' / 'deepseek' / 'openrouter' / 'ollama'
  ```

  | PROVIDER | Key env var | Small / big model | Embeddings (Lesson 6) |
  |----------|-------------|-------------------|-----------------------|
  | `openai` | `OPENAI_API_KEY` | gpt-5.6-luna / gpt-5.6-terra | ✅ text-embedding-3-small |
  | `deepseek` | `DEEPSEEK_API_KEY` | deepseek-v4-flash / deepseek-v4-pro | ❌ no endpoint — falls back to a local bag-of-words vector |
  | `openrouter` | `OPENROUTER_API_KEY` | openai/gpt-5.6-luna / openai/gpt-5.6-terra | ❌ same as above |
  | `ollama` | none needed | gemma4:e2b-mlx (local) | ✅ nomic-embed-text (pull it first) |

- Running all ten notebooks for real costs roughly $0.10 in API usage (gpt-5.6-luna pricing; DeepSeek is cheaper, Ollama is free).
- For Lesson 6's semantic search prefer `openai` or `ollama`: DeepSeek and OpenRouter have no embeddings endpoint, so the code degrades to a local bag-of-words vector, prints a warning, and still runs — but semantic quality drops.
- **The two tracks are deliberately different**: the concept track is about intuition and discussion, the code track about a reproducible, editable implementation. Within a lesson they complement each other — neither is a translation of the other.

---

## Lesson 1: Entering AI Engineering — From Foundation Models to AI Applications

### Learning Objectives
- Understand what AI engineering is and how it differs from traditional ML engineering
- Grasp the concept of Foundation Models and their evolution
- Explore typical AI application scenarios and their capability boundaries
- Develop a holistic view of AI application development

### Concept Lecture (1 hour)

**1. The Rise of AI Engineering (15 min)**
- A brief history: from language models to Large Language Models (LLMs)
- From LLMs to Foundation Models: the birth of multimodal capabilities
- Why AI engineering has become a distinct discipline

**2. What Can Foundation Models Do? (20 min)**
- Coding assistance: code generation, explanation, debugging
- Image and video creation: text-to-image, image-to-video
- Writing assistance: copywriting, rewriting, translation, summarization
- Education: personalized tutoring, knowledge explanation
- Conversational bots: customer service, virtual assistants
- Information aggregation: knowledge search, data synthesis
- Workflow automation: email classification, document organization

**3. How to Plan an AI Application (15 min)**
- Use case evaluation: what scenarios suit AI — and which don't
- Setting realistic expectations: what AI can and cannot do
- Milestone planning and ongoing maintenance
- The three-layer AI engineering stack: Application → Model → Infrastructure

**4. AI Engineering vs. ML Engineering vs. Full-Stack Engineering (10 min)**
- Core differences: prompt engineering replaces feature engineering; foundation models replace training from scratch
- Skill requirements across roles

### Hands-On Session (1 hour)

**Activity 1: Discovering AI's Capability Boundaries (20 min)**
- Platform: ChatGPT (free) / Claude (free) / Poe.com
- Tasks:
  1. Ask AI to write an email using natural language (experience language capability)
  2. Ask AI to explain a complex concept you don't understand (experience knowledge capability)
  3. Deliberately ask about a very recent event and observe AI's limitations (experience timeliness boundaries)
  4. Ask a question requiring precise calculation (experience reasoning boundaries)
- Discussion: Record cases where AI answers correctly and incorrectly; build an "AI Capability Checklist"

**Activity 2: Comparing Different AI Models (20 min)**
- Platform: Poe.com (compare multiple models on one platform)
- Tasks:
  1. Select 3 different models (e.g., GPT-4o, Claude 3.5, Gemini)
  2. Ask the same question to each
  3. Observe differences in style, accuracy, and depth
- Discussion: What "personality" does each model have? Why?

**Activity 3: Do Something Real with AI (20 min)**
- Task: Choose one of the following and complete it with AI assistance
  - Plan a weekend trip with ChatGPT (itinerary + budget)
  - Have AI summarize meeting notes (provide raw notes, let AI synthesize)
  - Translate an article using AI (Chinese ↔ English)
- Discussion: Where did AI help? Where was human intervention still needed?

---

## Lesson 2: Unveiling Foundation Models — How Models Are Made

### Learning Objectives
- Understand the training data that powers foundation models
- Grasp basic concepts of model architecture, scale, and training (no math required)
- Understand how a model "generates" responses (an intuitive view of sampling)
- Recognize the probabilistic nature of AI: why models sometimes hallucinate

### Concept Lecture (1 hour)

**1. Training Data: AI's "Textbooks" (15 min)**
- Where does training data come from? Web text, books, code
- Multilingual models: data distribution across Chinese, English, and other languages
- Domain-specific models: medical models, legal models, code models

**2. How Models Work (Layman's Version) (20 min)**
- An intuitive analogy: a super "next-word predictor"
- What model size means: what are parameters? What do 7B / 70B / 405B signify?
- Post-training: Supervised Fine-Tuning (SFT) → teaching the model to "follow instructions"
- Preference alignment (RLHF): making responses more aligned with human preferences
- Vivid analogy: SFT is like teaching a student "the correct answer"; RLHF is like teaching them "how to answer in a pleasing way"

**3. How Models Generate Responses (15 min)**
- Sampling fundamentals: the model predicts the next word, and loops to generate the full response
- Temperature: intuitively — high = more creative, low = more conservative
- Top-K and Top-P: knobs that control the model's "word selection range"
- Why does the same question get different answers? (AI's probabilistic nature)

**4. Where Do Hallucinations Come From? (10 min)**
- Models are not "knowledge bases" — they are "text generators"
- Their goal is to make text "look plausible," not "factually correct"
- Hallucination is a consequence of statistical patterns, not a design flaw

### Hands-On Session (1 hour)

**Activity 1: Adjusting the Model's "Creativity Knob" (20 min)**
- Platform: Google AI Studio (free, adjustable temperature, Top-P, Top-K)
- Tasks:
  1. Write a poem with Temperature = 0 → observe the result
  2. Write the same poem with Temperature = 0.5 → compare
  3. Write the same poem with Temperature = 1.5 → observe the "wildness"
  4. Record patterns: how does temperature affect output?
- Discussion: When should you use low temperature? High temperature?

**Activity 2: Triggering and Identifying AI Hallucinations (20 min)**
- Platform: ChatGPT / Claude
- Tasks:
  1. Ask: "Summarize Chapter 15 of *AI Engineering*" (the book only has 10 chapters)
  2. Ask: "Give me a biography of [a completely made-up person you invent]"
  3. Try to make AI admit: "I'm not sure" or "I don't know"
- Discussion: Under what conditions is AI most prone to hallucination? How can you tell if AI is "making things up"?

**Activity 3: Model Size Comparison (20 min)**
- Platform: Poe.com or Hugging Face Chat (select models of different sizes)
- Tasks:
  1. Use a small model (e.g., Llama 3.2-1B or similar) to answer a complex reasoning question
  2. Use a large model (e.g., GPT-4o / Claude 3.5) to answer the same question
  3. Compare quality and logical depth
- Discussion: Are larger models always better? When is a small model good enough?

---

## Lesson 3: AI Evaluation Fundamentals — How to Judge AI Responses

### Learning Objectives
- Understand why evaluating AI output is harder than evaluating traditional software
- Master core categories of AI evaluation methods
- Learn to use "AI as a Judge" to evaluate AI
- Develop a habit of critically examining AI outputs

### Concept Lecture (1 hour)

**1. Why Is AI Evaluation So Hard? (15 min)**
- Traditional software evaluation: input → output, a clear correct answer exists
- AI output evaluation: one question can have multiple "good" answers
- Open-endedness, subjectivity, context-dependency
- The fundamental challenge: what is a "good" response?

**2. Understanding Language Model Metrics (15 min)**
- Perplexity: how "surprised" the model is by a piece of text — intuitively: "how unexpected does this text feel to the model?"
- Exact evaluation vs. fuzzy evaluation
- Reference similarity: what BLEU, ROUGE, and similar metrics intuitively mean
- What is an embedding? A way to "score" text numerically

**3. AI as a Judge (20 min)**
- Why use AI to evaluate AI? Speed, cost, scalability
- How AI judging works: give AI a scoring rubric and let it score
- Writing effective evaluation rubrics
- Limitations of AI judges: bias, leniency, inconsistency
- What models make good judges?

**4. Comparative Evaluation (10 min)**
- A/B comparison: don't look at scores — just compare which is better
- The pitfalls of leaderboard rankings: the limits of benchmarks
- ELO scoring and the Arena model

### Hands-On Session (1 hour)

**Activity 1: Be the "AI Judge" Yourself (25 min)**
- Platform: ChatGPT / Claude (to generate responses for evaluation)
- Tasks:
  1. Ask AI 3 questions across different domains (common sense, creativity, logic)
  2. For each response, design a simple 1–5 scoring rubric
  3. Manually evaluate each response and write down your rationale
  4. Exchange evaluations with a partner and discuss differences
- Core insight: when you say "this response is a 5," what are your criteria?

**Activity 2: Let AI Be the Judge (20 min)**
- Platform: ChatGPT / Claude
- Tasks:
  1. Copy the 3 questions and responses from Activity 1 into a new chat
  2. Give AI a scoring rubric (e.g., accuracy, completeness, clarity — each 1–5)
  3. Compare AI's scores with your own
  4. Try rewording the rubric — observe how AI's scoring changes
- Discussion: Is the AI judge fair? Do its scores match yours?

**Activity 3: Compare Two AIs' "Writing Style" (15 min)**
- Platform: Poe.com (compare two models side by side)
- Tasks:
  1. Ask two different models to write a short essay on "AI's Impact on Education" (200 words)
  2. Blind evaluation: without looking at model names, which writes better? In what way?
  3. Reveal model identities
- Discussion: If you had to pick one as your "content creation assistant," which would you choose? Why?

---

## Lesson 4: AI System Evaluation in Practice — From "It Runs" to "It's Reliable"

### Learning Objectives
- Understand the four core evaluation dimensions for AI systems
- Master the model selection workflow: from requirements to decisions
- Understand the meaning and limits of public benchmarks
- Learn the basics of building an evaluation pipeline

### Concept Lecture (1 hour)

**1. Four Dimensions of AI System Evaluation (15 min)**
- Domain-specific capability: how well does the model handle specialized areas (medical, legal, coding)?
- Generation capability: text fluency, logic, creativity
- Instruction-following capability: how "obedient" is the model?
- Cost and latency: fast, good, cheap — the impossible triangle

**2. Model Selection: Build vs. Buy (20 min)**
- The five-step model selection workflow:
  1. Clarify requirements and constraints (budget, latency, accuracy)
  2. Shortlist candidate models
  3. Evaluate with your own data
  4. Comprehensive comparison
  5. Make a decision
- When to use an off-the-shelf API? (Buy)
- When to fine-tune your own? (Build)
- Case study: startup logic vs. enterprise logic

**3. Navigating Public Benchmarks (15 min)**
- Major benchmarks: MMLU, HumanEval, Chatbot Arena
- How to read a benchmark: high score ≠ good performance in your scenario
- Benchmark pitfalls: data contamination, overfitting, real-world disconnect
- Smart benchmark usage: use as reference, not as gold standard

**4. Designing Your Evaluation Pipeline (10 min)**
- Three steps: evaluate components → create evaluation guidelines → define methods and data
- A simple, practical evaluation framework
- Evaluation is not a one-time job — it's an ongoing process

### Hands-On Session (1 hour)

**Activity 1: "Interview" Different AI Models for Your Needs (25 min)**
- Platform: Poe.com or Google AI Studio
- Preparation: design 3 real tasks related to your work/study
- Tasks:
  1. Define success criteria for each task (e.g., "must include X information")
  2. Test at least 3 different models with the same input
  3. Create a simple scoring table and evaluate item by item
  4. Select the model that best fits your needs
- Discussion: If you could only use one model daily, which would you pick? Why?

**Activity 2: Explore the Chatbot Arena Leaderboard (20 min)**
- Platform: lmarena.ai (Chatbot Arena, free)
- Tasks:
  1. Browse the Elo leaderboard and observe model rankings
  2. Check rankings across categories (coding, writing, math, etc.)
  3. Think: is the #1 model necessarily the best for you?
  4. Find 3 sub-metrics you care about and record each model's performance
- Discussion: What can a leaderboard tell you? What can't it tell you?

**Activity 3: Design Your "Evaluation Guide" (15 min)**
- Task: imagine you're building an "AI customer service agent" — design an evaluation guide
  1. Write 5 evaluation criteria (e.g., "understands customer intent," "tone is friendly")
  2. Define behavioral anchors for each criterion on a 1–5 scale
  3. Think: what would "good AI customer service" and "bad AI customer service" look like as examples?
- Discussion: Once your criteria are clear, how much time can an AI judge save you?

---

## Lesson 5: Prompt Engineering — Learning to Talk Effectively with AI

### Learning Objectives
- Understand what prompt engineering is and why it works
- Master the six core best practices of prompt engineering
- Learn defensive prompt design to protect your AI applications
- Understand prompt attacks and defense strategies

### Concept Lecture (1 hour)

**1. Introduction to Prompting (15 min)**
- What is a prompt? System prompt vs. user prompt
- In-context learning: zero-shot vs. few-shot
- Why does prompt engineering work?
- Context length: is more information always better for AI?

**2. Six Best Practices for Prompt Engineering (25 min)**
- Practice 1: Write clear and explicit instructions — vague input = vague output
- Practice 2: Provide sufficient context — AI needs background information
- Practice 3: Break complex tasks into simpler subtasks — step-by-step thinking
- Practice 4: Give the model "time to think" — use "Let's think step by step" to trigger reasoning
- Practice 5: Continuously iterate and improve prompts — prompts need version control too
- Practice 6: Evaluate your prompts — use data, not gut feeling

**3. Defensive Prompt Engineering (15 min)**
- Prompt injection: how bad actors can "hijack" your AI
- Jailbreaking: how to make AI bypass safety restrictions
- Information extraction risk: your data can be "teased out"
- Defense strategies: input filtering, output review, system prompt hardening

**4. Organizing and Versioning Prompts (5 min)**
- Prompts are "code" too — they need version control and A/B testing
- From "casually writing a sentence" to "systematically managing a prompt library"

### Hands-On Session (1 hour)

**Activity 1: Evolving from "Bad Prompt" to "Good Prompt" (25 min)**
- Platform: ChatGPT / Claude
- Task: iteratively improve a prompt for one task
  1. Round 1: ask with a simple sentence (e.g., "Write a proposal for me")
  2. Round 2: add a role ("You are a senior product manager...")
  3. Round 3: add format requirements ("Use Markdown, include the following sections...")
  4. Round 4: add constraints ("No more than 500 words, target non-technical readers")
- Document the changes at each round and feel the power of a "good prompt"
- Tip: a Round 5 option is adding examples — this "few-shot" technique is explored in Activity 2 below

**Activity 2: Experience "Few-Shot Learning" (15 min)**
- Platform: ChatGPT / Claude
- Tasks:
  1. Zero-shot: directly say "Translate this into business English: It's such a nice day today"
  2. One-shot: first give one translation example, then ask AI to translate
  3. Few-shot: give 3 examples in different styles, then ask AI to translate
  4. Compare the results across the three approaches
- Discussion: When do you need to provide examples? How many examples are optimal?

**Activity 3: Try "Jailbreaking" AI — Understanding Safety Boundaries (20 min)**
- Platform: ChatGPT (stronger safety) / Poe.com (some models have weaker safety)
- Tasks (for educational understanding only — do not use for malicious purposes):
  1. Try to make AI "ignore previous instructions" (role-play jailbreak)
  2. Ask AI to pretend it's in "developer mode"
  3. Observe which models are easier to jailbreak and which are harder
  4. Think: if you were an AI app developer, how would you design defenses?
- Important reminder: this exercise is to understand security risks, not to teach wrongdoing

---

## Lesson 6: RAG and AI Agents — Making AI Tell the Truth

### Learning Objectives
- Understand the core principles and workflow of RAG (Retrieval-Augmented Generation)
- Understand the concept and architecture of AI Agents
- Learn about agent tools, planning, and memory mechanisms
- Recognize agent failure modes and evaluation approaches

### Concept Lecture (1 hour)

**1. RAG: Giving AI a "Search Engine" (20 min)**
- Intuitive understanding of RAG: before answering, AI looks up reference material
- RAG architecture in three steps: Retrieve → Augment → Generate
- Retrieval techniques: keyword search vs. semantic search vs. hybrid search
- Why does RAG dramatically reduce hallucinations? Answers now have "sources"
- RAG beyond text: image RAG, video RAG, code RAG
- Typical RAG applications: enterprise knowledge base Q&A, customer support, document assistants

**2. AI Agents: More Than Just Answering Questions (25 min)**
- What is an agent? From "Q&A machine" to "actor"
- The three pillars of agents: Tools → Planning → Memory
- Tool use: how does AI call a search engine, calculator, or API?
- Planning capability: how does AI break a large task into steps?
- Memory mechanisms: short-term memory (conversation context) vs. long-term memory (vector databases)
- Typical agent scenarios: auto-booking, research assistant, coding agent

**3. Agent Failure Modes and Evaluation (15 min)**
- Loop deadlock: agent gets stuck in an infinite loop
- Tool misuse: selecting the wrong tool or using tools incorrectly
- Task drift: gradually going off course
- The difficulty of evaluating agents: end-to-end validation of multi-step tasks
- Human-in-the-loop: keeping manual confirmation at key steps

### Hands-On Session (1 hour)

**Activity 1: Experience the Power of RAG — Perplexity AI (25 min)**
- Platform: Perplexity AI (free tier, RAG-powered search engine)
- Tasks:
  1. Ask a question requiring up-to-date information (e.g., "What was the biggest AI news in 2025?")
  2. Compare Perplexity (with source citations) vs. ChatGPT (without RAG)
  3. Observe how Perplexity annotates information sources
  4. Ask follow-up questions to test whether RAG cites accurately
  5. Ask a controversial question and observe how AI handles conflicting sources
- Discussion: With RAG, does your trust in AI answers increase?

**Activity 2: Build a Personal Knowledge Base RAG with NotebookLM (20 min)**
- Platform: Google NotebookLM (free, upload documents to build RAG directly)
- Tasks:
  1. Upload one of your own documents (PDF, web link, notes, etc.)
  2. Ask NotebookLM questions about that document
  3. Observe how NotebookLM answers based solely on your document
  4. Test: ask about content not in the document and see how it handles it
- Discussion: If you had a tool that could "ingest" all your files, what would you most want to use it for?

**Activity 3: Watch an Agent "Do a Task" (15 min)**
- Platform: ChatGPT (web search mode) / Claude (tool-use mode)
- Tasks:
  1. Give AI a multi-step task: "Search today's tech news, summarize the 3 most important stories, then predict next week's tech stock trends based on them"
  2. Observe how AI breaks down the task, calls tools, and organizes information
  3. Note where AI does well and where it gets stuck
- Discussion: What is the biggest difference between an agent and a regular chatbot?

---

## Lesson 7: Model Fine-Tuning — Building Your Own AI Expert

### Learning Objectives
- Understand what fine-tuning is and how it relates to prompt engineering and RAG
- Master the decision framework: "when to fine-tune, when not to fine-tune"
- Understand core concepts of Parameter-Efficient Fine-Tuning (PEFT)
- Understand the cost and data requirements of fine-tuning

### Concept Lecture (1 hour)

**1. Fine-Tuning Overview (15 min)**
- Intuitive understanding: giving a general model "advanced training" in a specialty
- Fine-tuning vs. prompt engineering vs. RAG: comparing the three adaptation approaches
- Pre-training → Fine-tuning → Inference
- What fine-tuning essentially does: adjusting model parameters to perform better on specific tasks

**2. When to Fine-Tune? When Not To? (20 min)**
- Scenarios suited for fine-tuning:
  - Need model to master highly specialized domain knowledge
  - Need a specific output style or format
  - Prompt engineering and RAG have been tried but aren't good enough
  - Have sufficient high-quality labeled data
- Scenarios not suited for fine-tuning:
  - Requirements change frequently
  - Don't have enough high-quality data
  - Prompt engineering or RAG is already good enough
  - Limited budget and time
- Fine-tuning and RAG: not an either/or — they can be combined

**3. Parameter-Efficient Fine-Tuning (PEFT) Introduction (15 min)**
- The cost of full fine-tuning: needs lots of GPUs and time
- LoRA intuitively: only modify a small part of the model — like "attaching sticky notes" rather than "rewriting the whole book"
- Quantization: "compressing" the model to reduce computation cost
- QLoRA: even more resource-efficient fine-tuning
- Why PEFT has made fine-tuning "accessible to everyone"

**4. Fine-Tuning Practical Considerations (10 min)**
- How much data do you need? Quality > Quantity
- Data format requirements: instruction-response pairs
- Common pitfalls: overfitting, catastrophic forgetting
- Cost estimation: API-based fine-tuning vs. self-hosted fine-tuning

### Hands-On Session (1 hour)

**Activity 1: Explore Fine-Tuning Concepts with OpenAI Playground (25 min)**
- Platform: OpenAI Playground (free registration, explore fine-tuning interface)
- Tasks:
  1. In the Playground, answer a specialized question using the base GPT model
  2. Understand what fine-tuning "training data" looks like (Q&A pair format)
  3. Design 3–5 "ideal answer" examples (your "gold standard" responses)
  4. Think: if these examples were used for fine-tuning, how would the model's behavior change?
- Discussion: Fine-tuning is like "giving AI a reference answer sheet" — is this analogy apt?

**Activity 2: Compare General Models vs. Specialized Models (20 min)**
- Platform: Poe.com or Hugging Face Chat
- Tasks:
  1. Use a general model to answer a very specialized question (e.g., "Explain Shor's algorithm for quantum computing")
  2. Find a domain-fine-tuned model (if available) or use Claude/GPT-4o's high-quality response as reference
  3. Compare: what does the general model lack in specialized domains?
  4. Think: if your work domain is very niche, how much value can fine-tuning bring?
- Discussion: When is "off-the-shelf AI good enough" and when is fine-tuning "a must"?

**Activity 3: Design a Fine-Tuning Dataset (15 min)**
- Task: imagine you want to fine-tune a "customer service AI"
  1. Write 5 common customer questions
  2. For each question, write the "ideal AI response" (aligned with company standards)
  3. Think about data quality control: are your responses good enough? Who reviews them?
- Discussion: What is the hardest part of fine-tuning? (Many think it's the tech — it's actually the data)

---

## Lesson 8: Data Is King — Managing AI's "Ingredients"

### Learning Objectives
- Understand the central role of data in AI engineering
- Master the dimensions of data quality assessment
- Learn about data acquisition, annotation, and augmentation methods
- Understand data synthesis and model distillation concepts

### Concept Lecture (1 hour)

**1. Introduction to Data Curation (15 min)**
- Data curation: from "feeding whatever" to "carefully selecting"
- Three dimensions of data quality: accuracy, completeness, consistency
- Data coverage: does your data represent all the scenarios you care about?
- Data quantity: how much data is "enough"? Quality > Quantity
- Garbage In, Garbage Out

**2. Data Acquisition and Annotation (15 min)**
- Data sources: public datasets, proprietary data, purchased data, user-generated data
- The challenge of human annotation: high cost, long cycle, annotation inconsistency
- Active learning intuitively: let AI help you pick "the most worth-annotating" data
- Pros and cons of crowdsourcing annotation platforms

**3. Data Augmentation and Synthesis (20 min)**
- What is data augmentation? "Generating" more data from existing data
- Traditional augmentation: flip, rotate (images) / synonym replacement (text)
- AI-powered data synthesis: let AI generate training data for you
- Real-world case: using GPT to generate fine-tuning data
- Model distillation: using a large model to "teach" a small model — knowledge transfer
- Distillation vs. directly using a small model: which is better?

**4. Data Processing Pipeline (10 min)**
- Data inspection: how to quickly spot data problems?
- Data deduplication: why is duplicate data a problem?
- Data cleaning and filtering: removing low-quality data
- Data formatting: standardizing format to fit model requirements

### Hands-On Session (1 hour)

**Activity 1: Synthesize Training Data with AI (25 min)**
- Platform: ChatGPT / Claude
- Tasks:
  1. Define a scenario (e.g., "restaurant customer complaint handling")
  2. Have AI generate 10 simulated customer complaints (diverse: angry, confused, picky)
  3. Have AI generate the "ideal customer service response" for each complaint
  4. Manually review the data: anything unreasonable? Any bias?
  5. Think: if this AI-generated data were used to train a customer service AI, what problems might arise?
- Core insight: AI generates data quickly, but quality control remains a human responsibility

**Activity 2: Identify "Dirty Data" (20 min)**
- Platform: any text editor / Google Sheets
- Task: given a simulated "customer feedback dataset" (provided by instructor or generated live)
  1. Find duplicate entries
  2. Find semantically contradictory data (e.g., "very satisfied" with a 1-star rating)
  3. Find inconsistently formatted data
  4. Document all problems found and estimate how long cleaning would take
- Discussion: if this data were used to train AI without cleaning, what would the consequences be?

**Activity 3: Explore Public Datasets (15 min)**
- Platform: Hugging Face Datasets (huggingface.co/datasets) — free browsing
- Tasks:
  1. Browse the dataset list and find 3 datasets related to your interests
  2. Check each dataset's size, format, and annotation method
  3. Read the dataset's "Data Card" to understand its origin and limitations
  4. Think: can these public datasets be used directly? What additional processing is needed?
- Discussion: What are the benefits and risks of using public datasets?

---

## Lesson 9: Inference Optimization — Making AI Faster and Cheaper

### Learning Objectives
- Understand the basic flow of AI inference and its performance metrics
- Master key factors affecting inference speed and cost
- Learn about major model optimization techniques (quantization, distillation, pruning, etc.)
- Understand basic concepts of AI accelerator hardware

### Concept Lecture (1 hour)

**1. Inference Overview (15 min)**
- What is inference? The process of a model "answering a question"
- Inference flow: Input → Tokenization → Model computation → Output → Detokenization
- Why is inference "lighter" than training but can still be expensive?
- The two phases of inference: Prefill vs. Decode

**2. Inference Performance Metrics (15 min)**
- Latency: how long does the user wait for the first word?
- Throughput: how many requests can be processed per second?
- TTFT (Time to First Token): time until the first word appears
- TPS (Tokens per Second): how many words generated per second
- Cost: how much per 1000 tokens?
- The relationship: fast, high-volume, cheap — the engineering impossible triangle

**3. AI Accelerator Hardware Basics (10 min)**
- CPU vs. GPU vs. TPU: intuitive analogies
  - CPU = a versatile worker, can do anything but not fast at any one thing
  - GPU = a team specialized in parallel computing — the acceleration engine for AI
  - TPU = Google's custom "AI-specific chip"
- Why is GPU so important for AI?
- Cloud inference vs. on-device (local) inference

**4. Model Optimization Techniques Overview (20 min)**
- Quantization: "compressing" the model — 32-bit → 8-bit → 4-bit
  - Intuitive analogy: converting a high-res image to standard-res — file gets smaller but it's still recognizable
- Knowledge distillation: a large model teaches a small model
- Pruning: removing unimportant connections in the model, like trimming branches
- Speculative decoding: a small model "guesses," a large model "confirms"
- KV cache optimization: remembering what's already been computed to avoid redundant work
- Practical optimization strategy: try quantization first; add other techniques if not enough

### Hands-On Session (1 hour)

**Activity 1: Experience the "Speed Difference" Across Models (25 min)**
- Platform: Groq (groq.com, known for extremely fast inference) / Poe.com
- Tasks:
  1. On Groq, use a Llama model to answer a question — feel the "instant reply" speed
  2. Ask the same question on a slower platform
  3. Use a stopwatch to record Time to First Token
  4. Think: in daily AI use, how important is speed to you? In what scenarios is speed more critical than quality?
- Discussion: if AI answers 50% faster but accuracy drops 5%, would you accept it?

**Activity 2: Calculate AI Usage Costs (20 min)**
- Platform: OpenAI Pricing page (openai.com/pricing) / Google AI pricing page
- Tasks:
  1. Look up the per-million-token prices for GPT-4o and GPT-4o-mini
  2. Estimate: if your app serves 1000 users/day, each averaging 500 words input + 300 words output, what's the monthly cost?
  3. Compare the cost difference between GPT-4o and GPT-4o-mini
  4. Think: would you use the more expensive but better model, or the cheaper but slightly worse model?
- Discussion: What does the cost structure of an AI application look like? Where can you "cut costs"?

**Activity 3: Explore "Compressed Models" on Hugging Face (15 min)**
- Platform: Hugging Face (huggingface.co)
- Tasks:
  1. Search for "GGUF" or "quantized" models
  2. Observe different quantized versions of the same model (e.g., Q4, Q5, Q8)
  3. Compare file size differences: original vs. quantized
  4. Understand: why can quantization make a model "smaller" while largely preserving its capability?
- Discussion: If you could one day run a "good enough" AI model on your phone, what would you most want to use it for?

---

## Lesson 10: AI System Architecture and Continuous Evolution — From Prototype to Production

### Learning Objectives
- Understand the five-layer architecture of production-grade AI systems
- Learn about AI system monitoring, observability, and orchestration
- Master the design philosophy of user feedback loops
- Gain a complete panoramic view of AI engineering practice

### Concept Lecture (1 hour)

**1. The Five-Step AI Engineering Architecture (25 min)**
- Step 1: Enhance Context
  - Query rewriting: helping users turn "poorly phrased" questions into better ones
  - Intent classification: understanding what the user actually wants
- Step 2: Put in Guardrails
  - Input guardrails: filtering harmful, jailbreak, and injection content
  - Output guardrails: filtering inappropriate, unsafe, or inaccurate content
  - Architecture guardrails: access control, rate limiting
- Step 3: Model Router and Gateway
  - Why model routing? Different questions go to different models
  - Simple questions → small model (cheap); complex questions → large model (expensive)
- Step 4: Reduce Latency with Caches
  - Exact cache: identical questions → return cached result directly
  - Semantic cache: similar questions → return cached result directly
- Step 5: Agent Patterns
  - Combining all the above capabilities

**2. Monitoring and Observability (15 min)**
- Monitoring vs. observability: knowing "something is wrong" vs. knowing "why it's wrong"
- What does an AI system need to monitor? Latency, cost, error rate, output quality, user satisfaction
- Drift detection: is the model's response quality degrading over time?
- AI pipeline orchestration: how to chain multiple AI calls into a complete workflow?

**3. User Feedback: Fuel for AI's Continuous Evolution (20 min)**
- Types of feedback: explicit (thumbs up/down) vs. implicit (copied the response, closed the page)
- Conversational feedback mining: automatically extracting user satisfaction signals from conversations
- Feedback design principles:
  - Simple: don't make users fill out surveys
  - Timely: collect naturally within the conversation flow
  - Actionable: feedback must translate into improvements
- Feedback limitations: survivorship bias, politeness bias, extremity bias
- Building the flywheel: collect feedback → analyze problems → improve model → better experience → more usage → more feedback

### Hands-On Session (1 hour)

**Activity 1: Design Guardrails for an AI Product (20 min)**
- Task: imagine you're building a "Children's Learning Assistant AI"
  1. List at least 5 "absolutely must not do" items (e.g., must not respond to violent or adult content)
  2. Design input filtering rules (detecting whether questions contain inappropriate content)
  3. Design output filtering rules (checking whether AI responses are suitable for children)
  4. Think: what if a user asks a sensitive question using metaphors or indirect language?
- Discussion: guardrails that are too strict limit AI capability; too loose creates safety risks — how to balance?

**Activity 2: Design a Feedback Collection Mechanism for Your AI (20 min)**
- Task: design a simple but effective user feedback plan
  1. Sketch a simple feedback UI (where in the chat interface, how users interact)
  2. Decide what feedback signals to collect: thumbs up/down, ratings, text comments?
  3. Design a question checklist: once feedback is collected, what questions will you ask yourself to analyze the data?
  4. Simulate a "user downvotes" scenario — how would you troubleshoot?
- Discussion: is more feedback always better? How to avoid "feedback fatigue"?

**Activity 3: Full Course Review and Future Outlook (20 min)**
- Review the core thread across all 10 lessons:
  - Entry (1–2) → Evaluation (3–4) → Adaptation Techniques (5–7) → Data (8) → Optimization (9) → Architecture Loop (10)
- Group discussion:
  1. Which lesson inspired you most? Why?
  2. What problem do you now most want to solve using AI?
  3. What do you think is the hardest part of AI engineering?
- Instructor closing: the core of AI engineering is not the technology itself, but "how to turn technology into a means of solving problems"
- Recommended follow-up learning resources and pathways

---

## Appendix: Hands-On Tools Quick Reference

| Tool / Platform | Purpose | Cost | Relevant Lessons |
|-----------------|---------|------|-------------------|
| ChatGPT | General AI chat, prompt engineering practice | Free / Paid | Lessons 1–10 |
| Claude | General AI chat, long-text processing | Free / Paid | Lessons 1–10 |
| Poe.com | Multi-model comparison | Free / Paid | Lessons 1–7 |
| Google AI Studio | Adjust generation parameters, model experiments | Free | Lessons 2, 4 |
| Perplexity AI | RAG-powered search experience | Free / Paid | Lesson 6 |
| Google NotebookLM | Personal knowledge base RAG | Free | Lesson 6 |
| Groq | Ultra-fast inference experience | Free | Lesson 9 |
| Hugging Face | Model browsing, dataset exploration | Free | Lessons 7–9 |
| Chatbot Arena (lmarena.ai) | Model leaderboard | Free | Lesson 4 |
| OpenAI Playground | Fine-tuning concept exploration | Free / Paid | Lesson 7 |
| Hugging Face Datasets | Public dataset browsing | Free | Lesson 8 |

---

> This course is based on Chip Huyen's *AI Engineering: Building Applications with Foundation Models* (O'Reilly, 2025).  
> Design principles: concept lectures emphasize intuitive understanding and core ideas.
> The **concept track** keeps a strict zero-code barrier and every tool it uses is free or has a free tier;
> the **code track** (notebooks) needs your own API key or local Ollama — about $0.10 to run all ten lessons.

# medorc-orby-chatbot

## Introduction to Natural Language Processing (NLP)

___
**Natural Language Processing (NLP)** is a discipline of building machines that can manipulate human language. It focuses on enabling computers to understand, interpret, manipulate, and generate human language. 🗣️💻 In essence, it's the technology that bridges the communication gap between humans and computers.

NLP combines computational linguistics—the rule-based modeling of human language—with statistical, machine learning, and deep learning models. This combination allows computers to process human language in the form of text or voice data and to 'understand' its full meaning, complete with the speaker's or writer's intent and sentiment.

### Core goals of NLP
* **Text and Speech Recognition:** Converting voice data into text data and understanding the structure of written text.
* **Understanding Meaning (NLU):** Going beyond literal definitions to figure out the intent, context, and sentiment of the language. This involves tasks like named entity recognition (identifying names, dates, locations) and relationship extraction.
* **Language Generation:** Generating natural-sounding human language in response to input. This can be seen in chatbots, automated report writing, and translation.
* **Sentiment Analysis:** Determining the emotional tone behind a piece of text, such as positive, negative, or neutral. This is widely used for analyzing customer reviews and social media.

## NLP types

---
Natural Language Processing (NLP) is a broad field of artificial intelligence, but it can be primarily broken down into two main, complementary components that dictate how a machine interacts with human language. Additionally, a third type represents the application of these components in creating interactive systems.

### 1. Natural Language Understanding (NLU): The "Reading" Part
**What it is:** How a computer comprehends human language to figure out intent, context, and meaning.

**Example:** When you ask Google Assistant, "Find Italian restaurants near me," NLU is what identifies your goal (find restaurants), the category (Italian), and the location (near me).

### 2. Natural Language Generation (NLG): The "Writing" Part
**What it is:** How a computer takes structured information and produces a natural-sounding human response.

**Example:** After finding the restaurants, the sentence "I found a few Italian places nearby" is created by NLG.

### 3. Natural Language Interaction (NLI): The "Conversation" Part
**What it is:** The complete, two-way dialogue that combines NLU (understanding you) and NLG (replying to you) to create a seamless conversational experience.

**Example:** A full, back-and-forth chat with a customer service bot.

## Types of NLP approach

___

| Approach                  | Core Idea                                                    | Pros                                                 | Cons                                                    |
| :------------------------ | :----------------------------------------------------------- | :--------------------------------------------------- | :------------------------------------------------------ |
| **Symbolic (Rule-Based)** | Use hand-written linguistic rules.                           | Explainable, Precise.                                | Brittle, Not Scalable.                                  |
| **Statistical (ML)** | Learn statistical patterns from data.                        | Robust, Scalable with data.                          | Needs labeled data, Manual feature engineering.         |
| **Neural (Deep Learning)**| Automatically learn context and features using neural networks. | State-of-the-art performance, Understands context. | Black box, Needs massive data and compute power. |


## Rasa 🤖

___

Rasa is the leading **open-source framework** for building production-grade, AI-powered chatbots and voice assistants. Unlike cloud-based platforms like Google Dialogflow or Amazon Lex, Rasa allows you to have full control over your application. You can host it on your own servers, ensuring complete data privacy and unlimited customization.

Its core philosophy is to enable developers to build assistants that can handle the complexity of real-world, non-linear conversations.

## The Core Components of Rasa
___

The Rasa framework is built on two main pillars that work together:

### 1. Rasa NLU (Natural Language Understanding)
This is the component responsible for **understanding the user's message**. It takes raw text from the user and extracts structured information. Its primary jobs are:

* **Intent Classification:** Figuring out *what* the user wants to do.
    * *User says:* "How much does a flight to Mumbai cost?"
    * *Intent:* `ask_flight_price`
* **Entity Recognition:** Extracting the key pieces of information from the message.
    * *User says:* "How much does a flight to **Mumbai** cost?"
    * *Entity:* `destination: "Mumbai"`

The NLU pipeline is highly configurable, allowing you to fine-tune it for your specific language and domain.

### 2. Rasa Core (Dialogue Management)
This is the "brain" of the assistant. Once the NLU has understood the user's message, Rasa Core **decides what the bot should do next**.

Instead of using rigid `if/else` statements, Rasa Core uses a machine learning-based approach. It learns the patterns of a conversation from example "stories" you provide. This allows it to:

* Handle unexpected user inputs and digressions.
* Maintain the context of the conversation.
* Decide when to ask a clarifying question, answer the user, or run custom code.

## The Rasa Development Workflow

___
Developing a chatbot in Rasa revolves around a few key files:

1.  **`nlu.yml`**: This is where you provide training data for the NLU model. You list your intents and provide many example sentences for each.
    ```yaml
    - intent: greet
      examples: |
        - hey
        - hello there
        - good morning
    
    - intent: check_balance
      examples: |
        - what's my account balance?
        - show me how much money I have
    ```

2.  **`stories.yml`**: Here, you write example conversations to train the dialogue management model (Rasa Core). These are happy paths that show how the bot should respond to user inputs.
    ```yaml
    - story: happy path
      steps:
      - intent: greet
      - action: utter_greet
      - intent: check_balance
      - action: action_get_balance
      - action: utter_display_balance
    ```

3.  **`domain.yml`**: This file is the "universe" of your assistant. It defines everything the bot knows: all intents, entities, responses (`utter_...`), and custom actions.

4.  **`actions.py`**: This is where you write custom Python code. If your bot needs to do something beyond just sending a message—like querying a database or calling an API—you write that logic here.

## Why Choose Rasa in 2025?

___
* **Data Privacy and Ownership:** Since you host it yourself, no user conversation data ever leaves your servers. This is critical for industries like finance, healthcare, and for complying with data regulations.
* **Full Customization:** You have complete control over every part of the NLU and dialogue pipeline. You can integrate state-of-the-art models and build a truly unique assistant.
* **No Vendor Lock-in:** You are not tied to a specific cloud provider's ecosystem or pricing model. This gives you long-term flexibility.
* **Active Community and Support:** Rasa has a large and active open-source community, meaning there are plenty of resources, tutorials, and help available.
* **It's Free:** The core Rasa Open Source framework is free to use. They offer an enterprise product, Rasa Pro, for more advanced collaboration and analytics tools.

**In short, Rasa is the go-to choice for developers and companies who need a powerful, private, and highly customizable conversational AI solution.**

## Necessary modules for Rasa

___
To get a Rasa project up and running, you'll need a few key Python modules, typically managed using `pip`.

* **Core Module:**
    * `rasa`: The main package, including NLU, Core, and the server.
        ```bash
        pip install rasa
        ```

* **Action Server Module:**
    * `rasa-sdk`: Required to run the **Action Server** for custom Python code.
        ```bash
        pip install rasa-sdk
        ```

* **Commonly Used Modules in Custom Actions (`actions.py`):**
    * `requests`: For making HTTP API calls.
    * Database connectors like `psycopg2-binary` (for PostgreSQL).

* **Optional but Recommended for Production:**
    * `gunicorn`: A production-grade WSGI server.

## Flow of the request from front-end to back-end

___
Here is the step-by-step journey of a user's message:

1.  **User Input (Front-end):** The user types a message in the chat interface.
2.  **HTTP Request:** The front-end sends a `POST` request to the Rasa server's API endpoint (`/webhooks/rest/webhook`).
3.  **Rasa Server - NLU:** The NLU pipeline processes the text to classify the intent and extract entities.
4.  **Rasa Server - Tracker:** The conversation state (`Tracker`) is updated.
5.  **Rasa Server - Core:** The Dialogue Management model predicts the next action.
6.  **Action Execution:**
    * A simple response (`utter_...`) is fetched from `domain.yml`.
    * A custom action (`action_...`) triggers an API call to the **Action Server**.
7.  **Action Server Logic:** The Action Server runs the relevant code from `actions.py` and returns the results.
8.  **Response to Front-end:** The Rasa server sends the final message(s) back to the front-end.
9.  **Display to User:** The front-end renders the bot's response in the chat window.

## Integration with front-end

___
Rasa is front-end agnostic and integrates via **connectors**.

* **The REST Channel (Most Flexible):** This is the default method. Any front-end that can make HTTP requests can communicate with your Rasa bot.
* **Web Chat Widgets:** Pre-built widgets like [Rasa Webchat](https://github.com/botfront/rasa-webchat) simplify web integration.
* **Other Built-in Channels:** Rasa also has connectors for Slack, Facebook Messenger, Telegram, etc., configured in `credentials.yml`.

## Total server count for the project including rasa

___
The number of servers depends on your environment and scale.

* **Development (1 Server):** Run both the Rasa server and Action server as separate processes on your local machine.
* **Production - Minimum Setup (2 Servers):**
    * **Server 1:** For the Rasa Server (NLU/Core).
    * **Server 2:** For the Action Server.
* **Production - High-Availability (5+ Servers/Nodes):** A scaled setup uses Docker/Kubernetes with a load balancer, multiple Rasa/Action server nodes, and a dedicated Redis server for a tracker store.

### Project File Structure

___
* `actions/`
    * `__init__.py`
    * `actions.py` - This is where you write your custom Python code.
* `data/`
    * `nlu.yml` - Your NLU training data (intents and examples).
    * `rules.yml` - Rules for handling simple, fixed conversation paths.
    * `stories.yml` - Example conversation paths for training the main dialogue model.
* `models/`
    * `<timestamp>.tar.gz` - Your trained models are saved here.
* `tests/`
    * `test_stories.py` - Contains files for testing your bot's conversations.
* `config.yml` - The main configuration file for your NLU and Core policies.
* `credentials.yml` - Used for connecting your bot to external channels (e.g., Slack).
* `domain.yml` - The "universe" of your bot; lists all intents, actions, and responses.
* `endpoints.yml` - Configures connections to the action server and tracker stores.

### Prerequisites

___
* Python 3.8+ and `pip`
* *(add any other prerequisites like database setup)*

### Installation & Setup

___
1.  **Clone the repo**
    ```sh
    git clone [https://github.com/Medorc/medorc-orby-chatbot.git](https://github.com/Medorc/medorc-orby-chatbot.git)
    ```
2.  **Create a virtual environment and install dependencies**
    ```sh
    python -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    ```
3.  **Train the Rasa model**
    ```sh
    rasa train
    ```
4.  **Run the servers (in two separate terminals)**
    ```sh
    # Terminal 1: Run the action server
    rasa run actions

    # Terminal 2: Run the Rasa server and talk to the bot
    rasa shell
    ```
## 🤖 Model Performance & Accuracy

The Orby NLU model was evaluated using a two-stage testing process to ensure high performance and robustness.

### 1. Initial Benchmark (Clean Data)

The model was first evaluated against a curated test set of 83 ideal user queries. It achieved a perfect score, demonstrating its ability to master the core intents and entities within a clean data environment.

**Key Metrics (Clean Data):**

| Metric         | Score |
| :------------- | :---- |
| Accuracy       | 1.0   |
| Macro F1-Score | 1.0   |
| Weighted F1-Score  | 1.0   |

**Intent Confusion Matrix (Clean Data):**
*This matrix shows zero errors in distinguishing between the 26 different intents.*
![Intent Confusion Matrix on Clean Data](./Results/clean_data_test/intent_confusion_matrix.png)

### 2. Real-World Stress Test (Messy Data)

To simulate a more realistic scenario, the model was then evaluated against a second test set containing typos, slang, and more complex phrasing. After a cycle of fine-tuning based on initial errors, the model's performance on this more difficult dataset is as follows:

**Key Metrics (Real-World Data):**

| Metric         | Score |
| :------------- | :---- |
| Accuracy       | 0.9X  |  | Macro F1-Score | 0.9X  |  | Weighted F1-Score  | 0.9X  |  *(You can find these scores in your latest `results/intent_report.json`)*

**Intent Confusion Matrix (Real-World Data):**
*This matrix shows the model's high performance, with minimal confusion on the more challenging test data.*
![Intent Confusion Matrix on Real-World Data](./Results/real_world_stress_test/intent_confusion_matrix.png)


### 3. The Narrative

This two-stage evaluation proves that the Orby model is not only capable of achieving 100% accuracy on a defined problem set but is also robust enough to be fine-tuned to handle the ambiguities of real-world user input with high precision.